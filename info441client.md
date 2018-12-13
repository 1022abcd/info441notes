# Sections
- [Essential Html](#essentia-html)
- [Introduction to Javascript](#introduction-to-javascript)
- [Javascript Functions](#javascript-functions)
- [The Document Object Model (DOM)](#the-document-object-model)
- [Event-Driven Application Architecture](#event-driven-application-architecture)
- [AJAX](#ajax)
- [MVC](#mvc)


# Essential HTML 

HTML is an acronym that stands for **H**yper **T**ext **M**arkup **L**anguage.

> `<!DOCTYPE html>`

That tells any program that reads this file to interpret the contents as HTML version 5 syntax.

The rest of an HTML document is a simple tree of **elements** which is made of nodes.

- Root -> Parent -> Child ->Leaf

- The nodes in an HTML document tree are known as **elements**.

#### Attributes
- The start tag of an element may also contain one or more attributes, which are used to specify options, provide additional information, or add subtler shades of meaning to an element.

---

# Introduction to Javascript

### let vs var

- **let** is block-scoped
```Javascript
    var x = 5;
    if (x > 0) {
        let x = 1;
        x = x + 1;
    }
    x //prints out 5
```

- **var** is not block-scoped 
```Javascript
    var x = 5;
    if (x > 0) {
        var x = 1;
        x = x + 1;
    }
    x //prints out 2 
```

### Constants
- It's used for declaring constants, which are variables that may be assigned a value only once.

>const ISCHOOL_URL = "https://ischool.uw.edu";

The key difference is that the value assigned to a constant may not change during the lifetime of the program. Attempting to do so will generate a runtime errors. 

### Strict Mode 
- It can be enabled by adding **"use strict";** to the top of your script, or to the top of a particular function.
- Older interpreters will simply evaluate this as a string literal that you never assign to a variable, so it effectively gets ignored. 
- But newer interpreters that implement strict mode interpret this as a signal to switch into strict mode. 
```Javascript
    //set the interpreter into strict mode
    "use strict";
    //declare a variable named `firstName`
    let firstName;
    //set the variable, 
    fistName = "Mary";

    firstName; //ReferenceError: fistName is not defined
```

### Objects
- In JavaScript an object is really just a **hash table**, which is a data structure that stores a set of **key-and-value pairs**. 
```Javascript
    //creates a new object with three properties
    let player = {
        firstName: "Mary"       //properties can be of any type
        lastName: "Rodriguez",  //and are separated by commas
        ranking: 4              //the last one having no trailing comma
    };

    //you can get the value associated with a key
    //using the `.` syntax
    player.firstName; // => "Mary"
```

#### Properties
Add
```Javascript
    //getting a value for a key that doesn't yet exist
    //just returns `undefined` with no error
    player.email; // => undefined

    //add a new key/value pair to the object
    player.email = "maryr@example.com";

    //get the value associated with that new key
    player.email; // => "maryr@example.com"
```

Delete
```Javascript
    //delete the key "email" and its associated value
    delete player.email;

    //getting the value for the key "email"
    //now returns `undefined`
    player.email; // => undefined
```

HasOwnProperty
```Javascript
    //test whether the key "email" exists
    if (player.hasOwnProperty("email")) {
        // "email" key/value exists in the object
    } else {
        // no "email" key/value in the object
    }
```

Object with Array
```Javascript
    let propName = "ranking";

    //get value associated with a key
    //that is stored in a variable
    player[propName]; // => 4


    //same syntax is used if the key is
    //not a legal JavaScript identifier
    player["key with spaces"] = "some value";

    ex:
    player["address"] = "1612 9th Ave NE" //adds new key/value pair
    player.address //print "1612 9th Ave NE"
```

### Ternary Condition Operator
if/else
>expression ? value-expression-if-true : value-expression-if-false;
```Javascript
    let y;
    if (x) {
        y = "foo"
    } else {
        y = "bar"
    }

    //Equal To
    let y = x ? "foo" : "bar";
```

### Passing Functions to Fucntions
```Javascript
    //returns a negative number if n1 < n2,
    //zero if n1 equals n2,
    //or a positive number if n1 > n2
    function compareNums(n1, n2) {
        //just subtract n2 from n1
        return n1 - n2;
    }

    let nums = [10,5,7,3,1,11,2,4,6,12,9,8];
    //sort with no comparison function 
    //sorts alphabetically as strings
    console.log("alphabetically");
    console.log(nums.sort());

    //sort with compareNums as the comparison 
    //function so they sort numerically
    console.log("numerically");
    nums.sort(compareNums); //[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 ]
```

### Closures
```Javascript
    //returns a negative number if n1 < n2,
    //zero if n1 equals n2,
    //or a positive number if n1 > n2
    function compareNums(n1, n2) {
        //just subtract n2 from n1
        return n1 - n2;
    }

    // `comparator` is a sort comparison function
    // (i.e., takes two array elements and returns a number)
    function ascending(comparator) {
        //return a new sort comparison function...
        return function(elem1, elem2) {
            //that invokes `comparator` and negates the result
            // (i.e., if comparator() returns a positive number,
            // we return a negative number and vice versa).
            return comparator(elem1, elem2);
        };
    }

    let nums = [10,5,7,3,1,11,2,4,6,12,9,8];
    //use `ascending()` to create a new comparison
    //function that negates compareNums()
    let compareNumsDesc = ascending(compareNums);

    //sort using the new descending comparator
    nums.sort(compareNumsDesc); 
    // These method is equivalent to 'Passing functions to functions'
    // example. It will return
    // [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 ]
```
---

# Javascript Functions

### Slicing
- The **.slice()** method takes two parameters: the array index to start at, and the array index to go up to but not include.

```Javascript
    let top10Females = BABYNAMES.filter(isFemale)
    .sort(byCountDescending)
    .slice(0,10);
    // will return first 10 elements in the array.
```

### Mapping
- A mapping operation transforms each element of the array by passing that array element through a function you provide (known as a transformer). 
- The **.map()** method in this example will create a new array for the outputs that is the same size as the input array,

```Javascript
    function addOne(value) {
        return value + 1;
    }

    var evens = [0,2,4,6,8,10];
    evens.map(addOne); // => [1,3,5,7,9,11]
```

### Reducing
- While mapping transforms each element into an array of the same size as the input array, reducing reduces the elements of an array to a single value.

```Javascript
    //returns the sum of `accumulator` and `num`
    function sum(accumulator, num) {
        return accumulator + num;
    }

    //create an array of a few numbers
    let nums = [1,2,3,4,5];

    //calculate the sum of all the numbers
    nums.reduce(sum, 0); // => 15
```

# The Document Object Model
When the browser executes a script, it adds a few objects to the global name space that are just "there." You don't have to create these objects or load them from anywhere—they are simply available because the browser added them before running your script.

- The **DOM**(global object) contains a JavaScript object for each element in your web page, organized in a tree data structure just like the elements.
- The root of that tree is accessible via a browser-supplied global variable named **document**. 
- That **variable** is an object that represents the entire page, and it has many properties and methods you can use to traverse, interrogate, and even manipulate the elements within then page.

### Getting References to Elements

A reference to the element with an **id** attribute
```Javascript
    // id attribute set to first-name-input:
    var nameInput = document.getElementById("first-name-input");
```

A reference to the element with the **style class**
```Javascript
    // element with the style class output-paragraph:
    var outputPara = document.querySelector(".output-paragraph");

    // select all hyperlink elements
    var links = document.querySelectorAll("a");
```

### Listening for Events
- **.addEventListener()** will add a function to the list of listeners for that event. You can add multiple functions for the same event, and the browser will call all of them, in the order they were added.

```Javascript
    //get a reference to the button element
    var button = document.querySelector("button");

    //tell the browser to call the inline anonymous function
    //whenever the "click" event occurs
    button.addEventListener("click", function() {
        console.log("my button was clicked!");
    });
```

```Javascript
    //To register a one-time event listener, just pass a JavaScript object with a property named once set to true as the third parameter:

    //tell the browser to call the inline function
    //only once after the next click
    button.addEventListener("click", function() {
        console.log("my button was clicked!");
    }, {once: true});
```

# Event-Driven Application Architecture

### State
-  At any moment, this state determines where the program is at and what it will do next.
- This state is stored in the program's variables and function parameters.
- In a browser-based JavaScript application, the program's state is commonly held in one global (or top-level scope) object that has one property for each state value you need to track.

---

### Event-Driven Programming
- Interactive applications, on the other hand, allow the user to modify the program's state while it's running via various input methods (keyboard, mouse, gesture, specialized controller, voice, etc.). 
- These programs are typically written in an event-driven programming style, where the program has two distinct phases:
    - The **initialization phase**, during which the program initializes its state and adds various event listener functions. These event listener functions will be invoked whenever the requested event occurs (e.g., mouse click, key press, page scroll, timer, etc.)
    - The **event phase**, during which the program waits for those events to occur. Each time an event occurs, the corresponding event listener function is invoked. That function in turn modifies the program's state, and updates the screen to match.

### Rendering

- To make the state visible on screen, we need to create some HTML elements, and write a function that synchronizes those elements' attributes with the current application state values. 
```Javascript
    //select the elements once at startup
    let circle = document.querySelector("svg circle");
    let rect = document.querySelector("svg rect");

    //render will render the state to the page elements
    function render(state) {
        //adjust element attriutes to match current state
        circle.setAttribute("cx", state.ball.x);
        circle.setAttribute("cy", state.ball.y);
        rect.setAttribute("y", state.paddle.y);
    }

    // also you can render the initial state
    render(state);
```
### Event Listeners

After initializing and rendering the state, the program would next need add event listeners for at least two events:

```Javascript
    function animate(){
        
    }
    //call animate() every 16 milliseconds
    state.ballTimer = setInterval(animate, 16);
```
```Javascript
    function adjustPaddle(eventObj){

    }
    document.body.addEventListener("mousemove", adjustPaddle)
```

---

# AJAX
- It is an acronym for **A**synchronous **J**avascript **A**nd **X**ML.
    - The HTTP request is done asynchronously, and your code provides a callback function, which is invoked once the server responds.

### JSON
- It is an acronym for **J**ava**S**cript**O**bject**N**otation.

### Fetch Data
1. The XMLHttpRequest object allows JavaScript developers to request JSON or XML-encoded data from the server, but the programming interface it exposed is quite complex to use.

```Javascript
    //create a new XMLHttpRequest object
    var request = new XMLHttpRequest();

    //configure it to do an asynchronous GET request for some URL
    request.open("GET", "/my/data/url", true);

    //add a listener for the "load" event, which
    //will happen when the data returns
    request.addEventListener("load", function() {
        if (request.status >= 200 && request.status < 400) {
            // Success!
            var data = JSON.parse(request.responseText);
        } else {
            // We reached our target server, but it returned an error
            //handle error...
        }
    });

    //add a listener for the "error" event, which
    //will happen if there was a network error
    request.addEventListener("error", function() {
        //handle error...
    })

    //finally, send the request to the server
    request.send();
```

2. Using jQuery library
```Javascript
    //assuming that the jQuery library has been added to the page...
    //second parameter is a function to be called when the request
    //is complete and the data has been returned
    $.getJSON("/my/data/url", function(data) {
        //`data` is the already-parsed JSON data returned from the server
    });
```

3. Using the **fetch()** function
```Javascript
    var promise = fetch("/my/data/url");

    //add a function to be called when the request completes successfully
    promise.then(function(response) {
        //parse response as JSON
        return response.json();
    });

    //Equivalent to 
    fetch("/my/data/url").then(function(response) {
        //parse response as JSON
        return response.json();
    });
```

**Full Example of Fetching**
```Javascript
    //last 24-hours of data from Fremont Bridge bike traffic
    var dataURL = "https://data.seattle.gov/resource/4xy5-26gy.json?$order=date%20desc&$limit=24";

    function parseAsJSON(response) {
    return response.json();
    }

    function handleError(err) {
    console.error(err);
    alert(err.message);
    }

    function renderRecord(record) {
    var tr = document.createElement("tr");
    var td = tr.appendChild(document.createElement("td"));
    td.textContent = moment(record.date).format("lll");
    
    td = tr.appendChild(document.createElement("td"));
    td.textContent = record.fremont_bridge_nb;
    td.classList.add("numeric");

    td = tr.appendChild(document.createElement("td"));
    td.textContent = record.fremont_bridge_sb;
    td.classList.add("numeric");

    return tr;
    }

    function renderTable(data) {
    console.log(data);
    var tbody = document.querySelector("tbody");
    tbody.textContent = "";
    
    //data is an array of objects
    data.forEach(function(record) {
        tbody.appendChild(renderRecord(record))
    });
    }

    fetch(dataURL)
    .then(parseAsJSON)
    .then(renderTable)
    .catch(handleError);
```

---

# MVC

### Model
- A model is simply an instance of a class (in the OOP sense) that is responsible for managing some chunk of data.
- It ensures that the data is created and modified correctly according to the rules of the application. 
- The model is also responsible for raising an event when the data inside the model changes.

```Javascript
    /**
     * Base class for all models
     */
    class Model {
        constructor() {
            //array of change event listeners
            //_prefix = should be treated as an internal private property, private data
            this._listeners = [];
        }

        /**
         * Adds a listener function that will be called when the model changes
         * @param {function} listener 
         * @returns {Model}
         */
        addChangeListener(listener) {
            //push the new listener function into the array
            this._listeners.push(listener);
            return this;
        }

        /**
         * Removes a change listener function
         * @param {function} listener 
         * @returns {Model}
         */
        removeChangeListener(listener) {
            //filter out the listener to remove
            this._listeners = this._listeners.filter(l => l !== listener);
            return this;
        }

        /**
         * Raises an change event
         * @returns {Model}
         */
        raiseChange() {
            //call the listener functions
            this._listeners.forEach(listener => listener());
            return this;
        }

        /**
         * Bubbles change events from another model up through this one
         * @param {Model} model 
         * @returns {Model}
         */
        bubbleChange(model) {
            model.addChangeListener(() => this.raiseChange());
            return this;
        }
    }
```
```Javascript
    /**
     * Represents a map of bare properties for a task
     * @typedef TaskProps
     * @property {string} title
     * @property {boolean} [done]
     */

    /**
     * Represents a single task
     */
    class Task extends Model {
        /**
         * Constructs a new task with an optional
         * set of initial properties
         * @param {TaskProps} [props]
         */
        constructor(props) {
            super();
            if (props) {
                this._title = props.title;
                this._done = props.done;            
            }
        }

        /**
         * Returns the task's title
         * @returns {string}
         */
        get title() {
            return this._title;
        }

        /**
         * Sets the task's title
         * @param {string} title 
         */
        set title(title) {
            if (!title || title.length === 0) {
                throw new Error("title must be non-blank");
            }
            this._title = title;
            this.raiseChange();
        }

        /**
         * Returns the task's done state
         * @returns {boolean}
         */
        get done() {
            return this._done;
        }

        /**
         * Sets the task's done state
         * @param {boolean} done 
         */
        set done(done) {
            this._done = done;
            this.raiseChange();
        }

        /**
         * Toggles the task's done state
         * @returns {Task}
         */
        toggleDone() {
            this._done = !this._done;
            this.raiseChange();
            return this;
        }

        /**
         * Converts this model into a simple object for
         * JSON serialization
         * @returns {TaskProps}
         */
        toJSON() {
            return {
                title: this._title, 
                done: this._done
            };
        }
    }
```
```Javascript
    let task = new Task();
    //this statement invokes `set title()`
    task.title = "Test"
    //and this statement invokes `get title()`
    let title = task.title;
```

### Views
- A view is an object that is responsible for rendering a model to an output device (typically the screen, but perhaps a printer). 
- The view just reads the data from the model and renders it to the output device. 
- It also listens for change events raised by the model and automatically re-renders itself whenever the model changes.

```Javascript
    class View {
        /**
         * Returns an HTML element that contains the rendered view
         * @returns {HTMLElement}
         */
        render() {return undefined;}
    }
```
```Javascript
    /**
     * Renders a TaskList as a simple unordered list
     */
    class TaskListView extends View {
        /**
         * Constructs the view
         * @param {TaskList} taskList 
         */
        constructor(taskList) {
            super();
            this._taskList = taskList;
        }

        render() {
            //create a <ul> for the list
            let ul = document.createElement("ul");

            //for each Task in the list...
            this._taskList.all().forEach(task => {
                //create an <li> and append it to the <ul>
                let li = ul.appendChild(document.createElement("li"));
                //set the textContent to the task title
                li.textContent = task.title;
                //add a "clickable" style class which we will
                //define in our CSS
                li.classList.add("clickable");
                //if the task is marked as done, add a "done"
                //style class, which we will define in our CSS
                if (task.done) {
                    li.classList.add("done");
                }
                //add a click event listener that calls toggleDone()
                li.addEventListener("click", () => task.toggleDone());
            });

            //return the <ul> element
            return ul;
        }
    }
```

### Controllers
- A controller is an object that is responsible for loading/saving models from/to persistent storage, and connecting those models to views. 
- It is also the component responsible for handling user events (mouse and keyboard interactions) and updating the models in response. 

```Javascript
    //load saved tasks from storage and parse them into a simple JavaScript array
    let taskProps = JSON.parse(localStorage.getItem("tasks"));
    //create a TaskList initializing it with the array
    let taskList = new TaskList(taskProps);

    //add a change listener that re-saves the task list to local storage
    taskList.addChangeListener(() => localStorage.setItem("tasks", JSON.stringify(taskList)));

    //create the task list view and pass it a reference to the model
    let taskListView = new TaskListView(taskList);
```
```Javascript
    /**
     * Renders the overall app view to the parent element
     * @param {View} appView 
     * @param {HTMLElement} parentElement 
     */
    function renderAppView(appView, parentElement) {
        //clear any content that might be there already
        parentElement.textContent = "";
        //render the app view into that parent element
        parentElement.appendChild(appView.render());    
    }

    /**
     * Renders the main application view
     * @param {Model} appModel
     * @param {View} appView 
     * @param {HTMLElement} parentElement 
     */
    function renderApp(appModel, appView, parentElement) {
        //render the app view
        renderAppView(appView, parentElement);
        //add a change listener to the app model that automatically
        //re-renders the app view whenever the model changes
        appModel.addChangeListener(() => renderAppView(appView, parentElement));
    }

    renderApp(taskList, taskListView, document.querySelector("#app"));
```