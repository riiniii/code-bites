---
title: 'JavaScript Closures'
description: "A code-bite on closures in JavaScript."
categories: [javascript]
comments: true
---
# JavaScript Closures

Even though JavaScript engines compile and interpret JavaScript code, JavaScript is still considered to be a **compiled** **language**. Why does this matter? 

This matters to us because during compilation time is when JavaScript **determines the lexical scope** of its variables, functions, and blocks in relation to each other.  

Thus, at compile time, our mapping of all the scopes in relation to each other is done. 

Let's give an example of code with three different scopes. 

```jsx
	var desserts = [{ name: 'Crepe Cake', dessertId: 0}, 
									{ name: 'Chocolate Cake', dessertId: 1},
									{ name: 'Chocolate Ice Cream', dessertId: 2}]
	
	function getDessertName(dessertId){
		for (let dessert of desserts){
			if (dessert.dessertId === dessertId){
				return dessert.name
			}
		}
	}

	var dessertName = getDessertName(0);

	console.log(dessertName);
	// Crepe Cake
```

In the above example, we have: 

1. global scope
2. function scope of getDessertName
3. block scope of the for loop inside the getDessertName function

Scope (1) nests scope (2) and (3), and scope (2) nests scope (3). Any scope that is nested under another parent scope can access all variables and functions in the parent scope.  

This is relevant for closure because closures allow us to save values **outside of its current scope** with the help of **functions**. If you aren't working with functions, then you don't have a closure! 

In layman terms, a closure is when a function returns a function that references variables outside of its own scope. This is really helpful when you want to save a value and come back to use it later. 

I personally often use it with event listeners. I tie a value to the event listener, then later it is called and can access the value I tied it too. Here's an example!

```jsx
const buttonInfo = {beep: 'boop', boop: 'beep'}
const buttonWrapper = (buttonType) => {
	const buttonData = buttonInfo[buttonType];
	return (event) => buttonData;
}

const beepButtonType = buttonWrapper('beep')

// beepButtonType can be called again whenever you want, and it can access the specific
// data it received when it was first called with buttonWrapper('beep')
// buttonData is saved whenever buttonWrapper is called.
```

Closures work well especially whenever you try to curry a function, or just generally in functional programming!

Closures are also good for when we want to privately make changes to a variable. An example of that would be below. 

```jsx

const incrementCakeLoveCount = () => {
	// our "private" variable, that cannot be accessed from outer scope!
	let cakeLoveCount = 0 
	return cake => {
		cakeLoveCount += cake.loveCount
		return cakeLoveCount
	}
}

const incrementer = incrementCakeLoveCount()
console.log(incrementer({loveCount: 5, type: 'chocolate'})) // 5
console.log(incrementer({loveCount: 5.5, type: 'strawberry-shortcake'})) // 10.5
```

Hopefully this code bite was an easy introduction or refresh on how closures work with scope, and how you can use them.