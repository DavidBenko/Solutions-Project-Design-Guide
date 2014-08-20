AnyPresence Solutions CoffeeScript Style Guide
=================================

This style guide outlines the coding conventions of the CoffeeScript code at [AnyPresence](http://anypresence.com).

Table of Contents
---------
- [Background](#background)
- [Language](#language)
- [Code Organization](#code-organization)
- [Spacing](#spacing)
- [Semicolons](#semicolons)
- [Linting](#linting)
- [Comments](#comments)
- [Quotes](#quotes)
- [Variables](#variables)
  - [Global Variables](#global-variables)
  - [Private Variables](#private-variables) 
- [Functions](#functions)
- [Naming](#naming)
- [Operators](#operators)
  - [Logical Operators](#logical-operators)
- [Conditionals](#conditionals)
- [Prototypes](#prototypes)
- [Closures](#closures)
- [Singletons](#singletons)
- [Backbone.js](#)
- [Object Oriented vs Procedural Programming](#object-oriented-vs-procedural-programming)


Background
---------
Here are some of the documents that informed the style guide. If something isn't mentioned here, it's probably covered in great detail in one of these:

- [CoffeeScript Style Guide](https://github.com/polarmobile/coffeescript-style-guide)
- [CoffeeScript FAQ](https://github.com/jashkenas/coffeescript/wiki/FAQ)
- [CoffeeScript-specific Style Guide](http://awardwinningfjords.com/2011/05/13/coffeescript-specific-style-guide.html)
- [Common CoffeeScript idioms](https://arcturo.github.io/library/coffeescript/04_idioms.html)


Language
---------
US English should be used throughout. 

**Preferred:**
```coffeescript
myColor = '#FFF'
```

**Not Preferred:**
```coffeescript
myColour = '#FFF'
```

Code Organization
---------
Organise modules first by type, then by function

```
models/
  shopping.coffee
  admin.coffee
views/
  shopping.coffee
  admin.coffee
```

This minimizes coupling and maximizes cohesion because dependencies tend to go the same way (ie routers depend on models and views, views depend on models) and cohesion tends to be high inside of a module containing models for a certain feature, or views for a certain feature.

Spacing
---------
- Indent using 2 spaces. Never indent with tabs.
- No whitespace at the end of line or on blank lines.
- Use UNIX-style newlines (`\n`), and a newline character as the last character of a file. Windows-style newlines (`\r\n`) are forbidden inside any repository.
- There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but often there should probably be new methods.

Semicolons
---------
Do not use them.

Linting
---------
[CoffeeLint](http://www.coffeelint.org/) is a style checker that helps keep CoffeeScript code clean and consistent. CoffeeScript does a great job at insulating programmers from many of JavaScript's bad parts, but it won't help enforce a consistent style across a code base. CoffeeLint can help with that.

Comments
---------
When they are needed, comments should be used to explain why a particular piece of code does something. Any comments that are used must be kept up-to-date or deleted.

Block comments should generally be avoided, as code should be as self-documenting as possible, with only the need for intermittent, few-line explanations.

**All** class-like objects and methods should be commented using [YUI Doc](http://yui.github.io/yuidoc/syntax/) style comments.


Quotes
---------
**Always** use single quotes, unless you are writing JSON or using string interpolation.

**Preferred:**
```coffeescript
foo = 'bar'
bar = "#{foo} is awesome"
```

**Not Preferred:**
```coffeescript
foo = "bar"
bar = foo + ' is awesome'
```

Variables
---------
Variables should be named as descriptively as possible. Single letter variable names should be avoided except in `for()` loops. 

#### Global Variables
Each project may expose at most one global variable.

#### Private Variables
The `do` keyword in CoffeeScript lets us execute functions immediately, a great way of encapsulating scope & protecting variables. In the example below, we're defining a variable `classToType` in the context of an anonymous function which's immediately called by do. That anonymous function returns a second anonymous function, which will be ultimate value of type. Since `classToType` is defined in a context that no reference is kept to, it can't be accessed outside that scope.

```coffeescript
# Execute function immediately
type = do ->
  classToType = {}
  for name in 'Boolean Number String Function Array Date RegExp Undefined Null'.split(' ')
    classToType['[object ' + name + ']'] = name.toLowerCase()

  # Return a function
  (obj) ->
    strType = Object::toString.call(obj)
    classToType[strType] or 'object'
```

In other words, `classToType` is completely private, and can never again be referenced outside the executing anonymous function. This pattern is a great way of encapsulate scope and hide variables.

Functions
---------
- When declaring a function that takes arguments, always use a single space after the closing parenthesis of the arguments list. 
- Do not use parentheses when declaring functions that take no arguments.
- When calling functions, choose to omit or include parentheses in such a way that optimizes for readability.

**Preferred:**
```coffeescript
foo = (arg1, arg2) ->
  # Do Stuff
  
bar = ->
  # Do Stuff
```

**Not Preferred:**
```coffeescript
foo = (arg1, arg2)->
  # Do Stuff
  
bar = () ->
  # Do Stuff
```

Naming
---------
Use `camelCase` (with a leading lowercase character) to name all variables, methods, and object properties.

Use `CamelCase` (with a leading uppercase character) to name all classes. (This style is also commonly referred to as `PascalCase`, `CamelCaps`, or `CapWords`, among [other alternatives](http://en.wikipedia.org/wiki/CamelCase#Variations_and_synonyms).)

(The official CoffeeScript convention is camelcase, because this simplifies interoperability with JavaScript. For more on this decision, see [here](https://github.com/jashkenas/coffee-script/issues/425).)

Operators
---------
Always add a single space before and after the use of an operator. 

**Preferred:**
```coffeescript
foo = 'bar';
answer = 42;
answer += 9;
answer++;
answer = 40 + 2;
```

**Not Preferred:**
```coffeescript
foo='bar';
answer=42;
answer+= 9;
++answer;
answer= 40+2;
```

When incrementing a variable, the `++`, `--`, etc are preferred to be after the variable instead of before to be consistent with other operators. Operators separated should always be surrounded by spaces unless there is only one operand.

**Preferred:**
```coffeescript
answer++;
```

#### Logical Operators

- `and` is preferred over `&&`.
- `or` is preferred over `||`.
- `is` is preferred over `==`.
- `not` is preferred over `!`.
- `or=` should be used when possible:

**Preferred:**
```coffeescript
myFavoriteVariable or= {}
```

**Not Preferred:**
```coffeescript
myFavoriteVariable = myFavoriteVariable || {}
```

Conditionals
---------
Conditionals should use the positive case if possible when using an `else` body. If there is no `else` body, it is fine to use the negative case.

**Preferred:**
```coffeescript
# If with else body
if someVariable 
	# Do Something
else 
	# Do Something


# If with no else body
if !someOtherVariable
	# Do Something
```


Prototypes
---------
**Do not extend built-in prototypes.**

**Preferred:**
```coffeescript
a = []
unless a.length
  console.log 'winning'
```

**Not Preferred:**
```coffeescript
Array::empty = ->
  not this.length

a = []
if a.empty()
  console.log 'losing' 
```

Closures
---------
Closures should be named to produce better stack traces, heap and cpu profiles. Use closures, but do not nest them. 

**Preferred:**
```coffeescript
afterConnect = ->
  console.log 'connected'

setTimeout (connect = ->
  client.connect afterConnect
), 1000

```
**Not Preferred:**
```coffeescript
setTimeout (->
  client.connect ->
    console.log 'losing'
), 1000
```

Singletons
---------
Singletons are classes which are either not instantiated or instantiated only once.

```coffeescript
class Singleton
  # You can add statements inside the class definition
  # which helps establish private scope (due to closures)
  # instance is defined as null to force correct scope
  instance = null
  # Create a private class that we can initialize however
  # defined inside this scope to force the use of the
  # singleton class.
  class PrivateClass
    constructor: (@message) ->
    echo: -> @message
  # This is a static method used to either retrieve the
  # instance or create a new one.
  @get: (message) ->
    instance ?= new PrivateClass(message)

a = Singleton.get 'Hello A'
a.echo() # => "Hello A"

b = Singleton.get 'Hello B'
b.echo() # => "Hello A"

Singleton.instance # => undefined
a.instance # => undefined
Singleton.PrivateClass # => undefined
```

Classes
-------
CoffeeScript provides a familiar syntax for declaring classes and class inheritance.  Once compiled to JavaScript, classes become constructor functions with efficient prototype chains to express default members and inheritance.

```coffeescript
###*
Base animal class provides attributes for names.
@class Animal
###
class Animal
  ###*
  Genus name of this animal.
  @property genus
  @type String
  ###
  genus: 'None'
  
  ###*
  Species name of this animal, excluding genus.
  @property species
  @type String
  ###
  species: 'none'
  
  ###*
  Common name of this animal.
  @property commonName
  @type String
  ###
  commonName: null
  
  ###*
  @constructor
  @param {String} genus genus name of this animal
  @param {String} species species name of this animal, excluding genus
  @param {String} commonName common name of this animal
  ###
  constructor: (@genus, @species, @commonName) ->
    # pass
  
  ###*
  Generates and returns the full species name of this animal.
  @method getSpeciesName
  @return {String} species name of this animal
  ###
  getSpeciesName: ->
    "#{@genus} #{@species}"
  
  ###*
  Returns the common name of this animal.
  @method getCommonName
  @return {String} common name of this animal
  ###
  getCommonName: ->
    @commonName


###*
Represents a Cockatoo animal.
@class Cockatoo
@extends Animal
###
class Cockatoo extends Animal
  ###*
  Generates and returns the common name of this cockatoo.
  @method getCommonName
  @return {String} common name of this cockatoo
  ###
  getCommonName: ->
    "#{super} Cockatoo"


# create an instance of a cockatoo
gangGang = new Cockatoo 'Callocephalon', 'fimbriatum', 'Gang-Gang'


# outputs "Gang-Gang Cockatoo"
console.log gangGang.getCommonName()
```


Backbone.js
---------
Adhere to all of the best practices outlined [here](https://gist.github.com/liammclennan/2886952#backbone-specific).


Object Oriented vs Procedural Programming
-----------------------------------------
While it may not seem apparent to beginner JavaScript developers, JavaScript has a rich object-oriented feature set.  These features should be maximized.  Avoid procedural programming conventions.  For example, instead of declaring orphaned variables and functions, use a class.

**Preferred, object-oriented:**
```coffeescript
class AP.MyClass
  counter: 0
  constructor: (@myRandomData) ->
    # pass
  increment: ->
    @counter++
```

**Not preferred, procedural:**
```javascript
# orphaned variable, not part of any class or object
counter = 0
# orphaned function, not part of any class or object
increment = -> counter++
```
