# Constructor vs Method

#### Understanding the Fundamental Difference Between Object Initialization and Object Behavior

> Constructors create and initialize objects. Methods define what those objects can do. Understanding this distinction is essential for writing correct object-oriented programs.

---

## 📌 Table of Contents

| #  | Section                                                   |
| -- | --------------------------------------------------------- |
| 01 | [What is a Constructor?](#what-is-a-constructor)          |
| 02 | [What is a Method?](#what-is-a-method)                    |
| 03 | [Constructor vs Method](#constructor-vs-method)           |
| 04 | [Key Differences Explained](#key-differences-explained)   |
| 05 | [Code Example](#code-example)                             |
| 06 | [When to Use a Constructor](#when-to-use-a-constructor)   |
| 07 | [When to Use a Method](#when-to-use-a-method)             |
| 08 | [Common Interview Questions](#common-interview-questions) |
| 09 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)     |
| 10 | [Resources](#resources)                                   |

---

## What is a Constructor?

* A **constructor** is a special member of a class that initializes an object when it is created.

* It is executed automatically whenever an object is instantiated using the `new` keyword.

* A constructor has the same name as the class and never specifies a return type.

* Its primary responsibility is to prepare an object for use by assigning initial values to its instance variables.

---

## What is a Method?

* A **method** is a block of code that defines the behavior or functionality of an object.

* Methods are called explicitly whenever their functionality is required.

* A method can accept parameters, return values, perform calculations, modify object state, or interact with other objects.

* Unlike constructors, methods can be invoked multiple times during an object's lifetime.

---

## Constructor vs Method

| Feature             | Constructor                                 | Method                              |
| ------------------- | ------------------------------------------- | ----------------------------------- |
| Purpose             | Initializes an object                       | Performs a specific operation       |
| Name                | Must be the same as the class               | Can have any valid identifier       |
| Return Type         | Not allowed                                 | Required (`void` or a data type)    |
| Invocation          | Called automatically during object creation | Called explicitly by the programmer |
| Number of Calls     | Once per object creation                    | Can be called multiple times        |
| Inheritance         | Not inherited                               | Inherited unless restricted         |
| Overloading         | Supported                                   | Supported                           |
| Overriding          | Not supported                               | Supported                           |
| Default Version     | Compiler may generate one                   | Never generated automatically       |
| Main Responsibility | Object initialization                       | Object behavior and business logic  |

---

## Key Differences Explained

### ✦ Execution

* A constructor executes automatically when an object is created.
* A method executes only when it is explicitly called.

### ✦ Purpose

* Constructors establish the initial state of an object before it can be used.
* Methods allow the object to perform useful operations throughout its lifetime.

### ✦ Return Type

* Constructors never declare a return type, not even `void`.
* Every method must specify a return type or use `void`.

### ✦ Inheritance

* Constructors belong only to the class in which they are declared and are never inherited.
* Methods participate in inheritance and can be overridden to provide specialized behavior.

### ✦ Flexibility

* Constructors are primarily concerned with object creation.
* Methods can perform validation, calculations, data processing, file handling, networking, and many other operations.

---

## Code Example

```java
class Student {

    private int rollNo;
    private String name;

    // Constructor
    Student(int rollNo, String name) {
        this.rollNo = rollNo;
        this.name = name;
    }

    // Method
    void display() {
        System.out.println("Roll No : " + rollNo);
        System.out.println("Name    : " + name);
    }

    public static void main(String[] args) {

        Student student = new Student(101, "Rahul");

        student.display();
    }
}
```

### Output

```text
Roll No : 101
Name    : Rahul
```

### ✦ Explanation

* `Student(101, "Rahul")` is a constructor that initializes the object.
* `display()` is a method that prints the object's information.
* The constructor executes automatically, whereas the method is called explicitly.

---

## When to Use a Constructor

* Initialize mandatory object data during creation.
* Ensure every object starts in a valid state.
* Perform one-time setup required before the object is used.
* Reduce the need for multiple setter calls immediately after object creation.

---

## When to Use a Method

* Perform calculations or business logic.
* Read or modify object data after initialization.
* Return information to the caller.
* Execute reusable operations throughout the object's lifetime.

---

## Common Interview Questions

**Q: What is the primary difference between a constructor and a method?**

* A constructor initializes an object, whereas a method defines the behavior of that object.

---

**Q: Can a constructor return a value?**

* No.
* Constructors never have a return type.

---

**Q: Can constructors be inherited?**

* No.
* Constructors are not inherited by subclasses.

---

**Q: Can constructors be overridden?**

* No.
* Only methods participate in runtime polymorphism through overriding.

---

**Q: Can constructors and methods be overloaded?**

* Yes.
* Both support overloading by using different parameter lists.

---

## Common Mistakes to Avoid

| Mistake                                                   | Fix                                                      |
| --------------------------------------------------------- | -------------------------------------------------------- |
| Giving a constructor a return type                        | Constructors never specify a return type                 |
| Using constructors for business logic                     | Keep constructors focused on initialization              |
| Expecting constructors to be inherited                    | Constructors belong only to their own class              |
| Confusing constructor overloading with method overloading | Both support overloading, but serve different purposes   |
| Calling methods before proper object initialization       | Initialize objects completely before using their methods |

---

## Resources

### Official Documentation

* Oracle Java Tutorials: Classes and Objects

    * https://docs.oracle.com/javase/tutorial/java/javaOO/classes.html

* Oracle Java Tutorials: Creating Objects

    * https://docs.oracle.com/javase/tutorial/java/javaOO/objectcreation.html

### In-Depth Articles

* Baeldung: Constructors in Java

    * https://www.baeldung.com/java-constructors

* GeeksforGeeks: Constructors in Java

    * https://www.geeksforgeeks.org/constructors-in-java/

* GeeksforGeeks: Methods in Java

    * https://www.geeksforgeeks.org/methods-in-java/

### Java Language Specification

* Java Language Specification: Constructors

    * https://docs.oracle.com/javase/specs/

---

*Made for CS Students | Internship & Job Prep Series*
