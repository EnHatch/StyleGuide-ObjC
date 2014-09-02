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
 
Use #pragma mark - to categorize methods in functional groupings and protocol/delegate implementations following this general structure.
 
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


