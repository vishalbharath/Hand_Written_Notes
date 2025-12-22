# Military Asset Management System (MAMS) - Technical Documentation

## Table of Contents
1. [Project Overview](#project-overview)
2. [Tech Stack & Architecture](#tech-stack--architecture)
3. [Data Models/Schema](#data-modelsschema)
4. [RBAC Explanation](#rbac-explanation)
5. [API Logging](#api-logging)
6. [Setup Instructions](#setup-instructions)
7. [API Endpoints](#api-endpoints)

---

## Project Overview

### Description
The Military Asset Management System (MAMS) is a comprehensive web-based application designed to enable commanders and logistics personnel to manage the movement, assignment, and expenditure of critical military assets (vehicles, weapons, ammunition, equipment) across multiple bases. The system provides transparency, streamlined logistics, and accountability through a secure role-based solution.

### Key Features
- **Real-time Dashboard**: Track Opening Balance, Closing Balance, Net Movement, Assigned, and Expended assets
- **Purchase Management**: Record and manage asset purchases with multi-level approval workflows
- **Transfer System**: Facilitate and log inter-base transfers with complete audit history
- **Assignment Tracking**: Assign assets to personnel and monitor usage patterns
- **Role-Based Access Control**: Secure access for Admin, Base Commander, and Logistics Officer roles
- **Comprehensive Audit Trail**: Complete logging of all transactions for accountability and compliance

### Assumptions
1. **Network Connectivity**: The system assumes reliable network connectivity between bases for real-time synchronization
2. **User Training**: Personnel using the system have received appropriate training on military asset management procedures
3. **Data Integrity**: Asset serial numbers and identification codes are unique and properly maintained
4. **Security Clearance**: All users have appropriate security clearances for their assigned roles
5. **Hardware Availability**: Adequate computing resources are available at each base for system operation

### Limitations
1. **Offline Functionality**: The current implementation requires internet connectivity; offline mode is not supported
2. **Real-time Tracking**: Physical asset location tracking (GPS) is not implemented in the current version
3. **Integration**: Direct integration with existing military ERP systems requires additional development
4. **Scalability**: The current architecture is designed for medium-scale operations (up to 50 bases, 10,000 assets)
5. **Mobile App**: Native mobile applications are not included in the current implementation
6. **Barcode/RFID**: Automated asset identification through barcode or RFID scanning is not implemented

---

## Tech Stack & Architecture

### Frontend Architecture
**Technology**: React 18 with JavaScript (ES6+)

**Reasoning**:
- **Component-Based Architecture**: Enables modular development and easy maintenance
- **Virtual DOM**: Provides efficient rendering for real-time dashboard updates
- **Large Ecosystem**: Extensive library support for military-grade UI components
- **Developer Experience**: Excellent debugging tools and development workflow
- **Performance**: Optimized for handling large datasets and frequent updates

**Key Libraries**:
- **Tailwind CSS**: Utility-first CSS framework for rapid, consistent styling
- **Lucide React**: Professional icon library with military-appropriate iconography
- **Date-fns**: Modern date manipulation library for timeline tracking
- **Clsx**: Conditional className utility for dynamic styling

### Backend Architecture (Planned)
**Technology**: Node.js with Express.js

**Reasoning**:
- **JavaScript Ecosystem**: Unified language across frontend and backend
- **Scalability**: Event-driven architecture suitable for real-time operations
- **Security**: Mature security middleware ecosystem for military applications
- **Performance**: Non-blocking I/O ideal for handling multiple concurrent requests
- **Deployment**: Easy containerization and cloud deployment options

**Key Components**:
- **Express.js**: Web application framework with robust middleware support
- **JWT**: JSON Web Tokens for secure, stateless authentication
- **Helmet**: Security middleware for HTTP header protection
- **Rate Limiting**: Protection against abuse and DoS attacks
- **CORS**: Cross-origin resource sharing configuration

### Database Architecture (Planned)
**Technology**: MySQL 8.0+

**Reasoning**:
- **ACID Compliance**: Ensures data integrity for critical military operations
- **Relational Model**: Perfect for complex asset relationships and hierarchies
- **Performance**: Optimized for read-heavy workloads with proper indexing
- **Security**: Enterprise-grade security features and encryption
- **Backup & Recovery**: Robust backup and point-in-time recovery capabilities
- **Compliance**: Meets military data handling and audit requirements

### Current Implementation
The current frontend implementation uses a **mock API service layer** that simulates backend functionality:
- **Local Storage**: Persistent user sessions and preferences
- **Mock Data**: Realistic sample data for demonstration and testing
- **Simulated Latency**: Network delay simulation for realistic user experience
- **Error Handling**: Comprehensive error scenarios and recovery mechanisms

---

## Data Models/Schema

### Core Entities and Relationships

#### 1. Users Table
```sql
CREATE TABLE users (
    id VARCHAR(36) PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    role ENUM('ADMIN', 'BASE_COMMANDER', 'LOGISTICS_OFFICER') NOT NULL,
    base_id VARCHAR(36),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    last_login TIMESTAMP NULL,
    FOREIGN KEY (base_id) REFERENCES bases(id)
);
```

#### 2. Bases Table
```sql
CREATE TABLE bases (
    id VARCHAR(36) PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    location VARCHAR(200) NOT NULL,
    commander_id VARCHAR(36),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (commander_id) REFERENCES users(id)
);
```

#### 3. Assets Table
```sql
CREATE TABLE assets (
    id VARCHAR(36) PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    type ENUM('VEHICLE', 'WEAPON', 'AMMUNITION', 'EQUIPMENT') NOT NULL,
    serial_number VARCHAR(100) UNIQUE NOT NULL,
    base_id VARCHAR(36) NOT NULL,
    status ENUM('AVAILABLE', 'ASSIGNED', 'MAINTENANCE', 'EXPENDED') DEFAULT 'AVAILABLE',
    assigned_to VARCHAR(36) NULL,
    purchase_id VARCHAR(36) NULL,
    condition_notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (base_id) REFERENCES bases(id),
    FOREIGN KEY (assigned_to) REFERENCES users(id),
    FOREIGN KEY (purchase_id) REFERENCES purchases(id)
);
```

#### 4. Purchases Table
```sql
CREATE TABLE purchases (
    id VARCHAR(36) PRIMARY KEY,
    asset_type ENUM('VEHICLE', 'WEAPON', 'AMMUNITION', 'EQUIPMENT') NOT NULL,
    asset_name VARCHAR(100) NOT NULL,
    quantity INT NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    total_amount DECIMAL(12,2) NOT NULL,
    supplier VARCHAR(200) NOT NULL,
    base_id VARCHAR(36) NOT NULL,
    purchased_by VARCHAR(36) NOT NULL,
    approved_by VARCHAR(36) NULL,
    status ENUM('PENDING', 'APPROVED', 'REJECTED', 'DELIVERED') DEFAULT 'PENDING',
    order_date DATE NOT NULL,
    delivery_date DATE NULL,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (base_id) REFERENCES bases(id),
    FOREIGN KEY (purchased_by) REFERENCES users(id),
    FOREIGN KEY (approved_by) REFERENCES users(id)
);
```

#### 5. Transfers Table
```sql
CREATE TABLE transfers (
    id VARCHAR(36) PRIMARY KEY,
    asset_id VARCHAR(36) NOT NULL,
    from_base_id VARCHAR(36) NOT NULL,
    to_base_id VARCHAR(36) NOT NULL,
    quantity INT NOT NULL DEFAULT 1,
    requested_by VARCHAR(36) NOT NULL,
    approved_by VARCHAR(36) NULL,
    status ENUM('PENDING', 'APPROVED', 'IN_TRANSIT', 'COMPLETED', 'REJECTED') DEFAULT 'PENDING',
    request_date DATE NOT NULL,
    approval_date DATE NULL,
    completion_date DATE NULL,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (asset_id) REFERENCES assets(id),
    FOREIGN KEY (from_base_id) REFERENCES bases(id),
    FOREIGN KEY (to_base_id) REFERENCES bases(id),
    FOREIGN KEY (requested_by) REFERENCES users(id),
    FOREIGN KEY (approved_by) REFERENCES users(id)
);
```

#### 6. Assignments Table
```sql
CREATE TABLE assignments (
    id VARCHAR(36) PRIMARY KEY,
    asset_id VARCHAR(36) NOT NULL,
    assigned_to VARCHAR(100) NOT NULL, -- Personnel name (not user ID)
    assigned_by VARCHAR(36) NOT NULL,
    base_id VARCHAR(36) NOT NULL,
    assignment_date DATE NOT NULL,
    expected_return_date DATE NULL,
    actual_return_date DATE NULL,
    status ENUM('ACTIVE', 'RETURNED', 'EXPENDED', 'DAMAGED') DEFAULT 'ACTIVE',
    purpose VARCHAR(200) NOT NULL,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (asset_id) REFERENCES assets(id),
    FOREIGN KEY (assigned_by) REFERENCES users(id),
    FOREIGN KEY (base_id) REFERENCES bases(id)
);
```

#### 7. Audit Logs Table
```sql
CREATE TABLE audit_logs (
    id VARCHAR(36) PRIMARY KEY,
    action VARCHAR(50) NOT NULL,
    entity_type VARCHAR(50) NOT NULL,
    entity_id VARCHAR(36) NOT NULL,
    user_id VARCHAR(36) NOT NULL,
    user_name VARCHAR(100) NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    details JSON,
    ip_address VARCHAR(45),
    user_agent TEXT,
    INDEX idx_timestamp (timestamp),
    INDEX idx_user_id (user_id),
    INDEX idx_entity (entity_type, entity_id),
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

### Entity Relationships

```
Users (1) ←→ (N) Bases (commander_id)
Users (1) ←→ (N) Assets (assigned_to)
Users (1) ←→ (N) Purchases (purchased_by, approved_by)
Users (1) ←→ (N) Transfers (requested_by, approved_by)
Users (1) ←→ (N) Assignments (assigned_by)
Users (1) ←→ (N) Audit_Logs (user_id)

Bases (1) ←→ (N) Assets (base_id)
Bases (1) ←→ (N) Purchases (base_id)
Bases (1) ←→ (N) Transfers (from_base_id, to_base_id)
Bases (1) ←→ (N) Assignments (base_id)

Assets (1) ←→ (N) Transfers (asset_id)
Assets (1) ←→ (N) Assignments (asset_id)
Assets (N) ←→ (1) Purchases (purchase_id)
```

---

## RBAC Explanation

### Role Hierarchy and Access Levels

#### 1. Admin Role
**Access Level**: System-wide (Global)

**Permissions**:
- `view_all`: Access to all bases and system-wide data
- `manage_users`: Create, update, delete user accounts
- `manage_bases`: Create, update, delete base information
- `approve_transfers`: Approve inter-base transfers
- `approve_purchases`: Approve purchase requests
- `view_audit_logs`: Access complete audit trail
- `system_configuration`: Modify system settings

**Capabilities**:
- View dashboard metrics across all bases
- Manage user accounts and role assignments
- Override security restrictions when necessary
- Access complete audit trails and system logs
- Approve high-value purchases and critical transfers

#### 2. Base Commander Role
**Access Level**: Base-specific (Local)

**Permissions**:
- `view_base`: Access to assigned base data only
- `approve_transfers`: Approve transfers involving their base
- `approve_purchases`: Approve purchase requests for their base
- `manage_assignments`: Assign assets to personnel
- `view_base_audit`: Access audit logs for their base

**Capabilities**:
- View base-specific dashboard and metrics
- Approve purchase requests from logistics officers
- Authorize inter-base transfers and asset movements
- Assign assets to personnel under their command
- Review base-specific audit logs and reports

#### 3. Logistics Officer Role
**Access Level**: Base-specific (Operational)

**Permissions**:
- `view_base`: Access to assigned base data only
- `create_transfers`: Initiate inter-base transfer requests
- `create_purchases`: Submit purchase requests
- `manage_assets`: Update asset status and information
- `create_assignments`: Assign assets to personnel

**Capabilities**:
- Create and submit purchase requests
- Initiate inter-base transfer requests
- Manage day-to-day asset assignments
- Track asset maintenance and status updates
- Generate operational reports

### RBAC Enforcement Method

#### 1. Authentication Layer
```javascript
// JWT Token Structure
{
  "sub": "user-id",
  "username": "logistics_officer",
  "role": "LOGISTICS_OFFICER",
  "baseId": "base-1",
  "permissions": ["view_base", "create_transfers", "create_purchases"],
  "iat": 1640995200,
  "exp": 1641081600
}
```

#### 2. Authorization Middleware
```javascript
const authorize = (requiredPermission) => {
  return (req, res, next) => {
    const { permissions, role, baseId } = req.user;
    
    // Check if user has required permission
    if (!permissions.includes(requiredPermission)) {
      return res.status(403).json({ error: 'Insufficient permissions' });
    }
    
    // Additional base-level access control
    if (requiredPermission.includes('base') && req.params.baseId !== baseId && role !== 'ADMIN') {
      return res.status(403).json({ error: 'Access denied to this base' });
    }
    
    next();
  };
};
```

#### 3. Frontend Permission Checking
```javascript
// AuthContext permission checking
const hasPermission = (permission) => {
  if (!user) return false;
  return rolePermissions[user.role]?.includes(permission) || false;
};

// Component-level access control
{hasPermission('approve_purchases') && (
  <button onClick={handleApprove}>Approve Purchase</button>
)}
```

#### 4. Database-Level Security
```sql
-- Row Level Security (RLS) policies
CREATE POLICY base_access_policy ON assets
  FOR ALL TO application_role
  USING (
    base_id = current_setting('app.current_base_id') 
    OR current_setting('app.user_role') = 'ADMIN'
  );
```

---

## API Logging

### Transaction Logging Strategy

#### 1. Audit Log Structure
```javascript
const auditLogEntry = {
  id: 'uuid-v4',
  action: 'ASSET_ASSIGNED',           // Action type
  entityType: 'ASSIGNMENT',           // Entity affected
  entityId: 'assignment-123',         // Specific entity ID
  userId: 'user-456',                 // User performing action
  userName: 'Major Sarah Johnson',    // User display name
  timestamp: '2024-01-15T10:30:00Z',  // ISO timestamp
  details: {                          // Action-specific details
    assetName: 'M4A1 Carbine',
    assignedTo: 'Sergeant Williams',
    previousStatus: 'AVAILABLE',
    newStatus: 'ASSIGNED'
  },
  ipAddress: '192.168.1.100',         // Client IP
  userAgent: 'Mozilla/5.0...',        // Browser info
  sessionId: 'session-789'            // Session identifier
};
```

#### 2. Logged Actions
```javascript
const AUDIT_ACTIONS = {
  // Authentication
  USER_LOGIN: 'USER_LOGIN',
  USER_LOGOUT: 'USER_LOGOUT',
  LOGIN_FAILED: 'LOGIN_FAILED',
  
  // Asset Management
  ASSET_CREATED: 'ASSET_CREATED',
  ASSET_UPDATED: 'ASSET_UPDATED',
  ASSET_ASSIGNED: 'ASSET_ASSIGNED',
  ASSET_RETURNED: 'ASSET_RETURNED',
  ASSET_EXPENDED: 'ASSET_EXPENDED',
  
  // Purchases
  PURCHASE_CREATED: 'PURCHASE_CREATED',
  PURCHASE_APPROVED: 'PURCHASE_APPROVED',
  PURCHASE_REJECTED: 'PURCHASE_REJECTED',
  PURCHASE_DELIVERED: 'PURCHASE_DELIVERED',
  
  // Transfers
  TRANSFER_CREATED: 'TRANSFER_CREATED',
  TRANSFER_APPROVED: 'TRANSFER_APPROVED',
  TRANSFER_COMPLETED: 'TRANSFER_COMPLETED',
  TRANSFER_REJECTED: 'TRANSFER_REJECTED',
  
  // System
  USER_CREATED: 'USER_CREATED',
  USER_UPDATED: 'USER_UPDATED',
  ROLE_CHANGED: 'ROLE_CHANGED',
  BASE_CREATED: 'BASE_CREATED'
};
```

#### 3. Logging Middleware Implementation
```javascript
const auditLogger = (action, entityType) => {
  return async (req, res, next) => {
    const originalSend = res.send;
    
    res.send = function(data) {
      // Log successful operations
      if (res.statusCode >= 200 && res.statusCode < 300) {
        const logEntry = {
          id: generateUUID(),
          action,
          entityType,
          entityId: req.params.id || extractIdFromResponse(data),
          userId: req.user.id,
          userName: req.user.name,
          timestamp: new Date().toISOString(),
          details: extractRelevantDetails(req, data),
          ipAddress: req.ip,
          userAgent: req.get('User-Agent'),
          sessionId: req.sessionID
        };
        
        // Async logging to avoid blocking response
        setImmediate(() => {
          auditLogService.create(logEntry);
        });
      }
      
      originalSend.call(this, data);
    };
    
    next();
  };
};
```

#### 4. Audit Query Capabilities
```javascript
// Audit log filtering and search
const getAuditLogs = async (filters) => {
  const {
    userId,
    action,
    entityType,
    startDate,
    endDate,
    baseId,
    page = 1,
    limit = 50
  } = filters;
  
  const query = `
    SELECT * FROM audit_logs 
    WHERE 1=1
    ${userId ? 'AND user_id = ?' : ''}
    ${action ? 'AND action = ?' : ''}
    ${entityType ? 'AND entity_type = ?' : ''}
    ${startDate ? 'AND timestamp >= ?' : ''}
    ${endDate ? 'AND timestamp <= ?' : ''}
    ORDER BY timestamp DESC
    LIMIT ? OFFSET ?
  `;
  
  return await db.query(query, [...params, limit, (page - 1) * limit]);
};
```

### Data Retention and Compliance

#### 1. Retention Policy
- **Audit Logs**: Retained for 7 years (military compliance requirement)
- **User Sessions**: 30 days after expiration
- **Failed Login Attempts**: 1 year for security analysis
- **System Events**: 3 years for operational analysis

#### 2. Data Archival
```javascript
// Monthly archival process
const archiveOldLogs = async () => {
  const cutoffDate = new Date();
  cutoffDate.setFullYear(cutoffDate.getFullYear() - 7);
  
  // Move to archive table
  await db.query(`
    INSERT INTO audit_logs_archive 
    SELECT * FROM audit_logs 
    WHERE timestamp < ?
  `, [cutoffDate]);
  
  // Remove from active table
  await db.query(`
    DELETE FROM audit_logs 
    WHERE timestamp < ?
  `, [cutoffDate]);
};
```

---

## Setup Instructions

### Prerequisites
- **Node.js**: Version 16.0 or higher
- **npm**: Version 8.0 or higher
- **MySQL**: Version 8.0 or higher (for backend implementation)
- **Git**: For version control

### Frontend Setup (Current Implementation)

#### 1. Clone and Install
```bash
# Clone the repository
git clone <repository-url>
cd military-asset-management

# Install dependencies
npm install
```

#### 2. Environment Configuration
Create a `.env` file in the root directory:
```env
# Development Configuration
VITE_APP_NAME=Military Asset Management System
VITE_APP_VERSION=1.0.0

# API Configuration (for future backend integration)
VITE_API_BASE_URL=http://localhost:3001/api
VITE_API_TIMEOUT=10000

# Authentication
VITE_SESSION_TIMEOUT=3600000
VITE_TOKEN_REFRESH_INTERVAL=300000

# Feature Flags
VITE_ENABLE_AUDIT_LOGS=true
VITE_ENABLE_REAL_TIME_UPDATES=false
VITE_ENABLE_NOTIFICATIONS=true

# Security
VITE_ENABLE_HTTPS=false
VITE_CORS_ORIGIN=http://localhost:3000
```

#### 3. Development Server
```bash
# Start development server
npm run dev

# The application will be available at http://localhost:5173
```

#### 4. Production Build
```bash
# Build for production
npm run build

# Preview production build
npm run preview
```

### Backend Setup (Implementation Guide)

#### 1. Project Structure
```bash
mkdir backend
cd backend
npm init -y

# Install dependencies
npm install express mysql2 sequelize bcryptjs jsonwebtoken
npm install helmet cors rate-limiter-flexible winston
npm install --save-dev nodemon jest supertest
```

#### 2. Database Setup
```bash
# Connect to MySQL
mysql -u root -p

# Create database
CREATE DATABASE mams_db;
USE mams_db;

# Run schema creation
source database/schema.sql;

# Insert sample data
source database/seed.sql;
```

#### 3. Backend Environment Configuration
Create `backend/.env`:
```env
# Server Configuration
NODE_ENV=development
PORT=3001
HOST=localhost

# Database Configuration
DB_HOST=localhost
DB_PORT=3306
DB_NAME=mams_db
DB_USER=mams_user
DB_PASSWORD=secure_password

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here
JWT_EXPIRES_IN=24h
JWT_REFRESH_EXPIRES_IN=7d

# Security
BCRYPT_ROUNDS=12
RATE_LIMIT_WINDOW=15
RATE_LIMIT_MAX_REQUESTS=100

# Logging
LOG_LEVEL=info
LOG_FILE=logs/mams.log
```

#### 4. Backend Server Structure
```javascript
// backend/src/index.js
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const rateLimit = require('express-rate-limit');

const authRoutes = require('./routes/authRoutes');
const dashboardRoutes = require('./routes/dashboardRoutes');
const purchaseRoutes = require('./routes/purchaseRoutes');
const transferRoutes = require('./routes/transferRoutes');
const assignmentRoutes = require('./routes/assignmentRoutes');

const app = express();

// Security middleware
app.use(helmet());
app.use(cors({
  origin: process.env.CORS_ORIGIN,
  credentials: true
}));

// Rate limiting
const limiter = rateLimit({
  windowMs: process.env.RATE_LIMIT_WINDOW * 60 * 1000,
  max: process.env.RATE_LIMIT_MAX_REQUESTS
});
app.use(limiter);

// Body parsing
app.use(express.json({ limit: '10mb' }));
app.use(express.urlencoded({ extended: true }));

// Routes
app.use('/api/auth', authRoutes);
app.use('/api/dashboard', dashboardRoutes);
app.use('/api/purchases', purchaseRoutes);
app.use('/api/transfers', transferRoutes);
app.use('/api/assignments', assignmentRoutes);

// Error handling
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Internal server error' });
});

const PORT = process.env.PORT || 3001;
app.listen(PORT, () => {
  console.log(`MAMS Backend running on port ${PORT}`);
});
```

### Database Schema Creation

#### 1. Create Schema File
Create `database/schema.sql` with all the table definitions provided in the Data Models section.

#### 2. Create Seed Data
Create `database/seed.sql`:
```sql
-- Insert sample bases
INSERT INTO bases (id, name, location, is_active) VALUES
('base-1', 'Fort Liberty', 'North Carolina, USA', TRUE),
('base-2', 'Camp Pendleton', 'California, USA', TRUE),
('base-3', 'Fort Bragg', 'North Carolina, USA', TRUE);

-- Insert sample users
INSERT INTO users (id, username, password_hash, name, email, role, base_id) VALUES
('user-1', 'admin', '$2b$12$hash...', 'System Administrator', 'admin@mams.mil', 'ADMIN', NULL),
('user-2', 'commander', '$2b$12$hash...', 'Colonel John Smith', 'commander@mams.mil', 'BASE_COMMANDER', 'base-1'),
('user-3', 'logistics', '$2b$12$hash...', 'Major Sarah Johnson', 'logistics@mams.mil', 'LOGISTICS_OFFICER', 'base-1');

-- Insert sample assets
INSERT INTO assets (id, name, type, serial_number, base_id, status) VALUES
('asset-1', 'M4A1 Carbine', 'WEAPON', 'W001234', 'base-1', 'AVAILABLE'),
('asset-2', 'HMMWV', 'VEHICLE', 'V567890', 'base-1', 'ASSIGNED'),
('asset-3', '5.56mm Ammunition', 'AMMUNITION', 'A789012', 'base-1', 'AVAILABLE');
```

### Testing Setup

#### 1. Frontend Testing
```bash
# Install testing dependencies
npm install --save-dev @testing-library/react @testing-library/jest-dom
npm install --save-dev @testing-library/user-event vitest jsdom

# Run tests
npm test
```

#### 2. Backend Testing
```bash
# In backend directory
npm install --save-dev jest supertest

# Create test files
mkdir tests
touch tests/auth.test.js tests/dashboard.test.js

# Run tests
npm test
```

---

## API Endpoints

### Authentication Endpoints

#### POST /api/auth/login
**Description**: Authenticate user and return JWT token

**Request Body**:
```json
{
  "username": "logistics",
  "password": "password123"
}
```

**Response**:
```json
{
  "success": true,
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user-3",
    "username": "logistics",
    "name": "Major Sarah Johnson",
    "role": "LOGISTICS_OFFICER",
    "baseId": "base-1"
  }
}
```

#### POST /api/auth/logout
**Description**: Invalidate user session

**Headers**: `Authorization: Bearer <token>`

**Response**:
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

### Dashboard Endpoints

#### GET /api/dashboard/metrics
**Description**: Get dashboard metrics for user's accessible scope

**Headers**: `Authorization: Bearer <token>`

**Response**:
```json
{
  "openingBalance": 500,
  "closingBalance": 487,
  "netMovement": -13,
  "totalAssigned": 45,
  "totalExpended": 8,
  "assetsByType": [
    {
      "type": "WEAPON",
      "count": 250,
      "available": 220,
      "assigned": 25,
      "maintenance": 3,
      "expended": 2
    }
  ],
  "recentActivities": [...]
}
```

### Purchase Management Endpoints

#### GET /api/purchases
**Description**: Get purchases list with filtering

**Headers**: `Authorization: Bearer <token>`

**Query Parameters**:
- `status`: Filter by purchase status
- `baseId`: Filter by base (Admin only)
- `page`: Page number (default: 1)
- `limit`: Items per page (default: 20)

**Response**:
```json
{
  "purchases": [
    {
      "id": "purchase-1",
      "assetType": "WEAPON",
      "assetName": "M4A1 Carbine",
      "quantity": 50,
      "unitPrice": 900,
      "totalAmount": 45000,
      "supplier": "Colt Defense LLC",
      "status": "APPROVED",
      "orderDate": "2024-01-15",
      "deliveryDate": "2024-02-01"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 45,
    "pages": 3
  }
}
```

#### POST /api/purchases
**Description**: Create new purchase request

**Headers**: `Authorization: Bearer <token>`

**Request Body**:
```json
{
  "assetType": "WEAPON",
  "assetName": "M4A1 Carbine",
  "quantity": 25,
  "unitPrice": 900,
  "supplier": "Colt Defense LLC",
  "orderDate": "2024-01-20",
  "notes": "Replacement rifles for training unit"
}
```

**Response**:
```json
{
  "success": true,
  "purchase": {
    "id": "purchase-123",
    "status": "PENDING",
    "createdAt": "2024-01-20T10:30:00Z"
  }
}
```

#### PUT /api/purchases/:id/approve
**Description**: Approve purchase request

**Headers**: `Authorization: Bearer <token>`

**Permissions**: `approve_purchases`

**Response**:
```json
{
  "success": true,
  "purchase": {
    "id": "purchase-123",
    "status": "APPROVED",
    "approvedBy": "user-2",
    "approvalDate": "2024-01-20T14:30:00Z"
  }
}
```

### Transfer Management Endpoints

#### GET /api/transfers
**Description**: Get transfers list

**Headers**: `Authorization: Bearer <token>`

**Response**:
```json
{
  "transfers": [
    {
      "id": "transfer-1",
      "assetId": "asset-1",
      "fromBase": {
        "id": "base-1",
        "name": "Fort Liberty"
      },
      "toBase": {
        "id": "base-2",
        "name": "Camp Pendleton"
      },
      "quantity": 10,
      "status": "COMPLETED",
      "requestDate": "2024-01-20",
      "completionDate": "2024-01-25"
    }
  ]
}
```

#### POST /api/transfers
**Description**: Create transfer request

**Headers**: `Authorization: Bearer <token>`

**Request Body**:
```json
{
  "assetId": "asset-1",
  "toBaseId": "base-2",
  "quantity": 5,
  "notes": "Equipment transfer for training exercise"
}
```

### Assignment Management Endpoints

#### GET /api/assignments
**Description**: Get asset assignments

**Headers**: `Authorization: Bearer <token>`

**Response**:
```json
{
  "assignments": [
    {
      "id": "assignment-1",
      "assetId": "asset-2",
      "assetName": "HMMWV",
      "assignedTo": "Sergeant Williams",
      "assignmentDate": "2024-01-22",
      "status": "ACTIVE",
      "purpose": "Patrol operations"
    }
  ]
}
```

#### POST /api/assignments
**Description**: Create new assignment

**Headers**: `Authorization: Bearer <token>`

**Request Body**:
```json
{
  "assetId": "asset-2",
  "assignedTo": "Sergeant Williams",
  "purpose": "Patrol operations",
  "expectedReturnDate": "2024-02-22",
  "notes": "Regular maintenance required weekly"
}
```

#### PUT /api/assignments/:id/return
**Description**: Return assigned asset

**Headers**: `Authorization: Bearer <token>`

**Response**:
```json
{
  "success": true,
  "assignment": {
    "id": "assignment-1",
    "status": "RETURNED",
    "actualReturnDate": "2024-01-25T09:00:00Z"
  }
}
```

### Audit Endpoints

#### GET /api/audit/logs
**Description**: Get audit logs (Admin only)

**Headers**: `Authorization: Bearer <token>`

**Permissions**: `view_audit_logs`

**Query Parameters**:
- `action`: Filter by action type
- `userId`: Filter by user
- `startDate`: Start date filter
- `endDate`: End date filter
- `page`: Page number
- `limit`: Items per page

**Response**:
```json
{
  "logs": [
    {
      "id": "audit-1",
      "action": "ASSET_ASSIGNED",
      "entityType": "ASSIGNMENT",
      "entityId": "assignment-1",
      "userId": "user-3",
      "userName": "Major Sarah Johnson",
      "timestamp": "2024-01-22T10:30:00Z",
      "details": {
        "assetName": "HMMWV",
        "assignedTo": "Sergeant Williams"
      }
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 50,
    "total": 234,
    "pages": 5
  }
}
```

### Error Response Format

All API endpoints return errors in a consistent format:

```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": {
      "field": "quantity",
      "issue": "Must be a positive integer"
    }
  },
  "timestamp": "2024-01-20T10:30:00Z",
  "requestId": "req-123456"
}
```

### Common HTTP Status Codes

- **200 OK**: Successful request
- **201 Created**: Resource created successfully
- **400 Bad Request**: Invalid request data
- **401 Unauthorized**: Authentication required
- **403 Forbidden**: Insufficient permissions
- **404 Not Found**: Resource not found
- **409 Conflict**: Resource conflict (e.g., duplicate serial number)
- **429 Too Many Requests**: Rate limit exceeded
- **500 Internal Server Error**: Server error

---

This documentation provides a comprehensive technical overview of the Military Asset Management System, covering all aspects from architecture to implementation details. The system is designed with security, scalability, and military operational requirements in mind.