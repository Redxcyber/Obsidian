
---

### **Understanding `final` Variables in Java**

In Java, the `final` keyword is used to declare constants, meaning their values **cannot be changed once assigned**. There are three types of `final` variables:

1. **Final Instance Variables** (Non-static)
2. **Final Static Variables** (Class-level)
3. **Final Local Variables** (Inside a method)

Your code contains **final instance variables**, so let's break it down.

---

## **Step-by-Step Analysis of Your Code**

### **1. What’s Wrong in Your Code?**

#### **Code Given:**

```java
package $15_Final_Keyword;

class Test{
    final int MIN = 1;   // Final instance variable (initialized here)
    final int NORMAL;    // Final instance variable (not yet initialized)
    final int MAX;       // Final instance variable (not yet initialized)
	
    static {  
        NORMAL = 5;  // ❌ ERROR! NORMAL is an instance variable, can't be assigned in a static block
    }
	
    Test(){
        MAX = 10;  // ✅ Correct. Final instance variable can be initialized in constructor
    }
}
```

#### **What is Wrong?**

- **`NORMAL` is an instance variable**, but you're trying to initialize it inside a `static` block.
- **Instance variables** belong to objects, but **static blocks** execute **before any object is created**.
- **Solution:** `NORMAL` should be initialized **inside the constructor**, not a static block.

---

### **2. Corrected Code**

```java
package Final_Keyword;

class Test {
    final int MIN = 1;   // ✅ Direct initialization
    final int NORMAL;    // ✅ Will be initialized in the constructor
    final int MAX;       // ✅ Will be initialized in the constructor
	
    Test() {
        NORMAL = 5;  // ✅ Correct: Final instance variable initialized inside constructor
        MAX = 10;    // ✅ Correct: Final instance variable initialized inside constructor
    }
}

public class _01_FinalVariable {
    public static void main(String[] args) {
        Test obj = new Test();
        System.out.println("MIN: " + obj.MIN);
        System.out.println("NORMAL: " + obj.NORMAL);
        System.out.println("MAX: " + obj.MAX);
    }
}
```

---

## **3. Explanation of `final` Variables**

### **A. Final Instance Variables**

- These **belong to an object**, meaning each object gets its own copy.
- **Rules:**
    1. Must be initialized **when declared** **or** inside the **constructor**.
    2. Once assigned, **they cannot be changed**.

#### **Example:**

```java
class Example {
    final int A = 10;  // ✅ Initialized at declaration
    final int B;       // ✅ Must be initialized in the constructor
	
    Example() {
        B = 20;  // ✅ Correct: Assigning in constructor
    }
}
```

🚫 **Incorrect:**

```java
class Example {
    final int B; 
	
    void setB() {
        B = 10;  // ❌ ERROR! Final variables cannot be assigned outside constructor
    }
}
```

---

### **B. Final Static Variables**

- These **belong to the class**, meaning all objects share the same copy.
- **Rules:**
    1. Must be initialized **when declared** **or** inside a **static block**.
    2. **Cannot be assigned inside a constructor** because constructors run when objects are created, but `static` variables should be set **before** any object exists.

#### **Example:**

```java
class Example {
    static final int A = 100;  // ✅ Initialized at declaration
    static final int B;        // ✅ Must be initialized inside static block
	
    static {
        B = 200;  // ✅ Correct: Final static variable initialized inside static block
    }
}
```

🚫 **Incorrect:**

```java
class Example {
    static final int B;
	
    Example() {
        B = 10;  // ❌ ERROR! Final static variables cannot be assigned in constructor
    }
}
```

---

### **C. Final Local Variables**

- These **exist inside a method** and **must be initialized before use**.
- **Rules:**
    1. Must be initialized before **first use**.
    2. Once assigned, cannot be changed.

#### **Example:**

```java
class Example {
    void show() {
        final int X;  
        X = 50;  // ✅ First assignment is allowed
        System.out.println(X);  // Output: 50
		
        X = 60;  // ❌ ERROR! Cannot change final variable
    }
}
```

---

## **4. Summary of `final` Variable Rules**

|Type|When to Initialize|Where to Initialize|
|---|---|---|
|**Instance (`final int x;`)**|Before constructor ends|1. When declared  <br>2. Inside constructor|
|**Static (`static final int x;`)**|Before class is used|1. When declared  <br>2. Inside static block|
|**Local (`final int x;`)**|Before first use|1. When declared  <br>2. Inside method before usage|

---

## **5. Example with Both Instance and Static Final Variables**

```java
class Example {
    final int instanceVar;       // Final instance variable
    static final int staticVar;  // Final static variable
	
    static { 
        staticVar = 100;  // ✅ Static final variable initialized inside static block
    }
	
    Example() {
        instanceVar = 50;  // ✅ Instance final variable initialized inside constructor
    }
	
    void display() {
        System.out.println("Instance Final: " + instanceVar);
        System.out.println("Static Final: " + staticVar);
    }
	
    public static void main(String[] args) {
        Example obj = new Example();
        obj.display();
    }
}
```

**Output:**

```sh
Instance Final: 50
Static Final: 100
```

---

## **6. Key Takeaways**

- **Final variables cannot be changed once assigned.**
- **Final instance variables** must be initialized **inside a constructor** (if not at declaration).
- **Final static variables** must be initialized **in a static block or at declaration**.
- **Final local variables** must be initialized before **first use**.