# Access Modifiers
#### Control Visibility | Enforce Encapsulation | Asked in Every Java Technical Round

> Access modifiers decide who can see and use your class, method, or variable. They are the enforcement mechanism behind encapsulation.

---

## 📌 Table of Contents

| # | Section |
|---|---------|
| 01 | [What are Access Modifiers](#what-are-access-modifiers) |
| 02 | [The Four Modifiers](#the-four-modifiers) |
| 03 | [Access Level Comparison Table](#access-level-comparison-table) |
| 04 | [Each Modifier in Detail](#each-modifier-in-detail) |
| 05 | [Rules and Restrictions](#rules-and-restrictions) |
| 06 | [Access Modifiers and Inheritance](#access-modifiers-and-inheritance) |
| 07 | [Code Example](#code-example) |
| 08 | [Common Interview Questions](#common-interview-questions) |
| 09 | [Common Mistakes to Avoid](#common-mistakes-to-avoid) |
| 10 | [When to Use What](#when-to-use-what) |
| 11 | [Resources](#resources) |

---

## What are Access Modifiers

- Keywords that control the visibility and accessibility of classes, methods, and variables
- Tell the JVM who is allowed to access a particular member
- The primary tool for implementing encapsulation in Java
- Applied to classes, constructors, methods, and fields
- Cannot be applied to local variables inside methods
- There are 4 access modifiers in Java: `private`, `default`, `protected`, `public`
- `private` is the most restrictive, `public` is the least restrictive

---

## The Four Modifiers

| Modifier | Keyword | Scope |
|----------|---------|-------|
| Private | `private` | Only within the same class |
| Default | no keyword | Only within the same package |
| Protected | `protected` | Same package + subclasses in any package |
| Public | `public` | Everywhere, no restriction |

---

## Access Level Comparison Table

| Modifier | Same Class | Same Package | Subclass (diff pkg) | Other Package |
|----------|-----------|--------------|---------------------|---------------|
| `private` | YES | NO | NO | NO |
| Default | YES | YES | NO | NO |
| `protected` | YES | YES | YES | NO |
| `public` | YES | YES | YES | YES |

---

## Each Modifier in Detail

### ✦ private
- Most restrictive access level
- Accessible only within the class it is declared in
- Not visible to subclasses, not even in the same package
- Cannot be applied to top-level classes or interfaces
- Primary tool for data hiding in encapsulation
- All sensitive fields like passwords, balance, and tokens should be `private`

### ✦ default (Package-Private)
- No keyword is written, this is the default when nothing is specified
- Accessible to all classes within the same package only
- Not accessible to subclasses in a different package
- Also called package-private or package-level access
- Used for internal helper classes and utilities not meant for external use
- A class with default access cannot be imported and used from another package

### ✦ protected
- Accessible within the same package AND by subclasses in any package
- Cannot be accessed by an unrelated class in a different package
- Cannot be applied to top-level classes
- More open than default for inheritance, more restricted than public
- Used when you want subclasses to access and override a method but not expose it globally
- Common in framework design where parent class exposes hooks to child classes

### ✦ public
- Least restrictive access level
- Accessible from anywhere in the program, any class, any package
- Used for APIs, service methods, and anything meant to be used externally
- Every class intended for external use must be declared `public`
- Public fields should be avoided except for constants (`public static final`)

---

## Rules and Restrictions

- Local variables inside methods cannot have access modifiers
- Top-level classes can only be `public` or `default`, not `private` or `protected`
- Interfaces are `public` by default, all their methods are `public` by default
- Constructors can have any access modifier
- A `private` constructor prevents object creation from outside the class (used in Singleton pattern)
- From Java 9, `private` methods are allowed inside interfaces
- A subclass cannot override a method and make it more restrictive
- A subclass CAN override a method and make it less restrictive (e.g. `protected` to `public`)
- `private` members from a superclass are NOT inherited by subclasses

---

## Access Modifiers and Inheritance

| Modifier in Parent | Accessible in Subclass (same pkg) | Accessible in Subclass (diff pkg) | Inherited |
|-------------------|----------------------------------|----------------------------------|-----------|
| `private` | NO | NO | NO |
| Default | YES | NO | Only same package |
| `protected` | YES | YES | YES |
| `public` | YES | YES | YES |

- `private` fields of a parent class are not visible in the child class
- They can still be accessed indirectly through `public` or `protected` getter methods
- Overriding a method cannot reduce its access (cannot go from `public` to `protected`)
- Violating this rule causes a compile-time error and breaks the Liskov Substitution Principle

---

## Code Example

### Java
```java
package com.example.bank;

public class BankAccount {
    // private: only this class can access balance directly
    private double balance;

    // private: internal use only, hidden from outside
    private String accountNumber;

    // protected: subclasses can access and override
    protected String bankName;

    // public: open for everyone to use
    public String holderName;

    public BankAccount(String holderName, double initialBalance) {
        this.holderName = holderName;
        this.balance = initialBalance;
        this.accountNumber = "ACC" + (int)(Math.random() * 10000);
        this.bankName = "National Bank";
    }

    // public method: external access to private balance
    public double getBalance() {
        return balance;
    }

    // public method: controlled way to modify private data
    public void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    // protected: subclasses can override this behavior
    protected void applyInterest(double rate) {
        balance += balance * rate / 100;
    }

    // private: internal helper, not exposed outside
    private boolean isValidAmount(double amount) {
        return amount > 0 && amount <= balance;
    }

    public void withdraw(double amount) {
        if (isValidAmount(amount)) balance -= amount;
    }
}

// Subclass in a different package
package com.example.savings;

import com.example.bank.BankAccount;

public class SavingsAccount extends BankAccount {

    public SavingsAccount(String holderName, double balance) {
        super(holderName, balance);
    }

    // Can access protected method from parent
    public void applyMonthlyInterest() {
        applyInterest(3.5);   // allowed: protected method
    }

    // Cannot access private balance directly
    // Cannot access private accountNumber
    // CAN access public holderName
    // CAN access protected bankName
}
```

---

## Common Interview Questions

**Q: What are the four access modifiers in Java?**
- The most direct version of this question, asked in almost every fresher round
- `private`, default (no keyword), `protected`, `public` in order of increasing access
- Always mention: default is also called package-private and has no explicit keyword

**Q: What is the difference between `protected` and default access?**
- The most commonly confused pair
- Default allows access only within the same package, subclasses in different packages cannot access it
- `protected` allows access within the same package AND by subclasses in any package
- One keyword difference, but the behavior is significantly different in inheritance scenarios

**Q: Can you reduce the access level of a method when overriding it?**
- A tricky but very commonly asked follow-up
- No. A subclass cannot make an overridden method more restrictive
- You can make it less restrictive (e.g. `protected` to `public`) but not more
- Reducing access would violate the Liskov Substitution Principle and causes a compile-time error

**Q: Why should instance variables be `private`?**
- Tests understanding of encapsulation, not just the modifier definition
- Making fields `private` prevents external code from directly reading or changing them
- Access is then controlled through `public` getters and setters, where validation logic can be added
- Best practice: always make fields `private` by default unless there is a clear reason not to

**Q: What is the default access modifier in Java?**
- Simple but often answered incorrectly
- When no modifier is written, the member has package-private access (accessible only within the same package)
- It is NOT `public`. Many students assume no keyword means public, which is wrong

**Q: Can a `private` constructor be used and why?**
- Tests practical knowledge of design patterns
- Yes. A `private` constructor prevents any external class from creating an object
- Used in the Singleton design pattern to ensure only one instance of the class exists

---

## Common Mistakes to Avoid

- Thinking no keyword means `public`, it means default (package-private)
- Confusing `protected` and default, `protected` allows subclasses from any package, default does not
- Saying `private` members are inherited by subclasses, they are not, they are not visible at all
- Trying to apply access modifiers to local variables, it causes a compile-time error
- Trying to make a top-level class `protected` or `private`, only `public` or default is allowed for top-level classes
- Overriding a method and making it more restrictive, this is illegal in Java

---

## When to Use What

| Situation | Use |
|-----------|-----|
| Sensitive data: passwords, balance, tokens | `private` |
| Internal helper methods not meant for outside use | `private` |
| Utility or helper classes used only within a package | Default |
| Methods a subclass should override but not expose globally | `protected` |
| Base class hook methods in a framework | `protected` |
| Public API methods used by external code | `public` |
| Constants meant to be shared everywhere | `public static final` |
| Singleton pattern constructor | `private` |

---

## Resources

- [GeeksforGeeks - Access Modifiers in Java](https://www.geeksforgeeks.org/java/access-modifiers-java/)
- [GeeksforGeeks - Public vs Protected vs Package vs Private](https://www.geeksforgeeks.org/java/public-vs-protected-vs-package-vs-private-access-modifier-in-java/)
- [GeeksforGeeks - Protected vs Private in Java](https://www.geeksforgeeks.org/java/protected-vs-private-access-modifiers-in-java/)
- [InterviewBit - OOPs Interview Questions](https://www.interviewbit.com/oops-interview-questions/)
- [PrepInsta - OOPs Interview Questions](https://prepinsta.com/interview-preparation/technical-interview-questions/oops/)

---

*Made for CS Students | Internship & Job Prep Series*