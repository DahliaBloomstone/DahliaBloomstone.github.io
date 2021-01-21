---
layout: post
title:      "Final React: Class vs. Functional Components and more! "
date:       2021-01-20 19:30:44 -0500
permalink:  final_react_class_vs_functional_components_and_more
---


Functional Components: Used only for display purposes, can access props from function parameter, sort of like static components 

For example, in my application, my "Footer" would be a functional component: 

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


Class-based Components: Used for handling state and accessing React lifecycle methods, can access props using this.props, will have componentDidMount, smart component, smart enough to maintain its own state (stores data of the component, rerenders whenever the component changes) 

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
