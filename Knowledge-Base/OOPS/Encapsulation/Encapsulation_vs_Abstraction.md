# Encapsulation vs Abstraction

#### Understanding the Difference Between Data Protection and Complexity Hiding

> Encapsulation protects an object's internal state, while abstraction hides implementation complexity. They work together, but they solve different problems.

---

## 📌 Table of Contents

| #  | Section                                                       |
| -- | ------------------------------------------------------------- |
| 01 | [Overview](#overview)                                         |
| 02 | [Encapsulation vs Abstraction](#encapsulation-vs-abstraction) |
| 03 | [Key Differences Explained](#key-differences-explained)       |
| 04 | [Code Example](#code-example)                                 |
| 05 | [Real-World Examples](#real-world-examples)                   |
| 06 | [When to Use Which](#when-to-use-which)                       |
| 07 | [Common Interview Questions](#common-interview-questions)     |
| 08 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)         |
| 09 | [Resources](#resources)                                       |

---

## Overview

* **Encapsulation** and **abstraction** are two core principles of Object-Oriented Programming that are often confused because both involve hiding something.
* Encapsulation focuses on **protecting data** by restricting direct access, whereas abstraction focuses on **reducing complexity** by exposing only essential functionality.
* In well-designed applications, encapsulation and abstraction complement each other to create secure, maintainable, and reusable software.

---

## Encapsulation vs Abstraction

| Feature           | Encapsulation                                  | Abstraction                      |
| ----------------- | ---------------------------------------------- | -------------------------------- |
| Primary Goal      | Protect object data                            | Hide implementation complexity   |
| Focus             | Data security                                  | Simplicity                       |
| Hides             | Internal data                                  | Internal implementation          |
| Achieved Using    | Classes, access modifiers, getters and setters | Abstract classes and interfaces  |
| User Knows        | How to access data                             | What operations are available    |
| User Doesn't Know | Internal data representation                   | How the operation is implemented |

---

## Key Differences Explained

### ✦ Purpose

* Encapsulation protects an object's internal state by preventing uncontrolled access to its data.
* Abstraction reduces complexity by exposing only the operations that users need while hiding implementation details.

---

### ✦ What Gets Hidden

* Encapsulation hides **data** from direct access using access modifiers such as `private`.
* Abstraction hides **implementation details**, allowing users to focus on functionality instead of internal logic.

---

### ✦ Implementation

* Encapsulation is implemented using classes, private fields, and controlled access methods.
* Abstraction is implemented using abstract classes, interfaces, and method declarations without exposing implementation.

---

### ✦ Design Perspective

* Encapsulation answers **"How can we protect the data?"**
* Abstraction answers **"What functionality should be exposed?"**

---

## Code Example

```java
// Encapsulation
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
}

// Abstraction
abstract class Payment {

    abstract void pay(double amount);
}

class UpiPayment extends Payment {

    @Override
    void pay(double amount) {
        System.out.println("Paid ₹" + amount + " using UPI");
    }
}
```

### ✦ Explanation

* `BankAccount` demonstrates **encapsulation** by hiding the `balance` field and allowing controlled access through methods.
* `Payment` demonstrates **abstraction** by defining what payment operation should exist without specifying how it is implemented.
* `UpiPayment` provides the actual implementation of the abstract method.

---

## Real-World Examples

| Scenario     | Encapsulation                                        | Abstraction                                                   |
| ------------ | ---------------------------------------------------- | ------------------------------------------------------------- |
| ATM          | Balance is protected inside the banking system       | User only sees Withdraw, Deposit, Balance options             |
| Car          | Engine data is protected from direct modification    | Driver only uses steering, brake, and accelerator             |
| Mobile Phone | Internal files are protected by the operating system | User interacts through apps and icons                         |
| Banking App  | Account details are stored securely                  | User performs transactions without knowing backend processing |

---

## When to Use Which

| Situation                                     | Use           |
| --------------------------------------------- | ------------- |
| Protecting object data                        | Encapsulation |
| Validating user input                         | Encapsulation |
| Hiding implementation details                 | Abstraction   |
| Designing APIs or frameworks                  | Abstraction   |
| Creating secure domain models                 | Encapsulation |
| Defining common behavior for multiple classes | Abstraction   |

---

## Common Interview Questions

**Q: What is the main difference between encapsulation and abstraction?**

* Encapsulation hides data and controls access to it.
* Abstraction hides implementation details and exposes only essential functionality.

---

**Q: Can encapsulation exist without abstraction?**

* Yes.
* A class can protect its data using private fields without using abstract classes or interfaces.

---

**Q: Can abstraction exist without encapsulation?**

* Yes.
* Abstract classes and interfaces define behavior, although most practical implementations also use encapsulation.

---

**Q: Which is achieved using private variables?**

* Encapsulation.

---

**Q: Which is achieved using abstract classes and interfaces?**

* Abstraction.

---

## Common Mistakes to Avoid

| Mistake                                                        | Better Approach                                    |
| -------------------------------------------------------------- | -------------------------------------------------- |
| Saying encapsulation and abstraction are the same              | Learn the purpose of each concept                  |
| Thinking getters and setters alone implement abstraction       | They primarily support encapsulation               |
| Assuming abstraction automatically protects data               | Use encapsulation to secure object state           |
| Using abstract classes when simple encapsulation is sufficient | Choose the concept based on the design requirement |

---

## Resources

### Official Documentation

* Oracle Java Tutorials: Classes and Objects
  https://docs.oracle.com/javase/tutorial/java/javaOO/

* Oracle Java Tutorials: Interfaces and Inheritance
  https://docs.oracle.com/javase/tutorial/java/IandI/

### Recommended Reading

* Baeldung: Encapsulation in Java
  https://www.baeldung.com/java-encapsulation

* Baeldung: Abstract Classes vs Interfaces
  https://www.baeldung.com/java-interface-vs-abstract-class

* GeeksforGeeks: Difference Between Abstraction and Encapsulation
  https://www.geeksforgeeks.org/difference-between-abstraction-and-encapsulation-in-java/

---

*Made for CS Students | Internship & Job Prep Series*
