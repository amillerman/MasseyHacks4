# MasseyHacks4
## Basic Outline:

- Introduction to HTML
  - How to include JS 
  - How to include CSS
  - How to see that they've loaded in the dev console
- Getting started with CSS
  - ID's, classes and media queries, oh my!
  - Inline styles and !important things
- Getting started with JS
  - How to use standard JS, and why nobody does it
  - How to use jQuery
- Frameworks and why we use them
  - MDI vs Bootstrap
- What's next?
  - Quick examples of larger frameworks like angular

  
Cascading style sheets are largely a way for us to define styles across multiple elements in one definition, but sometimes we may opt to apply specific styles to specific elements. Classes and id's allow you to do just that. 

An ID is something that must be unique to an element on the page. Only one element on a page is allowed to have a specific id. Think of it like your student ID number, it's specific to you, and you alone, in the context of your respective schools. ID's are special attributes of elements on a page because of this uniqueness, and allow for things like forms to use them when they're submitted (more on that later), and you can even link to them on the page! It's worth noting that in the  past, when the web was young, this attribute used to be called name, and you'll still see it as name on some pages. To add an ID to an html element, the code is as follows:

<input id="first-name" name="first-name" />

A css selector for an element by id is as follows:

#first-name{
    color: #ff0000;
}

A way to access an element by id in standard javascript is as follows:

console.log(document.getElementById("first-name"));

A class on the otherhand is something that can be given to multiple items on the same page, and is strictly used for css and js selection purposes. If you need multiple elements to have the same styles applied to them, it's easiest to give them all the same class bame and then you only need to definte the css once.

It's important to note that both of these atributes are case insensitive, so camel case isn't a goos option here. Hyphenated words are largely the norm for class names and ID's. 

References and reading material:
13 Noteworthy points from google's javascript style guide:
https://medium.freecodecamp.org/google-publishes-a-javascript-style-guide-here-are-some-key-lessons-1810b8ad050b

Basic HTML template modeled after:
https://www.sitepoint.com/a-basic-html5-template/

The real OG - Guide to sharing for webmasters via Facbeook for developers:
https://developers.facebook.com/docs/sharing/webmasters

