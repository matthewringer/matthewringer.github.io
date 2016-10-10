---
layout: post
title:  Fun with HTML and CSS Animation
date:   2016-04-04
categories: dev 
author: "Matt R"
featured_image: /images/success.gif
featured_image_alt: "White circles rotating on a red background"
tags: CODEPEN HTML5 CSS3 ANIMATION
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/pNe6fsaCVtI" frameborder="0" allowfullscreen></iframe>

The other morning while browsing my Facebook feed, procrastinating the inevitable start of my day, I ran across this neat little optical illusion. The premise is the inner ring of circles appears to rotate, when in actuality each ball is traveling a linear path across the face of the red circle. It struck me that this would be a fun way to explore linear transforms with CSS3 Animations and make something cool in the process. Recreating the effect was straight forward, still there were a few interesting discoveries along the way fell into three areas. 

1. Set where each circle should travel during its animation.
2. Timing when each circles animation should start.
3. Finding the right animation timing function to transform each circle through the animation.
4. Mobile weirdness and limitations. 

### CSS3 Animations
CSS3 includes support for animation of most HTML elements without using flash or JavaScript. So limiting the animation to only CSS3 sounded like a good constraint for this exercise. Essentially each animation allows you to transition from one CSS style to another, using the @keyframes rule, referenced with the animation-name property in your class. 

The @keyframes rule tells the browser where along a given transformation between each style it should be at a given point in the animation. This can be specified using  "from to" syntax.

{% highlight css %}
@keyframes example {
    from {background-color: green;}
    to {background-color: blue;}
}
{% endhighlight %}

or by percentile for more granular control

{% highlight css %}
@keyframes example {
    0%   {background-color: red;}
    10%  {background-color: yellow;}
    20%  {background-color: blue;}
    100% {background-color: green;}
}
{% endhighlight %}

### Laying Everything Out
The first task at hand was to arrange everything involved in the animation. This was straight forward, each element circle element would be evenly spaced around one edge of the side of the primary red circle, and the
inverse-coordinates determined where each circle would be at the 50% keyframe. A little math and a little pixel bumping and the transit of the first and fifth circles were looking pretty good. But as the other circles were added, it became clear that there was a bit of a problem, the circles were colliding in the center. Clearly this little hack wouldn't be as simple as lining everything up and hitting go.


<img class="img-thumbnail sm-thumbnail" src="/images/noon-six.gif" alt="Noon and Six"> <img class="img-thumbnail sm-thumbnail" src="/images/three-nine.gif" alt="Three and nine" ><img class="img-thumbnail sm-thumbnail" src="/images/collisions.gif" alt="Collisions" >

### Timing is the key to success
So starting everything at the same time wasn't going to cut it, that's where the animation-delay property comes in. Animation delay does what it sounds like, it allows you to delay the start of animation until some number of seconds after the element loads. 

Additionally, if you specify a negative value the animation appears as if it were already in progress when the element loads. Very useful for cases where elements need tobe in place before they are shown to the user. I learned this tip in a great [article][article] which came in very handy later.

So things were starting to come together, but the animation still left me flat, specifically the shape of my ring of circles wasn't very circular, more of a flat tire with a magnet inside. So close... 

<img class="img-thumbnail sm-thumbnail" src="/images/flattire.gif" alt="Flat Tire" >

### The best solution isn't always a straight line
When I looked at any given circle's movement it appeared to bounce off the 50% keyframe like a tennis ball. 
This magnetic bouncy squish effect was causing the balls to bunch near the middle, what I needed was a way to vary the speed of the animations speed during its life-cycle. Controlling the speed cure is done by setting the animation-timing-function. The default setting is linear, which was the obvious cause of the tennis ball effect. Out of the box you get these options:

* ease - a slow start, then fast, then end slowly (this is default)
* linear - the same speed from start to end
* ease-in - a slow start and linear finish
* ease-out - a linear start and slow end
* ease-in-out - a slow start linear middle and slow end
* cubic-bezier(n,n,n,n) - lets you define your own speed curve in a cubic-bezier function

Cycling through each yielded some interesting effects (you can try them for your self in my [codepen][codepen]), the ease-in-out was the closest but still left my circle a bit droopy. And that wasn't going to cut it with my OCD. Lucky for me there is a cool [web tool][cubicbeizer] to that lets you DIY your very own cubic beizer, a little trial an error and I was able to get the rotation effect as smooth as glass.      

### Mission Accomplished: 

<a href="http://codepen.io/supineUnicorn/pen/MypXLy"><img class="img-thumbnail sm-thumbnail" src="/images/success.gif" alt="Success, link to my codepen" ></a>

### Bonus!
While fussing over getting all the circles to start in a good place in my [codepen][codepen] example I stumbled on a neat bonus, by simply inverting the animation delay for each item, I could toggle the direction that the circles appear tobe rotating. Thanks math! 

### Wrapping up...
All and all a fun quick exercise into some of the lesser used (by me) capabilities of HTML5 and CSS3.

A few side notes, animations have varying levels support, Webkit and Mozilla based browsers do well, though some features seem not be fully supported in mobile versions, or at least changing some properties mid-animation do not work well in the mobile versions. 

More info on [animations][w3sanimations].

[article]:http://www.sitepoint.com/animation-advice-from-a-css-master/
[Liquid]:https://github.com/Shopify/liquid/wiki
[codepen]:http://codepen.io/supineUnicorn/pen/MypXLy
[cubicbeizer]:http://cubic-bezier.com/#.45,.48,.67,1.49
[w3sanimations]:http://www.w3schools.com/css/css3_animations.asp