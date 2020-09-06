# Structural Patterns

## 1. Decorator

- Problem :
  - New features to existing object dynamically
  - Without using subclassing

- Scenario:
  - Hello world msg function
  - Making msg fancier by decorating it with additional text like 
    <blink> Hello World </blink>

- Solution:
  - Functions are also objects in python
  - We can addtional features to functions using built in decorator feature available

## 2. Proxy

- handy when creating object that becomes resource intensive
- Problem: 
  -  Postpone object creation unless absolutely necessary
  -  Find a placeholder whcich will inturn create the object when absolute necessary

- Scenario:
  - Producer - created only when he is available because fixed number of producer objects can exist at a time
  - Artist (Proxy) - checks producer becomes available for
  - Guest

- Solution:
  - Clients: interacting with Proxy object most of time until reasource intensive object becomes available
  - Proxy: responsible for creating the resource intensive objects

- Adaptor and decorator related to proxy design pattern

## 3. Adapter:

- converts interface of class into another which the client is expecting

- Problem:
  - Interface incompatible between client and server

- Scenario:
  - We have two objects with a method each for speaking
    - Korean: speak_korean()
    - British: speak_english()
  - But Client would want like to use uniform interface : speak()

- Solution:
  - use of adaptor pattern that translates the method name in between client and server code

- Bridges and decorator realted to adapter pattern

## 4. Composite

- maintains tree structure to represent part while relationships

- Problem
  - Build a recursive tree data structure so that an element of tree can have its own sub elements
  - Eg: Creating Menu > Submenu > Sub-sub menu > ...

- Scenario: 
  - Display menu and sub menu items

- SOlution:
  - Component: abstract class
  - Child: concrete class that inherits from abstract class component 
  - Composite: 
    - concrete class that inherits from abstract class component
    - maintains child objects by adding and removing them to tree data strcuture

- Decorator, iterator and visitor related to composite pattern

## 5. Bridge

- The bridge pattern helps untangle an unnecessary complicated class hierarchy, 
  especially when implementation specific classes are mixed together with 
  implementation-indendent classes. 

- Problem:
  - There are two parallel or orthogonal abstractions. 
    - implementation-specific
    - implementation-independent. 

- Scenario:
  - Scenario involves this implementation-independent circle abstraction and 
    implementation-dependent circle abstraction. 
  - The implementation-dependent circle abstraction involves how to draw a circle, and 
  - implementation-independent circle abstraction involves how to define the properties of a circle and scale it. 
  
- Solution
  - The key to our solution is not trying to abstract both implementation-specific and 
    implementation-independent classes in a single class hierarchy. 

- The abstract factory and adaptor patterns are the related patterns to this rich design pattern.
