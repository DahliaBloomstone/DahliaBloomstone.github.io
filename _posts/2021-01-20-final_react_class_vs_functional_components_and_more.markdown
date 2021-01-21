---
layout: post
title:      "Final React: Class vs. Functional Components and more! "
date:       2021-01-20 19:30:44 -0500
permalink:  final_react_class_vs_functional_components_and_more
---

--------------------------------------------------------------------------------


**Functional Components:** Used only for display purposes, can access props from function parameter, sort of like static components. The syntax is also different, a functional component is a Javascript function that returns JSX. It can be known as a stateless component, whereas Class Components are known as Stateful. These components simply return UI: they accept data, display them and render UI.

For example, in my application, my "Footer" would be a functional component: You will notice there is no render method.

```
import React from 'react';
const Footer = () => {
  return (
    <div className='Footer'>
     <h4> <p><a href="https://github.com/DahliaBloomstone/react-redux-app/tree/main/character-creator/src/components">DahliaBloomstone</a> hi &#169;2020</p></h4>
    </div>
  )
}

export default Footer;

```


**Class-based Components:** Used for handling state and accessing React lifecycle methods, can access props using this.props, will have componentDidMount, is a smart component, smart enough to maintain its own state (stores data of the component, rerenders whenever the component changes). It is a Javascript class that extends React.Component which has a render method. This is more complex UI logic.

For example, in my application, my CharacterCard is a class component: 

```
import React, { Component } from 'react';
import { connect } from 'react-redux';
import { deleteCharacter, createCharacter } from '../actions/characters';

class CharacterCard extends Component {

  state = {
    count: 0
  }

  likerFunction = () => {
    let newLike = this.state.count + 1
    this.setState({
      count: newLike
    })
  }

  render() {
    console.log(this.props); //IMPORTANT 
    const { id, name, location, image_url, date, background_info, } = this.props.character;
    return ( 
      <div key={id} className="CharacterCard">
        <img className="CharacterImage" src={image_url} alt={name} />
        <h4 className="CharacterName">{name}</h4>
        <p>{date} &#124; {location}</p>
        <p>{background_info}</p>

        <button onClick={this.likerFunction}> Likes: {this.state.count} </button>

        <button
          type="button"
          title="Delete Character"
          className="btn-delete"
          onClick={() => this.props.deleteCharacter(this.props.character)}
        >:(</button>
      </div>
    )
  }

};

const mapStateToProps = (state) => {
  return { characters: state.characters }
}

export default connect(mapStateToProps, {deleteCharacter, createCharacter}, null)(CharacterCard);


```


These components also **pass props differently**. Inside a functional component, we pass props as an argument of the function. Inside a class component, you need to use *this* to refer to props.

How about handling state in functional vs. class components? I didn't use this in my application, but we can use something called useState, which is a hook. 

Hooks: functions that let you use React state and lifecycle features from functional components. They do not work inside classes. 

For class components, we handle state thinking about the React.Component constructor, state keys, initial values, and mounting. and the setState function.

Apparently, functional components are taking over and becoming more popular as they are shorter and simpler. 

--------------------------------------------------------------------------------



****Conditional Rendering:****ability to render different UI based on certain conditions. This will be important when thinking about showing and hiding elements, APIs, toggling, and authentication. Think if else statements!

We use JS operators like if to create elements that represent the current state and let React update the UI. We can look at the sort method in my application as an example:

```
import React, { Component } from 'react';
import { connect } from 'react-redux';
import './Characters.css';
import CharacterCard from '../components/CharacterCard';
import CharacterForm from './CharacterForm'; 
import { getCharacters } from '../actions/characters';

class Characters extends Component{

  constructor(props)
  { super(props)
    this.state = {sort: false, allCharacters: [] }
  }

 async componentDidMount() {
    console.log("App Mounted");
    const fetchedCharacters = await this.props.getCharacters()
    this.props.getCharacters()
    this.setState({sort: false, allCharacters: this.props.characters })
  }

  sortCharacters = () => {
    this.setState({allCharacters: this.props.characters.sort(function(characterA, characterB) {
      if(characterA.name < characterB.name) {
        return -1
      } else {
        return 1
      }
      })
    })
  }

  render() {
    console.log(this.props); 
    return (
      <>
      <div id="characters">
        <br></br>
        {<button onClick={this.sortCharacters}> Sort: </button>}
      </div>
      <div>
        <div className="CharactersContainer">
          <h1>Characters</h1>
          {this.state.allCharacters.map(character =>
            <CharacterCard
              key={character.id}
              character={character}
            />
          )}
        </div>
        <CharacterForm />
      </div>
        </>
    )
  }

};

const mapStateToProps = (state) => {
  return ({
    characters: state.characters
  })
};

export default connect(mapStateToProps, { getCharacters })(Characters);
```
