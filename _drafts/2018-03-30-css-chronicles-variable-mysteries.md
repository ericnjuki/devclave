---
layout: post
title: "CSS Chronicles: Variable Mysteries"
# date: 2018-03-30 6:34:00 +0300
tags: css
---

[Go to _real_ start of article](#Intro)

To mark the beginning of a new month, I decided to equip myself with new skills on my journey towards being an exceptional designer. Naively, I decided to conquer css. All of it. One. Property. Atatime. Turns out one does not simply learn all of css, but one can try. So I'm starting with all the stuff I don't know. First up: CSS Variables...

### Intro

CSS Variables are a actually a combination of two CSS features:

* [Custom Properties](#custom-properties)
* [var() function](#var-function)

#### Custom Properties

Are a CSS3 feature that allows the storing of values in your stylesheet.
Custom properties are just like normal CSS properties, but prefixed with two dashes and can accept _any_ value you want.
That's right, quoting the spec:
> The allowed syntax for custom properties is extremely permissive

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

#### var() Function

**[⬆ back to top](#intro)**