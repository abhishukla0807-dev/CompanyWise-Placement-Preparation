# Getters and Setters

#### Controlled Access to Object Data Through Public Methods

> Getters and setters provide a controlled way to read and modify private fields while preserving the integrity of an object's state.

---

## 📌 Table of Contents

| #  | Section                                                        |
| -- | -------------------------------------------------------------- |
| 01 | [What are Getters and Setters?](#what-are-getters-and-setters) |
| 02 | [Why Do We Need Them?](#why-do-we-need-them)                   |
| 03 | [How They Work](#how-they-work)                                |
| 04 | [Naming Convention](#naming-convention)                        |
| 05 | [Code Example](#code-example)                                  |
| 06 | [Benefits](#benefits)                                          |
| 07 | [Getter vs Setter](#getter-vs-setter)                          |
| 08 | [Best Practices](#best-practices)                              |
| 09 | [Common Interview Questions](#common-interview-questions)      |
| 10 | [Common Mistakes to Avoid](#common-mistakes-to-avoid)          |
| 11 | [Resources](#resources)                                        |

---

## What are Getters and Setters?

* **Getters** are public methods used to retrieve the value of private instance variables without exposing the variables directly.
* **Setters** are public methods used to update private instance variables while allowing validation before the value is stored.
* Together, getters and setters implement controlled access to object data, which is one of the primary goals of encapsulation.
* They act as an interface between an object's internal state and the outside world, allowing the implementation to change without affecting client code.

### ✦ Key Points

* Getter methods **read** object data.
* Setter methods **modify** object data.
* They usually operate on private fields.
* Validation logic is commonly implemented inside setters.
* They improve maintainability and flexibility.

---

## Why Do We Need Them?

* Private variables cannot be accessed directly from outside the class, making getter and setter methods necessary for controlled interaction.
* Setter methods ensure that only valid values are assigned, preventing objects from entering an invalid state.
* Getter methods allow the internal representation of data to remain hidden while providing access to the required information.
* If the internal implementation changes in the future, external code continues to work because it communicates through methods instead of fields.

---

## How They Work

```text
Private Field
      │
      ▼
 Getter Method
(Read Operation)

Setter Method
(Validation + Update)
      │
      ▼
Protected Object State
```

---

## Naming Convention

Java follows a standard naming convention for accessor methods.

| Method         | Convention          | Example      |
| -------------- | ------------------- | ------------ |
| Getter         | `getVariableName()` | `getName()`  |
| Boolean Getter | `isVariableName()`  | `isActive()` |
| Setter         | `setVariableName()` | `setName()`  |

Following these conventions improves readability and allows frameworks like Spring Boot, Hibernate, and JavaBeans to recognize properties automatically.

---

## Code Example

```java
class Student {

    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {

        if (name != null && !name.isBlank()) {
            this.name = name;
        }
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {

        if (age >= 18) {
            this.age = age;
        }
    }

    public static void main(String[] args) {

        Student student = new Student();

        student.setName("Rahul");
        student.setAge(20);

        System.out.println(student.getName());
        System.out.println(student.getAge());
    }
}
```

**Output**

```text
Rahul
20
```

### ✦ Explanation

* Both fields are declared `private`, preventing direct access.
* Getter methods return the current values.
* Setter methods validate the input before updating the fields.
* Invalid values are rejected, keeping the object in a consistent state.

---

## Benefits

* Protects object data from direct modification.
* Allows validation before updating fields.
* Improves maintainability by hiding implementation details.
* Supports backward compatibility when internal data structures change.
* Makes classes compatible with JavaBeans and enterprise frameworks.

---

## Getter vs Setter

| Getter                       | Setter                       |
| ---------------------------- | ---------------------------- |
| Returns the value of a field | Updates the value of a field |
| Usually has a return type    | Usually returns `void`       |
| Does not modify object state | Can modify object state      |
| Performs read operations     | Performs write operations    |
| Can include computed values  | Can include validation logic |

---

## Best Practices

* Declare instance variables as `private` and expose them only when necessary.
* Add validation inside setter methods instead of trusting external input.
* Do not generate setters for fields that should remain immutable.
* Keep getter methods lightweight and avoid expensive computations.
* Expose only the properties that are required by other classes.

---

## Common Interview Questions

**Q: Why do we use getters and setters instead of public variables?**

* They provide controlled access, support validation, and preserve encapsulation.

---

**Q: Can a class have only getters?**

* Yes.
* Read-only classes and immutable objects often expose only getter methods.

---

**Q: Is it necessary to create getters and setters for every field?**

* No.
* Only expose the fields that need to be accessed or modified from outside the class.

---

**Q: Why is validation usually performed inside setter methods?**

* It prevents invalid data from being stored inside the object.

---

**Q: Can getter methods return computed values instead of fields?**

* Yes.
* A getter may calculate and return a value without exposing internal implementation details.

---

## Common Mistakes to Avoid

| Mistake                                                         | Better Approach                       |
| --------------------------------------------------------------- | ------------------------------------- |
| Making every field `public`                                     | Keep fields `private`                 |
| Creating setters without validation                             | Validate input before assignment      |
| Generating getters and setters for every variable automatically | Expose only necessary properties      |
| Performing heavy business logic inside getters                  | Keep getters simple and predictable   |
| Returning mutable internal objects directly                     | Return defensive copies when required |

---

## Resources

### Official Documentation

* Oracle Java Tutorials: Controlling Access to Members
  https://docs.oracle.com/javase/tutorial/java/javaOO/accesscontrol.html

* Oracle JavaBeans Specification
  https://www.oracle.com/java/technologies/javase/javabeans-spec.html

### Recommended Reading

* Baeldung: Java Getter and Setter Guide
  https://www.baeldung.com/java-encapsulation

* GeeksforGeeks: Getter and Setter in Java
  https://www.geeksforgeeks.org/getter-and-setter-in-java/

---

*Made for CS Students | Internship & Job Prep Series*
