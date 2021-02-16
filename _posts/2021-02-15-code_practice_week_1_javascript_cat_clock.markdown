---
layout: post
title:      "Code Practice Week 1: Javascript Cat Clock "
date:       2021-02-15 21:13:10 -0500
permalink:  code_practice_week_1_javascript_cat_clock
---

![](https://user-images.githubusercontent.com/63209579/108010079-14efb080-6fd2-11eb-927c-1ba77dcc4602.png)

****A Cat Clock! Because cats never let you do anything. They are the best.

*But, what is happening in the code?
*
First, used setInterval because I needed to call a function every second. 

Every 1000 milliseconds we call the function. 

Set a function to get the current date and datetime.

Get the seconds from the current date, and divide it by 60 to know how far to rotate the seconds hand. Same thing for minutes and hours.

secondsRatio/minutesRatio is percentage of a minute. It allows for gradual movement around the clock.

In the HTML, we set the data-hour, minute, and second hands. Using querySelectors, we get the hour, minute, and second Hands. These are the elements we need to set the hands.

setProperty method takes the property we want to set, in the CSS. 360 degrees in our complete rotation. 

Call setClock() as soon as our page loads, will put the hands in the correct position for us.


```
setInterval(setClock, 1000)

const hourHand = document.querySelector('[data-hour-hand]')
const minuteHand = document.querySelector('[data-minute-hand]')
const secondHand = document.querySelector('[data-second-hand]')

function setClock() {
  const currentDate = new Date()
  const secondsRatio = currentDate.getSeconds() / 60
  const minutesRatio = (secondsRatio + currentDate.getMinutes()) / 60
  const hoursRatio = (minutesRatio + currentDate.getHours()) / 12
  setRotation(secondHand, secondsRatio)
  setRotation(minuteHand, minutesRatio)
  setRotation(hourHand, hoursRatio)
}

function setRotation(element, rotationRatio) {
  element.style.setProperty('--rotation', rotationRatio * 360)
}

setClock()

```


