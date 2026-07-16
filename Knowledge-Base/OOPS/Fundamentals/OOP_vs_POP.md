# OOP vs POP
#### Object-Oriented vs Procedure-Oriented Programming | Asked in Every First Technical Round

> OOP organizes code around objects. POP organizes code around functions. That one difference changes everything.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [What is POP](#what-is-pop) |
| 02 | [What is OOP](#what-is-oop) |
| 03 | [Side-by-Side Comparison](#side-by-side-comparison) |
| 04 | [POP - Pros and Cons](#pop---pros-and-cons) |
| 05 | [OOP - Pros and Cons](#oop---pros-and-cons) |
| 06 | [How Each Approach Works](#how-each-approach-works) |
| 07 | [Code Example](#code-example) |
| 08 | [Common Interview Questions](#common-interview-questions) |
| 09 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 10 | [When to Use What](#when-to-use-what) |
| 11 | [Resources](#resources) |

---

## What is POP

- Procedure-Oriented Programming, one of the oldest programming paradigms
- Program is written as a sequence of functions called one after another
- Each function performs a specific task and can call other functions
- Data is mostly global, accessible by all functions in the program
- Follows a top-down approach, execution flows from start to end
- Focus is on what steps to take, not on what entities exist
- Examples: C, Pascal, FORTRAN, BASIC

---

## What is OOP

- Object-Oriented Programming, a paradigm built around real-world entities
- Program is divided into objects, each combining its own data and methods
- Data is tied closely to the functions that operate on it
- Access to data is controlled, not freely shared across the program
- Follows a bottom-up approach, build small objects, combine them into a system
- Focus is on what things are and how they interact
- Examples: Java, C++, Python, C#

---

## Side-by-Side Comparison

| Factor | POP | OOP |
|--------|-----|-----|
| Basic unit | Function / Procedure | Object |
| Approach | Top-down | Bottom-up |
| Focus | Procedure over data | Data over procedure |
| Data access | Global, accessible by all functions | Private, controlled through methods |
| Data security | Low, data moves freely | High, encapsulation protects data |
| Code reuse | Through function calls | Through inheritance and composition |
| Real-world modeling | Difficult | Natural and intuitive |
| Overloading | Not supported | Supported |
| Inheritance | Not supported | Supported |
| Polymorphism | Not supported | Supported |
| Maintenance | Hard in large programs | Easier, changes are localized |
| Best for | Small, simple, sequential tasks | Large, complex, scalable systems |
| Examples | C, Pascal | Java, C++, Python |

---

## POP - Pros and Cons

### ✦ Advantages

- Simple to understand and write for small programs
- Execution flow is easy to trace from top to bottom
- Less memory overhead, no object creation cost
- Faster for simple, sequential tasks
- Suitable for system-level and embedded programming
- Easy for beginners to grasp the basics of programming

### ✦ Disadvantages

- Data is global, any function can accidentally modify it
- Hard to identify which function uses which data in large programs
- No concept of data hiding or access control
- Code is difficult to reuse in other applications
- Does not map well to real-world problems
- Harder to maintain as codebase grows
- No inheritance or polymorphism support

---

## OOP - Pros and Cons

### ✦ Advantages

- Data is protected through encapsulation, no accidental modification
- Code reuse through inheritance reduces duplication
- Models real-world entities naturally using objects and classes
- Polymorphism makes code flexible and easier to extend
- Modular structure, each class is independent and testable
- Easier to maintain, changes in one class do not break others
- Multiple developers can work on different classes without conflict

### ✦ Disadvantages

- More complex to design upfront than POP
- Object creation and method calls add memory and performance overhead
- Not the best choice for small scripts or simple sequential tasks
- Requires deeper understanding to design well
- Poor class design leads to tightly coupled, fragile code

---

## How Each Approach Works

### POP
- Program starts at the top and executes step by step
- Functions are called in sequence, each doing a specific task
- Data is declared globally so all functions can access it
- Adding a new feature often means modifying multiple existing functions
- Large programs become hard to debug because any function can change any data

### OOP
- Program is structured as a collection of objects that communicate
- Each object owns its data and exposes controlled methods
- A new feature is added by creating a new class or extending an existing one
- Bugs are easier to find because each class manages its own state
- Multiple objects can exist independently without interfering with each other

> POP is like a kitchen where everyone shares one big bowl of ingredients. OOP is like individual chefs each with their own station, tools, and ingredients. One is simpler for a single cook, the other scales when the kitchen gets bigger.

---

## Code Example

### Java

```java
// POP style - functions operating on separate data
class StudentPOP {
    static String name = "Aman";
    static int marks = 85;

    static void displayStudent() {
        System.out.println(name + " scored " + marks);
    }

    static void applyGrade() {
        if (marks >= 90) System.out.println("Grade: A");
        else System.out.println("Grade: B");
    }
}

// OOP style - data and behavior bundled in an object
class StudentOOP {
    private String name;
    private int marks;

    StudentOOP(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    void display() {
        System.out.println(name + " scored " + marks);
    }

    void applyGrade() {
        if (marks >= 90) System.out.println("Grade: A");
        else System.out.println("Grade: B");
    }
}
```



## Common Interview Questions

**Q: What is the difference between OOP and POP?**
- The most commonly asked question on this topic, appears in almost every fresher interview
- POP divides the program into functions with shared global data. OOP divides it into objects that own their data and control access to it
- Always mention the key contrast: data is exposed in POP, protected in OOP

**Q: Why was OOP introduced when POP already existed?**
- Tests whether you understand the limitations of POP, not just the features of OOP
- POP fails at scale: global data becomes hard to manage, code is difficult to reuse, real-world entities cannot be modeled naturally
- OOP solved these problems by introducing encapsulation, inheritance, and polymorphism

**Q: Does POP support inheritance or polymorphism?**
- Simple but tricky if you have not revised
- No. POP has no concept of inheritance, polymorphism, or overloading
- These are features exclusive to OOP and are one of its biggest advantages over POP

**Q: Which is faster, OOP or POP?**
- A nuanced question, often asked in product-based interviews
- POP is generally faster for small programs because there is no object creation overhead
- OOP trades some performance for structure, security, and maintainability, which matters more in large systems

**Q: Can C++ be used as both OOP and POP?**
- Tests knowledge of language flexibility
- Yes. C++ supports both paradigms. You can write pure procedural C-style code in C++, or use classes and objects for OOP
- Java does not offer this flexibility, it is strictly OOP

---

## Common Mistakes to Avoid

- Saying OOP is always better than POP, POP is genuinely better for small and performance-critical tasks
- Confusing top-down and bottom-up approaches, POP is top-down, OOP is bottom-up
- Saying C supports OOP, C is a purely procedural language with no native OOP support
- Thinking global data in POP is always a problem, it is a design choice that becomes a problem only in large programs
- Listing OOP features like inheritance and polymorphism without knowing that POP has no equivalent

---

## When to Use What

| Situation | Go with |
|-----------|---------|
| Small script or utility tool | POP |
| System-level or embedded programming | POP |
| Large application with multiple modules | OOP |
| Real-world entities with data and behavior | OOP |
| Performance-critical sequential tasks | POP |
| Team project with multiple developers | OOP |
| Code needs to be reused across projects | OOP |
| Quick mathematical computation | POP |

---

## Resources

- [GeeksforGeeks - Difference between OOP and POP](https://www.geeksforgeeks.org/cpp/difference-between-oop-and-pop/)
- [GeeksforGeeks - OOP Interview Questions](https://www.geeksforgeeks.org/interview-prep/oops-interview-questions/)
- [InterviewBit - OOPs Interview Questions](https://www.interviewbit.com/oops-interview-questions/)
- [PrepInsta - OOPs Interview Questions](https://prepinsta.com/interview-preparation/technical-interview-questions/oops/)
- [TutorialsPoint - OOP vs POP](https://www.tutorialspoint.com/difference-between-oop-and-pop)

---

*Made for CS Students | Internship & Job Prep Series*