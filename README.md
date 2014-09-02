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


