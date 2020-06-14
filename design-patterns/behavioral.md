# Behavioral Design Patterns

## 1. Observer

- Observer establishes a one-to-many relationship between a subject and multiple observers. 

- Problem:
  - a subject object need to be monitored, and other observer objects need to be notified 
    when there is a change in the subject. 

- Scenario:
  - In our scenario we need to be able keep track of core temperatures of reactors at a power plant. 
  - When there is a change in the core temperature registered observers need to be notified. 

- Solution:
  - For our solution we need an abstract class called subject, which has interfaces that allow 
    the operations, such as 
    - attaching an observer 
    - detaching an observer and 
    - notifying observers. 
  - We also need concrete subject classes inheriting from the abstracts subject class. 

- Singleton is related to the observer design pattern.

## 2. Visitor:

- The Visitor design pattern allows adding new features to an existing class 
  hierarchy without changing it. 
- It is sometimes necessary to add new operations dynamically to existing classes with minimal changes. 
- For our scenario, we present a House class. 
- Visitors in this scenario include HVAC specialist and Electrician. 
- HVAC specialist in our scenario is Visitor type 1 and Electrician is Visitor type 2. 
- The visitor pattern represents new operations to be performed on the various elements of 
- an existing class hierarchy. 
- Visitors can also provide operations on a composite object.

## 3. Iterator

- The iterator pattern allows a client to have sequential access to the elements of 
- an aggregate object without exposing its underlying structure. 
- The problem is that some programmers overcrowd the traversal interfaces of an 
- aggregate object for every possible way of iteration. We'll be building our own 
- iterator that takes advantage of a built-in Python iterator called zip(). 
- The iterator iterates through a list of German counting words. 
- It will iterate only up to a certain point based on a client input. 
- An iterator isolates access and traversal features from an aggregate object. 
- It also provides an interface for accessing the elements of an aggregate object. 
- An iterator keeps track of the objects being traversed. 
- One of the recommended solutions is to make the aggregate object create an iterator 
  for a client. 
- The composite design pattern is related to the iterator pattern.

## 4. Strategy

- The Strategy pattern offers a family of interchangeable algorithms to a client. 
- The problem we often see is that there is a need for dynamically changing the 
- behavior of an object. So we offer our Strategy class with its default behavior. 
- When there is a need, we provide another variation of the Strategy class by 
- dynamically replacing its default method with a new one. 
- Python allows adding methods dynamically by importing the types module.

## 5. Chain of Responsibility

-  opens up various possibilities of processing for a given request. 
-  The Chain of Responsibility pattern decouples the request and its processing. 
-  Our given problem is that many different types of processing needs to be done 
-  depending on what the request is. 
-  In our scenario, we receive an integer value and then we use different 
-  handlers to find out its range. 
-  As our solution, we used Abstract Handler that stores a Successor who will 
-  handle a request if it is not handled at the current handler. 
-  then Concrete Handlers check if they can handle the request. 
-  If they can, they handle it and return a true value indicating that 
-  the request was handled. 
-  Composite is related to the Chain of Responsibility design pattern.
