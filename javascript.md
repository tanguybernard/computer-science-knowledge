# Javascript

## Intro


## Class (a class is a Function)


    function Hero(name, level) {
    	this.name = name;
    	this.level = level;
    }
    
    // Adding a method to the constructor
    Hero.prototype.greet = function() {
    	return `${this.name} says hello.`;
    }

Syntaxe class :

    class Hero {
    	constructor(name, level) {
    		this.name = name;
    		this.level = level;
    	}
    
    	// Adding a method to the constructor
    	greet() {
    		return `${this.name} says hello.`;
        }
    }
