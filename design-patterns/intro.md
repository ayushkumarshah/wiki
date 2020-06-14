# Intro to design Patterns

They are well known and documented solutions to

- Recurring challenges in an OOP environment

## Motivation

- No need to reinvent the wheel and waste your time
- Systematic reuse of design ideas or best pratices yields lower cost and higher quality

## IMportant Characteristics:

- Language Neutral
- Dynamic (always new design patterns are coming)
- Incomplete (You need able to customize it accoording to use)

## Types of Design patterns

1. Creational Patterns
2. Structural Patterns
3. Behavioral Patterns

### 1. Creational Patterns:
- Useful when needed to create objects for specific purpose in a systematic way
- Benefits: Flexibility
- **Mechanisms used: Polymorphism, Interface**
- Eg. you need to restrict number of objects instantiated (You can use singleton design pattern)
- Eg: Different subtypes of objects from the same class can be created at runtime
- Other creational patetrns
  - Singleton
  - Factory
  - Abstract Factory
  - Builder
  - Prototype

### 2. Structural Design Patterns
- Contains Various ways to assemble classes and thier instances
- Establish useful realationships between software components in certain configurtions
- To accomplish both functional an non functional goals.
- Different goals yield diffrerent structures.
- **Mechanisms used: Inheritance, Interface**
- Examples:
  - Decorator
  - Proxy
  - Adaptor
  - Composite
  - Bridge

### 3. Behavioral Patterns

- Common solutions to programming problems occuring when trying to effectively regulate communications
  among objects i.e. best pratcies on how to make different objects interact with each other.
- Focus: Define the protocols in between the objects to work together to achieve the common goal.
- **Mechanisms used: Methods and their signatures, Interface**
- Examples:
  - Observer
  - Visitor
  - Iterator
  - Strategy
  - Chain of Responsibility

## Pattern Context

### 1. Participants

- classes involved to from a design pattern. 
- These classes play different roles to achieve the goal

### 2. Quality Attributes

- They include non functional requirements: Usability, modifiability, reliabaility, performance
- Imapct on the entire software
- Addressed by only the architectural solutions

### 3. Forces

- Various factors or trade offs to conider when adopting a design pattern
- Manifested in quality attributes
- Unintended consequences if not considered like:

### 4. Consequences

- Side effects: worse performance
- Decision makers:
  - choosing the design pattern despite the consequences
  - vital step since design patterns can cause more problems instead of solving prblems when miused.

## Pattern Language

### 1. Name

- Should capture the gist of the pattern
- Become part of vocabulary during design process
- Needs to be meaningful and memorable

### 2. Context

- Provides scenario and insights when patterns may be used

### 3. Problem

- Describes a design challenge the pattern is trying to address

### 4. Solution

- Specifies the pattern itself in terms of:
  - Structure: specifies relationship among elements used in the pattern
  - Behavior: specifies interactions between all those elements 

### 5. Related Patterns

- Lists other patterns:
  - used together with the pattern being dwescribed or
    - Similar but different patterns
    - Important to describe the subtle differenes bwteen the patterns


