AnyPresence Solutions Java Style Guide
=================================

This style guide outlines the coding conventions of the Java code at [AnyPresence](http://anypresence.com).

Table of Contents
---------
- [Background](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#background)
- [Language](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#language)
- [Code Organization](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#code-organization)
- [Spacing](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#spacing)
- [Comments](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#comments)
- [Annotations](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#annotations)
- [Variables](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#variables)
- [Naming](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#naming)
- [Methods](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#methods)
- [Operators](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#operators)
- [Conditionals](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#conditionals)
- [Ternary Operator](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#ternary-operator)
- [Exception Handling](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#exception-handling)
- [Singletons](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#singletons)
- [Dependency Management](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/java-style.md#dependency-management)


Background
---------
Here are some of the documents that informed the style guide. If something isn't mentioned here, it's probably covered in great detail in one of these:

- [Code Conventions for the Java Programming Language](http://www.oracle.com/technetwork/java/codeconvtoc-136057.html)
- [Google Java Style](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html)
- [Code Style Guidelines for Contributors](https://source.android.com/source/code-style.html)

Language
---------
US English should be used throughout. 

**Preferred:**
```java
int myColor = Color.argb(255, 134, 175, 255);  
```

**Not Preferred:**
```java
int myColour = Color.argb(255, 134, 175, 255);  
```

Code Organization
---------
Code should be organized in the following format:
- Class/interface documentation comment
- `class` or `interface` statement
- Class/interface implementation comment (` /*...*/`), if necessary
- Class (`static`) variables
- Instance variables
- Constructors
- Methods (grouped by functionality, not scope or accessibility)



Spacing
---------
- Indent using 4 spaces. Never indent with tabs.
- Method braces and other braces (`if`/`else`/`switch`/`while` etc.) **always** line up vertically in the same column as their construct.

**Preferred:**
```java
if (oatmeal == tasty)
{
    //Do something
}
else 
{
    //Do something else
}
```

**Not Preferred:**
```java
if (oatmeal == tasty) {
  //Do something
} else {
  //Do something else
}
```

- There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but often there should probably be new methods.

Comments
---------
When they are needed, comments should be used to explain why a particular piece of code does something. Any comments that are used must be kept up-to-date or deleted.

Block comments may be used at the beginning of each file and before each method. They can also be used in other places, such as within methods. Comments are indented at the same level as the code they describe. They may be in `/* ... */` style or `// ...` style. For multi-line `/* ... */` comments, subsequent lines must start with `*` aligned with the `*` on the previous line. 

**Preferred:**
```java
/*
 * This is
 * okay
 */
 
 
 // And so
 // is this.
 
```
Comments are not enclosed in boxes drawn with asterisks or other characters.

Tip from [Google's Java Style Guide](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html#s4.8.6.1-block-comment-style):
> Tip: When writing multi-line comments, use the /* ... */ style if you want automatic code formatters to re-wrap the lines when necessary (paragraph-style). Most formatters don't re-wrap lines in // ... style comment blocks.

**Never** use trailing-line comments. Instead, place single-line comments directly above the code they describe.

**Preferred:**
```java
if (myExtraSpecialNumber == 2) 
{
    // special case
    return true;
} 
else 
{
    // works only for odd number
    return isPrime(myExtraSpecialNumber);
}
```

**Not Preferred:**
```java
if (myExtraSpecialNumber == 2) 
{
    return TRUE;            /* special case */
} 
else 
{
    return isPrime(myExtraSpecialNumber);      /* works only for odd number */
}
```

**All** public methods should be commented in the class's header file using Javadoc style comments. 
```java
/**
 * Returns an Image object that can then be painted on the screen. 
 * The url argument must specify an absolute {@link URL}. The name
 * argument is a specifier that is relative to the url argument. 
 * <p>
 * This method always returns immediately, whether or not the 
 * image exists. When this applet attempts to draw the image on
 * the screen, the data will be loaded. The graphics primitives 
 * that draw the image will incrementally paint on the screen. 
 *
 * @param  url  an absolute URL giving the base location of the image
 * @param  name the location of the image, relative to the url argument
 * @return      the image at the specified URL
 * @see         Image
 */
 public Image getImage(URL url, String name) 
 {
        try 
        {
            return getImage(new URL(url, name));
        } 
        catch (MalformedURLException e) 
        {
            return null;
        }
 }
```

Annotations
---------
Use standard Java annotations. Annotations should precede other modifiers for the same language element. Simple marker annotations (e.g. `@Override`) can be listed on the same line with the language element. If there are multiple annotations, or parameterized annotations, they should each be listed one-per-line in alphabetical order.

Android standard practices for the three predefined annotations in Java are:

- `@Deprecated`: The `@Deprecated` annotation must be used whenever the use of the annotated element is discouraged. If you use the `@Deprecated` annotation, you must also have a `@deprecated` Javadoc tag and it should name an alternate implementation. In addition, remember that a `@Deprecated method` is still supposed to work. If you see old code that has a `@deprecated` Javadoc tag, please add the `@Deprecated` annotation.
- `@Override`: The `@Override` annotation must be used whenever a method overrides the declaration or implementation from a super-class. For example, if you use the `@inheritdocs` Javadoc tag, and derive from a class (not an interface), you must also annotate that the method `@Override`s the parent class's method.
- `@SuppressWarnings`: The `@SuppressWarnings` annotation should only be used under circumstances where it is impossible to eliminate a warning. If a warning passes this "impossible to eliminate" test, the `@SuppressWarnings` annotation must be used, so as to ensure that all warnings reflect actual problems in the code. When a `@SuppressWarnings` annotation is necessary, it must be prefixed with a `TODO` comment that explains the "impossible to eliminate" condition. This will normally identify an offending class that has an awkward interface. 
For example: 
```java
// TODO: The third-party class com.third.useful.Utility.rotate() needs generics `
@SuppressWarnings("generic-cast")
List<String> blix = Utility.rotate(blax);
```
When a `@SuppressWarnings` annotation is required, the code should be refactored to isolate the software elements where the annotation applies.


Variables
---------
Variables should be named as descriptively as possible. Single letter variable names should be avoided except in `for()` loops. Every variable declaration (field or local) declares only one variable: declarations such as `int a, b;` are not used. Class and member modifiers, when present, appear in the order recommended by the [Java Language Specification](http://java.sun.com/docs/books/jls/second_edition/html/classes.doc.html):
```java
public protected private abstract static final transient volatile synchronized native strictfp
```

Naming
---------
[Google naming conventions](https://google-styleguide.googlecode.com/svn/trunk/javaguide.html#s5.2-specific-identifier-names) should be adhered to wherever possible.

Long, descriptive method and variable names are good. Non-public, non-static field names start with `m`. Static field names start with `s`. Other fields start with a lower case letter.

**Preferred:**
```java
String bestStringEver;
private String mPrivateString;
static String sStaticString;
```

**Not Preferred:**
```java
String strB;
private String _privateString;
static String staticString;
```

Class names are typically nouns or noun phrases. For example, `Character` or `ImmutableList`. Constant names use `CONSTANT_CASE`: all uppercase letters, with words separated by underscores.

**Preferred:**
```java
static final int NUMBER = 5;
```

**Not Preferred:**
```java
static final int kNumber = 5;
```

Methods
---------
Try to come up with meaningful method names that succinctly describe the purpose of the method, making your code self-documenting and reducing the need for additional comments.

Compose method names using mixed case letters, beginning with a lower case letter and starting each subsequent word with an upper case letter.

Begin method names with a strong action verb (for example, `deposit`). If the verb is not descriptive enough by itself, include a noun (for example, `addInterest`). Add adjectives if necessary to clarify the noun (for example, `convertToEuroDollars`).

Use the prefixes `get` and `set` for getter and setter methods. For example, use the method names `getBalance` and `setBalance` to access or change the instance variable `balance`.

If the method returns a boolean value, use `is` or `has` as the prefix for the method name. For example, use `isOverdrawn` or `hasCreditLeft` for methods that return `true` or `false` values. Avoid the use of the word "not" in the boolean method name, always use the positive case.

**Preferred:**
```java
public void depositMoney(int money){}

public int getBalance(){}

public void setBalance(int balance){}

public bool hasMoney(){}

public bool isOverdrawn(){}
```

**Not Preferred:**
```java
public int balance(){}

public void addBalance(int balance){}

public bool money(){}

public bool isNotOverdrawn(){}
```

Operators
---------
Always add a single space before and after the use of an operator. 

**Preferred:**
```java
String foo = "bar";
int answer = 42;
answer += 9;
answer++;
answer = 40 + 2;
```

**Not Preferred:**
```java
String foo="bar";
int answer=42;
answer+= 9;
++answer;
answer= 40+2;
```

When incrementing a variable, the `++`, `--`, etc are preferred to be after the variable instead of before to be consistent with other operators. Operators separated should always be surrounded by spaces unless there is only one operand.

**Preferred:**
```java
answer++;
```

Conditionals
---------
Conditionals should use the positive case if possible when using an `else` body. If there is no `else` body, it is fine to use the negative case.

**Preferred:**
```java
// If with else body
if(bankAccount.isOverdrawn())
{
	// Do Something
}
else 
{
	// Do Something
}

// If with no else body
if(!bankAccount.isOverdrawn())
{
	// Do Something
}
```

**Not Preferred:**
```java
if(!bankAccount.isOverdrawn())
{
	// Do Something
}
else 
{
	// Do Something
}
```


Ternary Operator
---------
The Ternary operator, `?:` , should only be used when it increases clarity or code neatness. A single condition is usually all that should be evaluated. Evaluating multiple conditions is usually more understandable as an `if` statement, or refactored into instance variables. In general, the best use of the ternary operator is during assignment of a variable and deciding which value to use.

Non-boolean variables should be compared against something, and parentheses are added for improved readability. If the variable being compared is a boolean type, then no parentheses are needed.

**Preferred:**
```java
result = (a > b) ? x : y;
```
**Not Preferred:**
```java
result = a > b ? x = c > d ? c : d : y;
```

Exception Handling
---------
**Never** ignore exceptions. Sometimes it is tempting to write code that completely ignores an exception like this:
```java
void setServerPort(String value) 
{
    try 
    {
        serverPort = Integer.parseInt(value);
    } 
    catch (NumberFormatException e) { }
}
```

You must never do this. While you may think that your code will never encounter this error condition or that it is not important to handle it, ignoring exceptions like above creates mines in your code for someone else to trip over some day. You must handle every `Exception` in your code in some principled way. The specific handling varies depending on the case. Typical responses are to log it, or if it is considered "impossible", rethrow it as an `AssertionError`.

**Never** catch general exceptions. Sometimes it is tempting to do something like this:
```java
try 
{
    // may throw IOException 
    someComplicatedIOFunction();  
    // may throw ParsingException 
    someComplicatedParsingFunction();  
    // may throw SecurityException
    someComplicatedSecurityFunction();   
    // phew, made it all the way 
} 
catch (Exception e) 
{
    // I'll just catch all exceptions 
    // with one generic handler!
    handleError();                      
}
```
You should **not** do this. In almost all cases it is inappropriate to catch generic `Exception` or `Throwable`, preferably not `Throwable`, because it includes `Error` exceptions as well. It is very dangerous. It means that `Exception`s you never expected (including `RuntimeException`s like `ClassCastException`) end up getting caught in application-level error handling. It obscures the failure handling properties of your code. It means if someone adds a new type of `Exception` in the code you're calling, the compiler won't help you realize you need to handle that error differently. And in most cases you shouldn't be handling different types of exception the same way, anyway.

Singletons
---------
Singleton objects should use a thread-safe pattern for creating their shared instance. Do not use a "double-locking" lazy load pattern as it is [inherently broken](http://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html).

Define the singleton as a static field in a separate class. The semantics of Java guarantee that the field will not be initialized until the field is referenced, and that any thread which accesses the field will see all of the writes resulting from initializing that field.

```java
class HelperSingleton 
{
  static Helper singleton = new Helper();
}
```

Dependency Management
---------
[Gradle](http://www.gradle.org/) should be used for project dependencies. The `build.gradle` allows someone to see which libraries are being used and where to find them. 

Best practices for Gradle dependency management can be found [here](http://www.gradle.org/docs/current/userguide/dependency_management.html).
