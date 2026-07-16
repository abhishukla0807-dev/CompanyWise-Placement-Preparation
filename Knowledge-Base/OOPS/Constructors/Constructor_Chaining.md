# Constructor Chaining

#### Reusing Constructors Within a Class and Across Inheritance Hierarchies

> Constructor chaining improves code reuse by allowing one constructor to invoke another instead of duplicating initialization logic.

---

## 📌 Table of Contents

| #  | Section                                                           |
| -- | ----------------------------------------------------------------- |
| 01 | [What is Constructor Chaining?](#what-is-constructor-chaining)    |
| 02 | [Why Do We Need It?](#why-do-we-need-it)                          |
| 03 | [Types of Constructor Chaining](#types-of-constructor-chaining)   |
| 04 | [How Constructor Chaining Works](#how-constructor-chaining-works) |
| 05 | [Using `this()`](#using-this)                                     |
| 06 | [Using `super()`](#using-super)                                   |
| 07 | [Code Example](#code-example)                                     |
| 08 | [this() vs super()](#this-vs-super)                               |
| 09 | [Rules of Constructor Chaining](#rules-of-constructor-chaining)   |
| 10 | [Advantages](#advantages)                                         |
| 11 | [Common Interview Questions](#common-interview-questions)         |
| 12 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)             |
| 13 | [Resources](#resources)                                           |

---

## What is Constructor Chaining?

* **Constructor chaining** is the process of invoking one constructor from another constructor. Instead of repeating initialization logic in multiple constructors, one constructor delegates the work to another, making the code cleaner and easier to maintain.

* Java supports constructor chaining through the `this()` and `super()` keywords. Depending on the requirement, chaining can occur within the same class or between a child class and its parent class.

### ✦ Key Points

* Reduces duplicate initialization code.
* Improves readability and maintainability.
* Ensures constructors execute in a predictable order.
* Frequently used in classes that support multiple ways of object creation.

---

## Why Do We Need It?

* Large classes often contain several constructors with similar initialization logic. Writing the same statements in every constructor increases maintenance effort and makes the code more error-prone.

* Constructor chaining centralizes common initialization in a single constructor. Other constructors simply delegate the work, making future modifications easier and ensuring consistent object initialization.

---

## Types of Constructor Chaining

| Type                             | Keyword   | Purpose                                             |
| -------------------------------- | --------- | --------------------------------------------------- |
| Within the same class            | `this()`  | Invokes another constructor of the current class    |
| Between parent and child classes | `super()` | Invokes a constructor of the immediate parent class |

---

## How Constructor Chaining Works

```text
Object Creation
       │
       ▼
Constructor Invoked
       │
       ▼
this() or super()
       │
       ▼
Required Constructor Executes
       │
       ▼
Remaining Constructor Body Executes
```

---

## Using `this()`

* The `this()` keyword calls another constructor of the same class.
* It is commonly used when multiple constructors share common initialization logic.
* Control transfers to the invoked constructor first, and then returns to the calling constructor after completion.
* This approach avoids repeating identical code across constructors.

### Example

```java
class Student {

    private int rollNo;
    private String name;

    Student() {
        this(101, "Rahul");
        System.out.println("Default Constructor");
    }

    Student(int rollNo, String name) {
        this.rollNo = rollNo;
        this.name = name;
        System.out.println("Parameterized Constructor");
    }

    public static void main(String[] args) {
        new Student();
    }
}
```

**Output**

```text
Parameterized Constructor
Default Constructor
```

---

## Using `super()`

* The `super()` keyword invokes the constructor of the immediate parent class.
* It ensures that the parent portion of an object is initialized before the child class performs its own initialization.
* If `super()` is not written explicitly, Java automatically inserts a call to the parent's no-argument constructor when available.
* It is commonly used in inheritance to initialize inherited state.

### Example

```java
class Animal {

    Animal() {
        System.out.println("Animal Constructor");
    }
}

class Dog extends Animal {

    Dog() {
        super();
        System.out.println("Dog Constructor");
    }

    public static void main(String[] args) {
        new Dog();
    }
}
```

**Output**

```text
Animal Constructor
Dog Constructor
```

---

## Code Example

```java
class Employee {

    private int id;
    private String name;
    private String department;

    Employee() {
        this(101, "Rahul", "Development");
    }

    Employee(int id, String name) {
        this(id, name, "General");
    }

    Employee(int id, String name, String department) {
        this.id = id;
        this.name = name;
        this.department = department;
    }

    void display() {
        System.out.println(id + " " + name + " " + department);
    }

    public static void main(String[] args) {

        Employee e1 = new Employee();
        Employee e2 = new Employee(102, "Priya");

        e1.display();
        e2.display();
    }
}
```

---

## `this()` vs `super()`

| Feature    | `this()`                     | `super()`                   |
| ---------- | ---------------------------- | --------------------------- |
| Calls      | Constructor of current class | Constructor of parent class |
| Used For   | Constructor overloading      | Inheritance                 |
| Target     | Same class                   | Immediate superclass        |
| Invocation | First statement              | First statement             |
| Purpose    | Reuse initialization logic   | Initialize parent object    |

---

## Rules of Constructor Chaining

* A constructor can invoke either `this()` or `super()`, but never both in the same constructor.
* Both `this()` and `super()` must appear as the **first statement** inside a constructor.
* Constructor chaining eventually ends with a constructor that does not invoke another constructor.
* Recursive constructor calls are not allowed because they lead to compilation errors.
* If no constructor is explicitly invoked, Java inserts a call to `super()` automatically.

---

## Advantages

* Eliminates duplicate initialization code.
* Makes constructors easier to understand and maintain.
* Promotes consistent object initialization.
* Simplifies constructor overloading.
* Supports proper initialization in inheritance hierarchies.

---

## Common Interview Questions

**Q: What is constructor chaining?**

* Constructor chaining is the process of calling one constructor from another constructor using `this()` or `super()`.

---

**Q: What is the difference between `this()` and `super()`?**

* `this()` calls another constructor in the same class, whereas `super()` calls a constructor of the parent class.

---

**Q: Can `this()` and `super()` be used together in the same constructor?**

* No.
* Both must be the first statement, so only one can be used.

---

**Q: Why must `this()` and `super()` be the first statement?**

* Java ensures object initialization happens in a well-defined order before executing any other statements.

---

**Q: Does Java automatically insert `super()`?**

* Yes.
* If no constructor call is written explicitly, Java inserts `super()` to invoke the parent's no-argument constructor.

---

## Common Mistakes to Avoid

| Mistake                                              | Fix                                             |
| ---------------------------------------------------- | ----------------------------------------------- |
| Using both `this()` and `super()` in one constructor | Use only one constructor call                   |
| Placing statements before `this()` or `super()`      | Constructor calls must always be first          |
| Creating recursive constructor calls                 | Ensure constructor chains terminate correctly   |
| Repeating initialization code in every constructor   | Delegate common logic using `this()`            |
| Forgetting that `super()` is inserted automatically  | Be aware of the parent's available constructors |

---

## Resources

### Official Documentation

* Oracle Java Tutorials: Using the `this` Keyword
  https://docs.oracle.com/javase/tutorial/java/javaOO/thiskey.html

* Oracle Java Tutorials: Inheritance
  https://docs.oracle.com/javase/tutorial/java/IandI/

### In-Depth Articles

* Baeldung: Constructors in Java
  https://www.baeldung.com/java-constructors

* GeeksforGeeks: Constructor Chaining in Java
  https://www.geeksforgeeks.org/constructor-chaining-java-examples/

* GeeksforGeeks: `this` Keyword in Java
  https://www.geeksforgeeks.org/this-reference-in-java/

---

*Made for CS Students | Internship & Job Prep Series*
