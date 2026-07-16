# Parameterized Constructor

#### Initializing Objects with Custom Values | One of the Most Frequently Used Constructors in Java Applications

> A parameterized constructor allows every object to start with its own state, making classes more flexible, reusable, and meaningful.

---

## 📌 Table of Contents

| #  | Section                                                                                                             |
| -- | ------------------------------------------------------------------------------------------------------------------- |
| 01 | [What is a Parameterized Constructor?](#what-is-a-parameterized-constructor)                                        |
| 02 | [Why Do We Need It?](#why-do-we-need-it)                                                                            |
| 03 | [How a Parameterized Constructor Works](#how-a-parameterized-constructor-works)                                     |
| 04 | [Characteristics](#characteristics)                                                                                 |
| 05 | [Syntax](#syntax)                                                                                                   |
| 06 | [Code Example](#code-example)                                                                                       |
| 07 | [Parameterized Constructor vs Default Constructor](#parameterized-constructor-vs-default-constructor)               |
| 08 | [Constructor Overloading with Parameterized Constructors](#constructor-overloading-with-parameterized-constructors) |
| 09 | [Best Practices](#best-practices)                                                                                   |
| 10 | [Common Interview Questions](#common-interview-questions)                                                           |
| 11 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)                                                               |
| 12 | [When to Use a Parameterized Constructor](#when-to-use-a-parameterized-constructor)                                 |
| 13 | [Resources](#resources)                                                                                             |

---

## What is a Parameterized Constructor?

* A **parameterized constructor** is a constructor that accepts one or more parameters during object creation, allowing each object to be initialized with its own set of values. Instead of relying on default values, the constructor receives information from the caller and uses it to establish the initial state of the object.


* Parameterized constructors are widely used because most real-world objects are not identical. A `Student` object should have its own roll number, a `BankAccount` should have its own account number, and an `Employee` should have its own name and salary. Parameterized constructors make this customization possible from the moment the object is created.

### ✦ Key Points

* Accepts one or more parameters.
* Initializes objects with user-provided values.
* Executes automatically during object creation.
* Eliminates the need for multiple setter calls immediately after object creation.
* Helps create fully initialized and valid objects.

### ✦ Real-World Analogy

* Consider booking a hotel room online. Every booking requires details such as the guest's name, check-in date, and room type. Without these details, the booking cannot be completed.
* A parameterized constructor works in a similar way. The required information is supplied during object creation, ensuring that the object is initialized correctly from the beginning.

---

## Why Do We Need It?

- Most real-world objects are not identical. Every object usually contains different data, such as a student's roll number or an employee's salary.


- A parameterized constructor allows these values to be supplied during object creation, ensuring the object starts with meaningful information.


- It removes the need to call multiple setter methods immediately after creating an object, making initialization concise and less error-prone.


- It helps maintain object consistency because mandatory fields are initialized before the object is used.


---

## How a Parameterized Constructor Works

When an object is created using a parameterized constructor, Java follows a well-defined sequence of operations.

1. Memory is allocated for the object.
2. Constructor arguments are received.
3. The constructor initializes instance variables using those arguments.
4. The object becomes fully initialized and ready for use.

```text
Object Creation
       │
       ▼
Memory Allocation
       │
       ▼
Arguments Passed
       │
       ▼
Constructor Executes
       │
       ▼
Instance Variables Initialized
       │
       ▼
Object Ready
```

---

## Characteristics

| Feature               | Description                              |
| --------------------- | ---------------------------------------- |
| Parameters            | One or more                              |
| Automatic Invocation  | Yes                                      |
| Object Initialization | Uses caller-provided values              |
| Return Type           | Not Allowed                              |
| Constructor Name      | Same as the class name                   |
| Compiler Generation   | No, it must be written by the programmer |

---

## Syntax

```java
class Student {

    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

### ✦ Explanation

* The constructor name must exactly match the class name.
* Parameters receive values supplied during object creation.
* The `this` keyword distinguishes instance variables from constructor parameters having the same name.
* The constructor executes automatically whenever a new object is created using the `new` keyword.

---

## Code Example

```java
class Student {

    private int rollNo;
    private String name;
    private String branch;

    Student(int rollNo, String name, String branch) {
        this.rollNo = rollNo;
        this.name = name;
        this.branch = branch;
    }

    void display() {
        System.out.println("Roll No : " + rollNo);
        System.out.println("Name    : " + name);
        System.out.println("Branch  : " + branch);
    }

    public static void main(String[] args) {

        Student s1 = new Student(101, "Rahul", "CSE");
        Student s2 = new Student(102, "Priya", "IT");

        s1.display();

        System.out.println();

        s2.display();
    }
}
```

**Output**

```text
Roll No : 101
Name    : Rahul
Branch  : CSE

Roll No : 102
Name    : Priya
Branch  : IT
```

---

## Parameterized Constructor vs Default Constructor

| Feature               | Default Constructor | Parameterized Constructor            |
| --------------------- | ------------------- | ------------------------------------ |
| Parameters            | None                | One or more                          |
| Object Initialization | Default values      | User-provided values                 |
| Compiler Can Generate | Yes                 | No                                   |
| Custom Initialization | Limited             | Complete                             |
| Practical Usage       | Less common         | Used in most real-world applications |

---

## Constructor Overloading with Parameterized Constructors

A class can contain multiple parameterized constructors as long as their parameter lists are different. This is known as **constructor overloading**.

Constructor overloading provides flexibility by allowing objects to be created in multiple ways depending on the information available. For example, one constructor may initialize only a student's name, while another initializes the name, roll number, and branch.

Java determines which constructor to invoke based on the number, order, and data types of the arguments supplied during object creation.

---

## Best Practices

* Initialize all mandatory fields inside the constructor to ensure the object starts in a valid state.
* Use meaningful parameter names that clearly describe the expected values.
* Prefer the `this` keyword when parameter names are identical to instance variables, as it improves readability and eliminates ambiguity.
* Keep constructor logic focused on object initialization. Complex business logic should be implemented in separate methods rather than inside constructors.

---

## Common Interview Questions

**Q: What is a parameterized constructor?**

* A parameterized constructor is a constructor that accepts one or more arguments and initializes an object using the values supplied during object creation.

---

**Q: Why do we use parameterized constructors?**

* They allow different objects of the same class to have different initial values, making object creation more flexible and reducing additional initialization code.

---

**Q: Can a class have both a default constructor and a parameterized constructor?**

* Yes. A class can contain multiple constructors with different parameter lists through constructor overloading.

---

**Q: Does Java automatically create a default constructor if a parameterized constructor is present?**

* No. Once any constructor is explicitly defined, the compiler does not generate a default constructor automatically.

---

**Q: Why is the `this` keyword commonly used inside parameterized constructors?**

* It distinguishes instance variables from constructor parameters when both share the same name.

---

## Common Mistakes to Avoid

| Mistake                                                        | Fix                                                            |
| -------------------------------------------------------------- | -------------------------------------------------------------- |
| Forgetting to initialize instance variables                    | Assign every required field inside the constructor             |
| Omitting the `this` keyword when needed                        | Use `this` to clearly refer to instance variables              |
| Writing business logic inside constructors                     | Keep constructors focused on initialization only               |
| Expecting Java to generate a default constructor automatically | Define a no-argument constructor explicitly if required        |
| Creating objects with incomplete information                   | Make important fields mandatory through constructor parameters |

---

## When to Use a Parameterized Constructor

| Situation                                            | Recommended                               |
| ---------------------------------------------------- | ----------------------------------------- |
| Every object requires different initial values       | ✅ Yes                                     |
| Mandatory fields must be initialized                 | ✅ Yes                                     |
| Creating immutable objects                           | ✅ Highly Recommended                      |
| Domain models such as Employee, Student, BankAccount | ✅ Yes                                     |
| Framework requires a no-argument constructor         | ⚠️ Provide both constructors if necessary |

---

## Resources

* Oracle Java Tutorials: Classes and Objects
* Oracle Knowledge Documentation
* Baeldung: Java Constructors
* GeeksforGeeks: Constructors in Java

---

*Made for CS Students | Internship & Job Prep Series*
