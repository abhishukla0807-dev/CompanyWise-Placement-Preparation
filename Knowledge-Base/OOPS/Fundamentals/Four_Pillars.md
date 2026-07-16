# Four Pillars of OOP
#### Encapsulation | Inheritance | Polymorphism | Abstraction | Must Know for Every Technical Round

> These four pillars are not just theory. Every class, framework, and design pattern in OOP is built on top of them.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [Overview of All Four Pillars](#overview-of-all-four-pillars) |
| 02 | [Encapsulation](#encapsulation) |
| 03 | [Inheritance](#inheritance) |
| 04 | [Polymorphism](#polymorphism) |
| 05 | [Abstraction](#abstraction) |
| 06 | [How the Pillars Connect](#how-the-pillars-connect) |
| 07 | [Code Example](#code-example) |
| 08 | [Common Interview Questions](#common-interview-questions) |
| 09 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 10 | [When to Use What](#when-to-use-what) |
| 11 | [Resources](#resources) |

---

## Overview of All Four Pillars

| Pillar | One Line | Real-World Example |
|--------|----------|--------------------|
| Encapsulation | Hide data, expose only what is needed | ATM hides internal cash mechanism, shows only buttons |
| Inheritance | Child class reuses parent class properties | Dog inherits from Animal |
| Polymorphism | Same method, different behavior per object | `makeSound()` barks for Dog, meows for Cat |
| Abstraction | Hide complexity, show only essential features | You press brake, you do not see the braking internals |

---

## Encapsulation

- Bundles data and methods together inside a single class
- Hides internal data using `private` access modifier
- Exposes controlled access through public `getters` and `setters`
- Prevents accidental or unauthorized modification of data
- Makes code easier to maintain, internal changes do not affect outside code

### ✦ Key Points
- Encapsulation hides **HOW** data is stored
- It is the first line of defence for data security in OOP
- A class with all private fields and public methods is fully encapsulated
- Changing internal logic does not break code that uses the class

### ✦ Real-World Analogy
- A capsule holds medicine inside and controls how and when it is released
- You take the capsule, you do not touch the medicine directly
- Same idea: object holds data inside, you access it only through defined methods

---

## Inheritance

- A child class acquires properties and methods of a parent class
- Uses the `extends` keyword in Java
- Avoids rewriting common logic across multiple classes
- Models an IS-A relationship: Dog IS-A Animal, Car IS-A Vehicle
- Java supports single, multilevel, and hierarchical inheritance with classes
- Multiple inheritance with classes is not supported in Java to avoid the diamond problem
- Every class in Java implicitly inherits from `java.lang.Object`

### ✦ Key Points
- Constructors are not inherited
- Child class can override parent methods to change behavior
- `super` keyword is used to call parent class constructor or methods
- `final` classes cannot be extended
- `private` methods are not visible to child classes, cannot be overridden

### ✦ Types of Inheritance

| Type | Description |
|------|-------------|
| Single | One child inherits from one parent |
| Multilevel | A inherits B, B inherits C |
| Hierarchical | Multiple children inherit from one parent |
| Multiple | Not supported in Java via classes, only via interfaces |
| Hybrid | Combination, achieved through interfaces |

### ✦ Real-World Analogy
- A child inherits the surname, eye color, and habits from parents
- The child can still develop new traits of their own
- Same idea: child class inherits all non-private members and can add or override them

---

## Polymorphism

- One name, many forms
- Same method behaves differently depending on the object calling it
- Poly = many, Morph = forms

### ✦ Compile-Time Polymorphism
- Also called static polymorphism or early binding
- Achieved through method overloading
- Same method name, different parameters (type or count)
- Resolved by the compiler before runtime

### ✦ Runtime Polymorphism
- Also called dynamic polymorphism or late binding
- Achieved through method overriding
- Child class redefines a method from the parent class
- Resolved by the JVM at runtime using dynamic method dispatch
- Parent reference can hold a child object

### ✦ Key Points
- Overloading = same name, different parameters, same class
- Overriding = same name, same parameters, different class (parent and child)
- Static methods cannot be overridden, they are hidden
- `final` methods cannot be overridden
- Runtime polymorphism is implemented through the JVM's virtual method table

### ✦ Real-World Analogy
- A person is a son at home, a student in college, an employee at work
- Same person, different roles and behaviors depending on context
- Same idea: same method name, different behavior depending on the object

---

## Abstraction

- Hides complex implementation details from the user
- Shows only what is necessary, not how it works internally
- Achieved using abstract classes and interfaces in Java
- Reduces complexity and coupling between different parts of a system

### ✦ Abstract Class
- Declared with `abstract` keyword
- Can have both abstract and concrete methods
- Cannot be instantiated directly
- A child class must implement all abstract methods

### ✦ Interface
- All methods are abstract by default (before Java 8)
- From Java 8 onwards, interfaces can have default and static methods
- A class can implement multiple interfaces
- Used to achieve multiple inheritance in Java

### ✦ Abstract Class vs Interface

| Factor | Abstract Class | Interface |
|--------|---------------|-----------|
| Methods | Abstract and concrete | Abstract by default |
| Variables | Any type | `public static final` only |
| Constructor | Yes | No |
| Multiple inheritance | Not supported | Supported |
| Use when | Shared base behavior | Defining a contract |

### ✦ Key Points
- Abstraction hides **WHAT** is complex inside
- Encapsulation hides **HOW** data is stored (most common confusion in interviews)
- ATM: you see deposit and withdraw, not the transaction logic inside
- List.add() hides resizing logic, you just call the method

### ✦ Real-World Analogy
- You drive a car by pressing the accelerator, you do not need to know how fuel combustion works
- A TV remote shows you buttons, not the circuit board behind them
- Same idea: expose a simple interface, hide the complex internals

---

## How the Pillars Connect

- Encapsulation enables Abstraction: hiding data is the first step to hiding complexity
- Inheritance enables Polymorphism: without a parent type, runtime dispatch has nothing to work through
- Abstraction sets the contract, Encapsulation enforces it
- All four work together in every well-designed OOP system

| Pillar | Hides | Enables |
|--------|-------|---------|
| Encapsulation | Data (HOW it is stored) | Abstraction, Security |
| Abstraction | Complexity (WHAT is complex) | Simpler interfaces |
| Inheritance | Code duplication | Polymorphism, Reuse |
| Polymorphism | Specific type details | Flexibility, Extensibility |

---

## Code Example

### Java
```java
// Encapsulation
class BankAccount {
    private double balance;

    BankAccount(double balance) {
        this.balance = balance;
    }

    public void deposit(double amount) { balance += amount; }
    public void withdraw(double amount) { if (amount <= balance) balance -= amount; }
    public double getBalance() { return balance; }
}

// Abstraction
abstract class Animal {
    String name;

    Animal(String name) { this.name = name; }

    abstract void makeSound();  // abstract method, no implementation here

    void breathe() {
        System.out.println(name + " is breathing");  // concrete method
    }
}

// Inheritance + Polymorphism
class Dog extends Animal {
    Dog(String name) { super(name); }

    @Override
    void makeSound() {
        System.out.println(name + " says: Woof!");
    }
}

class Cat extends Animal {
    Cat(String name) { super(name); }

    @Override
    void makeSound() {
        System.out.println(name + " says: Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a1 = new Dog("Bruno");   // parent reference, child object
        Animal a2 = new Cat("Whiskers");

        a1.makeSound();   // Bruno says: Woof!
        a2.makeSound();   // Whiskers says: Meow!
        a1.breathe();     // Bruno is breathing

        BankAccount acc = new BankAccount(1000);
        acc.deposit(500);
        System.out.println(acc.getBalance());  // 1500.0
    }
}
```

---

## Common Interview Questions

**Q: What are the four pillars of OOP?**
- The most asked OOP question in every fresher interview, service and product both
- Encapsulation, Inheritance, Polymorphism, Abstraction
- Never just list them. Give a one-line definition and a real example for at least two

**Q: What is the difference between Abstraction and Encapsulation?**
- The most commonly confused pair in OOP interviews
- Abstraction hides complexity, shows only what is needed. Encapsulation hides data, controls access through methods
- Example: ATM screen is abstraction. Private balance field with getter and setter is encapsulation

**Q: What is the difference between method overloading and method overriding?**
- Tests your understanding of both types of polymorphism
- Overloading: same name, different parameters, resolved at compile time
- Overriding: same name, same parameters, different class, resolved at runtime

**Q: Can we achieve multiple inheritance in Java?**
- Tricky question, very commonly asked
- Not through classes, Java does not support it to avoid the diamond problem
- Yes through interfaces, a class can implement multiple interfaces

**Q: What is the difference between an abstract class and an interface?**
- Tests depth of understanding on abstraction
- Abstract class can have concrete methods and constructors, interface cannot (before Java 8)
- A class extends one abstract class but implements multiple interfaces

**Q: What is runtime polymorphism? How does it work internally?**
- Asked in product-based companies and senior fresher rounds
- When a parent reference holds a child object and calls an overridden method, the JVM decides at runtime which version to run
- Internally handled through the virtual method table in the JVM

---

## Common Mistakes to Avoid

- Saying abstraction and encapsulation are the same thing, they solve different problems
- Listing all four pillars without being able to explain even one with a real example
- Confusing method overloading with method overriding, one is compile-time, one is runtime
- Thinking inheritance is just about reusing code, it also defines an IS-A relationship
- Saying Java supports multiple inheritance, it does not through classes, only through interfaces
- Saying `abstract` and `interface` are interchangeable, they have clear differences in usage

---

## When to Use What

| Situation | Pillar to Apply |
|-----------|----------------|
| Protecting sensitive data from outside access | Encapsulation |
| Reusing common logic across multiple classes | Inheritance |
| Same method name, different behavior per class | Polymorphism |
| Hiding internal complexity from the user | Abstraction |
| Defining a contract multiple classes must follow | Interface (Abstraction) |
| Sharing common base behavior with partial implementation | Abstract Class |
| Adding new class without breaking existing code | Polymorphism |

---

## Resources

- [GeeksforGeeks - OOP Concepts in Java](https://www.geeksforgeeks.org/java/four-main-object-oriented-programming-concepts-of-java/)
- [GeeksforGeeks - Encapsulation, Inheritance, Polymorphism, Abstraction](https://www.geeksforgeeks.org/java/understanding-encapsulation-inheritance-polymorphism-abstraction-in-oops/)
- [GeeksforGeeks - OOP Interview Questions](https://www.geeksforgeeks.org/interview-prep/oops-interview-questions/)
- [InterviewBit - OOPs Interview Questions](https://www.interviewbit.com/oops-interview-questions/)
- [PrepInsta - OOPs Interview Questions](https://prepinsta.com/interview-preparation/technical-interview-questions/oops/)

---

*Made for CS Students | Internship & Job Prep Series*