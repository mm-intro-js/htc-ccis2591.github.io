---
title:  JavaScript Data
layout: notes
---

# Variables
JavaScript variables are a little more *interesting* than variables in other languages as they can be a little peculiar when you look at them closely.  Have you noticed that you don't __*have*__ to say `var` when making a variable?  Ever wonder why that might be?  

All the details can be found by going to the source [JavaScript Reference `var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var). However let's see if we can't explore and discuss this a little bit.  

## Declared Variables
First let's talk about variables that we declare using `var`.  The JavaScript Reference says:

>Variable declarations, wherever they occur, are processed before any code is executed. The scope of a variable declared with var is its current execution context, which is either the enclosing function or, for variables declared outside any function, global.

### Hoisting
The first thing that is says about our variable declarations is that they are processed first. That means that the following are basically equivalent:

Use then declare:
{% highlight JavaScript %}
cat = "Abby";
var cat;
{% endhighlight %}

AND

Declare then use:
{% highlight JavaScript %}
var cat;
cat = "Abby";
{% endhighlight %}

This is called __hoisting__ and it can make it *appear* as if you are using a variable before you declare it. (You aren't, because the variable declarations are processed first.) Using variables before you declare them is not a good thing to do, but you *can* do it in JavaScript. This is one of those things that a lot of people don't like about the language, but JavaScript's flexibility also makes it a pretty powerful language.  What is it that they say about power and responsibility?

>With great power there must also come — great responsibility!
>
>~Stan Lee (Amazing Fantasy #15, August 1962)

So use your JavaScript power wisely and always declare your variables at the top of their scope.  What is their scope?  I'm so glad you asked...

### Scoping
Go ahead and enter this code into your browser console:

{% highlight JavaScript %}
var cat = "Abby";

var meow = function() {
  var sound = "meow";
  console.log(cat + " says " + sound);
}
{% endhighlight %}

It's probably pretty obvious that if you now type in `cat` it will give you back `Abby`.  But what about if you enter in `sound`?  Do you expect it will give you back `meow`?  Does it?

Even though variable declarations are processed first, they remain within the scope in which they are defined.  So you've got `cat` and `meow` defined outside of any function, which makes them global.  The variable `sound` however is declared in a function making it local to that function.  It only exists within the scope (the { } curly brackets) of the function definition.  

### IIFE - Immediately Invoked Function Expression
You may have noticed that if you try to look for a variable in the Developer Tools, there are a lot of global variables out there just from the browser itself.  While this is convenient for access to the DOM and all those browser things, it really makes it hard to look at "just your stuff" and worse, sometimes you may hide or overwrite something that has already been created because there is just so much stuff out there.

To help minimize this, clever JavaScript developers figured out that by wrapping all of their code in a function, they could scope it nicely and keep it separate from all that other stuff.  But how do you name a function that does everything?  Easy answer, you don't, you make it *anonymous* and then just make it run right away.

We'll discuss functions in more detail next week and you can review all the [IIFEs details here](http://benalman.com/news/2010/11/immediately-invoked-function-expression/).  The important part for now is just to pick up on this IIFE syntax to separate your data from the global scope and gain a little privacy.  Use it in all of your JS files.

{% highlight JavaScript %}
// Make our IIFE
(function(){

  // Put all your code here

}())  // End the definition and call the function to run the code.
{% endhighlight %}

For example:

{% highlight JavaScript %}
// Make our IIFE
(function(){

  // Code from before
  var cat = "Abby";

  var meow = function() {
    var sound = "meow";
    console.log(cat + " says " + sound);
  }

}())  // End the definition and call the function to run the code.
{% endhighlight %}

## Undeclared variables
So what about variables that don't get declared with the word `var`?  If you haven't already noticed, you can get away with out ever saying `var` anything, so what's it for and why don't we *have* to use it?


# Arrays
Working with arrays is very common in JavaScript programming.  While they are really no different than in many other languages, it is important to have the basics down - including multi-dimensional arrays.

Basic Array Example:
{% highlight JavaScript %}
// Make an empty array
var emptyArray = [];

// Declare with data
var myCats = ["Bart", "Abby", "Kyo", "Fred"];

// Get count of items
var catCount = myCats.length;

// Get something out by position
var oldest = myCats[0];

{% endhighlight %}


Multi-dimensional Array Example:
{% highlight JavaScript %}
// Make a cats array
var myCats = ["Bart", "Abby", "Kyo", "Fred"];

// Make a dogs array
var myDogs = ["Skadi", "Loki"];

// Make a Multi-dimensional pets array
var pets = [myCats, myDogs];

// Get a cat (cats are 1st of course)
var cat = pets[0][0];
var dog = pets[1][0];

{% endhighlight %}

## Array Methods
There are some handy methods for working with arrays in JavaScript.  Arrays are objects, and you can call methods on them by using the dot operator.

- push
- pop
- join
- slice
- concat
- shift & unshift
- sort

{% highlight JavaScript %}
// Make a cats array
var myCats = ["Bart", "Abby", "Kyo", "Fred"];

// Add a cat (push adds to end)
myCats.push("Ginger");

// Remove a cat (pop removes from the end)
var ginger = myCats.pop();
console.log(ginger);

// Unshift & Shift add/remove from the beginning
myCats.unshift("Chai");

var chai = myCats.shift();
console.log(chai);

// Make a comma separated list
var prettyList = myCats.join(', ');

{% endhighlight %}

# Objects
In the multi-dimensional array example, we saw one way to store two groups of data - dogs and cats - together.  However the only way that we knew the first array contained cats and the second dogs, was because we put them there.  If you didn't see that I started with an array called myCats, then combined it with an array called myDogs, it would just look like a bunch of names.

{% highlight JavaScript %}
// Some multi-dimensional array of names?
var names = [ ["Bart", "Abby", "Kyo", "Fred"], ["Skadi", "Loki"] ];

{% endhighlight %}

Objects let us group and organize data in more conceptual, human readable and understandable ways.  It allows us to identify and label data the data the object contains.  This makes the data a lot easier to understand:

{% highlight JavaScript %}
// A nice clear object
var pets = {

  cats : ["Bart", "Abby", "Kyo", "Fred"],
  dogs : ["Skadi", "Loki"]

};

console.log( "Cats:" + pets.cats );
console.log( "Dogs:" + pets.dogs );

{% endhighlight %}

JavaScript is an object oriented language, but it isn't class based like C# or Java. JavaScript objects are based on prototypes instead of classes, which makes them interestingly different. We won't dive into this too deep, as it goes a bit beyond what we really need to know.  However if you are familiar with objects from C# or Java (or another class based language), then JavaScript objects can sometimes behave surprisingly differently. (If you want more details on this, you can find more info on the web.)

We've been working with JavaScript objects - the DOM Document, DOM Elements, and even Arrays.  These objects have both __properties__, the object's data, and __methods__ - functions or behaviors associated to that object. We'll look more at  functions and object methods next week.

# JSON
JSON stands for JavaScript Object Notation, and not surprisingly looks a lot like what you saw above in the code to create a JavaScript object.  It has become popular for exchanging data in web applications in recent years as it is:

- JavaScript native - easily go from text to JS Object
- Human readable
- Easy to read and write - both for people and computers
- simpler and smaller than equivalent XML (the older standard)

We'll be working with some web API's later on in the course and they will be giving you back data in JSON format.

Simple Pet JSON
{% highlight JavaScript %}
{
  "cats" : ["Bart", "Abby", "Kyo", "Fred"],
  "dogs" : ["Skadi", "Loki"]
}
{% endhighlight %}

More complex Cat JSON - nested data/objects
{% highlight JavaScript %}
{
  "cats" : [
    {
      "name" : "Bart",
      "weight" : 16
    },
    {
      "name" : "Abby",
      "weight" : 13
    },
    {
      "name" : "Kyo",
      "weight" : 10
    },
    {
      "name" : "Fred",
      "weight" : 11
      }
    ]
}
{% endhighlight %}

# Storing Data in the Browser
In the past, web developer used [cookies](http://www.w3schools.com/js/js_cookies.asp) to store data in browsers.  While you may still run across this, many people now turn off cookies in the browser (to avoid malware and tracking info).  For those who do this, sites that use cookies to store information for their site may not work properly.

Fortunately there are now better ways to store data in the browser, however it is new, so in most cases you'll need to provide support for those that don't have the new HTML5 storage options by falling back to cookies.  And knowing many people turn off cookies, you'll want to ensure that even those people have a good experience on your site, even if it is perhaps not as *rich*.

## HTML5 storage options
In browser that support HTML5 features, you have access to `localStorage` and `sessionStorage`.  Local storage remains (or persists) longer than the session storage.  Session storage is gone when the *session* ends, or when the browser is closed.  Local storage stays until you as a developer remove it, or until the user removes it through the browser preferences.  (While this may not remain true, in practice this has been more difficult for someone to do.)

## Storage methods
With either storage option - local or session - you use the same set of methods to add, get, and remove data:

- setItem
- getItem
- removeItem

{% highlight JavaScript %}

// Store the use name locally
// Data stored must be a string
localStorage.setItem("userName", "Mary");

// Get the name from storage
localStorage.getItem("userName");

// Remove the name from storage
localStorage.removeItem("userName");

{% endhighlight %}

The key thing to be aware of here is that the data you store must be a string.  So does that mean that you can't store more complex data like the information on my cats?  Absolutely not.  Remember that JSON is basically a string of data, but it is in a format that can be easily converted to a JavaScript object.  

The JSON object has methods on it to convert back and forth between JSON text and JavaScript objects.

- use JSON.stringify to convert JavaScript objects to JSON strings
- use JSON.parse to convert JSON strings to JavaScript objects

Storing the cat Data
{% highlight JavaScript %}
// Make the object from JSON data
var myPets = {
  "cats" : [
    {
      "name" : "Bart",
      "weight" : 16
    },
    {
      "name" : "Abby",
      "weight" : 13
    },
    {
      "name" : "Kyo",
      "weight" : 10
    },
    {
      "name" : "Fred",
      "weight" : 11
      }
    ],
  "dogs" : [
    {
      "name" : "Skadi",
      "weight" : 103
    },
    {
      "name" : "Loki",
      "weight" : 98
      }
    ]
};

// Convert the object back to a string for storage
var stringPets = JSON.stringify(myPets);
localStorage.setItem("myPets", stringPets);

// Get it back from storage and convert to an object
var storedPets = localStorage.getItem("myPets");
var petObject = JSON.parse(storedPets);

{% endhighlight %}
