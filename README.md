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

This can get a bit tedious, especially when you start wanting to add more styles to each element. Every element takes you more time to alter and get just right since you have to tinker with them one by one. The alternative is to define these styles in a stylesheet and apply them with the use of selectors like classes and id's. Let's get into how those work, and then we can fix our example.

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

If !important is inserted after the property value, but before the semicolon, it will 

References and reading material:
13 Noteworthy points from google's javascript style guide:
https://medium.freecodecamp.org/google-publishes-a-javascript-style-guide-here-are-some-key-lessons-1810b8ad050b

Basic HTML template modeled after:
https://www.sitepoint.com/a-basic-html5-template/

The real OG - Guide to sharing for webmasters via Facbeook for developers:
https://developers.facebook.com/docs/sharing/webmasters

