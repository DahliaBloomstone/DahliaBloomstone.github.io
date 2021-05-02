---
layout: post
title:      "CUTE CSS ART"
date:       2021-05-02 19:33:00 -0400
permalink:  cute_css_art
---


![](https://user-images.githubusercontent.com/63209579/116831625-89bc9a80-ab7e-11eb-8898-95e8ae274918.png)

Viewport units. What are those? They’re truly “responsive length units” in the sense that their value changes every time the browser resizes. 

There are four viewport-based units in CSS. These are vh, vw, vmin and vmax:

* * Viewport Height (vh). This unit is based on the height of the viewport. A value of 1vh is equal to 1% of the viewport height.

* * Viewport Width (vw). This unit is based on the width of the viewport. A value of 1vw is equal to 1% of the viewport width.

* * Viewport Minimum (vmin). This unit is based on the smaller dimension of the viewport. If the viewport height is smaller than the width, the value of 1vmin will be equal to 1% of the viewport height. Similarly, if the viewport width is smaller than the height, the value of 1vmin will be equal to 1% of the viewport width.

* * Viewport Maximum (vmax). This unit is based on the larger dimension of the viewport. If the viewport height is larger than the width, the value of 1vmax will be equal to 1% of viewport height. Similarly, if the viewport width is larger than the height, the value of 1vmax will be equal to 1% of hte viewport width.

Configuring the animation
To create a CSS animation sequence, you style the element you want to animate with the animation property or its sub-properties. This lets you configure the timing, duration, and other details of how the animation sequence should progress. This does not configure the actual appearance of the animation, which is done using the @keyframes at-rule as described in Defining the animation sequence using keyframes below.

I'm also using CSS animation and keyframes. Example: 
```
.eyes {
  position: absolute;
  width: 5vmin;
  height: 4vmin;
  background: #000;
  border-radius: 50%;
  bottom: -15vmin;
  right: 18vmin;
  box-shadow: 13vmin 0 #000;
  animation: blink 1.5s infinite;
}

@keyframes blink {
  0% {transform: scale(1, 0.1);}
  100% {transform: scale(1, 1);}
}
```


The sub-properties of the animation property are:

animation-name
Specifies the name of the @keyframes at-rule describing the animation’s keyframes.
animation-duration
Configures the length of time that an animation should take to complete one cycle.
animation-timing-function
Configures the timing of the animation; that is, how the animation transitions through keyframes, by establishing acceleration curves.
animation-delay
Configures the delay between the time the element is loaded and the beginning of the animation sequence.
animation-iteration-count
Configures the number of times the animation should repeat; you can specify infinite to repeat the animation indefinitely.
animation-direction
Configures whether or not the animation should alternate direction on each run through the sequence or reset to the start point and repeat itself.
animation-fill-mode
Configures what values are applied by the animation before and after it is executing.
animation-play-state
Lets you pause and resume the animation sequence.


Helpful tutorials and articles: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations and https://www.youtube.com/watch?v=pGaw-eb-nPM&list=WL&index=10, and https://htmlcolorcodes.com/color-picker/. 
