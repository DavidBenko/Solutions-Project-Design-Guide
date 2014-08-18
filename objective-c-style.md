AnyPresence Solutions Objective-C Style Guide
=================================

This style guide outlines the coding conventions of the iOS code at [AnyPresence](http://anypresence.com).

Table of Contents
---------
- [Background](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#background)
- [Language](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#language)
- [Code Organization](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#code-organization)
- [Spacing](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#spacing)
- [Comments](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#comments)
- [Variables](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#variables)
	- [Variable Qualifiers](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#variable-qualifiers)
	- [Property Attributes](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#property-attributes)
	- [Private Properties](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#private-properties)
	- [Types](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#types)
- [Naming](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#naming)
- [Booleans](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#booleans)
- [Methods](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#methods)
- [Functions](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#functions)
- [Operators](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#operators)
- [Conditionals](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#conditionals)
- [Ternary Operator](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#ternary-operator)
- [Dot-Notation Syntax](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#dot-notation-syntax)
- [Literals](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#literals)
- [Constants](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#constants)
- [Enumerated Types](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#enumerated-types)
- [Blocks](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#blocks)
- [Error Handling](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#error-handling)
- [Singletons](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#singletons)
- [Memory Management](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#memory-management)
- [Dependency Management](https://github.com/AnyPresence-Services/Solutions-Project-Design-Guide/blob/master/objective-c-style.md#dependency-management)


Background
---------
Here are some of the documents from Apple that informed the style guide. If something isn't mentioned here, it's probably covered in great detail in one of these:

- [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
- [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
- [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
- [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)


Language
---------
US English should be used throughout. 

**Preferred:**
```objc
UIColor *myColor = [UIColor whiteColor];
```

**Not Preferred:**
```objc
UIColor *myColour = [UIColor whiteColor];
```

Code Organization
---------
Use `#pragma mark -` to categorize methods in functional groupings and protocol/delegate implementations following this general structure.

```objc
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

The physical files should be kept in sync with the Xcode project files in order to avoid file sprawl. Any Xcode groups created should be reflected by folders in the filesystem. Code should be grouped not only by type, but also by feature for greater clarity.

When possible, always turn on "Treat Warnings as Errors" in the target's Build Settings and enable as many [additional warnings](http://boredzo.org/blog/archives/2009-11-07/warnings) as possible. If you need to ignore a specific warning, use [Clang's `pragma` feature](http://clang.llvm.org/docs/UsersManual.html#controlling-diagnostics-via-pragmas).



Spacing
---------
- Indent using tabs. Never indent with spaces. Be sure to set this preference in Xcode.
- Method braces and other braces (`if`/`else`/`switch`/`while` etc.) always open on the same line as the statement but close on a new line.

**Preferred:**
```objc
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```

**Not Preferred:**
```objc
if (user.isHappy)
{
    //Do something
}
else 
{
    //Do something else
}
```

- There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but often there should probably be new methods.
- Prefer using auto-synthesis. But if necessary, `@synthesize` and `@dynamic` should each be declared on new lines in the implementation.
- Colon-aligning method invocation is preferred if the method signature has >= 3 colons and colon-aligning makes the code more readable.

**Preferred:**
```objc
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```
**Not Preferred:**
```objc
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

Comments
---------
When they are needed, comments should be used to explain why a particular piece of code does something. Any comments that are used must be kept up-to-date or deleted.

Block comments should generally be avoided, as code should be as self-documenting as possible, with only the need for intermittent, few-line explanations.

**All** public methods should be commented in the class's header file using [Doxygen](http://www.stack.nl/~dimitri/doxygen/) style comments. This comment style shows method information in Xcode's help overlay. 

```objc
/**
  Initialize a new Automobile object
  @param name The model name
  @param number the model number
  @param price the price
  @returns a newly initialized object
 */
- (id)initAutomobileWithModelName:(NSString *)name
                      modelNumber:(NSUInteger)number
                            price:(NSDecimalNumber *)price;
 
/**
  Returns a list of all current model names.
  The names are represented as NSString objects.
  @returns a list of names
 */
+ (NSArray *)allCurrentModelNames;
```

Variables
---------
Variables should be named as descriptively as possible. Single letter variable names should be avoided except in `for()` loops.

Asterisks indicating pointers belong with the variable, e.g., `NSString *text` not `NSString* text` or `NSString * text`, except in the case of constants.

Property definitions should be used in place of naked instance variables whenever possible. Direct instance variable access should be avoided except in initializer methods (`init`, `initWithCoder:`, etc…), `dealloc` methods and within custom setters and getters. For more information on using Accessor Methods in Initializer Methods and dealloc, see [here](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6).

**Preferred:**
```objc
@interface MyClass : NSObject

@property (strong, nonatomic) NSString *myString;

@end
```
**Not Preferred:**
```objc
@interface MyClass : NSObject {
  NSString *myString;
}
```

#### Variable Qualifiers

When it comes to the variable qualifiers [introduced with ARC](https://developer.apple.com/library/ios/releasenotes/objectivec/rn-transitioningtoarc/Introduction/Introduction.html#//apple_ref/doc/uid/TP40011226-CH1-SW4), the qualifer (`__strong`, `__weak`, `__unsafe_unretained`, `__autoreleasing`, `__block`) should be placed between the asterisks and the variable name, e.g., `NSString * __weak text`.

#### Property Attributes
Property attributes should be explicitly listed. The order of properties should be storage then atomicity, which is consistent with automatically generated code when connecting UI elements from Interface Builder.

**Preferred:**
```objc
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *myString;
```

**Not Preferred:**
```objc
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *myString;
```

Properties with mutable counterparts (e.g. `NSString`) should prefer `copy` instead of `strong`. Why? Even if you declared a property as `NSString` somebody might pass in an instance of an `NSMutableString` and then change it without you noticing that.

**Preferred:**
```objc
@property (copy, nonatomic) NSString *myString;
```

**Not Preferred:**
```objc
@property (strong, nonatomic) NSString *myString;
```

#### Private Properties
Private properties should be declared in class extensions (anonymous categories) in the implementation file of a class. Named categories (such as `APPrivate` or `private`) should never be used unless extending another class. The Anonymous category can be shared/exposed for testing using the `+Private.h` file naming convention.

**For Example:**
```objc
@interface APDetailViewController ()

@property (strong, nonatomic) GADBannerView *googleAdView;
@property (strong, nonatomic) ADBannerView *iAdView;
@property (strong, nonatomic) UIWebView *adXWebView;

@end
```

#### Types
`NSInteger` and `NSUInteger` should be used instead of `int`, `long`, etc per Apple's best practices and 64-bit safety. `CGFloat` is preferred over `float` for the same reasons. This future proofs code for 64-bit platforms.

All Apple types should be used over primitive ones. For example, if you are working with time intervals, use `NSTimeInterval` instead of `double` even though it is synonymous. This is considered best practice and makes for clearer code.

Naming
---------
Apple naming conventions should be adhered to wherever possible, especially those related to [memory management rules](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html) ([NARC](http://stackoverflow.com/a/2865194/340508)).

Long, descriptive method and variable names are good.

**Preferred:**
```objc
UIButton *settingsButton;
```
**Not Preferred:**
```objc
UIButton *setBut;
```

A two letter prefix (e.g. `AP`) should always be used for class names and constants, however may be omitted for Core Data entity names. Constants should be camel-case with all words capitalized and prefixed by the related class name for clarity.

**Preferred:**
```objc
static NSTimeInterval const APDetailViewControllerNavigationFadeAnimationDuration = 0.3;
```

**Not Preferred:**
```objc
static NSTimeInterval const fadetime = 1.7;
```

Properties should be camel-case with the leading word being lowercase. Use auto-synthesis for properties rather than manual `@synthesize` statements unless you have good reason.

**Preferred:**
```objc
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

**Not Preferred:**
```objc
id varnm;
```

Booleans
---------
Since `nil` resolves to `NO` it is unnecessary to compare it in conditions. Never compare something directly to `YES`, because `YES` is defined to `1` and a `BOOL` can be up to 8 bits.

This allows for more consistency across files and greater visual clarity.

**Preferred:**
```objc
if (someObject) {}
if (![anotherObject boolValue]) {}
```

**Not Preferred:**
```objc
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
```

If the name of a `BOOL` property is expressed as an adjective, the property can omit the "is" prefix but specifies the conventional name for the get accessor, for example:

```objc
@property (assign, getter=isEditable) BOOL editable;
```

Text and example taken from the [Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE).

Methods
---------
In method signatures, there should be a space after the method type (`-`/`+` symbol). There should be a space between the method segments (matching Apple's style). Always include a keyword and be descriptive with the word before the argument which describes the argument.

The usage of the word `and` is reserved. It should not be used for multiple parameters as illustrated in the `initWithWidth:height:` example below.

**Preferred:**
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**Not Preferred:**
```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

Functions
---------
C functions should be used to perform a specific task that does not alter the state of the object. C functions should be marked `static` to keep them internal. 

Only use functions if you do not need `self` or any properties, instance variables, or methods of `self`.

**Preferred:**
```c
static int multiplyTwoNumbers(int x, int y){
	return x * y;
}
```

**Not Preferred:**
```objc
// Simple tasks should be done in C functions
- (int) multiplyTwoNumbers:(int)x y:(int)y{
	return x * y;
}

// Do not modify the state of self using C functions
static void alterSomething(Klass* self){
	self.property = value;
}
```

Operators
---------
Always add a single space before and after the use of an operator. 

**Preferred:**
```objc
NSString *foo = @"bar";
NSInteger answer = 42;
answer += 9;
answer++;
answer = 40 + 2;
```

**Not Preferred:**
```objc
NSString *foo=@"bar";
NSInteger answer=42;
answer+= 9;
++answer;
answer= 40+2;
```

The `++`, `--`, etc are preferred to be after the variable instead of before to be consistent with other operators. Operators separated should always be surrounded by spaces unless there is only one operand.

**Preferred:**
```objc
answer++;
```

Conditionals
---------
Conditionals should use the positive case if possible when using an `else` body. If there is no `else` body, it is fine to use the negative case.

The exception is when checking against the existance of an `NSError` object, in which case checking the negative case with an `else` body is acceptable.

**Preferred:**
```objc
// If with else body
if(someVariable){
	// Do Something
}
else {
	// Do Something
}

// If with no else body
if(!someOtherVariable){
	// Do Something
}

// Check for error with else body
if(!error){
	// Do Something
}
else {
	// Do Something
}
```

**Not Preferred:**
```objc
if(!someVariable){
	// Do Something
}
else {
	// Do Something
}
```


Ternary Operator
---------
The Ternary operator, `?:` , should only be used when it increases clarity or code neatness. A single condition is usually all that should be evaluated. Evaluating multiple conditions is usually more understandable as an `if` statement, or refactored into instance variables. In general, the best use of the ternary operator is during assignment of a variable and deciding which value to use.

Non-boolean variables should be compared against something, and parentheses are added for improved readability. If the variable being compared is a boolean type, then no parentheses are needed.

**Preferred:**
```objc
result = a > b ? x : y;
```
**Not Preferred:**
```objc
result = a > b ? x = c > d ? c : d : y;
```

Dot-Notation Syntax
---------
Dot-notation should **always** be used for accessing and mutating properties. Bracket notation is preferred in all other instances.

**Preferred:**
```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**Not Preferred:**
```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

Literals
---------
`NSString`, `NSDictionary`, `NSArray`, and `NSNumber` literals should be used whenever creating immutable instances of those objects. Pay special care that `nil` values can not be passed into `NSArray` and `NSDictionary` literals, as this will cause a crash.

**Preferred**
```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**Not Preferred:**
```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```

Constants
---------
Constants are preferred over in-line string literals or numbers, as they allow for easy reproduction of commonly used variables and can be quickly changed without the need for find and replace. Constants should be declared as `static` constants and not `#defines` unless explicitly being used as a macro.

**Preferred:**
```objc
static NSString * const APAboutViewControllerCompanyName = @"AnyPresence, Inc";
static CGFloat const APImageThumbnailHeight = 50.0;
```

**Not Preferred:**
```objc
#define CompanyName @"AnyPresence, Inc"
#define thumbnailHeight 2
```

Enumerated Types
---------
When using enums, it is recommended to use the new fixed underlying type specification because it has stronger type checking and code completion. The SDK now includes a macro to facilitate and encourage use of fixed underlying types: `NS_ENUM()`

**Preferred:**
```objc
typedef NS_ENUM(NSInteger, APLeftMenuTopItemType) {
  APLeftMenuTopItemMain,
  APLeftMenuTopItemShows,
  APLeftMenuTopItemSchedule
};
```
You can also make explicit value assignments (showing older k-style constant definition):
```objc
typedef NS_ENUM(NSInteger, APGlobalConstants) {
  APPinSizeMin = 1,
  APPinSizeMax = 5,
  APPinCountMin = 100,
  APPinCountMax = 500
};
```
Older k-style constant definitions should be avoided unless writing CoreFoundation C code (unlikely).

**Not Preferred:**
```objc
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500
};
```

Blocks
---------
Blocks should have a space between their return type and name. Block definitions should omit their return type when possible. Block definitions should omit their arguments if they are void. Parameters in block types should be named unless the block is initialized immediately.

**Preferred:**
```objc
void (^blockName1)(void) = ^{
    // Do Something
};

id (^blockName2)(id) = ^ id (id args) {
    // Do Something
};
```

Error Handling
---------
When methods return an error parameter by reference, **always** check the error before continuing.

**Preferred:**
```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
    // Handle Error
}
```
**Not Preferred:**
```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
    // Ignored the value of error
}
```
Some of Apple’s APIs write garbage values to the error parameter (if non-`NULL`) in successful cases, so switching on the error can cause false negatives (and subsequently crash).

Singletons
---------
Singleton objects should use a thread-safe pattern for creating their shared instance.

```objc
+ (instancetype)sharedInstance {
   static id sharedInstance = nil;

   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });

   return sharedInstance;
}
```
This will prevent possible and [sometimes prolific crashes](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html).

Memory Management
---------
**Always** use Automatic Reference Counting (ARC). 

Dependency Management
---------
[Cocoapods](http://cocoapods.org/) should be used for project dependencies. The `podfile` allows someone to see which libraries are being used and where to find them. 

If you need to make changes to a dependency, fork that dependency and transfer the repository to GitHub user `RickSnyder`.
