---
layout: post
title: "Front end Chronicles: CSS Variables"
date: 2018-03-30 6:34:00 +0300
tags: css
---

## Contents
* [Skip intro](#what-are-they-css-variables)
* [Notes](#more-notes-about-css-variables)
* [Examples](#nifty-examples)

### Intro
<span class="dropcaps">T</span>o mark the beginning of a new month, I decided to equip myself with new skills on my journey towards becoming an exceptional designer. Naïvely, I decided to conquer CSS. All of it. One. Property. Atatime. Turns out one does not simply learn all of CSS, but one can try. And so begins the journey towards CSS Mastery. First up: CSS Variables...

### What are they? (CSS variables)

CSS Variables are actually a combination of two CSS features:

* [Custom Properties](#custom-properties)
* [var() function](#var-function)


If you're from the Object-Oriented Programming world, think of ```Custom properties``` as _setters_ and the ```var()``` function as a _getter_. If you're not from that world then... read on.

#### Custom Properties

Custom properties are just like normal CSS properties, but prefixed with two dashes and can accept _any_ value you want.

_Syntax_

{% highlight css %}
--property-name: value;

/* examples */

/* value can be any valid css property value */
--main-line-height: 2px;
--main-color: Red;
--default-transition: all 2s ease-in;

/* or a javascript statement */
{% endhighlight %}
_[⬆ back to top](#contents)_

#### var() Function
Used to access the value of a custom property. The ```var()``` function, as defined by CSS, can only be used to access values set by a ```custom property```.

_Syntax_

{% highlight css %}
property: var(--custom-property, [fallback value(s)]?);

/* examples */

color: var(--main-color);

font-style: var(--default-font, Helvetica, Arial); /* 'Helvetica, Arial' 
becomes the fallback value */

/* can also be used to set the value of another custom property */
--header-color: var(--main-color, blue); /* fall back to blue if --main-color
 is not defined */
{% endhighlight %}
_[⬆ back to top](#contents)_

#### Fallbacks
Fallbacks are only er.. fallen back to when the custom property in question is not defined. Otherwise, naturally, ```css variables``` are ignored by browsers that don't support them.

Include a fallback property right before the the one containing a ```css variable```.

{% highlight css %}
color: red;
color: var(--main-color); /* ignored by non-supporting browsers so the color 
remains red */
{% endhighlight %}

How is this useful? I don't know. But a guess is that you could use not-widely-supported css along with ```css variables``` and add fallbacks:

{% highlight css %}
body {
    --main-color: rgba(10, 10, 10, 0.7);
}
p {
    color: black; /* fall back for browsers that don't support variables _and_ rgba() */
    color: var(--main-color); 
}
{% endhighlight %}
_[⬆ back to top](#contents)_

#### More notes about CSS Variables

##### Less magic strings == Less errors
By convention, define all your global variables in the ```:root``` selector

{% highlight css %}
:root {
    --default-transition: all 0.3s ease;
    --borders: 3px solid rgba(10, 10, 10, 0.7);
}
{% endhighlight %}

The ```:root``` selector in HTML/CSS is like ```html``` but with a higher specificity.

##### Theming
```css variables``` make theming a cinch. There are many ways to go about it, but the most straightforward is defining multiple rules for different themes:

{% highlight css %}
.blue-theme {
    --primary-color: blue;
}
.red-theme {
    --primary-color: red;
}
{% endhighlight %}

...and switching between them using a toggle.

##### custom properties cascade

Which basically means that the value of a custom property set lower in the stylesheet is the one that gets applied:

{% highlight css %}
:root {
    --preferred-color: red;
}

.some-element {
    --preferred-color: blue;
    background: var(--preferred-color)
    /* background will be blue */
}
{% endhighlight %}

##### ...and are inherited too
Which means if we a custom property's value on a div say ```<div class"some-class"></div>```:
{% highlight css %}
.some-class {
    --preferred-color: red;
}
{% endhighlight %}

Then ```--preferred-color``` will be set to red in all the descendants of ```some-class``` i.e// 
```some-class *```

_[⬆ back to top](#contents)_

#### Nifty example
When creating multiple rules each just slightly different from the rest:

{% highlight css %}
.one {
  border: 1px solid blue;
}

.two {
  border: 1px solid red;
}

.three {
  border: 1px solid green
}

.four {
  border: 2px solid red;
}
{% endhighlight %}

...you can instead do:

{% highlight css %}
div {
  --div-border-width: 1px;
  --div-border-style: solid;
  --div-border-color: red;  
}

div.one {
  --div-border-color: blue;
}

div.three {
  --div-border-color: green;
}

div.four {
  --div-border-width: 2px;
}
{% endhighlight %}
_[⬆ back to top](#contents)_

___Fin___