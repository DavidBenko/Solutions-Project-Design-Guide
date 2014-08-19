AnyPresence Solutions CoffeeScript Style Guide
=================================

This style guide outlines the coding conventions of the CoffeeScript code at [AnyPresence](http://anypresence.com).

Table of Contents
---------
- [Background](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#background)
- [Language](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#language)
- [Code Organization](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#code-organization)
- [Spacing](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#spacing)
- [Semicolons](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#semicolons)
- [Linting](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#linting)
- [Comments](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#comments)
- [Quotes](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#quotes)
- [Variables](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#variables)
  - [Global Variables](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#global-variables)
  - [Private Variables](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#private-variables) 
- [Functions](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#functions)
- [Naming](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#naming)
- [Operators](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#operators)
  - [Logical Operators](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#logical-operators)
- [Conditionals](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#conditionals)
- [Prototypes](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#prototypes)
- [Closures](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#closures)
- [Singletons](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#singletons)
- [Backbone.js](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/coffeescript-style.md#)

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

Quotes
---------
**Always** use single quotes, unless you are writing JSON or using string interpolation.

**Preferred:**
```coffeescript
foo = 'bar'
```

**Not Preferred:**
```coffeescript
foo = "bar"
```

Variables
---------
Variables should be named as descriptively as possible. Single letter variable names should be avoided except in `for()` loops. 

#### Global Variables
Each project may expose at most one global variable.

#### Private Variables
Prefix private variables with `_`. This is a convention to compensate for JavaScript's lack of private properties on objects. Being able to identify private methods is important because it tells us that we don't need to test those methods and that they will not be coupled to anything outside of the object.

**Preferred:**
```coffeescript
_privateVariable = 6
```

The `do` keyword in CoffeeScript lets us execute functions immediately, a great way of encapsulating scope & protecting variables. In the example below, we're defining a variable `_classToType` in the context of an anonymous function which's immediately called by do. That anonymous function returns a second anonymous function, which will be ultimate value of type. Since `_classToType` is defined in a context that no reference is kept to, it can't be accessed outside that scope.

```coffeescript
# Execute function immediately
type = do ->
  _classToType = {}
  for name in 'Boolean Number String Function Array Date RegExp Undefined Null'.split(' ')
    _classToType['[object ' + name + ']'] = name.toLowerCase()

  # Return a function
  (obj) ->
    strType = Object::toString.call(obj)
    _classToType[strType] or 'object'
```

In other words, `_classToType` is completely private, and can never again be referenced outside the executing anonymous function. This pattern is a great way of encapsulating scope and hiding variables.

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
Conditionals should use the positive case if possible when using an `else` body. If there is no `else` body, it is fine to use the negative case. Prefer `unless` over `if not`.

**Preferred:**
```coffeescript
# If with else body
if someVariable 
	# Do Something
else 
	# Do Something


# If with no else body
unless someOtherVariable
	# Do Something
```

**Not Preferred:**
```coffeescript
if not someVariable
  # Do Something


unless(someVariable)
	# Do Something
else
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
Singletons should use this pattern ([adapted from Google](http://code.google.com/p/jslibs/wiki/JavascriptTips#Singleton_pattern) to work in "strict" mode)

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

Backbone.js
---------
Adhere to all of the best practices outlined [here](https://gist.github.com/liammclennan/2886952#backbone-specific).
