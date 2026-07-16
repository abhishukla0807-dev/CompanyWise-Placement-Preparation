# Data Hiding

#### Protecting Internal Object State Through Controlled Access

> Data hiding protects an object's internal state by restricting direct access and exposing only what is necessary through a controlled interface.

---

## 📌 Table of Contents

| #  | Section                                                                   |
| -- | ------------------------------------------------------------------------- |
| 01 | [What is Data Hiding?](#what-is-data-hiding)                              |
| 02 | [Why Do We Need Data Hiding?](#why-do-we-need-data-hiding)                |
| 03 | [How Data Hiding Works](#how-data-hiding-works)                           |
| 04 | [Characteristics](#characteristics)                                       |
| 05 | [Data Hiding Using Access Modifiers](#data-hiding-using-access-modifiers) |
| 06 | [Code Example](#code-example)                                             |
| 07 | [Data Hiding vs Encapsulation](#data-hiding-vs-encapsulation)             |
| 08 | [Advantages](#advantages)                                                 |
| 09 | [Common Interview Questions](#common-interview-questions)                 |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)                     |
| 11 | [When to Use Data Hiding](#when-to-use-data-hiding)                       |
| 12 | [Resources](#resources)                                                   |

---

## What is Data Hiding?

* **Data hiding** is the practice of restricting direct access to an object's internal data and allowing interaction only through carefully designed methods.
* It protects important information from accidental modification and helps maintain a valid object state throughout its lifecycle.
* In Java, data hiding is primarily achieved using the **private** access modifier, which prevents external classes from accessing instance variables directly.
* Data hiding is one of the key techniques used to implement encapsulation, but the two concepts are not identical.

### ✦ Key Points

* Protects internal object data.
* Prevents unauthorized modification.
* Uses access modifiers to control visibility.
* Encourages interaction through methods.
* Improves software reliability.

---

## Why Do We Need Data Hiding?

* Direct access to instance variables allows any part of the program to modify an object's state, making it difficult to maintain data integrity.
* Restricting access ensures that updates occur only after validation, preventing invalid or inconsistent values.
* Internal implementation remains independent of external code, allowing developers to modify the class without affecting its users.
* Data hiding improves security, maintainability, and long-term scalability of object-oriented applications.

---

## How Data Hiding Works

```text
Object Data
      │
      ▼
private Variables
      │
      ▼
Public Methods
      │
      ▼
Validation
      │
      ▼
Safe Object State
```

---

## Characteristics

| Feature          | Description                    |
| ---------------- | ------------------------------ |
| Direct Access    | Restricted                     |
| Data Protection  | High                           |
| Validation       | Performed through methods      |
| Access Control   | Managed using access modifiers |
| Object Integrity | Preserved                      |

---

## Data Hiding Using Access Modifiers

| Access Modifier | Same Class | Same Package | Subclass | Other Package |
| --------------- | :--------: | :----------: | :------: | :-----------: |
| `private`       |      ✅     |       ❌      |     ❌    |       ❌       |
| Default         |      ✅     |       ✅      |     ❌    |       ❌       |
| `protected`     |      ✅     |       ✅      |     ✅    |       ❌       |
| `public`        |      ✅     |       ✅      |     ✅    |       ✅       |

### ✦ Why `private` is Preferred

* `private` provides the highest level of protection for instance variables.
* External classes cannot modify the data without using the class's public methods.
* The class remains responsible for maintaining its own consistency.

---

## Code Example

```java
class Employee {

    private double salary;

    public Employee(double salary) {
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {

        if (salary > 0) {
            this.salary = salary;
        }
    }
}

public class Main {

    public static void main(String[] args) {

        Employee employee = new Employee(50000);

        employee.setSalary(60000);

        System.out.println(employee.getSalary());
    }
}
```

**Output**

```text
60000.0
```

### ✦ Explanation

* The `salary` field is declared as `private`, preventing direct access.
* The setter validates input before updating the value.
* The getter provides controlled read access.
* Invalid updates can be rejected without exposing internal implementation.

---

## Data Hiding vs Encapsulation

| Data Hiding                     | Encapsulation                               |
| ------------------------------- | ------------------------------------------- |
| Restricts access to data        | Bundles data and methods into a single unit |
| Achieved using access modifiers | Achieved using classes and access control   |
| Focuses on protecting data      | Focuses on organizing and protecting data   |
| Security-oriented concept       | Object-oriented design principle            |
| Part of encapsulation           | Uses data hiding as one of its techniques   |

---

## Advantages

* Prevents accidental modification of object data.
* Protects sensitive information from external classes.
* Makes validation easier before changing object state.
* Reduces dependencies between different modules.
* Simplifies maintenance by hiding implementation details.

---

## Common Interview Questions

**Q: What is data hiding?**

* Data hiding is the process of restricting direct access to an object's internal data and providing controlled access through methods.

---

**Q: Which access modifier is mainly used for data hiding?**

* `private`
* It completely hides instance variables from external classes.

---

**Q: Is data hiding the same as encapsulation?**

* No.
* Data hiding is a technique, whereas encapsulation is a broader object-oriented principle.

---

**Q: Why is data hiding important?**

* It protects object integrity, prevents invalid updates, and improves maintainability.

---

**Q: Can data hiding be achieved without getters and setters?**

* Yes.
* A class may expose only the operations required while keeping its internal data completely hidden.

---

## Common Mistakes to Avoid

| Mistake                                              | Better Approach                              |
| ---------------------------------------------------- | -------------------------------------------- |
| Declaring important fields as `public`               | Keep instance variables `private`            |
| Updating fields directly from outside the class      | Use controlled methods                       |
| Returning mutable internal objects directly          | Return defensive copies when required        |
| Skipping validation inside setters                   | Validate all user input                      |
| Assuming data hiding and encapsulation are identical | Understand their individual responsibilities |

---

## When to Use Data Hiding

| Situation                        | Recommended |
| -------------------------------- | ----------- |
| Protecting sensitive information | ✅ Yes       |
| Validating user input            | ✅ Yes       |
| Designing reusable classes       | ✅ Yes       |
| Building enterprise applications | ✅ Yes       |
| Maintaining object integrity     | ✅ Yes       |
| Exposing internal implementation | ❌ Avoid     |

---

## Resources

### Official Documentation

* Oracle Java Tutorials: Controlling Access to Members
  https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html

### Recommended Reading

* Baeldung: Encapsulation in Java
  https://www.baeldung.com/java-encapsulation

* GeeksforGeeks: Data Hiding in Java
  https://www.geeksforgeeks.org/data-hiding-in-java/

* Oracle Java Language Specification
  https://docs.oracle.com/javase/specs/

---

*Made for CS Students | Internship & Job Prep Series*
