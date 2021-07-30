---
layout: post
title:      "glass website tutorial "
date:       2021-03-29 13:24:20 -0400
permalink:  blog_the_content_of_your_blog_post_goes_here
---


![](https://user-images.githubusercontent.com/63209579/112896825-e246d680-90ac-11eb-8311-1798afc13b38.png)

I'm trying to work on both design and code challenges every single week. So, what's this week?! 
I think I'm going to try to build a glass website in html and css, and also try some stuff out in adobe character animator and unreal engine! Whenever I create a new app or webpage, I want to only put my original artwork on there! So it's exciting to be creating characters and uploading them to something simple like Giphy, and adding them quickly to the code! 

So I'll first get started with the glass website, and then I'll create characters to add to it and add images here for everyone reading this! (0-3 people) 

https://github.com/DahliaBloomstone/Glass-Website/blob/main/README.md

I had to resize all of the images, which I actually needed a refresher on:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Glass Website</title>
    <link rel="preconnect" href="https://fonts.gstatic.com" />
    <link
      href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&display=swap"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body>
    <main>
      <section class="glass">
        <div class="dashboard">
          <div class="user">
            <img src="./images/avatar.png" style="width:5em; height:5em;" alt="" />
            <img src="./images/fuzzyY.png" style="width:5em; height:5em;" alt="" />
            <h2>Dahlia Bloomstone</h2>
            <p>Pro Member</p>
          </div>
          <div class="links">
            <div class="link">
              <img src="./images/streams.png" alt="" />
              <h2>Streams</h2>
            </div>
            <div class="link">
              <img src="./images/steam.png" alt="" />
              <h2>Games</h2>
            </div>
            <div class="link">
              <img src="./images/upcoming.png" alt="" />
              <h2>New</h2>
            </div>
            <div class="link">
              <img src="./images/library.png" alt="" />
              <h2>Library</h2>
            </div>
          </div>
          <div class="pro">
            <h2>Join pro for free games.</h2>
            <div>
            <img src="./images/lady.png" style="width:10em; height:10em;" alt="" /> </div>
          </div>
        </div>
        <div class="games">
          <div class="status">
            <h1>My Favorite Games</h1>
            <input type="text" />
          </div>
          <div class="cards">
            <div class="card">
              <img src="./images/19821.png" style="width:10em; height:10em;" alt="" />
              <div class="card-info">
                <h2>Insaniquarium</h2>
                <p>Mobile Version</p>
                <div class="progress"></div>
              </div>
              <h2 class="percentage">   90%</h2>
            </div>
            <div class="card">
              <img src="./images/bloons.png" style="width:10em; height:10em;" alt="" />
              <div class="card-info">
                <h2>Bloons TD 6</h2>
                <p>Mobile Version</p>
                <div class="progress"></div>
              </div>
              <h2 class="percentage">70%</h2>
            </div>
            <div class="card">
              <img src="./images/book.png" alt="" />
              <div class="card-info">
                <h2>Bookworm</h2>
                <p>Ipad Version</p>
                <div class="progress"></div>
              </div>
              <h2 class="percentage">0%</h2>
            </div>
          </div>
        </div>
      </section>
    </main>
    <div class="circle1"></div>
    <div class="circle2"></div>
  </body>
</html>
```
