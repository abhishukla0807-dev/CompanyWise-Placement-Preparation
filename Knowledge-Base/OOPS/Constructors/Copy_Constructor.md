# Copy Constructor

#### Creating a New Object from an Existing Object | A Fundamental Concept for Object Copying in Java

> Java does not provide a built-in copy constructor like C++, but it is a widely accepted pattern for creating copies of objects with the same state.

---

## 📌 Table of Contents

| #  | Section                                                           |
| -- | ----------------------------------------------------------------- |
| 01 | [What is a Copy Constructor?](#what-is-a-copy-constructor)        |
| 02 | [Why Do We Need It?](#why-do-we-need-it)                          |
| 03 | [How a Copy Constructor Works](#how-a-copy-constructor-works)     |
| 04 | [Characteristics](#characteristics)                               |
| 05 | [Syntax](#syntax)                                                 |
| 06 | [Code Example](#code-example)                                     |
| 07 | [Copy Constructor vs Assignment](#copy-constructor-vs-assignment) |
| 08 | [Advantages](#advantages)                                         |
| 09 | [Common Interview Questions](#common-interview-questions)         |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)             |
| 11 | [When to Use a Copy Constructor](#when-to-use-a-copy-constructor) |
| 12 | [Resources](#resources)                                           |

---

## What is a Copy Constructor?

* A **copy constructor** is a constructor that creates a new object by copying the values of another object of the same class.
* Unlike a parameterized constructor, the constructor accepts an object instead of individual values.
* Java does not automatically generate a copy constructor. If object copying is required, the programmer must implement it explicitly.
* The copied object is a **new object** with its own memory, even though it initially contains the same data.

### ✦ Key Points

* Accepts an object of the same class as its parameter.
* Creates a separate object with identical field values.
* Used to duplicate an object's state.
* Implemented manually in Java.

### ✦ Real-World Analogy

* Think of photocopying a document.
* The copied document contains the same information, but it is an independent copy.
* Changes made to one document do not affect the other.

---

## Why Do We Need It?

* Sometimes an application needs another object with the same initial state as an existing object.
* Passing every field again through a parameterized constructor becomes difficult when a class contains many attributes.
* A copy constructor simplifies object duplication and keeps the copying logic centralized.
* It improves readability by clearly expressing the intention of creating a copy.

---

## How a Copy Constructor Works

```text
Original Object
       │
       ▼
Copy Constructor
       │
       ▼
Copies Field Values
       │
       ▼
New Independent Object
```

---

## Characteristics

| Feature            | Description              |
| ------------------ | ------------------------ |
| Parameter          | Object of the same class |
| Creates New Object | Yes                      |
| Memory Shared      | No                       |
| Compiler Generated | No                       |
| Programmer Defined | Yes                      |

---

## Syntax

```java
class Student {

    int id;
    String name;

    Student(Student s) {
        this.id = s.id;
        this.name = s.name;
    }
}
```

---

## Code Example

```java
class Student {

    private int rollNo;
    private String name;

    Student(int rollNo, String name) {
        this.rollNo = rollNo;
        this.name = name;
    }

    Student(Student student) {
        this.rollNo = student.rollNo;
        this.name = student.name;
    }

    void display() {
        System.out.println(rollNo + " " + name);
    }

    public static void main(String[] args) {

        Student s1 = new Student(101, "Rahul");

        Student s2 = new Student(s1);

        s1.display();
        s2.display();
    }
}
```

**Output**

```text
101 Rahul
101 Rahul
```

---

## Copy Constructor vs Assignment

| Feature                 | Copy Constructor | Assignment (`=`) |
| ----------------------- | ---------------- | ---------------- |
| Creates New Object      | Yes              | No               |
| Copies Values           | Yes              | No               |
| Memory Location         | Different        | Same Reference   |
| Object Independence     | Yes              | No               |
| Changes Affect Original | No               | Yes              |

---

## Advantages

* Simplifies object duplication without passing every field individually.
* Keeps object initialization logic inside the class.
* Improves readability when copying complex objects.
* Produces an independent object instead of another reference to the same object.
* Frequently used while implementing immutable objects and defensive copying.

---

## Common Interview Questions

**Q: Does Java have a built-in copy constructor?**

* No.
* Java does not automatically generate copy constructors like C++.
* Developers implement them manually whenever required.

---

**Q: Is a copy constructor mandatory in Java?**

* No.
* It is used only when object copying is needed.

---

**Q: What is copied in a copy constructor?**

* The constructor copies the values of the object's fields into a newly created object.

---

**Q: Is a copy constructor different from assignment?**

* Yes.
* Assignment copies only the reference, whereas a copy constructor creates a completely new object.

---

**Q: Can a copy constructor perform deep copying?**

* Yes.
* It depends on how the programmer copies mutable fields inside the constructor.

---

## Common Mistakes to Avoid

| Mistake                                                 | Fix                                       |
| ------------------------------------------------------- | ----------------------------------------- |
| Confusing assignment with copying                       | Assignment copies references, not objects |
| Assuming Java provides a copy constructor automatically | Implement it manually                     |
| Forgetting to copy all required fields                  | Copy every important instance variable    |
| Sharing mutable objects unintentionally                 | Perform deep copying when necessary       |
| Using copy constructors without validation              | Validate copied values if required        |

---

## When to Use a Copy Constructor

| Situation                          | Recommended                |
| ---------------------------------- | -------------------------- |
| Duplicate an existing object       | ✅ Yes                      |
| Defensive copying                  | ✅ Yes                      |
| Creating immutable classes         | ✅ Recommended              |
| Cloning complex objects            | ✅ Alternative to `clone()` |
| Only another reference is required | ❌ Use assignment instead   |

---

## Resources

* Oracle Java Tutorials: Classes and Objects
* Oracle Knowledge Documentation
* Baeldung: Copy Constructors in Java
* GeeksforGeeks: Copy Constructor in Java

---

*Made for CS Students | Internship & Job Prep Series*
