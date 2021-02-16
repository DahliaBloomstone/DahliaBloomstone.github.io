---
layout: post
title:      "Code Practice Week 1: Javascript Cat Clock "
date:       2021-02-15 21:13:10 -0500
permalink:  code_practice_week_1_javascript_cat_clock
---

![](https://user-images.githubusercontent.com/63209579/108010079-14efb080-6fd2-11eb-927c-1ba77dcc4602.png)












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


