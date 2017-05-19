# 1. What exactly is an instance in Java?

An object and an instance are the same thing.

Personally I prefer to use the word "instance" when referring to a specific object of a specific type, for example "an instance of type Foo". But when talking about objects in general I would say "objects" rather than "instances".

A reference either refers to a specific object or else it can be a null reference.

They say that they have to create an instance to their application. What does it mean?
They probably mean you have to write something like this:
```sh
$ Foo foo = new Foo();
```
# 2. What is the difference between extends and implements?
- Extends -> For inheriting the Base Class.
- Implements -> For implementing an Interface.
# 3. What are classes, references and objects?



#### 1. A Class is like the Blueprint for a house. Using this blueprint, you can build as many houses as you like.
#### 2. Each house you build (or instantiate, in OO lingo) is an Object, also known as an Instance.
#### 3. Each house also has an Address, of course. If you want to tell someone where the house is, you give them a card with the address written on it. That card is the object's Reference.
#### 4. If you want to visit the house, you look at the address written on the card. This is called Dereferencing.
###### You can copy that reference as much as you like, but there's just one house -- you're just copying the card that has the address on it, not the house itself. Java methods are always pass-by-value, but the value could be an object's Reference
