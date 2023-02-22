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