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
class Calculator {
    // Same method name, different parameters
    void add(int a, int b) {
        System.out.println("Sum: " + (a + b));
    }
    
    void add(int a, int b, int c) {
        System.out.println("Sum: " + (a + b + c));
    }
}
// DRY RUN (Calculator):  
// 1. new Calculator() creates instance c  
// 2. c.add(10, 20):  
//    - compiler picks add(int,int)  
//    - computes 10 + 20 = 30  
//    - prints: sum from 1st method: 30  
// 3. c.add(10, 20, 30):  
//    - compiler picks add(int,int,int)  
//    - computes 10 + 20 + 30 = 60  
//    - prints: sum from 2nd method: 60 
```
**Decision made at compile time**

### 2. Dynamic Polymorphism (Runtime) = Method Overriding
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
```
**Decision made at runtime based on actual object type**

## 🏦 Real Banking Example
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
        if (checkEligibility()) {           // Uses parent's method
            double rate = getHomeLoanRate(); // Uses OVERRIDDEN method
            return "Loan approved! Rate: " + rate;
        }
        return "Not eligible";
    }
}

OR

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
    double getHomeLoanRoi() {             // override to provide SBI rate  
        return 12.85;  
    }  

    String applyHomeLoan() {  
        boolean status = checkEligibility();  // inherited method  
        if (status) {  
            double rate = getHomeLoanRoi();   // calls SBI override  
            return "Your loan approved with ROI :: " + rate;  
        } else {  
            return "You are not eligible for home loan";  
        }  
    }  

    public static void main(String[] args) {  
        SBIBank bank = new SBIBank();  
        System.out.println(bank.applyHomeLoan());  
    }  
}  

// DRY RUN (SBIBank):  
// 1. new SBIBank() → instance of SBIBank  
// 2. applyHomeLoan():  
//    a. checkEligibility() → returns true  
//    b. getHomeLoanRoi() → override returns 12.85  
//    c. returns string "Your loan approved with ROI :: 12.85"  
// 3. prints message  

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
