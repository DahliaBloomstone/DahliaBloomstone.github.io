---
layout: post
title:      "UNREAL ENGINE AND SPARK AR "
date:       2021-04-12 17:33:21 -0400
permalink:  unreal_engine_and_spark_ar
---


I have been wanting to experiment with unreal engine, spark AR and Lens studio for a few weeks. Last week I played with Adobe Aero for hours, but Unreal and Spark specifically are interesting in relation to Javascript coding. 

First, for two weeks I couldn't open Unreal Engine, and had this issue a lot of people have had with this message: ![](https://linustechtips.com/uploads/monthly_2020_12/Error.png.b451cbbec0ed5724e2d7b804f1f7f5e4.png)

I figured out the issue here is that the xcode I had installed was the beta version so unreal could not open. This also happened to work for many people but not for me: 

Other solution for those who don't want to install Xcode:

Install Command Line Tools (if you haven't already):

xcode-select --install

Change the active directory:

sudo xcode-select -switch /Library/Developer/CommandLineTools

With SPARK AR, I'm going to dive into Scripting basics: ![](https://scontent-lga3-2.xx.fbcdn.net/v/t39.2365-6/135566695_456791438685337_5382770519534050908_n.png?_nc_cat=107&ccb=1-3&_nc_sid=ad8a9d&_nc_ohc=B9Ee49aiv9gAX8PN_1w&_nc_ht=scontent-lga3-2.xx&oh=cd4a4c07fbf76648ab2ace5da532386b&oe=609ADCE8)

Spark AR Studio supports JavaScript for adding logic and interactivity to your effects. This guide will cover the basics to help get you started with scripting.

Spark AR studio will open your scripts with the default editor assigned to JavaScript/TypeScript files on your macOS or Windows operating system. If you don't already have one installed, you can download an editor such as Visual Studio Code and set it as the default app for opening JavaScript/TypeScript files.
Reactive Programming

Spark AR Studio uses reactive programming, a declarative programming model that uses asynchronous data streams. This guide will cover the benefits and use of reactive programming within Spark AR Studio. This is not something I felt entirely familiar with so it is really interesting. 

Spark comes with pre-populated Javascript Files: 
```
//==============================================================================
  // Welcome to scripting in Spark AR Studio! Helpful links:
  //
  // Scripting Basics - https://fb.me/spark-scripting-basics
  // Reactive Programming - https://fb.me/spark-reactive-programming
  // Scripting Object Reference - https://fb.me/spark-scripting-reference
  // Changelogs - https://fb.me/spark-changelog
  //
  // For projects created with v87 onwards, JavaScript is always executed in strict mode.
  //==============================================================================
  
  // How to load in modules
  const Scene = require('Scene');
  
  // Use export keyword to make a symbol available in scripting debug console
  export const Diagnostics = require('Diagnostics');
  
  // Enables async/await in JS [part 1]
  (async function() {
  
  // To use variables and functions across files, use export/import keyword
  // export const animationDuration = 10;
  
  // Use import keyword to import a symbol from another file
  // import { animationDuration } from './script.js'
  
  // To access scene objects
  // const [directionalLight] = await Promise.all([
  //   Scene.root.findFirst('directionalLight0')
  // ]);
  
  // To access class properties
  // const directionalLightIntensity = directionalLight.intensity;
  
  // To log messages to the console
  // Diagnostics.log('Console message logged from the script.');
  
  // Enables async/await in JS [part 2]
  })();
	
```

Scripting is broken down into modules with each module implementing a particular functionality.

I am really excited to get into these new softwares and start creating. 
