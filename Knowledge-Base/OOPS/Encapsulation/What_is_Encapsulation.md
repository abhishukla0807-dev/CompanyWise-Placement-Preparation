# What is Encapsulation?

#### Protecting Data and Controlling Access | One of the Four Pillars of Object-Oriented Programming

> Encapsulation combines data and the methods that operate on it into a single unit while controlling how that data is accessed and modified.

---

## 📌 Table of Contents

| #  | Section                                                                                   |
| -- | ----------------------------------------------------------------------------------------- |
| 01 | [What is Encapsulation?](#what-is-encapsulation)                                          |
| 02 | [Why Do We Need Encapsulation?](#why-do-we-need-encapsulation)                            |
| 03 | [How Encapsulation Works](#how-encapsulation-works)                                       |
| 04 | [Characteristics](#characteristics)                                                       |
| 05 | [Key Components](#key-components)                                                         |
| 06 | [Code Example](#code-example)                                                             |
| 07 | [How Encapsulation Improves Software Design](#how-encapsulation-improves-software-design) |
| 08 | [Advantages](#advantages)                                                                 |
| 09 | [Common Interview Questions](#common-interview-questions)                                 |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)                                     |
| 11 | [When to Use Encapsulation](#when-to-use-encapsulation)                                   |
| 12 | [Resources](#resources)                                                                   |

---

## What is Encapsulation?

* **Encapsulation** is the process of wrapping data (variables) and the methods that operate on that data into a single unit called a **class**.
* It restricts direct access to an object's internal state and allows interaction only through well-defined methods.
* The primary goal of encapsulation is to protect object data from unauthorized or unintended modification.
* In Java, encapsulation is commonly achieved using **private instance variables** and **public getter and setter methods**.

### ✦ Key Points

* Combines data and behavior inside a class.
* Protects object state from direct access.
* Provides controlled access through methods.
* Improves maintainability and security.
* Forms the foundation of reliable object-oriented design.

---

## Why Do We Need Encapsulation?

* Directly exposing instance variables makes it difficult to control how data is modified, increasing the chances of invalid object states.
* Encapsulation allows validation before updating object data, ensuring that only meaningful and acceptable values are stored.
* It separates implementation details from the public interface, allowing internal changes without affecting the code that uses the class.
* Most modern Java frameworks rely on encapsulation because it promotes modular, reusable, and maintainable software.

---

## How Encapsulation Works

```text
Instance Variables
      │
      ▼
private Access Modifier
      │
      ▼
Getter / Setter Methods
      │
      ▼
Controlled Access
      │
      ▼
Protected Object State
```

---

## Characteristics

| Feature           | Description                                                |
| ----------------- | ---------------------------------------------------------- |
| Data Hiding       | Restricts direct access to object data                     |
| Controlled Access | Allows interaction through methods                         |
| Access Modifiers  | Uses `private`, `protected`, or `public` appropriately     |
| Maintainability   | Internal implementation can change without affecting users |
| Reusability       | Well-designed classes are easier to reuse                  |

---

## Key Components

### ✦ Private Fields

* Instance variables are usually declared `private` so they cannot be accessed directly from outside the class.
* This prevents accidental modification and keeps the object's internal state protected.

### ✦ Getter Methods

* Getter methods provide controlled read access to private variables.
* They can include additional logic before returning data if required.

### ✦ Setter Methods

* Setter methods update private variables through a controlled interface.
* Validation logic can be added to reject invalid values before updating the object.

---

## Code Example

```java
class BankAccount {

    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
}

public class Main {

    public static void main(String[] args) {

        BankAccount account = new BankAccount(5000);

        account.deposit(1000);
        account.withdraw(1500);

        System.out.println(account.getBalance());
    }
}
```

**Output**

```text
4500.0
```

### ✦ Explanation

* The `balance` variable is private and cannot be modified directly.
* All updates occur through `deposit()` and `withdraw()`.
* Validation ensures that invalid transactions are ignored.
* The object remains in a consistent and valid state.

---

## How Encapsulation Improves Software Design

* Reduces coupling by hiding implementation details from other classes.
* Makes debugging easier because object state changes through controlled methods.
* Prevents accidental data corruption by validating updates.
* Allows internal implementation to evolve without breaking existing code.
* Supports modular architecture and clean object-oriented design.

---

## Advantages

* Protects sensitive data from unauthorized access.
* Improves code maintainability by separating implementation from interface.
* Makes validation easier before updating object data.
* Reduces dependencies between different parts of an application.
* Encourages reusable and well-structured classes.

---

## Common Interview Questions

**Q: What is encapsulation?**

* Encapsulation is the process of combining data and methods into a single class while restricting direct access to the object's internal state.

---

**Q: How is encapsulation achieved in Java?**

* By declaring fields as `private` and providing controlled access through public getter and setter methods.

---

**Q: Is encapsulation the same as data hiding?**

* No.
* Data hiding is one part of encapsulation.
* Encapsulation includes both bundling data with methods and controlling access to that data.

---

**Q: Which access modifier is most commonly used for encapsulation?**

* `private`
* It prevents direct access to instance variables from outside the class.

---

**Q: Can a class be encapsulated without setters?**

* Yes.
* Immutable classes expose only getter methods while keeping their internal state unchanged after object creation.

---

## Common Mistakes to Avoid

| Mistake                                                      | Better Approach                                     |
| ------------------------------------------------------------ | --------------------------------------------------- |
| Declaring all fields as `public`                             | Keep instance variables `private`                   |
| Creating setters without validation                          | Validate data before updating fields                |
| Treating encapsulation and abstraction as identical concepts | Understand that they solve different problems       |
| Exposing mutable objects directly                            | Return defensive copies when necessary              |
| Making every field accessible                                | Expose only what is required by the class interface |

---

## When to Use Encapsulation

| Situation                        | Recommended |
| -------------------------------- | ----------- |
| Protecting object data           | ✅ Yes       |
| Validating user input            | ✅ Yes       |
| Designing reusable classes       | ✅ Yes       |
| Building enterprise applications | ✅ Yes       |
| Creating immutable objects       | ✅ Yes       |
| Hiding implementation details    | ✅ Yes       |

---

## Resources

### Official Documentation

* Oracle Java Tutorials: Classes and Objects
  https://docs.oracle.com/javase/tutorial/java/javaOO/

### Recommended Reading

* Baeldung: Encapsulation in Java
  https://www.baeldung.com/java-encapsulation

* GeeksforGeeks: Encapsulation in Java
  https://www.geeksforgeeks.org/encapsulation-in-java/

* Oracle Java Language Specification
  https://docs.oracle.com/javase/specs/

---

*Made for CS Students | Internship & Job Prep Series*
