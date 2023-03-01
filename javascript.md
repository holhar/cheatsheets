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

The output of the code snippet above will be `Iron Man is copyrighted by Marvel`.

Changing `avengersHero.editor` afterwards would also change the output!

### Constructors vs Constructor Functions

In Javascript an attempt was made to make object creation similar to languages like Java. Let's take for example:

    function SuperHero(name, strength) {
        this.name = name;
        this.strength = strength;
    }

Notice the capitalized name, indicating that it's a constructor function. Let's see how it can be used:

    var superman = new SuperHero('Superman', 100);

    console.log('Hello, my name is ' + superman.name);

This code snippet outputs `Hello, my name is Superman`.

You might think that this looks just like Java, and that is exactly the point! 
What this `new` syntax really does is to it creates a new empty object, and then calls the constructor function by forcing `this` to be the newly created object.

#### Why is this syntax not recommended then?

Let's say that we want to specify that all super heroes have a `sayHello` method.
This could be done by putting the `sayHello` function in a common prototype object:

    function SuperHero(name, strength) {
        this.name = name;
        this.strenth = strength;
    }

    SuperHero.prototype.sayHello = function() {
        console.log('Hello, my name is ' + this.name);
    }

    var superman = new SuperHero('Superman', 100);
    superman.sayHello();

This would output 'Hello, my name is Superman'.

But the syntax `SuperHero.prototype.sayHello` looks anything but Java like!
The new operator mechanism sort of half looks like Java but at the same time is completely different.

#### Is there a recommended alternative to `new`?

The recommended way to go is to ignore the Javascript `new` operator altogether and use `Object.create`:

    var superHeroPrototype = {
        sayHello: function() {
            console.log('Hello, my name is ' + this.name);
        }
    };

    var superman = Object.create(superHeroPrototype);
    superman.name = 'Superman';

Unlike the `new` operator, one thing that Javascript absolutely got right where Closures.