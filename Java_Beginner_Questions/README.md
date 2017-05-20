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

# 4. what is a reference?
A reference is the address of the memory location where the object is stored.

When you create an object from a class, Java allocates the amount of memory the object requires to store the object. Then, if you assign the object to a variable, the variable is actually assigned a reference to the object, not the object itself. 
This reference is the address of the memory location where the object is stored.
To declare a variable using a reference type, you simply list the class name as the data type.

For example, the following statement defines a variable that can reference objects created from a class named Ball:
```sh
 Ball b;
```
To create a new instance of an object from a class, you use the new keyword along with the class name:
```sh
 Ball b = new Ball();
```
key concepts in working with reference types is the fact that a variable of a particular type doesn’t actually contain an object of that type. Instead, it contains a reference to an object of the correct type. An important side effect is that two variables can refer to the same object.
```sh
Ball b1 = new Ball();
Ball b2 = b1;
```
Here, both b1 and b2 refer to the same instance of the Ball class.

# 5. Java -What is an instance variable? 

Instance variables belong to an instance of a class. Another way of saying that is instance variables belong to an object, since an object is an instance of a class. Every object has it’s own copy of the instance variables.

Instance variable is the variable declared inside a class, but outside a method: something like:
```sh
class IronMan{

     /** These are all instance variables **/
     public String realName;
     public String[] superPowers;
     public int age;

     /** Getters / setters here **/
}
Now this IronMan Class can be instantiated in other class to use these variables, something like:

class Avengers{
        public static void main(String[] a){
              IronMan ironman = new IronMan();
              ironman.realName = "Tony Stark";
              // or
              ironman.setAge(30);
         }

}
```
# 6. what is new keyword ?
The new keyword is used to allocate memory at run time. All objects get memory in Heap memory area.

# 7. What is difference between references and objects in java?
A reference is an entity which provides a way to access object of its type. An object is an entity which provides a way to access the members of it's class or type.
Generally, You can't access an object without a reference to it.

For example:

class Student{  
void aMethod()
    {
        // some business logic.
        System.out.println("Method function gets invoked by invoking object")
    }

  
 public static void main(String args[]){  
  Student s1=new Student();  //creating an object of Student  
  // Here s1 is a reference to an object of Student class.
  s1.aMethod(); //accessing member through reference variable  
  
 }  
}  


