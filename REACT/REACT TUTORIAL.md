
- React is a ==JavaScript Library==
###  Library vs Framework
- Library - Predefined code 
- Framework - It is a template , Gives a structure

#### React vs React Js vs React native
 - React and React Js are same.
 - React can be used using JavaScript and TypeScript
 - React using JavaScript is said to be React Js
 - React native is used to build cross platform applications like android app, ios app
 - The competitor of react native is flutter
 - React native is a framework

#### Components
 - A React component is a reusable piece of code responsible for rendering a part of the user interface
 - React follows a component based development
 - A component can be of a button or to the entire page
 - we can reuse a component 
 - A component is self contained because we write the logic inside the component for how the component should behave .

#### Virtual DOM
- DOM is document object model
- React takes the copy of DOM as Virtual DOM 
 ![[Pasted image 20250627093845.png]]
 - If a change is made it does not update in the Actual DOM it update the virtual dom and compare the actual DOM with the DIFF 
 - After comparing it only updates the changed or updates part in the Actual Dom
 - This reduces the Time and makes it Efficient 

#### Single Page Application(SPA)

- Take an Example of Google maps
- If you click layers it does not load the page to change the view from normal view to satellite view 
- In a same page by replacing a component with another component and loading it .

#### Props
- props is a property and an input for our component
- the data can be passed from one component to another component using these props
- props are immutable 
- props are like passing a parameter into an function 
- We can reuse a component by passing props to the component
- We should use a defaultProps if we don't pass an props to an component 
-  the default props can be sent directly to the constructor of our component. Thus, the props need to be added to the reactDOM.render by us.

#### Conditional Rendering 
- the process of delivering elements and components based on certain conditions.
- An `if...else` block can be used 
- 














1) Create a Folder and open it in VS CODE
2) open the terminal and enter the command
```node
npm create vite@latest
```
3) Click yes and type ==client== for project name 
4) select the framework as ==react== 
5) select the variant as ==Javascript==
6) now run the below commands
```node
cd client
npm install
npm run dev 
```
7) open the App.jsx file and clear the contents and type ==rafce== (create a basic component structure)
8) clear the contents in the index.css 
9) Inside the ==src== create folders:
   - assets - contains the assets for our project like images and icons
   - components - contains components for our website
   - pages - contains various pages of our webpage
   - context - stores state variables and functions that can be used in various Components.
10) Install tailwind in our project 
   ```node
npm install tailwindcss @tailwindcss/vite
```
11)  In the ==vite.config.ts== file add this plugins
```node
import tailwindcss from '@tailwindcss/vite'
export default defineConfig({ plugins: [ tailwindcss(), ],})
```
12) In the index.css file add this 
```css
@import "tailwindcss";
```
13) In the terminal write this code to add the packages
```node
npm install react-router-dom //used to create routing in our project
npm install react-hot-toast // used to get toast notifications
```
14) For the fonts go for google fonts and select the required font and select ==get embedded code== and paste the code in index.css file
15) In the index.css file after adding the font 
    ```node
*{

  font-family: "Outfit", sans-serif;;

}
:root {

  --color-primary: #4fbf8b;

  --color-primary-dull: #44ae7c;

}
```
16) In the ==main.jsx== file import this and change the StrictMode to BrowserRouter
```node
import { BrowserRouter } from 'react-router-dom'
```