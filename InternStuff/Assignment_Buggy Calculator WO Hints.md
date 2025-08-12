
**Objective:**  
Write a simple calculator that performs addition, subtraction, multiplication, and division of two numbers. The provided code has intentional bugs. The assignee must identify and fix the issues using IntelliJ's debugging tools.

---

### **Given Code (with bugs):**

```java
public class BuggyCalculator {

    public static void main(String[] args) {
        int a = 10;
        int b = 0;

        System.out.println("Addition: " + add(a, b));
        System.out.println("Subtraction: " + subtract(a, b));
        System.out.println("Multiplication: " + multiply(a, b));
        System.out.println("Division: " + divide(a, b)); 
    }

    public static int add(int x, int y) {
        return x - y; 
    }

    public static int subtract(int x, int y) {
        return x + y; 
    }

    public static int multiply(int x, int y) {
        return x * y;
    }

    public static int divide(int x, int y) {
        return x / y; 
    }
}
```

---

### **Instructions:**

1. **Open** the project in IntelliJ IDEA.
    
2. **Run** the program and observe the outputs.
    
3. Use **breakpoints and the debugger** to step through the code.
    
4. Identify and **fix the bugs** in each operation.
    
5. Handle the **division by zero** case gracefully (e.g., return a message or a default value).
    
6. Refactor the code if necessary to improve readability.
    

---

### **Deliverables:**

- A corrected and working version of the calculator.
    
- A brief explanation (1–2 paragraphs) of how the bugs were found and fixed using debugging.
    

---
## **Assignment: Buggy Calculator with Unit Tests**

**Objective:**  
Fix a simple calculator program with intentional bugs. Use IntelliJ’s debugging tools and JUnit tests to identify and correct the issues.

---

### **Part 1: Buggy Calculator Code**

Save as `BuggyCalculator.java`:

```java
public class BuggyCalculator {

    public static int add(int x, int y) {
        return x - y; 
    }

    public static int subtract(int x, int y) {
        return x + y; 
    }

    public static int multiply(int x, int y) {
        return x * y;
    }

    public static int divide(int x, int y) {
        if (y == 0) {
            throw new ArithmeticException("Division by zero is not allowed");
        }
        return x / y;
    }
}
```

---

### **Part 2: Test Code**

Save as `BuggyCalculatorTest.java` in the `test` directory (assuming a typical Maven/Gradle project structure):

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class BuggyCalculatorTest {

    @Test
    public void testAdd() {
        assertEquals(15, BuggyCalculator.add(10, 5));
    }

    @Test
    public void testSubtract() {
        assertEquals(5, BuggyCalculator.subtract(10, 5));
    }

    @Test
    public void testMultiply() {
        assertEquals(50, BuggyCalculator.multiply(10, 5));
    }

    @Test
    public void testDivide() {
        assertEquals(2, BuggyCalculator.divide(10, 5));
    }

    @Test
    public void testDivideByZero() {
        Exception exception = assertThrows(ArithmeticException.class, () -> {
            BuggyCalculator.divide(10, 0);
        });
        assertEquals("Division by zero is not allowed", exception.getMessage());
    }
}
```

---

### **Instructions:**

1. **Open the project** in IntelliJ IDEA.
    
2. **Run the tests** using the test runner in IntelliJ.
    
3. Use **debugging** to step through failing tests and identify bugs.
    
4. **Fix the calculator methods** so that all tests pass.
    
5. Optionally, **refactor the code** for clarity or add more tests (e.g., negative numbers, edge cases).
    

---

### **Deliverables:**

- A fully functional and corrected `BuggyCalculator.java`.
    
- All tests passing in `BuggyCalculatorTest.java`.
    
- A brief report or README summarizing:
    
    - Which bugs were found.
        
    - How they were fixed.
        
    - What tools or techniques (e.g., breakpoints, stepping) were used.
        

