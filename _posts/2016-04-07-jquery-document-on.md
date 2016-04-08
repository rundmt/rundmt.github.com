---
layout: post
title:  "jQuery attaching events document.on vs document.ready"
date:   2016-04-7 9:45:00
categories: jQuery events
---

jQuery makes javascript very easy for beginners to grasp. However, there are a few things that can trip up newbies when it comes to event attaching. I've experienced this first hand when I was new, and I've experienced this when teaching others about jQuery.

### Basic Form

When you first start learning jQuery, we learn to add events like this.

<script src="https://gist.github.com/rundmt/1e2014821f770977faf69f779b123e34.js"></script>

Notice how the event for `.add-input` is inside `document.ready()`. This means that once the document is ready we will attach a event click listener to `.add-input`.

<p data-height="268" data-theme-id="0" data-slug-hash="oxpGeJ" data-default-tab="result" data-user="derektorq" class="codepen">See the Pen <a href="http://codepen.io/derektorq/pen/oxpGeJ/">Jquery Event Example</a> by Derek Tor (<a href="http://codepen.io/derektorq">@derektorq</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

This code works fine in most cases, but what happens if an element is added after `document.ready()`.

### Dynamic Form (Naive Example)

Let's take a simple example of making a dynamic form. Say we're making an app and we want to add inputs to our form.

In the example below we have the basic form example from before, with and extra button. When the new "+" button is clicked it will append an input to the form creating a form with multiple inputs. However, the problem is the newly generated input buttons don't work the same way as the first button.

<script src="https://gist.github.com/rundmt/2125be3eb95c983be6cea110087c4018.js"></script>

<p data-height="268" data-theme-id="0" data-slug-hash="aNbYxx" data-default-tab="result" data-user="derektorq" class="codepen">See the Pen <a href="http://codepen.io/derektorq/pen/aNbYxx/">Jquery Event Example 1</a> by Derek Tor (<a href="http://codepen.io/derektorq">@derektorq</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

Try clicking the "Add Input" button of a newly generated input, in the Codepen above.

Here's where things get tricky.

This code above says add a click event listener to the `add-input` class. However since the new elements are added after the `$(document).ready()` the events for `$('.add-input').click()` never get called again after the first `ready()` event.

### Dynamic Form (Callback Example)

To fix problem we must attach our event listeners in the callback when we click the "+" button. So now every single time an input gets added it will also add `click()` event to it as well. Unfortunately this comes with it's own problems.

Since we're adding an event for every input we add, we are also re-adding the event listeners for every button resulting in multiple events.

To stop this we must add `$(".add-input").unbind( "click" );`. This allows us to remove all previous events that were attached. This leaves us with a single click event for each input button.

<script src="https://gist.github.com/rundmt/d94551175e0b43c85dcd0faa47e4c535.js"></script>

<p data-height="268" data-theme-id="0" data-slug-hash="bpaoLe" data-default-tab="result" data-user="derektorq" class="codepen">See the Pen <a href="http://codepen.io/derektorq/pen/bpaoLe/">jQuery Event Callback Example</a> by Derek Tor (<a href="http://codepen.io/derektorq">@derektorq</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>


Our code for what should be a simple dynamic form has grown into a mess. It is complex to say the least with all of the adding and removing of events. Imagine if we had a much more complex form, the code would leave us in [callback hell](http://callbackhell.com/). Luckily there is a better way.

### Dynamic Form ($(document).on Example)

As of jQuery 1.7, we now have the `.on()` method. `on()` is nifty, because it keeps track of the document even as we dynamically add inputs. With `on()` there is no need for adding complex callback code. We don't need to remove events only to add them back right after.

<script src="https://gist.github.com/rundmt/c7f8ce31935a7655dedcf0b0aa75eeae.js"></script>

<p data-height="268" data-theme-id="0" data-slug-hash="ONzxwN" data-default-tab="result" data-user="derektorq" class="codepen">See the Pen <a href="http://codepen.io/derektorq/pen/ONzxwN/">jQuery Event $(document).on Example</a> by Derek Tor (<a href="http://codepen.io/derektorq">@derektorq</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

We get the same result, but the resulting code is so much cleaner. No matter how many inputs we add, the code works without any problems.

### Conclusion

`$(document).ready()` is a great function to call when things the DOM is ready, but beginners can't rely on it for everything. `$(document).on()` is fantastic for adding event listeners, because it listens for any selector added on the document no matter when it is added.
