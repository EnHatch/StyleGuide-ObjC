Objective-C-Style-Guide
=======================

Table of Contents
=======================

-  Code Organization
-  Spacing
-  Comments
-  Naming
 -    Underscores
 -    Image Naming
-  Methods
-  Variables
-  Property Attributes
-  Dot-Notation Syntax
-  Literals
-  Constants
-  Enumerated Types
-  Case Statements
-  Private Properties
-  Booleans
-  Conditionals
-  Ternary Operator
-  Init Methods
-  Class Constructor Methods
-  CGRect Functions
-  Golden Path
-  Error handling
-  Singletons
-  Line Breaks
-  Xcode Project

Code Organization
=======================
Use ```#pragma mark``` - to categorize methods in functional groupings and protocol/delegate implementations following this general structure.


```Objective-C
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
Spacing
=======================
Indent using 2 spaces (this conserves space in print and makes line wrapping less likely). Never indent with tabs. Be sure to set this preference in Xcode.

Method braces and other braces (if/else/switch/while etc.) always open on the same line as the statement but close on a new line.

####Preferred:
```Objective-C
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```
####Not Preferred:
```Objective-C
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but often there should probably be new methods.

Prefer using auto-synthesis. But if necessary, @synthesize and @dynamic should each be declared on new lines in the implementation.

Colon-aligning method invocation should often be avoided. There are cases where a method signature may have >= 3 colons and colon-aligning makes the code more readable. Please do NOT however colon align methods containing blocks because Xcode's indenting makes it illegible.

###Preferred:
```Objective-C
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```
###Not Preferred:
```Objective-C
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

Comments
=======================
When they are needed, comments should be used to explain why a particular piece of code does something. Any comments that are used must be kept up-to-date or deleted.

Block comments should generally be avoided, as code should be as self-documenting as possible, with only the need for intermittent, few-line explanations. Exception: This does not apply to those comments used to generate documentation.

Naming
=======================
Apple naming conventions should be adhered to wherever possible, especially those related to memory management rules (NARC).
Long, descriptive method and variable names are good.

####Preferred:
```Objective-c
UIButton *settingsButton;
```
####Not Preferred:
```Objective-c
UIButton *setBut;
```

A three letter prefix should always be used for class names and constants, however may be omitted for Core Data entity names. 
Constants should be camel-case with all words capitalized and prefixed by the related class name for clarity.

####Preferred:
```Objective-c
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

####Not Preferred:
```Objective-c
static NSTimeInterval const fadetime = 1.7;
```

Properties should be camel-case with the leading word being lowercase. Use auto-synthesis for properties rather than manual ```Objective-c@synthesize``` statements unless you have good reason.

####Preferred:
```Objective-c
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

####Not Preferred:
```Objective-c
id varnm;
```

###Underscores

When using properties, instance variables should always be accessed and mutated using ```self..``` This means that all properties will be visually distinct, as they will all be prefaced with ```self..```

An exception to this: inside initializers, the backing instance variable (i.e. _variableName) should be used directly to avoid any potential side effects of the getters/setters.

Local variables should not contain underscores.

###Image Naming

Image names should be named consistently to preserve organization and developer sanity. They should be named as one camel case string with a description of their purpose, followed by the un-prefixed name of the class or property they are customizing (if there is one), followed by a further description of color and/or placement, and finally their state.

For example:
```Objective-c
RefreshBarButtonItem / RefreshBarButtonItem@2x and 
RefreshBarButtonItemSelected/RefreshBarButtonItemSelected@2x
ArticleNavigationBarWhite / ArticleNavigationBarWhite@2x and 
ArticleNavigationBarBlackSelected / ArticleNavigationBarBlackSelected@2x.
```
Images that are used for a similar purpose should be grouped in respective groups in an Images folder.

Methods
=======================
In method signatures, there should be a space after the method type (-/+ symbol). There should be a space between the method segments (matching Apple's style). Always include a keyword and be descriptive with the word before the argument which describes the argument.
The usage of the word "and" is reserved. It should not be used for multiple parameters as illustrated in the ```initWithWidth:height:``` example below.

####Preferred:
```Objective-C
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

####Not Preferred:
```Objective-C
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```

Variables
=======================
Variables should be named as descriptively as possible. Single letter variable names should be avoided except in ```for()``` loops.
Asterisks indicating pointers belong with the variable, e.g., ```NSString *text not NSString* text orNSString * text```, except in the case of constants.

Private properties should be used in place of instance variables whenever possible. Although using instance variables is a valid way of doing things, by agreeing to prefer properties our code will be more consistent.

Direct access to instance variables that 'back' properties should be avoided except in initializer methods (```init```, ```initWithCoder:```, etc…), ```dealloc``` methods and within custom setters and getters. For more information on using Accessor Methods in Initializer Methods and dealloc, see here.

####Preferred:
```Objective-C
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

####Not Preferred:
```Objective-C
@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
```

Property Attributes
=======================
Property attributes should be explicitly listed, and will help new programmers when reading the code. The order of properties should be storage then atomicity, which is consistent with automatically generated code when connecting UI elements from Interface Builder.

####Preferred:
```Objective-C
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

####Not Preferred:
```Objective-C
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

Properties with mutable counterparts (e.g. ```NSString```) should prefer copy instead of ```strong```. Why? Even if you declared a property as ```NSString``` somebody might pass in an instance of an ```NSMutableString``` and then change it without you noticing that.
####Preferred:
```Objective-C
@property (copy, nonatomic) NSString *tutorialName;
```

####Not Preferred:
```Objective-C
@property (strong, nonatomic) NSString *tutorialName;
```

Dot-Notation Syntax
=======================
Dot syntax is purely a convenient wrapper around accessor method calls. When you use dot syntax, the property is still accessed or changed using getter and setter methods. Read more here

Dot-notation should always be used for accessing and mutating properties, as it makes code more concise. Bracket notation is preferred in all other instances.

####Preferred:
```Objective-C
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```
####Not Preferred:
```Objective-C
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

Literals
=======================
```NSString```, ```NSDictionary```, ```NSArray```, and ```NSNumber``` literals should be used whenever creating immutable instances of those objects. Pay special care that ```nil``` values can not be passed into ```NSArray``` and ```NSDictionary``` literals, as this will cause a crash.
####Preferred:
```Objective-C
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```
####Not Preferred:
```Objective-C
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```





