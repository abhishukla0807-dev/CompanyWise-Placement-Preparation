# Static vs Non-Static
#### Class-Level vs Object-Level Members | Core Java Concept | Asked in Every Technical Round

> Static belongs to the class. Non-static belongs to the object. That one difference drives everything else.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [What is Static](#what-is-static) |
| 02 | [What is Non-Static](#what-is-non-static) |
| 03 | [Side-by-Side Comparison](#side-by-side-comparison) |
| 04 | [Static Members - Variables, Methods, Blocks](#static-members) |
| 05 | [Non-Static Members - Variables, Methods](#non-static-members) |
| 06 | [Access Rules Between Static and Non-Static](#access-rules-between-static-and-non-static) |
| 07 | [Memory Allocation](#memory-allocation) |
| 08 | [Code Example](#code-example) |
| 09 | [Common Interview Questions](#common-interview-questions) |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 11 | [When to Use What](#when-to-use-what) |
| 12 | [Resources](#resources) |

---

## What is Static

- Declared using the `static` keyword
- Belongs to the class itself, not to any individual object
- Only one copy exists in memory, shared across all objects of the class
- Loaded into memory when the class is loaded by the JVM
- Can be accessed directly using the class name, no object needed
- Exists even if no object of the class has been created

---

## What is Non-Static

- Declared without the `static` keyword
- Belongs to a specific object (instance) of the class
- Each object gets its own independent copy
- Memory is allocated when an object is created with `new`
- Must be accessed through an object reference
- Does not exist until an object is created

---

## Side-by-Side Comparison

| Factor | Static | Non-Static |
|--------|--------|------------|
| Belongs to | Class | Object (Instance) |
| Keyword | `static` | No keyword |
| Memory allocated | When class is loaded | When object is created |
| Memory location | Method Area (Class Area) | Heap |
| Copies in memory | One, shared by all objects | One per object |
| Access via | Class name or object | Object reference only |
| Needs object to call | No | Yes |
| Can access static members | Yes | Yes |
| Can access non-static members | No (directly) | Yes |
| Can be overridden | No | Yes |
| `this` keyword available | No | Yes |
| Example | `Math.random()`, `count` | `name`, `age`, `display()` |

---

## Static Members

### ✦ Static Variable (Class Variable)
- Shared across all objects of the class
- Only one copy in memory regardless of how many objects exist
- Stored in the Method Area (not heap)
- Initialized when the class is loaded
- Changed from one object, changes reflected across all objects
- Common use: counters, constants, shared configuration values

```java
class Student {
    static int count = 0;   // shared by ALL Student objects

    Student() {
        count++;   // every new object increments the same count
    }
}
```

---

### ✦ Static Method
- Belongs to the class, not to any object
- Called using the class name directly
- Cannot access non-static variables or methods directly
- Cannot use `this` keyword (no object context)
- Cannot be overridden (only hidden in subclass)
- JVM executes `main()` as a static method before any object is created
- Common use: utility methods, factory methods, helper functions

```java
class MathUtils {
    static int square(int n) {
        return n * n;
    }
}

// Called without creating an object
int result = MathUtils.square(5);   // 25
```

---

### ✦ Static Block
- Runs automatically once when the class is first loaded into memory
- Runs before any constructor or `main()` method
- Used for complex static variable initialization
- Only executes once per class load, not once per object

```java
class Config {
    static String dbUrl;

    static {
        dbUrl = "jdbc:mysql://localhost:3306/mydb";
        System.out.println("Static block executed");
    }
}
```

---

## Non-Static Members

### ✦ Non-Static Variable (Instance Variable)
- Each object holds its own independent copy
- Stored on the heap inside the object
- Created when object is created, destroyed when object is garbage collected
- Represents the unique state of each individual object
- Must be accessed via an object reference

```java
class Student {
    String name;   // each Student object has its own name
    int marks;     // each Student object has its own marks
}
```

---

### ✦ Non-Static Method (Instance Method)
- Belongs to the object, not the class
- Can access both static and non-static members freely
- Must be called on an object reference
- Can be overridden by subclasses
- `this` keyword is available inside instance methods

```java
class Student {
    String name;

    void display() {           // instance method
        System.out.println("Name: " + this.name);
    }
}
```

---

## Access Rules Between Static and Non-Static

| Who is calling | Can access static members | Can access non-static members |
|----------------|--------------------------|-------------------------------|
| Static method | YES (directly) | NO (needs an object) |
| Non-static method | YES (directly) | YES (directly) |
| Static block | YES (directly) | NO (needs an object) |

- Static method accessing non-static: must create an object first, then access via that object
- Non-static method accessing static: allowed directly, no restriction

```java
class Example {
    static int x = 10;
    int y = 20;

    static void staticMethod() {
        System.out.println(x);        // OK: static accessing static
        // System.out.println(y);     // ERROR: static cannot access non-static directly
        Example obj = new Example();
        System.out.println(obj.y);    // OK: accessed through object
    }

    void instanceMethod() {
        System.out.println(x);        // OK: non-static can access static
        System.out.println(y);        // OK: non-static can access non-static
    }
}
```

---

## Memory Allocation

| Member | Where Stored | When Allocated | When Freed |
|--------|-------------|----------------|------------|
| Static variable | Method Area | Class loading | JVM shutdown |
| Static method | Method Area | Class loading | JVM shutdown |
| Instance variable | Heap (inside object) | `new` keyword | Object is garbage collected |
| Instance method | Method Area (shared) | Class loading | JVM shutdown |
| Local variable | Stack | Method call | Method returns |

- Methods (both static and non-static) are stored only once in the Method Area
- Non-static methods are NOT duplicated per object, the JVM passes the object reference internally
- Instance variables are stored per object on the heap
- Static variables are stored once in the Method Area, shared by all

---

## Code Example

### Java
```java
class Student {
    // Non-static: each object has its own copy
    String name;
    int marks;

    // Static: one shared copy for all objects
    static int totalStudents = 0;

    // Static block: runs once when class loads
    static {
        System.out.println("Student class loaded");
    }

    // Constructor: non-static, runs per object
    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
        totalStudents++;   // updating shared static variable
    }

    // Non-static method: needs object to call
    void display() {
        System.out.println(name + " | Marks: " + marks);
    }

    // Static method: no object needed
    static void showTotal() {
        System.out.println("Total Students: " + totalStudents);
        // System.out.println(name);  // ERROR: cannot access non-static
    }
}

public class Main {
    public static void main(String[] args) {
        // Static block runs here when class loads
        Student s1 = new Student("Aman", 90);
        Student s2 = new Student("Priya", 85);

        s1.display();              // Non-static: called via object
        s2.display();

        Student.showTotal();       // Static: called via class name
        // Output: Total Students: 2
    }
}
```

---

## Common Interview Questions

**Q: What is the difference between static and non-static members?**
- The most direct question, asked in every fresher round
- Static belongs to the class, shared across all objects, accessed via class name
- Non-static belongs to each object, each has its own copy, accessed via object reference

**Q: Why can a static method not access non-static members directly?**
- Tests depth of understanding, not just the rule
- Static methods can run before any object is created
- Non-static members belong to objects, if no object exists there is nothing to access
- The JVM has no way of knowing which object's data to use without an object reference

**Q: Can a non-static method access static members?**
- Simple but important, catches students who only know one direction of the rule
- Yes. Non-static methods belong to objects and can freely access class-level static members
- No restriction exists in this direction

**Q: Why is `main()` declared static in Java?**
- A classic question asked in almost every Java interview
- JVM needs to call `main()` to start the program before any object exists
- If `main()` were non-static, JVM would need an object to call it, but no object can be created without first running the program

**Q: Can static methods be overridden in Java?**
- A trap question, very commonly asked
- No. Static methods cannot be overridden because they belong to the class, not the object
- What appears to be overriding is actually method hiding, a different concept
- Runtime polymorphism does not apply to static methods

**Q: What is a static block and when does it run?**
- Tests knowledge of class loading, asked in mid-level and product-based rounds
- A static block runs once when the class is first loaded into memory by the JVM
- It runs before any constructor, before `main()`, and is used for complex static initialization

---

## Common Mistakes to Avoid

- Accessing non-static members directly inside a static method, this causes a compile-time error
- Thinking non-static methods are stored per object in memory, methods are always in the Method Area, only instance variables are per object
- Saying static methods can be overridden, they cannot, they are hidden not overridden
- Calling a static method on an object reference instead of the class name, it works but is misleading and bad practice
- Forgetting that `this` is not available inside static methods
- Thinking static block runs every time an object is created, it runs only once when the class is loaded

---

## When to Use What

| Situation | Use |
|-----------|-----|
| Counter or tracker shared across all objects | Static variable |
| Constants like `PI` or `MAX_SIZE` | `static final` variable |
| Utility method that does not need object data | Static method |
| One-time complex setup at class load | Static block |
| Data unique to each object | Non-static variable |
| Behavior that depends on object state | Non-static method |
| Factory methods to create objects | Static method |
| Method that needs `this` or instance data | Non-static method |

---

## Resources

- [GeeksforGeeks - Static vs Non-Static Methods in Java](https://www.geeksforgeeks.org/java/static-methods-vs-instance-methods-in-java/)
- [GeeksforGeeks - Static vs Non-Static Variables in Java](https://www.geeksforgeeks.org/java/difference-between-static-and-non-static-variables-in-java/)
- [GeeksforGeeks - Static Method in Java](https://www.geeksforgeeks.org/java/static-method-in-java-with-examples/)
- [GeeksforGeeks - OOP Interview Questions](https://www.geeksforgeeks.org/interview-prep/oops-interview-questions/)
- [InterviewBit - Java Interview Questions](https://www.interviewbit.com/java-interview-questions/)

---

*Made for CS Students | Internship & Job Prep Series*