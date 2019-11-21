# React Image Slider Tutorial
Learn about how I made my [React Image Slider](https://github.com/nklansford/react-image-slider). Mini-course below!

## Tools Used :wrench: :nut_and_bolt:
- [Atom](https://atom.io/)
- [platformio-ide-terminal](https://atom.io/packages/platformio-ide-terminal)
- [Node.js](https://nodejs.org/en/) (assumed it is installed on your machine in these instructions)



# :zap: Make Your Own React Image Slider :zap:

## Setting Up Your Project :octocat: :wrench:

<!-- - [Clone this project](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository) onto your own machine. -->

- If at any time you get lost or are confused about how a file should look, feel free to view my [finished project](https://github.com/nklansford/react-image-slider).

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
    - ```JavaScript
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

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

  - This would be a good time to set up a GitHub repo and make an initial commit on your master branch, create a develop branch, and start working on develop. (note that you will need to change the `name` field in `package.json` to your project name. Make sure that it is a web-safe name).

  - DOWNLOAD: Go to the `student materials` above in this repo and download `images`. In your file tree, find the `public` folder, create an `image` folder, and put both downloaded folders (`icons` and `tiles`) in `images` in your project.

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

(but actually though... I don't think I have ever been mad at anyone named Phil :thinking: )

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

- In `App.jsx` modify your code to match:
```
import React from 'react';
import ImageSlider from './ImageSlider';
import './App.css';
import data from '../data/images';
function App() {
  return (
    <>
      <h1 className="image-slider-title">Let it snow, let it snow</h1>
      <ImageSlider images={data}/>
    </>
  );
}
export default App;
```
- In `index.js` modify your code to match:
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './components/App';
ReactDOM.render(<App />, document.getElementById('root'));
```
- Save and make sure that you don't have any errors in your terminal. I would recommend keeping your Atom terminal open so that you can see if it is refreshing the page or throwing errors. If it throws an error make sure you look at the terminal, it has pretty smart suggestions.

Let's take a closer look at `index.js`. This is where all of the imports from the other files come together. Think about this being comparable to how SASS organizes your stylesheets so that you have one big import location and then other subfiles that have the actual information and structure. This file's job is going to be to import the React library, tell it to compile, and pay attention to your other files, as well as another very imporant element that we will discuss below:

  - The line `ReactDOM.render(<App />, document.getElementById('root'));` is a good way to introduce jsx. It stands for Javascript XML. If you remember from Scripting for Interactivity, XML could be described as a less-specific HTML. In other words, HTML is a type of XML. In XML you can create your own tags and assign them a purpose or rule. (Perhaps a helpful analogy is how you can create classes in CSS and assign them meaning.) JSX utilizes that idea and mixes in the functionality of Javascript. So this line of code might read in english, "Hey React! I want you to tell the browser to show the contents of `App.jsx` as if it were placed where `id="root"` occurs."

  - Your next question should be how does it know `app` is a thing and where is `id="root"`?

    - Let's talk about `root` first since it is easier to explain. REACT MADE ROOT FOR YOU! Wasn't that nice of it? You may have noticed that in the `public` folder there is an actual `index.html` file. This is where a lot of the React defaults and compiling setup happens. Again, it's *not* for your main content.

      - In React, your project gets ready to compile in `index.html`, which gets infomation from `index.js`, which pulls from your other files. (Maybe a helpful Comparison: You don't put your styles into `styles.css` when using SASS. Instead, you have `styles.scss` which imports all of the rules in your subfiles.) A key difference is that you will not be able to see the fully compiled version in `index.html` like you can in SASS. Remember, this tells the React DOM to communicate with the browser DOM. So, your best bet in figuring out errors are your terminal and browser console. (NOTE: you don't have to use this built in feature of pointing to `root` in the html template. However, for one page that has one component it keeps things simpler.)

      - For our purposes, just know that `root` is a container on a plain webpage.

    - `App` is the element that is to be rendered in `root`. See  `import App from './components/App';` on the 4th line of your code in `index.js`. This is a function that becomes an element to be the default export in `App.jsx`. Open `App.jsx` and see what I mean. See how it is a function: `function App()` and also the default export: `export default App;`. Because it is a named function, it can be treated as a callable element in React.
  - Now let's take a look at the part that has all of the content! (Also, don't forget to commit your code to `develop`!)

## Let's Code! 👩‍💻👨‍💻

Something to note about this project is that we are working from a finished product, backwards and then forward again. This means that I am looking at things that I built and then rebuilding them. So, some things are already setup that are not necessarily a rule of React or something that you should *just know* or *always do*. With that in mind, let's look at our good ol' `App.jsx` file. See the line `<ImageSlider images={data}/>`. This is one of those instances! This is just how I set up this project and is by no means the only way of building this component. I will walk you through building the other files the way that I chose to set it up based on what I learned about React. Just keep in mind the principles you learn here and know that the setup and possibilities can be endless!

### Image Setup 	🖼
Let's start with `src/data/images.js`! We'll set it up and look at how we connect it back to `App.jsx`.

- Open the file. Ahh, a completely blank file. How terrifying. Okay, for real, TAKE A DEEP BREATH DESIGNER, you can do it.

- So, this is what we want out of the image slider: we want one image to be seen at a time with a forward and back arrow that shows a new picture depending on the arrow you click. Essentially it is a list of images being shown one at a time by using arrows.

- So, we need a list of images. You could make an html list, which would be perfectly acceptable, but in this case I used an array of images. We'll make a json list in our `.js` file. So, we could make a list called `data` that lists the images and then do an `export default data;` at the bottom of the file similar to the setup in `App.js`. However, a shorthand is to create it this way:
  - ```
  export default [
      "./images/tiles/bork.png",
      //enter the rest of the images here!
  ];
    ```
  - Once you enter in the rest of the image files, this file is set!

- It connects to `App.jsx` through the line that is seen in `App.jsx`:  `import data from '../data/images';`. Since the image list is the only thing in the file and we set it to the default export, you are able to name the import in `App.jsx` something meaningful and it will import the default from `images.js`.

- Notice the line in `App.jsx`: `<ImageSlider images={data}/>` calls the information from data. We will come back to that line and what it means in the next section, but it is good to notice that our images are being called here.

### Image Slider :dizzy:

- The first thing we will want to do is import our necessary content from the other files. We know that we will eventually want to style it so add these two lines at the top of your file:
```
import React from 'react';
import './ImageSlider.css';
```

#### Getting in the Images
- We know that we want to see our images. We also know that we want to see the forward and backward arrows on each side of the image. So, we can enter We see things by using `render()`. Enter this code in `ImageSlider.jsx` below your imports.
```
render() {
  return (
    <div className="image-slider">
      <img className="image-slider__arrow slider__arrow--previous" alt="show previous" src="./images/icons/previous-arrow.png" />
      <img className="image-slider__image" alt="" src="#" />
      <img className="image-slider__arrow slider__arrow--next" alt="show next" src="./images/icons/next-arrow.png" />
    </div>
  );
}
```
Yay! Looks like html wrapped inside javascript! Notice that one difference is that classes in jsx have to be `className` since `class` is something different in this language.

- Notice on the line `<img className="image-slider__image" alt="" src="#" />` that `src` has a placeholder. Go ahead and replace the placeholder with `{currentImage}`. I wanted you to put that in yourself to bring special attention to it. Right now, that doesn't do anything; it is what we are building next. We want this to be our list of images from `images.js`. We will make something called a constructor so that we can organize what we see from the list. Enter this block of code above the previous block of code, but still under the imports:
```
class ImageSlider extends React.Component {
  constructor() {
    super();
      this.state = {
        currentIndex: 0
      }
  }
```
The constructor says that we only want to see the first image in the list from images. Remember that `images.js` is an array. This means that each item has an inherent index starting with `0`. So, we are simply saying to select the first one. Notice that it is not connected to our other block of code yet.

- To connect the two, we will need to specify `images` and the `currentIndex`. Inside `render(){}` right above `return (` enter this code:
```
const { images } = this.props;
const { currentIndex } = this.state;
const currentImage = images[currentIndex];
```
This is where I will bring up props. Props are a key element in React. Take a look at `App.jsx` again. See the line `<ImageSlider images={data}/>`. `images` is called a prop, short for property. You can name this whatever you want. Much like a class in css, you can call it whatever and specify it's meaning later either in the same file or in a sepearte one. We named this prop `images` and will treat it much like a regular html `src`. We are already passing in the images from `data` to the prop. But now, with the added lines in `ImageSlider.jsx` (Go ahead and look at that file again) that you just entered, the `image` prop is being told to only show the `currentIndex`. Note that the `currentIndex` is `0` as specified further up the file. In short, you are passing in the list of images, starting at the top of your list!

#### Getting in the Arrows

- Now, we will want the ability to use the arrows to get to the other images. We already have the arrow images in our `ImageSlider.jsx` file, so they are technically there. However, we need them to be functional. We will start with the forward arrow. Let's make a function that tells an object to move the `currentIndex` forward by `1` when it is clicked and also loop back to the first image if we reach the end of the list. We will worry about creating the logic first and then "link" it to the element once we are done.

- We are dealing with our image prop again so we will tell the function that we are talking about it and specifically, the `length` of it (Helpful note: `length` refers to the the numbers that are inherently assigned to each object in an array. EX: `0`,`1`,`2`....). In `ImageSlider.jsx`, enter this code right above `render () {`:
```
indexForward = () => {
  const length = this.props.images.length;
}
```
Enter into a new line right beneath `const length = this.props.images.length;`.

- We will want an if-else statement that says "If the index is `0` through the last image, go forward one. Otherwise go back to the first image in the list." Enter this code on your new line beneath `const length = this.props.images.length;`:
```
if(this.state.currentIndex < length - 1){
  this.setState({
    currentIndex: this.state.currentIndex + 1
  });
} else {
  this.setState({
    currentIndex: 0
  });
}
```
All together your function should look like:
```
indexForward = () => {
  const length = this.props.images.length;
  if(this.state.currentIndex < length - 1){
    this.setState({
      currentIndex: this.state.currentIndex + 1
    });
  } else {
    this.setState({
      currentIndex: 0
    });
  }
}
```

- Now, copy and paste that whole function right underneath itself. Change `indexForward` to `indexBackward`.
- We want the reverse functionality of the first function so we will some lines in the `if else` statement. We now want our function to say, "If the index is more than the first one, go back one image. Otherwise go back to the last image."
  - Change the `if` statement to:
  ```
  if(this.state.currentIndex > 0){
    this.setState({
      currentIndex: this.state.currentIndex - 1
    });
  ```
  - Change the `else` statement to:
  ```
} else {
    this.setState({
      currentIndex: length - 1
    });
  ```
- Now we need to connect our logic to the actual arrow elements. The beauty of React is that we can add the `onClick` event listener right into the "html" element.
  - In `<div className="image-slider">` Find the backward arrow image. Right in between `<img` and `className` enter the code `onClick={this.indexBackward}`.
  - Find the forward arrow image and in the same spot enter `onClick={this.indexForward}`.

  - Wasn't that super satisfying? NO TRAVERSAL. No more `child.next.previous.help.idk.where.i.am.anymore();`

#### Final Touches

- At the very bottom of your `ImageSlider.jsx` remember to export it by entering `export default ImageSlider;`

- In `index.css` add the following styles:
```
@import url('https://fonts.googleapis.com/css?family=Megrim&display=swap');
body {
  width: 380px;
  margin: 80px auto;
}
```
This will get the google font in the styles and center your element.

- In `ImageSlider.css` add the following styles:
```
  .image-slider {
  display: flex;
  flex-flow: row wrap;
  width: 380px;
  justify-content: space-between;
}
.image-slider__arrow{
  display: block;
  align-self: center;
}
.image-slider__image {
  padding: 0px;
}
```
This establishes the layout.

- In `App.css` add the following styles:
```
.image-slider-title {
  font-family: 'Megrim', cursive;
  text-align: center;
}
```
This styles the header.

- Note: single broken up stylesheets are considered best web practice now rather than one alphabetized stylesheet. It is easier to come back to later and can make it easier to repeat elements. (Similar idea to SASS)
