# MasseyHacks4
## Basic Outline:

- Introduction to front end web dev
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

## Introduction to front end web dev

Front end web development can be an art, a very frustrating art that gets painted differently on thousands of different canvases that try to view it, so it's important that we try to get a firm understanding of how to draw our webpages, and what tools are at our disposal.

Let's get started with some terminology. The Document object model ([the DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)) is where everything on the page is drawn, and it provides us a way to manipulate it, with thigs like Javascript. 

So to get started, there are some standard html tags that start off a webpage we need to add to a file. Let's work off the sample file in this repository to see what we'll need.

Note the two external files we're including in our page, namely the stylesheet and the script:

```html
	<link rel="stylesheet" href="css/styles.css?v=1.0">
```

The style tag needs to be included in the head of the document. You can include many stylesheets (this is part of how you use libraries like bootstrap, angular and material for example) if you need to, but for stylesheets you control, adding this query at the end of the stylesheet link can help you a lot down the line. One of the problems while developing for the web is that you visit the same page over and over again. This leads to issues where you don't see code updating when you refresh the page, but it's due to the browser trying to be smart and help the average user by not downloading files it already thinks it has (like your stylesheet) when it doesn't think anything has changed in that file. By adding and changing the version number in the stylesheet include, you can make sure the browser updates your css code when you refresh the page without having to do something like clear your browsers cache or hard refresh (harder to do on something like a phone).

Now for including the javascript:

```javascript
	<script type="text/javascript" src="js/script.js"></script>
```

Much like the stylesheet, it's good to get a version number on your javascript too to save you from caching confusion. Notice, though, that we're adding the javascript file at the bottom of the body tag. We do this for speed; the content on the page loads sequentially, and javascript files can be the larger files, along with introduce all kinds of changes to the DOM once they are loaded, which takes time for the browser to interpret and put into effect. This is particularly troublesome when you would like your page to load things like images first, to better the user experience. By adding these includes to the very end of the body, they'll be prioritized lower and load later, making the page seem to load faster to the user. This is kind of an older practice, and it does depend on the situation you're in, but it's still good to do generally. There's also the concept of loading a script async or deferring it (see a good description of the differences [here](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)).
  
To see that your resources have loaded on your webpage, open the developer tools in your browser (commonly the hotkey in Windows is f12 across most browsers), and click the Network tab.

![alt text](https://github.com/amillerman/MasseyHacks4/blob/master/img/example1.png "Screenshot of the network panel")

  
## Getting started with CSS

Cascading style sheets are largely a way for us to define styles across multiple elements in one definition, but sometimes we may opt to apply specific styles to specific elements. Classes and id's allow you to do just that, but there is also the option of using what are called inline styles. Let's start there, so we can see why developers opt for cascading stylesheets over inline styles.

### Inline styles

An inline style is exactly what it sounds like - a style that is applied directly inline to an element. So if you wanted to make a list of apples, and have the colour of the text correspond to the colour of the apple in the list.

```html
<ul>
	<li style="color: #ff0000;">Royal Gala Apples</li>
	<li style="color: #00ff00;">Mutsu Apples</li>
	<li style="color: #ff0000;">Red Delicious Apples</li>
	<li style="color: #ffff00;">Golden Delicious Apples</li>
	<li style="color: #00ff00;">Granny Smith Apples</li>
</ul>
```

This can get a bit tedious, especially when you start wanting to add more styles to each element. Every element takes you more time to alter and get just right since you have to tinker with them one by one. The alternative is to define these styles in a stylesheet and apply them with the use of selectors, like classes and id's. *Note* that tag names are also valid selectors, so you may apply styles to tags themselves too. Let's get into how those work, and then we can fix our example.

### What is an ID

An ID is something that must be unique to an element on the page. Only one element on a page is allowed to have a specific id. Think of it like your student ID number, it's specific to you, and you alone, in the context of your respective schools. ID's are special attributes of elements on a page because of this uniqueness, and allow for things like forms to use them when they're submitted (more on that later), and you can even link to them on the page! It's worth noting that in the  past, when the web was young, this attribute used to be called name, and you'll still see it as name on some pages. To add an ID to an html element, the code is as follows:

```html
<input id="first-name" name="first-name" />
```

A css selector for an element by id is as follows:

```css
#first-name{
    color: #ff0000;
}
```

A way to access an element by id in standard javascript is as follows:

```javascript
console.log(document.getElementById("first-name"));
```

### What is a class

A class, on the otherhand, is something that can be given to multiple items on the same page, and is strictly used for css and js selection purposes. If you need multiple elements to have the same styles applied to them, it's easy to give them all the same class name and then you only need to definte the css once. And because elements can have more than 1 class applied to them, you can stack together different styles to have them work together and make your code cleaner overall.


```html
<ul>
	<li class="padding-10 red">Royal Gala Apples</li>
	<li class="padding-10 green">Mutsu Apples</li>
	<li class="padding-10 red">Red Delicious Apples</li>
	<li class="padding-10 yellow">Golden Delicious Apples</li>
	<li class="padding-10 green">Granny Smith Apples</li>
</ul>
```

```css
.padding-10{
	padding: 10px;
	backbground-color: #999999;
}
.red{
	color: #ff0000;
}
.green{
	color: #00ff00;
}
.yellow{
	color: #ffff00;
}
```

We now have added 10 pixels of padding around each list item, to give them some breathing room, a background colour of a light grey (to make that nasty yellow text a bit more legible, and now each list items text colour is defined in one place, so if I don't like that particular green on the list, I can change it once, and it'll change it for all the elements with that class; efficient!

It's important to note that both of these atributes are case insensitive, so camel case isn't a good option here. Hyphenated words are largely the norm for class names and ID's. 

### Very !important

Sometimes you will have elements that have the same style properties applied to them in more than one place. This makes it harder to determine exactly what element will take precedent. There is a "chain of command," so to speak, when it comes to which style will be applied over which, and it has to do with a few factors. Those factors include which style is more specifically selecting the element, the order the styles are defined, whether the style is being applied inline vs in a stylesheet, and if the property is !important or not. Let's look at some examples.

```html
<div id="wrapper">
	<div class="padding-20">
		Channels
	</div>
</div>
```

```css
.padding-20{
	padding: 20px;
}
#wrapper .padding-20{
	padding: 20px 10px 20px 10px; /* top, right, bottom, left (think clockwise) */
}
```

In this example, the second definition will take precedent, because it is not only being defined for the padding-20 class, but it's SPECIFICALLY for padding-20 classes within the wrapper. It's a more specific definition, so its styles will override the normal padding-20 definition.

Now let's do an example with a use of !important:



```html
<div id="wrapper">
	<div class="margin-10">
		Authors
	</div>
</div>
```

```css
.margin-10{
	margin: 10px !important; 
}

.margin-10{
	margin: 12px;
}
```

If !important is inserted after the property value, but before the semicolon, it will take precedent over anything and everything (except a more specifically defined version of the style also using !important). This means that the property could be defined first on the css sheet and no non-!important property would overwrite it defined later in the sheet, nor if it's more strictly defined using classes and id's, and !important even trumps inline styles! It's very powerful, with great power comes great responsibility, and a phrase we use at work all the time when this property gets thrown around more than it should be is: If everything is !important, nothing is. !important is very powerful and should not be relied on for regular use. It's meant to be a trump card to be used sparingly. It's also worth noting that you can use it in your inline styles too.

### Media Queries

Last but certainly not least are media queries. These are a nifty way to help you define styles for your page when it's on certain sizes of devices. Ever notice how a website looks different on your phone than on a desktop? In the past, we used to accomplish this by building two versions of the website, and then serving up the desired version based on browser detection, device detection, etc. This was super cumbersome, very time consuming from a development standpoint, and it wasn't very reliable since new devices and technology is constantly coming out, while websites remain without being updated.

The much cleaner solution is to use medi queries in your css definitions, and cleaning up some of the html to enable it ready for use on any sized device. A media query goes around a block of css and defines what range of screen width it'll be applied for. It sounds a bit odd, so let's jump into an example.

[Sample 2](https://github.com/amillerman/MasseyHacks4/blob/master/sample/sample2.html)

So in that example, we have some css classes width property being overwritten when the max width of the browser is less than 768 pixels. This works for a couple reasons: 

- That viewport meta data helps make sure that the page's width is based on the actual devices browser width, along with also stopping users from zooming on the page and creating horrible horizontal scrollbar problems. This way, on a smaller phones browser screen, the window will actually be a reasonable size and we can plan to display the content correctly on those smaller screens. 
- Since our media queries actual css isn't any more specific than the normal css (we're assinging the width to .col-3 and .col-6, but we were already doing that before too), it's important that the media query is defined AFTER the initial css. This way, since it's CASCADING stylesheets, the second definition is the one that's used.

Media queries are very important in modern web development, and help enable us to do lots of clean page organization, without having to rely on clunky javascript checking for page widths or browser compatability (though that last part is definitely still a thing in CSS!).

CSS may seem simple on the surface, but it's got a lot more to it than meets the eye. It can also be increadibly frustrating, especially when you start to use libraries to help make the visual designing of websites easier (mdi, bootstrap, etc). With enough patience, you can make more happen with CSS than most will believe (it's even got decent animations now!).

## Getting started with Javascript

Standard javascript syntax is a lot like most languages, where you have if statements, loops, etc, but it also comes with ways to try to interact with the DOM and bind things to elements on the page. The problem is the way it interacts with the DOM, which tends to be cumbersome unfortunately, and lots of libraries have been written to make it easier to interact with the DOM. Some of the popular ones among them are jQuery and AngularJS. 

AngularJS is a very advanced library that builds on javascript to change the way we interact with the DOM entirely. Instead of manipulating it directly, we do so using controllers, directives, factories, and other systems that angular has defined to do the heavy lifting, while not manipulating the dom directly after it's been rendered. It greatly expands what you can do with front end development, but it requires a great deal of time to grasp decently, and lots of experience and patience to use well. It's beyond the scope of this workshop, but I highly recommend looking into it in your spare time, because it's becoming a mainstream way of developing on the web. You can find out how to get started with it [here](https://docs.angularjs.org/misc/started).

jQuery on the other hand is much easier to pick up and get started using right away. It very directly interacts with the DOM and manipulates elements directly through the code. Let's look at another sample page to see how we can get started using it.

[Sample 3](https://github.com/amillerman/MasseyHacks4/blob/master/sample/sample3.html)

So remember when we talked about selectors in CSS? Well this is where that knowledge comes in handy again. Those selectors are the same when we're using jQuery, so in this example, we can see we have applied a click event handler to all "button" tags, and we are toggling (either showing or hiding, depending on the current state of the element) all paragraph tags on the page when a button is clicked. This is a very simplistic example of what you can do with jQuery, but it does show off several aspects.

First off, we can bind actions to events. An event can be anything from a key press, to you scrolling the page, to clicking an element. You can even define custom events, to control the flow more accurately. So in this example, we are binding an action (defined in the function) to the click event on every button on the page. 

- We selected every button by using $("button")
- We assigned those buttons a click event by applying .on("click", _function that defines the action we take_)
- When this event is triggered, it will find every p tag, and toggle it, using $("p").toggle();

We can use jQuery to do all kinds of DOM manipulations, from assigning styles to an element, to changing its classes, to iterating through JSON data and drawing new elements onto the page. You can do requests to the server to retrieve new information, to make your webpage more interactive, and remove the need to constantly be loading a new page every time you need to retrieve new information. 

But a library like jQuery comes at a cost, and it comes down to direct DOM manipulation being a fickle thing. Any changes you may make to the structure of your site will cause a lot of changes needed to your jQuery. Manipulating the DOM directly also leads to a lot of possible flow and logic errors as your site grows, and a lot of the time jQuery code tends to not be reusable, so you're writing things from the ground up over and over again. It's still a bit clunky, and in a world where web browsing is primarily done from the phone now, efficiency in speed and space are getting to be more and more important. It's still got its uses, but it's slowly falling out of being the goto for developers.

## Frameworks and why we use them

As I said before, CSS can be a nightmare to write a lot of the time, especially when you're worried about cross device compatability. With that in mind, developers have started to use standardized libraries that can be used right out of the box to make your web pages pretty with the use of just a few classes. Let's look at an example using [Material Design](https://getmdl.io/started/index.html).

[Sample 4](https://github.com/amillerman/MasseyHacks4/blob/master/sample/sample4.html)

This is where we really see classes shine, in frameworks like these. Mdl is a framework developed by google (recognise that + button from somewhere? Like gmail?) that is based on their entire [Material design ruleset](https://material.io/guidelines/material-design/introduction.html). It's meant to try to help users create interfaces that work on all devices, and take all types of users into account, making sure that buttons and other tappable items are large enough to be useful without being overly large to take away from the site or applications aesthetic. This design ruleset supersedes web development; it's used in a lot of native android applications as well, and makes its way into normal desktop applications as well. I'm a big fan of what Google does, and Material Design is the direction we've been moving for a while now where I work. It paves the way for more intuitive web design and adds an aesthetic that works very well. There are many small plugins you can find for it, to add addtional functionality to it, and it [integrates](https://material.angular.io/) with larger systems like AngularJS in a very nice way.


References and reading material:
13 Noteworthy points from google's javascript style guide:
https://medium.freecodecamp.org/google-publishes-a-javascript-style-guide-here-are-some-key-lessons-1810b8ad050b

Basic HTML template modeled after:
https://www.sitepoint.com/a-basic-html5-template/

The real OG - Guide to sharing for webmasters via Facbeook for developers:
https://developers.facebook.com/docs/sharing/webmasters

