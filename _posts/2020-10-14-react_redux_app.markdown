---
layout: post
title:      "REACT REDUX APP #"
date:       2020-10-14 23:25:02 +0000
permalink:  react_redux_app
---

create github repository
npx create-react-app character-creator 
cd into the file 
npm start

deleted unnecessary files

API: generates.photos 
https://generated.photos/
create an account

https://generated.photos/account#apikey

API KEY:
https://api.generated.photos/api/v1/faces?api_key=YOUR_API_KEY


npm install axios 
add api key to app.js 

command shift c to go to console 
should see Object data to see api key data 

you can specify with indeces specific images 

Example: specifying female images 
&gender=female 
in the api key at the end write: 
    axios.get('https://api.generated.photos/api/v1/faces?api_key=-oSJ9MnkYiiimwgLEOefKQ&gener=female').then(res => {

then in the .then statement:
 .then(res => {
      console.log(res.data.faces[0].urls[4][512]);
			
	


