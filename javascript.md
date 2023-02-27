# JavaScript Cheat Sheet

## Angular for Java Developers

POI: https://blog.angular-university.io/javascript-for-java-developers/

### Objects Only - No Classes

A JavaScript object is a multi-level 'hash map' of key/value pairs, with no class definition needed.

    // create an empty object - no class definition needed
    var superhero = {};

    superhero.name = 'Spider-Man';
    superhero.strength = 100

### Functions Are Just Values

Functions in Javascript are just values of type `Function`.

    var flyFunction = function() {
        console.log('Crawling like a spider!');
    };

    superhero.fly = flyFunction;

This creates a function (a value of type `Function`) and assigns it to a variable `flyFunction`. 
A new property named `fly` is then created in the superhero object, that can be invoked like this:

    superhero.fly();

### The 'this' Keyword Usage

    var superman = {
        heroName: 'Superman',

        sayHello: function() {
            console.log("Hello, I'm " + this.heroName);
        }
    }

    superman.sayHello(); // => output: 'Hello, I'm Superman'

#### What if we pass the function around?

By passing around `sayHello`, we can easily end up in a context where there is no `heroName` property:

    var failThis = superman.sayHello;

    failThis(); // => output: 'Hello, I'm undefined'

#### Why does `this` not work anymore?

This is because the variable `failThis` belongs to the global scope, which contains no member variable named `heroName`.
To solve this:

NOTE: In JavaScript the value of the `this` keyword is completely overridable to be anything that we want!

    // overrides 'this' with superman
    hello.call(superman); // => output: 'Hello, I'm Superman'

The value of `this` depends on both the context on which the function is called, and on *how* the function is called.

### Classic vs Prototypal Inheritance

In JavaScript, there is no class inheritance, instead objects can inherit directly from other objects.
The way this works is that each object has an implicit property that points to a 'parent' object.

That property is called `__proto__`, and the parent object is called the object's **prototype**, hence the name Prototypal Inheritance.

### How does `prototype` work?

When looking up a property, Javascript will try to find the property in the object itself.
If it does not find it then it tries in it's prototype, and so on.
For example:

    var avengersHero = {
        editor: 'Marvel'
    }

    var ironMan = {};

    ironMan.__proto__ = avengersHero;

    console.log('Iron Man is copyrighted by ' + ironMan.editor);