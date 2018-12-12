# Sections
- [Essential Html](#essentia-html)
- [Introduction to Javascript](#introduction-to-javascript)
- [Javascript Functions](#javascript-functions)
- [The Document Object Model (DOM)](#the-document-object-model)
- [Event-Driven Application Architecture](#event-driven-application-architecture)


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