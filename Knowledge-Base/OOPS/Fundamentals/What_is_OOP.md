# What is OOP
#### Foundation of Object-Oriented Programming | Asked in Every First Technical Round

> OOP is a way of writing code by organizing it around real-world entities called objects, instead of just functions and logic.

---

## 📌 Table of Contents

| # | Section                                                         |
|---|-----------------------------------------------------------------|
| 01 | [What is OOP](#what-is-oop)                                     |
| 02 | [The 4 Pillars of OOP](#the-4-pillars-of-oop)                   |
| 03 | [OOP vs Procedural Programming](#oop-vs-procedural-programming) |
| 04 | [OOP - Pros and Cons](#oop---pros-and-cons)                     |
| 05 | [How It Works Internally](#how-it-works-internally)             |
| 06 | [Code Example](#code-example)                                   |
| 07 | [Common Interview Questions](#common-interview-questions)       |
| 08 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)           |
| 09 | [When to Use What](#when-to-use-what)                           |
| 10 | [Resources](#resources)                                         |

---

## What is OOP

- A programming paradigm built around objects and classes
- Models real-world entities directly in code
- Each object bundles its own data and the actions it can perform
- Focuses on what things are, not just what steps to follow
- Used in Java, C++, Python, C#, and most modern languages
- Designed to make large codebases easier to build, maintain, and scale

---

## The 4 Pillars of OOP

### ✦ Encapsulation
- Wrapping data and methods together inside a class
- Hides internal details from the outside world
- Access is controlled through public methods only
- Example: a `BankAccount` class where balance is private, accessible only via `deposit()` and `withdraw()`

### ✦ Inheritance
- A class can acquire properties and methods of another class
- Promotes code reuse, no need to rewrite common logic
- The parent class is called superclass, the child is called subclass
- Example: `Animal` is a parent class, `Dog` and `Cat` extend it and inherit its behavior

### ✦ Polymorphism
- One method name, multiple behaviors depending on the object
- Compile-time: method overloading, same name different parameters
- Runtime: method overriding, child class redefines parent method
- Example: `makeSound()` called on a `Dog` object barks, called on a `Cat` object meows

### ✦ Abstraction
- Hiding complex implementation, showing only what is necessary
- User interacts with a simple interface, not internal workings
- Achieved using abstract classes and interfaces
- Example: you press the brake in a car, you do not need to know how the braking system works

---

## OOP vs Procedural Programming

| Factor | OOP | Procedural |
|--------|-----|------------|
| Organized around | Objects and classes | Functions and procedures |
| Data handling | Data is tied to objects | Data is separate from functions |
| Code reuse | Through inheritance | Through function calls |
| Real-world modeling | Natural and intuitive | Less intuitive |
| Maintainability | Easier for large projects | Gets complex as code grows |
| Security | Better, data can be hidden | Lower, data is more exposed |
| Examples | Java, C++, Python | C, Pascal |

---

## OOP - Pros and Cons

### ✦ Advantages

- Models real-world problems naturally using objects
- Code reuse through inheritance reduces duplication
- Encapsulation protects data from unintended modification
- Easier to maintain and update large codebases
- Polymorphism makes code flexible and extensible
- Modular structure makes team collaboration easier
- Abstraction keeps interfaces clean and simple

### ✦ Disadvantages

- More complex to design upfront compared to procedural code
- Not always the best choice for small or simple programs
- Can lead to over-engineering if used without discipline
- Requires deeper understanding to use effectively
- Slightly slower than procedural in performance-critical systems

---

## How It Works Internally

- You define a class, the compiler registers its structure in the method segment
- When you create an object, memory is allocated on the heap for its data
- A reference on the stack points to that object on the heap
- Methods are shared across all objects of a class, not duplicated per object
- When a method is called on an object, the runtime passes the object's reference automatically
- Inheritance builds a chain, the child class extends the parent's memory layout

> Think of OOP like a company. Each department is a class. Each employee is an object. Encapsulation keeps internal department processes hidden. Inheritance means a senior role inherits all junior responsibilities plus adds more.

---


## Code Example

### Java
```java
// Abstraction + Encapsulation
class Animal {
    private String name;
 
    Animal(String name) {
        this.name = name;
    }
 
    public String getName() {
        return name;
    }
 
    void makeSound() {
        System.out.println("Some sound");
    }
}
 
// Inheritance + Polymorphism
class Dog extends Animal {
    Dog(String name) {
        super(name);
    }
 
    @Override
    void makeSound() {
        System.out.println(getName() + " says: Woof!");
    }
}
 
class Cat extends Animal {
    Cat(String name) {
        super(name);
    }
 
    @Override
    void makeSound() {
        System.out.println(getName() + " says: Meow!");
    }
}
 
public class Main {
    public static void main(String[] args) {
        Animal a1 = new Dog("Bruno");
        Animal a2 = new Cat("Whiskers");
 
        a1.makeSound();   // Bruno says: Woof!
        a2.makeSound();   // Whiskers says: Meow!
    }
}
```


## Common Interview Questions

**Q: What is OOP and why is it used?**
- Tests your conceptual understanding, not just the definition
- OOP organizes code around objects that combine data and behavior, making large programs easier to build and maintain
- Always mention at least two pillars and relate them to real-world use

**Q: What are the 4 pillars of OOP?**
- The most asked OOP question across all company types
- Encapsulation, Inheritance, Polymorphism, Abstraction
- Know a one-line definition and a real-world example for each, never just list the names

**Q: What is the difference between OOP and procedural programming?**
- Tests whether you understand why OOP exists, not just what it is
- Procedural is step-by-step instructions, OOP is modeling entities with their own data and behavior
- Mention: OOP scales better, procedural is simpler for small tasks

**Q: Which OOP language have you used and how did you apply OOP concepts in a project?**
- Tests practical experience, very common in fresher interviews
- Pick one project, name the language, and explain one specific pillar you used with a concrete example
- Do not say "I used classes and objects", that is too vague

**Q: Is Java 100% object-oriented?**
- A tricky follow-up, often asked after the basics
- No, because Java has primitive data types like `int`, `char`, `float` which are not objects
- Languages like Smalltalk and Ruby are considered 100% object-oriented

---

## Common Mistakes to Avoid

- Listing the 4 pillars without being able to explain any one of them with an example
- Confusing abstraction and encapsulation, abstraction hides complexity, encapsulation hides data
- Saying OOP is always better than procedural, it depends on the scale and type of problem
- Thinking inheritance means copying code, it means building on top of existing structure
- Confusing method overloading with method overriding, one is compile-time, one is runtime

---

## When to Use What

| Situation | Approach |
|-----------|----------|
| Large codebase with multiple developers | OOP |
| Small utility script or automation task | Procedural |
| Real-world entities with data and behavior | OOP |
| Performance-critical system-level code | Procedural or mixed |
| Building reusable libraries or frameworks | OOP |
| Quick one-time data transformation | Procedural |

---

## Resources


- [GeeksforGeeks - OOP Concepts](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/)
- [GeeksforGeeks - OOP Interview Questions](https://www.geeksforgeeks.org/interview-prep/oops-interview-questions/)
- [InterviewBit - OOPs Interview Questions](https://www.interviewbit.com/oops-interview-questions/)
- [JavaTpoint - OOP Concepts](https://www.javatpoint.com/java-oops-concepts)
---

*Made for CS Students | Internship & Job Prep Series*