# What is a Class
#### The Building Block of OOP | Asked in Every Fresher Technical Round

> A class is a user-defined blueprint that defines what an object will look like and how it will behave.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [What is a Class](#what-is-a-class) |
| 02 | [Components of a Class](#components-of-a-class) |
| 03 | [Types of Classes](#types-of-classes) |
| 04 | [Class vs Structure](#class-vs-structure) |
| 05 | [How a Class Works Internally](#how-a-class-works-internally) |
| 06 | [Code Example](#code-example) |
| 07 | [Common Interview Questions](#common-interview-questions) |
| 08 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 09 | [When to Use What](#when-to-use-what) |
| 10 | [Resources](#resources) |

---

## What is a Class

- A user-defined data type that acts as a template for creating objects
- Groups related data and methods into a single unit
- Does not occupy memory on its own, no instance exists until an object is created
- Exists at compile time, not at runtime
- One class can produce unlimited objects, each with its own data
- Not a real-world entity itself, but describes what real-world entities will look like
- Every object-oriented program is built on top of classes

---

## Components of a Class

### ✦ Data Members (Fields / Attributes)
- Variables declared inside the class that hold the state of an object
- Can be `private`, `public`, or `protected`
- Each object gets its own copy of instance data members
- Static data members are shared across all objects of the class

### ✦ Member Methods (Functions / Behaviors)
- Functions defined inside the class that operate on the data members
- Define what an object can do
- Can be instance methods or static methods
- Methods are shared across all objects, not duplicated per object

### ✦ Constructor
- Special method that runs automatically when an object is created
- Used to initialize data members
- Has the same name as the class
- No return type, not even `void`

### ✦ Destructor
- Special method that runs automatically when an object is destroyed or goes out of scope
- Used to free resources and clean up memory
- In Java, handled automatically by the garbage collector
- In C++, defined explicitly with `~ClassName()`

### ✦ Access Modifiers
- Keywords that control which parts of the class are visible from outside
- `private`: accessible only within the class
- `public`: accessible from anywhere
- `protected`: accessible within the class and its subclasses

---

## Types of Classes

| Type | Description | Key Point |
|------|-------------|-----------|
| Concrete Class | A regular, fully implemented class | Can be instantiated directly |
| Abstract Class | Has at least one abstract method with no body | Cannot be instantiated, must be extended |
| Final Class | Declared with `final` keyword in Java | Cannot be extended or subclassed |
| Singleton Class | Only one instance allowed throughout the program | Constructor is private |
| Inner Class | Defined inside another class | Has access to outer class members |
| Anonymous Class | A class with no name, defined and instantiated in one step | Used for one-time use, often with interfaces |
| Generic Class | Accepts type parameters | `class Box<T>` works with any data type |

---

## Class vs Structure

| Factor | Class | Structure |
|--------|-------|-----------|
| Default access | `private` | `public` |
| Inheritance | Supported | Not supported in C, limited in C++ |
| Methods | Fully supported | Supported in C++ only |
| Use case | Complex objects with behavior | Lightweight data containers |
| Memory | Heap (when instantiated) | Stack (usually) |
| OOP features | Fully supported | Limited |

> In Java, there is no `struct`. Everything is a class. In C++, the only real difference between `struct` and `class` is the default access modifier.

---

## How a Class Works Internally

- When the compiler reads a class definition, it stores the class structure in the **method/code segment** of memory
- No memory is reserved for data at this stage
- When `new ClassName()` is called, memory is allocated on the **heap** for that object's data members
- The constructor runs and initializes the fields
- A reference on the **stack** points to the object on the heap
- Methods are stored once in the code segment, not duplicated per object
- Static members are stored in a special static memory area, shared across all objects

> Think of a class as a mold for making clay pots. The mold takes no clay itself. Every pot made from it is a separate, independent object. The mold lives in the factory (code segment), the pots live on the shelf (heap).

---

## Code Example

### Java
```java
class Student {
    // Data members
    private String name;
    private int rollNo;
    private static int totalStudents = 0;  // shared across all objects

    // Constructor
    Student(String name, int rollNo) {
        this.name = name;
        this.rollNo = rollNo;
        totalStudents++;
    }

    // Instance methods
    void display() {
        System.out.println("Name: " + name + " | Roll No: " + rollNo);
    }

    // Static method
    static int getTotalStudents() {
        return totalStudents;
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Aman", 101);
        Student s2 = new Student("Priya", 102);

        s1.display();   // Name: Aman | Roll No: 101
        s2.display();   // Name: Priya | Roll No: 102

        System.out.println("Total: " + Student.getTotalStudents());  // Total: 2
    }
}
```

---

## Common Interview Questions

**Q: What is a class in OOP?**
- The most basic question, asked in every fresher round
- A class is a user-defined data type that bundles data and methods into a single unit and acts as a blueprint for creating objects
- Always follow with: "It does not occupy memory on its own, memory is only allocated when an object is created"

**Q: What is the difference between a class and an object?**
- The most common follow-up after the class definition question
- Class is the template, object is the instance created from it
- Class exists at compile time, object exists at runtime and occupies heap memory

**Q: Can a class exist without any objects?**
- Tests whether you understand that a class is just a definition
- Yes. A class can be defined and compiled without ever creating an object from it
- Static methods and static variables in the class can still be used without an object

**Q: What is a static member in a class?**
- Tests understanding of class-level vs object-level data
- A static member belongs to the class itself, not to any individual object
- All objects share the same static member. Changing it from one object changes it for all

**Q: What is the difference between an abstract class and a concrete class?**
- Common follow-up in product-based and service-based company rounds
- A concrete class is fully implemented and can be instantiated directly
- An abstract class has at least one method with no body and cannot be instantiated, it must be extended by a subclass

**Q: What is a constructor and why is it important?**
- Asked in almost every technical round alongside class questions
- A constructor initializes the object's data members the moment the object is created
- It has the same name as the class, no return type, and runs automatically without being called explicitly

---

## Common Mistakes to Avoid

- Saying a class occupies memory, it does not, only objects do
- Confusing static and instance members, static belongs to the class, instance belongs to each object
- Saying a constructor has a `void` return type, it has no return type at all
- Thinking abstract classes and interfaces are the same, they are not
- Saying Java has `struct`, it does not, Java uses classes for everything
- Forgetting that `final` classes cannot be extended, `String` in Java is a `final` class

---

## When to Use What

| Situation | Use |
|-----------|-----|
| Modeling a real-world entity with data and behavior | Concrete Class |
| Defining a base template others must implement | Abstract Class |
| Preventing subclassing for security or design reasons | Final Class |
| Ensuring only one instance exists globally | Singleton Class |
| Quick one-time implementation of an interface | Anonymous Class |
| Writing reusable code that works with any data type | Generic Class |
| Grouping lightweight data with no behavior | Structure (C++ only) |

---

## Resources

- [GeeksforGeeks - Classes and Objects in Java](https://www.geeksforgeeks.org/java/object-oriented-programming-oops-concept-in-java/)
- [GeeksforGeeks - OOP Interview Questions](https://www.geeksforgeeks.org/interview-prep/oops-interview-questions/)
- [InterviewBit - OOPs Interview Questions](https://www.interviewbit.com/oops-interview-questions/)
- [GeeksforGeeks - Java OOP Concepts](https://www.geeksforgeeks.org/java/four-main-object-oriented-programming-concepts-of-java/)

---

*Made for CS Students | Internship & Job Prep Series*