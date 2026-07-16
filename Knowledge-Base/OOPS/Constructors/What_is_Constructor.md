# What is a Constructor
#### Object Initialization in Java | Types, Rules, Chaining | Asked in Every Technical Round

> A constructor is a special method that runs automatically when an object is created. Its only job is to initialize the object's state.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [What is a Constructor](#what-is-a-constructor) |
| 02 | [Rules of a Constructor](#rules-of-a-constructor) |
| 03 | [Types of Constructors](#types-of-constructors) |
| 04 | [Constructor vs Method](#constructor-vs-method) |
| 05 | [Constructor Overloading](#constructor-overloading) |
| 06 | [Constructor Chaining](#constructor-chaining) |
| 07 | [Constructor in Inheritance](#constructor-in-inheritance) |
| 08 | [Code Example](#code-example) |
| 09 | [Common Interview Questions](#common-interview-questions) |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 11 | [When to Use What](#when-to-use-what) |
| 12 | [Resources](#resources) |

---

## What is a Constructor

- A special block of code that initializes an object when it is created
- Automatically called by the JVM when `new` keyword is used
- Has the same name as the class
- Has no return type, not even `void`
- Can have access modifiers: `public`, `private`, `protected`, or default
- Cannot be `static`, `final`, `abstract`, or `synchronized`
- Every class has at least one constructor, provided by the compiler if none is written
- Does not create the object, the `new` keyword does. The constructor only initializes it

---

## Rules of a Constructor

- Name must exactly match the class name (case-sensitive)
- No return type of any kind, not even `void`
- Cannot be declared `static` (constructors are always tied to an object)
- Cannot be declared `final` (constructors are never inherited, so `final` has no meaning)
- Cannot be declared `abstract` (constructors must have a body)
- `this()` or `super()` must be the first statement if used inside a constructor
- Both `this()` and `super()` cannot appear in the same constructor
- Default values assigned by JVM before constructor runs: `int = 0`, `boolean = false`, `String = null`

---

## Types of Constructors

### ✦ Default Constructor
- Provided automatically by the compiler if no constructor is defined
- Takes no parameters
- Initializes all instance variables to their default values
- Once a constructor is explicitly defined, the compiler no longer provides this

```java
class Student {
    String name;
    int marks;
    // Compiler provides: Student() {}
}

Student s = new Student();
// name = null, marks = 0 (default values)
```

---

### ✦ No-Argument Constructor
- Defined explicitly by the programmer with no parameters
- Unlike the default constructor, this one can have initialization logic
- Useful when you want to set specific initial values without passing arguments

```java
class Student {
    String name;
    int marks;

    Student() {
        name = "Unknown";
        marks = 0;
        System.out.println("Student object created");
    }
}
```

---

### ✦ Parameterized Constructor
- Accepts one or more parameters
- Used to initialize fields with specific values passed at object creation
- Gives control over the initial state of every object

```java
class Student {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }
}

Student s = new Student("Aman", 90);
```

---

### ✦ Copy Constructor
- Accepts an object of the same class as a parameter
- Creates a new object with the same data as the passed object
- Java does not provide a copy constructor by default, must be written manually
- Produces an independent object, changes to the copy do not affect the original

```java
class Student {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    // Copy Constructor
    Student(Student s) {
        this.name = s.name;
        this.marks = s.marks;
    }
}

Student s1 = new Student("Aman", 90);
Student s2 = new Student(s1);   // independent copy of s1
```

---

### ✦ Private Constructor
- Constructor declared with `private` access modifier
- Prevents any external class from creating an object directly
- Used in Singleton pattern to ensure only one instance exists
- Used in utility classes where no object creation is needed

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}   // no external instantiation

    public static Singleton getInstance() {
        if (instance == null) instance = new Singleton();
        return instance;
    }
}
```

---

## Constructor vs Method

| Factor | Constructor | Method |
|--------|-------------|--------|
| Name | Same as class name | Any valid identifier |
| Return type | None (not even `void`) | Must have a return type |
| Called by | JVM automatically on `new` | Explicitly by programmer |
| Purpose | Initialize object state | Define object behavior |
| Inheritance | Not inherited | Inherited |
| Overriding | Cannot be overridden | Can be overridden |
| `static` allowed | No | Yes |
| `final` allowed | No | Yes |

---

## Constructor Overloading

- Defining multiple constructors in the same class with different parameter lists
- Each constructor handles a different way of creating the object
- The compiler decides which constructor to call based on the arguments passed
- Improves flexibility, objects can be created in multiple ways

```java
class Student {
    String name;
    int marks;

    Student() {
        this("Unknown", 0);   // calls parameterized constructor
    }

    Student(String name) {
        this(name, 0);
    }

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }
}
```

---

## Constructor Chaining

- One constructor calls another constructor in the same or parent class
- Within the same class: use `this()`
- To call parent class constructor: use `super()`
- Must always be the first statement in the constructor
- Avoids duplicate initialization logic across constructors

```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class Student extends Person {
    int rollNo;

    Student(String name, int age, int rollNo) {
        super(name, age);       // calls Person constructor first
        this.rollNo = rollNo;
    }
}
```

---

## Constructor in Inheritance

- When a child class object is created, the parent class constructor runs first
- If `super()` is not explicitly written, Java automatically inserts `super()` as the first call
- If the parent class has no default constructor, the child must explicitly call `super(args)`
- Constructors are NOT inherited, child class must define its own
- Order of execution: parent constructor runs fully before child constructor body starts

```java
class Animal {
    Animal() {
        System.out.println("Animal constructor");
    }
}

class Dog extends Animal {
    Dog() {
        super();   // automatically inserted by Java if not written
        System.out.println("Dog constructor");
    }
}

new Dog();
// Output:
// Animal constructor
// Dog constructor
```

---

## Code Example

### Java
```java
class BankAccount {
    private String owner;
    private double balance;
    private static int totalAccounts = 0;

    // No-arg constructor
    BankAccount() {
        this("Unknown", 0.0);
    }

    // Parameterized constructor
    BankAccount(String owner, double balance) {
        this.owner = owner;
        this.balance = balance;
        totalAccounts++;
    }

    // Copy constructor
    BankAccount(BankAccount acc) {
        this.owner = acc.owner;
        this.balance = acc.balance;
        totalAccounts++;
    }

    void display() {
        System.out.println(owner + " | Balance: " + balance);
    }

    static int getTotalAccounts() {
        return totalAccounts;
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount a1 = new BankAccount("Aman", 5000);
        BankAccount a2 = new BankAccount();
        BankAccount a3 = new BankAccount(a1);   // copy of a1

        a1.display();   // Aman | Balance: 5000.0
        a2.display();   // Unknown | Balance: 0.0
        a3.display();   // Aman | Balance: 5000.0

        System.out.println("Total: " + BankAccount.getTotalAccounts());   // 3
    }
}
```

---

## Common Interview Questions

**Q: What is a constructor in Java?**
- The most direct question, appears in every fresher round
- A constructor is a special block with the same name as the class, no return type, called automatically by JVM when an object is created, used to initialize instance variables
- Always follow with: "It does not create the object, `new` does. The constructor only sets the initial state"

**Q: What is the difference between a default constructor and a no-argument constructor?**
- The most commonly confused pair in constructor questions
- Default constructor is provided by the compiler when no constructor is written. No-argument constructor is written explicitly by the programmer and can contain initialization logic
- Once any constructor is explicitly defined, the compiler stops providing the default constructor

**Q: Can a constructor have a return type?**
- Simple trap question, asked to test attention to detail
- No. Constructors have no return type at all, not even `void`
- If you add a return type, Java treats it as a regular method with the same name as the class, not a constructor

**Q: What happens if a parent class has only a parameterized constructor and the child class does not call `super()`?**
- Tests deep understanding of constructor chaining in inheritance
- Compile-time error. Java automatically inserts `super()` but if no default constructor exists in the parent, this call fails
- Solution: explicitly call `super(args)` as the first statement in the child constructor

**Q: Can constructors be inherited?**
- Very commonly asked, many students get this wrong
- No. Constructors are not inherited. Each class must define its own constructors
- A child class can call a parent constructor using `super()` but it does not inherit it

**Q: What is a private constructor used for?**
- Tests practical design knowledge, often asked in product-based rounds
- Prevents external classes from creating objects of the class directly
- Used in Singleton pattern to ensure only one instance exists, and in utility classes with only static methods where no object creation is needed

---

## Common Mistakes to Avoid

- Writing `void` as the return type of a constructor, this turns it into a regular method
- Thinking the compiler always provides a default constructor, it stops doing so the moment any constructor is explicitly written
- Placing `this()` or `super()` anywhere other than the first line of a constructor
- Using both `this()` and `super()` in the same constructor, only one is allowed and it must be first
- Saying constructors are inherited, they are not
- Confusing copy constructor with object cloning, copy constructor creates a new independent object, cloning via `clone()` has different behavior and needs `Cloneable` interface

---

## When to Use What

| Situation | Constructor to Use |
|-----------|-------------------|
| Object needs no specific initial values | Default or no-arg constructor |
| Object needs specific values at creation | Parameterized constructor |
| Need an independent copy of an existing object | Copy constructor |
| Only one instance of a class should exist | Private constructor with static factory method |
| Multiple ways to create an object | Constructor overloading |
| Child class needs parent fields initialized | `super()` call in child constructor |
| Avoid duplicate initialization across constructors | Constructor chaining with `this()` |

---

## Resources

- [GeeksforGeeks - Constructors in Java](https://www.geeksforgeeks.org/java/constructors-in-java/)
- [GeeksforGeeks - Copy Constructor in Java](https://www.geeksforgeeks.org/java/copy-constructor-in-java/)
- [GeeksforGeeks - Constructor Interview Questions](https://www.geeksforgeeks.org/java-interview-questions-constructors/)
- [InterviewBit - Java Interview Questions](https://www.interviewbit.com/java-interview-questions/)
- [PrepInsta - OOPs Interview Questions](https://prepinsta.com/interview-preparation/technical-interview-questions/oops/)

---

*Made for CS Students | Internship & Job Prep Series*