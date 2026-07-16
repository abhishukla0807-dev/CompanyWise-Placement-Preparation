# What is an Object
#### Instance of a Class | Memory Allocation | Runtime Behavior | Asked in Every Technical Round

> An object is a real, live instance of a class. It occupies memory, holds actual data, and can execute behavior.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [What is an Object](#what-is-an-object) |
| 02 | [Properties of an Object](#properties-of-an-object) |
| 03 | [How an Object is Created](#how-an-object-is-created) |
| 04 | [Object in Memory - The Full Picture](#object-in-memory---the-full-picture) |
| 05 | [Stack vs Heap - Side by Side](#stack-vs-heap---side-by-side) |
| 06 | [Object Lifecycle](#object-lifecycle) |
| 07 | [Garbage Collection](#garbage-collection) |
| 08 | [Code Example](#code-example) |
| 09 | [Common Interview Questions](#common-interview-questions) |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 11 | [Resources](#resources) |

---

## What is an Object

- A real instance of a class created at runtime
- Occupies memory in the **heap** the moment it is created
- Holds its own copy of all instance variables defined in the class
- Can call any non-private method defined in its class
- Every object is independent, changing one object's data does not affect another
- Multiple objects can be created from one class simultaneously
- The reference variable pointing to the object lives on the **stack**, not the heap

---

## Properties of an Object

### ✦ State
- The data an object holds at any point in time
- Stored in instance variables (fields) defined in the class
- Each object has its own independent state
- Example: a `Student` object has `name = "Aman"` and `marks = 90`

### ✦ Behavior
- The actions an object can perform
- Defined by the methods of the class
- Methods are not stored per object, they are shared from the class in the method area
- Example: a `Student` object can call `display()` or `getGrade()`

### ✦ Identity
- What makes one object distinct from another even if they hold the same data
- In Java, each object has a unique memory address on the heap
- The JVM assigns a unique hash code to each object by default
- `==` checks identity (same memory address), `.equals()` checks state (same data)

---

## How an Object is Created

- Step 1: JVM reads the class definition from the method area
- Step 2: `new` keyword triggers the JVM to allocate memory on the heap for the object
- Step 3: All instance variables are initialized to default values (0, null, false)
- Step 4: The constructor runs and sets the actual values
- Step 5: A reference to the heap address is returned and stored in a stack variable

```
Student s = new Student("Aman", 101);
```

- `Student` tells the JVM which class blueprint to use
- `new` allocates memory on the heap
- `Student("Aman", 101)` calls the constructor
- `s` is the reference variable stored on the stack, pointing to the object on the heap

---

## Object in Memory - The Full Picture

| What | Where it lives | Lifecycle |
|------|---------------|-----------|
| Object's instance variables | Heap | Lives as long as the object is referenced |
| Reference variable (e.g. `s`) | Stack | Lives as long as the method is executing |
| Class methods | Method Area (Code Segment) | Loaded once, shared by all objects |
| Static variables | Method Area | Loaded once when class is loaded, never per object |
| Local variables inside methods | Stack | Created when method is called, destroyed when method returns |
| Primitive fields inside an object | Inside the object on Heap | Lives with the object |

### JVM Memory Areas Involved

- **Heap** - Where every object lives. Shared by all threads. Managed by the Garbage Collector
- **Stack** - Where references and local variables live. One stack per thread. LIFO order
- **Method Area** - Where class definitions, method bytecode, and static variables are stored
- **Metaspace** - Replaced PermGen from Java 8. Stores class metadata using native memory

---

## Stack vs Heap - Side by Side

| Factor | Stack | Heap |
|--------|-------|------|
| Stores | References, local variables, method calls | Actual objects and their instance data |
| Allocation | Automatic, on method call | Manual via `new` keyword |
| Deallocation | Automatic, on method return | Handled by Garbage Collector |
| Speed | Faster | Slower |
| Size | Small and fixed | Large and dynamic |
| Thread access | Each thread has its own stack | Shared across all threads |
| Order | LIFO | No specific order |
| Error when full | `StackOverflowError` | `OutOfMemoryError` |
| Scope | Limited to the current method | Globally accessible while referenced |

---

## Object Lifecycle

- **Creation** - `new` is called, memory is allocated on heap, constructor runs
- **In use** - Object is referenced by one or more variables, methods can be called on it
- **Unreachable** - No active reference points to the object anymore
- **Eligible for GC** - JVM marks it as garbage, it can be collected at any time
- **Destroyed** - Garbage Collector reclaims the heap memory, object no longer exists

> An object becomes unreachable when the reference variable goes out of scope, is set to `null`, or is reassigned to another object.

---

## Garbage Collection

- Java handles memory deallocation automatically through the Garbage Collector
- When an object has no active references, it becomes eligible for garbage collection
- GC runs on heap memory and removes unreferenced objects
- Heap is divided into generations to make GC efficient

### Heap Generations

| Generation | Purpose |
|------------|---------|
| Young Generation (Eden) | All new objects are created here first |
| Survivor Space (S0, S1) | Objects that survive Eden GC are moved here |
| Old (Tenured) Generation | Long-lived objects that survived multiple GC cycles |
| Metaspace | Class metadata, not part of heap (from Java 8) |

- Minor GC runs on Young Generation frequently
- Major GC runs on Old Generation less frequently but takes longer
- `System.gc()` can suggest a GC run but does not guarantee it
- GC pause is called **Stop-the-World**, all threads are paused during collection

---

## Code Example

### Java
```java
class Student {
    // Instance variables - stored on HEAP inside the object
    private String name;
    private int marks;

    // Static variable - stored in METHOD AREA, shared by all objects
    private static int totalStudents = 0;

    // Constructor - runs when object is created on heap
    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
        totalStudents++;
    }

    void display() {
        // Local variable - stored on STACK during method execution
        String grade = marks >= 90 ? "A" : "B";
        System.out.println(name + " | Marks: " + marks + " | Grade: " + grade);
    }

    static int getTotal() {
        return totalStudents;
    }
}

public class Main {
    public static void main(String[] args) {
        // s1 and s2 are references stored on STACK
        // The actual Student objects are stored on HEAP
        Student s1 = new Student("Aman", 95);
        Student s2 = new Student("Priya", 88);

        s1.display();   // Aman | Marks: 95 | Grade: A
        s2.display();   // Priya | Marks: 88 | Grade: B

        System.out.println("Total Students: " + Student.getTotal());  // 2

        // s1 is now unreachable, eligible for garbage collection
        s1 = null;
    }
}
```

**Memory layout for the above code:**
- `s1`, `s2` references live on the **Stack** inside `main()`
- Two `Student` objects live on the **Heap**
- `totalStudents` lives in the **Method Area**
- `grade` inside `display()` lives on the **Stack** and dies when `display()` returns
- After `s1 = null`, the first object is eligible for Garbage Collection

---

## Common Interview Questions

**Q: What is an object in OOP?**
- The most basic question, sets the foundation for all other OOP questions
- An object is a real instance of a class that occupies memory on the heap, holds its own data, and can execute the methods defined in its class
- Always follow with: the reference lives on the stack, the object lives on the heap

**Q: Where is an object stored in memory?**
- Very commonly asked in Java and system-level interviews
- The object itself is stored on the heap. The reference variable pointing to it is stored on the stack
- Methods are not stored in the object, they are shared from the Method Area

**Q: What is the difference between `==` and `.equals()` in Java?**
- Directly tests knowledge of object identity vs object state
- `==` compares memory addresses (are these the exact same object in heap)
- `.equals()` compares the content or state of two objects (do they hold the same values)

**Q: What happens when an object has no references?**
- Tests understanding of the object lifecycle and garbage collection
- It becomes unreachable and eligible for garbage collection
- The JVM's GC will eventually reclaim its heap memory, but timing is not guaranteed

**Q: What is `NullPointerException` and why does it happen?**
- One of the most common runtime errors, always asked in Java interviews
- It happens when you try to call a method or access a field on a reference that points to nothing (null)
- The reference exists on the stack but there is no object on the heap for it to point to

**Q: What is the difference between Stack and Heap memory?**
- Frequently asked in memory-focused rounds and system design discussions
- Stack is for references and local variables, fast, LIFO, per thread
- Heap is for objects, slower, large, shared across threads, managed by GC

---

## Common Mistakes to Avoid

- Saying the object is stored on the stack, only the reference is on the stack, the object itself is always on the heap
- Confusing `==` with `.equals()`, `==` checks same object in memory, `.equals()` checks same value
- Thinking static variables are stored inside each object, they are not, static variables live in the Method Area and are shared
- Saying garbage collection is triggered immediately when a reference is set to null, GC runs on its own schedule
- Confusing `StackOverflowError` with `OutOfMemoryError`, stack overflow is from too many nested method calls, out of memory is from too many objects on the heap

---

## Resources

- [GeeksforGeeks - How are Java Objects Stored in Memory](https://www.geeksforgeeks.org/java/how-are-java-objects-stored-in-memory/)
- [GeeksforGeeks - Stack vs Heap Memory Allocation](https://www.geeksforgeeks.org/dsa/stack-vs-heap-memory-allocation/)
- [GeeksforGeeks - Java Memory Management](https://www.geeksforgeeks.org/java/java-memory-management/)
- [Baeldung - Memory Management Interview Questions](https://www.baeldung.com/java-memory-management-interview-questions)
- [InterviewBit - Java Interview Questions](https://www.interviewbit.com/java-interview-questions/)

---

*Made for CS Students | Internship & Job Prep Series*