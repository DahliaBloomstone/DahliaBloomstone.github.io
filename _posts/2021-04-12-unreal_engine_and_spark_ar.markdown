---
layout: post
title:      "UNREAL ENGINE AND SPARK AR "
date:       2021-04-12 21:33:21 +0000
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
