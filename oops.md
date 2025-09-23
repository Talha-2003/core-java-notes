# Java Inheritance & Polymorphism - Simplified Notes

## 🏛️ Inheritance Basics

**Inheritance** = Child class gets properties/methods from parent class

### Simple Example
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

### 🔑 Key Rules:
1. **Method Priority**: Child > Parent > Grandparent > Object
2. **Object Class**: Ultimate parent of ALL Java classes
3. **One-way street**: Parent can't access child methods

## ⚡ Polymorphism = "Many Forms"

### 1. Static Polymorphism (Compile-time) = Method Overloading

```java
=====================
 Static Polymorphism (Compile-time) = Method Overloading
=====================

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

=====================
 DRY RUN (Calculator):
=====================

 1. new Calculator() creates instance c
    - JVM allocates memory for object c
    - Constructor is called (default constructor used here)

 2. c.add(10, 20):
    - Compiler checks method signature: add(int, int)
    - Matches with: void add(int a, int b)
    - Executes: System.out.println("Sum: " + (10 + 20))
    - Output: Sum: 30

 3. c.add(10, 20, 30):
    - Compiler checks method signature: add(int, int, int)
    - Matches with: void add(int a, int b, int c)
    - Executes: System.out.println("Sum: " + (10 + 20 + 30))
    - Output: Sum: 60

=====================
 Why it's called Compile-time Polymorphism:
=====================
 - Method selection is done by compiler based on method signature
 - No decision is deferred to runtime
 - Overloaded methods are resolved during compilation
 - Hence, it's called static or compile-time polymorphism
**Decision made at compile time**
```
```
//=====================
// Dynamic Polymorphism (Runtime) = Method Overriding
//=====================

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
        Bank b = new SBI();  // Step 1: Parent reference, Child object

        double rate = b.getInterestRate();  // Step 2: Runtime decision
        System.out.println("Rate of Interest: " + rate);  // Output: 7.5
    }
}

=====================
 DRY RUN (Test):
=====================

// 1. Bank b = new SBI();
//    - Reference type: Bank
//    - Object type: SBI
//    - JVM allocates memory for SBI object
//    - Parent reference holds child object

// 2. b.getInterestRate();
//    - Compiler checks Bank class: method exists ✅
//    - At runtime, JVM checks actual object type: SBI
//    - SBI overrides getInterestRate()
//    - Executes SBI's version → returns 7.5

// 3. Output:
//    Rate of Interest: 7.5

//=====================
// Why it's called Runtime Polymorphism:
//=====================
// - Method selection is deferred until runtime
// - Based on actual object type, not reference type
// - Enables flexibility and dynamic behavior
// - Common in frameworks, interfaces, and abstract classes

```java

//=====================
// Dynamic Polymorphism (Runtime) = Method Overriding
//=====================

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
        if (checkEligibility()) {           // Uses parent's method
            double rate = getHomeLoanRate(); // Uses OVERRIDDEN method
            return "Loan approved! Rate: " + rate;
        }
        return "Not eligible";
    }
}

//=====================
// OR Example
//=====================

class RBIBank {
    boolean checkEligibility() {
        // docs verification logic
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
        boolean status = checkEligibility();  // inherited method
        if (status) {
            double rate = getHomeLoanRoi();   // overridden method
            return "Your loan approved with ROI :: " + rate;
        } else {
            return "You are not eligible for home loan";
        }
    }

    public static void main(String[] args) {
        SBIBank bank = new SBIBank();  // Step 1: Object created
        System.out.println(bank.applyHomeLoan());  // Step 2: Method call
    }
}

//=====================
// DRY RUN (SBIBank):
//=====================

// 1. SBIBank bank = new SBIBank();
//    - JVM creates object of SBIBank
//    - Inherits methods from RBIBank

// 2. bank.applyHomeLoan();
//    a. checkEligibility() → inherited from RBIBank → returns true
//    b. getHomeLoanRoi() → overridden in SBIBank → returns 12.85
//    c. Message constructed: "Your loan approved with ROI :: 12.85"

// 3. Output:
//    Your loan approved with ROI :: 12.85

//=====================
// Why it's called Runtime Polymorphism:
//=====================
// - Method selection is deferred until runtime
// - Based on actual object type (SBIBank), not reference type (RBIBank)
// - JVM decides which version of method to execute
// - Enables flexible and dynamic behavior in inheritance
```

## ⚠️ Important Concepts

### equals() Method Behavior
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
// DRY RUN (equals):  
// 1. b1.equals(b2):  
//    - Object.equals() compares references → false  
//    - prints: Both Banks Are Equal ?? :: false  
// 2. s1.equals(s2):  
//    - String overrides equals() to compare content → true  
//    - prints: Strings Are Equal ?? :: true  

// Note: Object.equals() compares addresses  
//       String overrides equals() to compare content  
```

### 🎯 Quick Summary Table

| Concept | What | When | Example |
|---------|------|------|---------|
| **Inheritance** | Child gets parent's stuff | Code reuse needed | `class Child extends Parent` |
| **Overloading** | Same method, different parameters | Compile-time | `add(int a)` vs `add(int a, int b)` |
| **Overriding** | Child changes parent's method | Runtime | Child provides own `calculate()` |

## 💡 Remember These Points:

1. **Inheritance Chain**: Child → Parent → Grandparent → Object
2. **Overloading** = Same class, different parameters
3. **Overriding** = Child class, same method signature
4. **Object class** = Default parent with basic methods like `equals()`, `toString()`
5. **super keyword** = Access parent's methods/constructors

This should make the concepts much clearer! The key is understanding that inheritance is about **code reuse** while polymorphism is about **flexibility in method execution**.
