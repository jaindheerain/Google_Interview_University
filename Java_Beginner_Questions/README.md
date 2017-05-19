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
Extends -> For inheriting the Base Class.
Implements -> For implementing an Interface.
