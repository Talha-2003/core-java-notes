

---

```markdown
# 🌟 Java Inheritance & Polymorphism – Simplified Notes

---

## 🏛️ Inheritance Basics

**Inheritance** → Child class automatically gets the properties and methods of its parent class.  
Helps with **code reuse**, **hierarchy**, and **logical grouping**.

### 📘 Simple Example
```java
class Parent {
    void m1() {
        System.out.println("Parent's m1()");
    }
}

class Child extends Parent {
    // Child gets m1() from Parent automatically
    void m2() {
        System.out.println("Child's m2()");
    }
}

public class Test {
    public static void main(String[] args) {
        Child c = new Child();
        c.m1();  // Uses Parent's method
        c.m2();  // Uses Child's method
    }
}
```

### 🔑 Key Rules
1. **Method Priority**: Child → Parent → Grandparent → Object  
2. **Object Class**: Root of all Java classes  
3. **One-way Access**: Parent cannot access child methods  

---

## ⚡ Polymorphism = “Many Forms”

---

### 1️⃣ Static Polymorphism (Compile-time) → Method Overloading

```java
class Calculator {
    // Same method name, different parameters
    void add(int a, int b) {
        System.out.println("Sum: " + (a + b));
    }

    void add(int a, int b, int c) {
        System.out.println("Sum: " + (a + b + c));
    }

    public static void main(String[] args) {
        Calculator c = new Calculator();  // Step 1: Object created

        c.add(10, 20);                    // Step 2: Compiler selects add(int, int)
        // Output: Sum: 30

        c.add(10, 20, 30);                // Step 3: Compiler selects add(int, int, int)
        // Output: Sum: 60
    }
}
```

#### 🧪 DRY RUN
1. `new Calculator()` → Object created  
2. `c.add(10, 20)` → Compiler picks `add(int, int)` → Output: 30  
3. `c.add(10, 20, 30)` → Compiler picks `add(int, int, int)` → Output: 60  

**Why Compile-time?**  
- Method selection happens during compilation  
- Based on method signature  
- No runtime decision involved  

---

### 2️⃣ Dynamic Polymorphism (Runtime) → Method Overriding

```java
class Bank {
    double getInterestRate() {
        return 5.0;  // Default rate
    }
}

class SBI extends Bank {
    @Override
    double getInterestRate() {
        return 7.5;  // SBI's specific rate
    }
}

public class Test {
    public static void main(String[] args) {
        Bank b = new SBI();  // Parent reference, Child object
        double rate = b.getInterestRate(); // Runtime decision
        System.out.println("Rate of Interest: " + rate); // Output: 7.5
    }
}
```

#### 🧪 DRY RUN
1. `Bank b = new SBI();` → Reference type: Bank, Object type: SBI  
2. `b.getInterestRate()` → Compiler checks Bank ✅, JVM runs SBI’s version  
3. Output: `Rate of Interest: 7.5`

**Why Runtime?**  
- Method selection deferred until runtime  
- Based on actual object type, not reference type  

---

### 🏦 Real Banking Example – Runtime Polymorphism

```java
class RBIBank {
    boolean checkEligibility() {
        return true;  // Basic check
    }

    double getHomeLoanRate() {
        return 8.5;  // RBI's base rate
    }
}

class SBIBank extends RBIBank {
    @Override
    double getHomeLoanRate() {
        return 9.5;  // SBI's actual rate
    }

    String applyLoan() {
        if (checkEligibility()) {
            double rate = getHomeLoanRate();
            return "Loan approved! Rate: " + rate;
        }
        return "Not eligible";
    }
}
```

---

#### 🔁 OR Example – Same Concept, Different Naming

```java
class RBIBank {
    boolean checkEligibility() {
        return true;
    }

    double getHomeLoanRoi() {
        return 10.85;
    }

    double getPersonalLoanRoi() {
        return 11.65;
    }
}

public class SBIBank extends RBIBank {
    @Override
    double getHomeLoanRoi() {
        return 12.85;  // SBI's specific rate
    }

    String applyHomeLoan() {
        if (checkEligibility()) {
            double rate = getHomeLoanRoi();
            return "Your loan approved with ROI :: " + rate;
        }
        return "You are not eligible for home loan";
    }

    public static void main(String[] args) {
        SBIBank bank = new SBIBank();
        System.out.println(bank.applyHomeLoan());
    }
}
```

#### 🧪 DRY RUN
1. `SBIBank bank = new SBIBank();` → Object created  
2. `applyHomeLoan()` → `checkEligibility()` → true → `getHomeLoanRoi()` → 12.85  
3. Output: `"Your loan approved with ROI :: 12.85"`

---

## ⚠️ Important Concepts

### 🔍 equals() Method Behavior

```java
public class Demo {
    public static void main(String[] args) {
        String s1 = new String("hello");
        String s2 = new String("hello");

        System.out.println(s1.equals(s2));  // TRUE - compares content

        Bank b1 = new Bank();
        Bank b2 = new Bank();
        System.out.println(b1.equals(b2));  // FALSE - compares memory address
    }
}
```
#Every class in Java ultimately inherits from java.lang.Object
#### 🧪 DRY RUN
- `s1.equals(s2)` → true 
→ String overrides equals() → compares content → true   
Every class inherit the equals() method from object (ultimate super)
In default case Object.equals() checks if two references point to the same object in memory or not.
But string Overrides equals() instead of checking memory , it compares the character inside the string just as a son doesnot listen to its parents and do opposite of what they say.

- `b1.equals(b2)` →false
-  Object default equals() → compares memory address → false
- Bank class doesnot override equals() , so it uses object.equals() to comparenthe memory address and found their memory location different.
- 'new Bank()' creates two different objects at two dofferent location therefore return false.
---

## 🎯 Quick Summary Table

| Concept        | What it means                        | When it happens | Example                          |
|----------------|--------------------------------------|------------------|----------------------------------|
| **Inheritance**| Child gets parent’s methods/fields   | Always           | `class Child extends Parent`     |
| **Overloading**| Same method name, different params   | Compile-time     | `add(int)` vs `add(int, int)`    |
| **Overriding** | Child redefines parent’s method      | Runtime          | `Child overrides calculate()`    |

---

## 💡 Final Takeaways

- **Inheritance Chain**: Child → Parent → Grandparent → Object  
- **Overloading**: Same class, different parameters  
- **Overriding**: Child class, same method signature  
- **Object class**: Root class with methods like `equals()`, `toString()`  
- **super keyword**: Access parent’s methods/constructors  

---
```

---

This is now **GitHub-ready** — clean headings, code blocks, DRY RUN sections, and emoji cues for quick scanning.  
If you want, I can also add **UML diagrams** for inheritance and polymorphism so your `.md` looks even more professional. Would you like me to do that next?
