# Creational Patterns

## 1. Factory

- Name : Factory
- Context:
  - encapsultaes object creation
  - object specialized in creating other objects
- Problem:
  - used when not sure what type of objects to be used.
  - Decisions to be made at runtime about what classes to use.

- Scenario:
  - Pet shop to sell dogs. But now need to sell cats as well. 

## 2. Abstract Factory

- Abstract factory design pattern used when
  the user expects family of realted objects at given time
  but don't need to know which family until runtime


## 3. Singleton

- Problem: 
  - An OOP way of creating global variable
  - When you need Only one object to be instantiated from a class

- Scenario: 
  - need for keeping cache of information that needs to be shared by various 
    elements of software system. 
  - By keeping infromation in single object, no need to retrieve information from the 
    original source everytime
  - An information cache - shared by mutliple objects

## 4 . Builder

- Solution to anti pattern (opposite of best practice) called telescoping construction
- Problem: 
  - Telescoping construction anti pattern occurs when software developer attempts to
    build a complex object using excessive number of constructors

- SOlution: partitions process of building complex objects into 4 different roles:
  - Director : incharge of building product using builder object
  - Abstract Builder : provides all interfaces required to build object. Concrete builder inherits from this class
  - Concrete builder: inherits from the builder class implements the details of the interface for a specific product
  - Product: object being built
- Builder pattern doesn't rely on polymorphisn like factory and abstract factor but
  focuses on reducing complexity by using divide and conquer approach instead

## 5. Prototype

- clones object acording to prototypicak instance
- Problems:
  - useful to create many identical objects individaully; since it is expensive
- Scenario: Mass production of cars with same colour and same options; better option is to clone
- Solution:
  - Creating a prototypical instance first
  - Simply clone it whenever you need replica
