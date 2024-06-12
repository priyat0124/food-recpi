1.App.js
import React, { useEffect, useState } from 'react'
import './App.css'; 
import Recipe from './Recipe'; 
const App = () => { 
const APP_ID = <YOUR_APP_ID>; 
const APP_KEY = <YOUR_APP_KEY>; 
const [recipes, setRecipes] = useState([]); 
const [search, setSearch] = useState(""); 
const [query, setQuery] = useState("chicken"); 
useEffect(() => { 
	getRecipes(); 
}, [query]) 
const getRecipes = async () => { 
	const response = await fetch 
	(`https://api.edamam.com/search?q=${query}&app_id=${APP_ID}&app_key=${APP_KEY}`); 
	const data = await response.json(); 
	setRecipes(data.hits); 
}; 
const updateSearch = e => { 
	setSearch(e.target.value); 
}; 
const getSearch = e => { 
	e.preventDefault(); 
	setQuery(search); 
	setSearch(""); 
} 
return ( 
	<div className="App"> 
<form className="search-form" onSubmit={getSearch} > 
		<input className="search-bar" type="text" value={search} onChange={updateSearch} /> 
<button className="search-button" type="submit" > 
Search </button> 
</form> 
	<div className="recipes"> 
		{recipes.map(recipe => ( 
		<Recipe 
			key={recipe.recipe.label} 
			title={recipe.recipe.label} 
			calories={recipe.recipe.calories} 
			image={recipe.recipe.image} 
			ingredients={recipe.recipe.ingredients} /> 
))} 
</div> 
</div> 
); 
} 
export default App;

2.Recipe.js
import React from "react"; 
import style from './recipe.module.css'; 
const Recipe = ({title,calories,image,ingredients}) =>{ 
	return( 
		<div className={style.recipe}> 
			<h1>{title}</h1> 
			<ol> 
				{ingredients.map(ingredient=>( 
					<li>{ingredient.text}</li> 
				))} 
			</ol> 
<p>Calories : {calories}</p> 
<img className={style.image} src={image} alt=""/> 
</div> 
); 
} 
export default Recipe;

3. CSS
.App{ 
min-height: 100vh; 
background-image: linear-gradient(15deg, #13547a 0%, #80d0c7 100%); 
} 
.search-form{ 
min-height: 10vh; 
display: flex; 
justify-content: center; 
align-items: center; 
} 
.search-bar{ 
width: 50%; 
border:none; 
padding: 10px; 
border-radius: 5px; 
box-shadow: 5px 10px #979b91; 
} 
.search-button{ 
background: #4da1ab; 
border: 5px solid white; 
border-radius: 8px; 
padding: 10px 20px; 
color: white; 
font-size: larger; 
margin: 0 0 0 10px; 
} 
.search-button:hover { 
background-color:#fa709a ; 
} 
.recipes{ 
display: flex; 
justify-content: space-around; 
flex-wrap: wrap; 
}


4. Recipr.module.css
@import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap'); 
.recipe{ 
	border-radius: 10px; 
	box-shadow: 0px 5px 20px rgb(63, 60, 60); 
	margin: 20px; 
	display: flex; 
	flex-direction: column; 
	justify-content: space-around; 
	background-image: linear-gradient(to right, 
		#e4afcb 0%, #b8cbb8 0%, #b8cbb8 0%, 
		#e2c58b 30%, #c2ce9c 64%, #7edbdc 100%); 
	align-items: center; 
	min-width: 40%; 
	font-family: 'Lobster', cursive; 
} 
.image{ 
	border-radius: 10px; 
	margin:0px 0px 20px 0px; 
}
