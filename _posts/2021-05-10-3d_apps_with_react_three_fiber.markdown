---
layout: post
title:      "3D APPS WITH REACT THREE FIBER "
date:       2021-05-10 20:56:22 +0000
permalink:  3d_apps_with_react_three_fiber
---

![](https://user-images.githubusercontent.com/63209579/117723607-93fb1c00-b1b0-11eb-8822-b3399f69b098.png)

Three.js is a library that makes it easier to create 3D graphics in the browser, it uses a canvas + WebGL to display the 3D models and animations, you can learn more here.

react-three-fiber reduces the time spent on animations because of its reusable components, binding events and render loop. 

1. Create React App
2. Install dependencies: yarn add @react-spring/core react-spring react-three-fiber
3. also: three
4. create a new component: box.js

Bunch of hooks: Spring animates the rotation and scale of the boxes. 
```
import React, { useState, useEffect, useRef } from 'react' 
import { useSpring } from '@react-spring/core'
import { a } from "@react-spring/three" 

```


1. Down here what is happening: array of x,y,andz coordinates. 
2. It will hold the state. 
3. Define the spring and specify the parameters of the animation. 
4. Define the layout (rotation, scale)
5. Render the box buffer geometry, the size of the cube. 
6. Attach the material (mesh standard material) 
```
export const Box = ({ position }) => {
    const [ active, setActive] = useState(0)
    const activeRef = useRef(active)
    activeRef.current = active
  
    useEffect(() => {
      let timeout
      const toggleActive = () => {
        timeout = setTimeout(() => {
          setActive(Number(!activeRef.current))
          toggleActive()
        }, Math.random() * 2000 + 1000)
      }
      toggleActive()
      return () => {
        clearTimeout(timeout)
      }
    }, [])
  
    const { spring } = useSpring({
      spring: active,
      config: { mass: 5, tension: 400, friction: 50, precision: 0.0001 }
    })
  
    const scale = spring.to([0, 1], [1, 2])
    const rotation = spring.to([0, 1], [0, Math.PI])
    const color = spring.to([0, 1], ["#50c878", "#e45858"])
  
    return (
      <a.mesh
        rotation-y={rotation}
        scale-x={scale}
        scale-y={scale}
        scale-z={scale}
        position={position}
      >
        <boxBufferGeometry attach="geometry" args={[1, 1, 1]}/>
        <a.meshStandardMaterial roughness={0.5} attach="material" color={color}/>
      </a.mesh>
    )
  }
```

TOGGLE ACTIVE: must call for the boxes to be able to animate. 

Define an affect that will trigger the state? 
useEffect. It returns the function. 

export Box.js and import it in app.js

ambientLight, pointLight, camera and canvas:
* the canvas: is used to draw the graphics on the browser.
* ambientLight: This is used to light all objects in a scene or model equally, it accepts props such as the intensity of the light.
* pointLight: This works similar to the light of a light bulb, light is emitted from a single point to all directions, this will be necessary for the active state of our application.


```
import React from "react";
import { Canvas } from "react-three-fiber";
import { Box } from "./Box";

function App() {
  return (
    <Canvas camera={{ position: [-10, 10, 10], fov: 35 }}>
      <ambientLight />
      <pointLight position={[-10, 10, -10]} castShadow />
      {[-3, 0, 3].map((x) =>
        [-3, 0, 3].map((z) => <Box position={[x, 0, z]} />)
      )}
    </Canvas>
  );

}

export default App;
```

helpful article; https://www.smashingmagazine.com/2020/11/threejs-react-three-fiber/
