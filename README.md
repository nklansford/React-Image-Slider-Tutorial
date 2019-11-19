# React-Image-Slider-Tutorial
Learn about how I made my React Image Slider. Mini-course below!

## Tools Used :wrench: :nut_and_bolt:
- [Atom](https://atom.io/)
- [platformio-ide-terminal](https://atom.io/packages/platformio-ide-terminal)
- [Node.js](https://nodejs.org/en/) (assumed it is installed on your machine in these instructions)



# :zap: Make Your Own React Image Slider :zap:

## Setting Up Your Project :octocat: :wrench:

<!-- - [Clone this project](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository) onto your own machine. -->

- Locate the folder where you want the project to live on your machine in the terminal.
  - If you have [platformio-ide-terminal](https://atom.io/packages/platformio-ide-terminal) installed in [Atom](https://atom.io/): open a project folder in an Atom window and open your terminal in the editor. You should see your name and project name on the line you are typing on.
  - If you do not have it and would not like to download it, then navigate to your folder in your machine's [built in terminal/shell](https://www.macworld.com/article/2042378/master-the-command-line-navigating-files-and-folders.html).


- Now that you are in the correct folder in the terminal, enter this command `npx create-react-app react`. This will create a new project folder that has the React framework in it.

- `cd` into new directory

- enter `npm start` in the terminal
- you should be seeing a sample react page something like this:
<img src="images/tutorial-images/React-Starter-Page.png" />

- ### Delete the following :no_good:
  - `apps-test.js`

  - `serviceWorker.js`

  - `App.test.js`

  - `public/logo.svg`

  - In `index.js` delete the following lines of code:
    - `import * as serviceWorker from './serviceWorker';`
    - ```
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();```


- ### Create the following :nut_and_bolt:
  - In the `src` folder, add two folders:
    - `components`

    - `data`

  - Inside `components` create the following files:
    - `ImageSlider.jsx`

    - `ImageSlider.css`

    - Move `App.css` into this folder

    - Move `App.js` into this folder and rename it to `App.jsx` (This is more accurate as this is the language/semantics we will be using)

  - Inside `data` create the following files:

    - `images.js`

    - Your file structure should look like this:
    ```
    src
    |
    |--components
    |    |
    |    |--App.css
    |    |--App.jsx
    |    |--ImageSlider.css
    |    |--ImageSlider.jsx
    |
    |--data
    |    |--images.js
    |
    |--index.js
    |--index.css
    ```
    The rest of the files should remain in the same location/naming.

  - This would be a good time to set up a GitHub repo and make an initial commit on your master branch, create a develop branch, and start working on develop.

  - Go to the `student materials` above and download `images`. In your file tree, find the `public` folder, create an `image` folder, and put both downloaded folders (`icons` and `tiles`) in `images` in your project.

## Laying the Foundation :boom: :house:

Now we will actually setup the internal parts of the files you just created and think about some concepts of React.

### What is React :question:

It is a JavaScript library for building user interfaces [(see the React website)](https://reactjs.org/). Unlike other JS libraries that you may have been exposed to in other courses (such as JQuery) this will completely change your entire file tree. Take another look at your project folder `src`. *GASP*! THERE IS NO `index.html`! Wha? But there is an `index.js`.

The 1000 foot view is that all of your "html" and markup will be in various JavaScript (and JavaScript XML) files. But it will be rendered as if it were just normal html in the DOM.

So if you are like me, you may be thinking along the lines of JonTron in his FlexTape video...
<br />
<img src="images/tutorial-images/jontron.jpg" />

Also, this oddly hilariously ABSOLUTELY NEVER relevant reaction:

<img src="images/tutorial-images/jontron-3.gif" />

Why would I make my life harder like this when I could just you know... PUT IT IN AN HTML FILE AND IT ALREADY RENDERS LIKE HOW IT LOOKS IN THE FILE? What are you tryna pull React?

So here are some reasons why you may find this actually pretty amazing tool useful:
- It makes app building simpler
- You can make widgets easier
- instead of messing with traversal in JQuery, you can just write the action in the html and vice versa

In other words,
<img src="images/tutorial-images/jontron-2.jpg" />



  - Another important aspect is that React uses JS and also JSX (as seen by the file endings in your file tree). JSX is a language that allows you to write html in javascript statements and javascript in html tags by utilizing a specific syntax. Browsers do not understand it, so it will be compiled into regular JS in a "React DOM" and then to the browser's DOM.

  As we build this image slider component I think you will see why React becomes really useful and cleaner than you expect.

## Set up your files :construction:

Okay, so when react set up your project, it did some of the dirty work (file setup) for you. Here is what you will need to do next in your actual files.

- In `index.js` modify your code to match:
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './components/App';
ReactDOM.render(<App />, document.getElementById('root'));
```
Think about this being comparable to how SASS organizes your stylesheets so that you have one big import location and then other subfiles that have the actual information and structure. This file's job is going to be to import the React library, tell it to compile, and pay attention to your other files.

  - The line `ReactDOM.render(<App />, document.getElementById('root'));` is a good way to introduce jsx. It stands for Javascript XML. If you remember from Scripting for Interactivity, XML could be described as a less-specific HTML. In other words, HTML is a type of XML. In XML you can create your own tags and assign them a purpose or rule. (Perhaps a helpful analogy is how you can create classes in CSS and assign them meaning.) JSX utilizes that idea and mixes in the functionality of Javascript. So this line of code might read in english, "Hey React! I want you to tell the browser to show the contents of `App.jsx` as if it were placed where `id="root"` occurs."

  - Your next question should be how does it know `app` is a thing and where is `id="root"`?

    - Let's talk about `root` first since it is easier to explain. REACT MADE ROOT FOR YOU! Wasn't that nice of it? You may have noticed that in the `public` folder there is an actual `index.html` file. This is where a lot of the React defaults and compiling setup happens. Again, it's *not* for your main content.
      - (Maybe a helpful Comparison: You don't put your styles into `styles.css` when using SASS. Instead, you have `styles.scss` which imports all of the rules in your subfiles. In React, it gets ready to compile in `index.html`, pulls from `index.js`, which pulls from your other files. A key difference is that you will not be able to see the full compiled version in `index.html` like you can in SASS. Remember, this tells the React DOM to communicate with the browser DOM. So, your best bet in figuring out errors are your terminal and browser console. (NOTE: you don't have to use this built in feature of pointing to `root` in the html template. However, for one page that has one component it keeps things simpler.)
      - For our purposes, just know that `root` is a container on a plain webpage.
