---
layout: post
title:      "Figma Design + React + Responsive Site | UI/UX"
date:       2021-04-26 20:40:37 -0400
permalink:  figma_design_react_responsive_site_ui_ux
---

I'm still learning all of the design + code stuff from the ground up!

 Implementation from design to code:

Since the launch of the Figma API, many people have speculated about the possibility of automatically turning Figma documents into React components.
 
 Getting Started with Create React App.
 
-Figma inspect is a great feature by Figma by which you can convert your design element into code.. it provides various options from which you can convert your design into Android (XML), iOS (Swift), Web (CSS) with so much ease.. you just have to select any element from the design and it will generate the code for it.

-A design system is a living style guide that’s collaborative and code-connected. It’s not just a style guide where designers are the only contributors. It’s shared across the whole team, including designers, developers, product managers, etc. As a result, the design system should be cohesive, dynamic, reusable and maintainable both in design and code.

https://github.com/DahliaBloomstone/design-2-code

https://www.w3schools.com/graphics/svg_examples.asp I'm also thinking about How To Animate SVG With CSS. 

I also learned about React Tilt and parallax: 

```
Basic - background image with fixed blur effect
import { Parallax } from 'react-parallax';

const Container = () => (
    <Parallax blur={10} bgImage="path/to/image.jpg" bgImageAlt="the cat" strength={200}>
        Content goes here. Parallax height grows with content height.
    </Parallax>
);
```

yarn add react-parallax

Install
yarn: yarn add react-tilt
npm: npm install --save react-tilt

resources: https://www.npmjs.com/package/react-parallax and https://www.npmjs.com/package/react-tilt
