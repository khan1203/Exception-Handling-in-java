# 🎯 Section 4: Advanced / Conceptual & Application Questions — Exception Handling in Java

---

### 1️⃣ Question: Explain why **finally** block executes even if there is a `return` statement in `try` or `catch`.

**Answer:**
- The **`finally` block is always executed**, regardless of whether an exception occurs or whether `try` or `catch` has a `return` statement.
- This is because `finally` is intended for **cleanup code**, such as closing files, releasing resources, or closing network connections.

**Example:**
```java
public class FinallyDemo {
    static int test() {
        try {
            return 10;
        } finally {
            System.out.println("Finally block executed");
        }
    }

    public static void main(String[] args) {
        System.out.println(test());
    }
}
```
**Output:**
```
Finally block executed
10
```

---

### 2️⃣ Question: What is the difference between **throw** and **throws**? Give examples.

**Answer:**
| Keyword | Purpose | Example |
|---------|---------|---------|
| `throw` | Used to **explicitly throw an exception** from a method or block | `throw new IOException("File error");` |
| `throws` | Declares **which exceptions a method may throw**, propagating responsibility to caller | `void readFile() throws IOException { ... }` |

**Example:**
```java
import java.io.*;

public class ThrowThrowsDemo {
    static void readFile() throws IOException {
        throw new IOException("File not found");
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```
**Output:**
```
Caught: File not found
```

---

### 3️⃣ Question: Explain **exception propagation** in Java with an example.

**Answer:**
- Exception propagation occurs when an exception is **not caught in the current method**, so it **travels up the call stack** to the caller method until handled or the program terminates.

**Example:**
```java
public class PropagationDemo {
    static void method1() {
        int data = 5 / 0;
    }

    static void method2() {
        method1();
    }

    public static void main(String[] args) {
        try {
            method2();
        } catch (ArithmeticException e) {
            System.out.println("Exception caught in main: " + e);
        }
    }
}
```
**Output:**
```
Exception caught in main: java.lang.ArithmeticException: / by zero
```

---

### 4️⃣ Question: Why should **checked exceptions** be handled or declared?

**Answer:**
- Checked exceptions are **compile-time exceptions** that the compiler forces the programmer to handle.
- Ensures **robustness** in programs that deal with I/O, network, or external resources.

**Example:**
```java
import java.io.*;

public class CheckedExceptionDemo {
    public static void main(String[] args) {
        try {
            FileReader fr = new FileReader("data.txt");
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        }
    }
}
```

---

### 5️⃣ Question: Explain **unchecked exceptions** and give examples.

**Answer:**
- Unchecked exceptions are **runtime exceptions**, not checked at compile time.
- Indicate **programming errors** like invalid logic, null pointers, or division by zero.

**Examples:** `ArithmeticException`, `NullPointerException`, `ArrayIndexOutOfBoundsException`

**Example:**
```java
public class UncheckedDemo {
    public static void main(String[] args) {
        int a = 10, b = 0;
        System.out.println(a / b);
    }
}
```
**Explanation:** Runtime handles them; uncaught exceptions terminate the program.

---

### 6️⃣ Question: Explain the concept of **user-defined exceptions**.

**Answer:**
- Java allows programmers to **create custom exceptions** for specific application needs.
- Extend **`Exception`** or **`RuntimeException`**.

**Example:**
```java
class InvalidAgeException extends Exception {
    InvalidAgeException(String msg) {
        super(msg);
    }
}

public class CustomExceptionApp {
    static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) throw new InvalidAgeException("Age < 18 not allowed");
    }

    public static void main(String[] args) {
        try {
            validateAge(15);
        } catch (InvalidAgeException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```
**Output:**
```
Caught: Age < 18 not allowed
```

---

### 7️⃣ Question: What happens if a **finally block throws an exception**?

**Answer:**
- Exception in `finally` **overrides any exception in try/catch**.
- Original exception may be **lost**.

**Example:**
```java
public class FinallyExceptionDemo {
    public static void main(String[] args) {
        try {
            int data = 5 / 0;
        } finally {
            int arr[] = new int[2];
            arr[5] = 10;
        }
    }
}
```
**Explanation:** Avoid throwing exceptions in `finally`; it can **mask the original exception**.

---

### 8️⃣ Question: Explain **exception hierarchy** in Java.

**Answer:**
- All exceptions and errors inherit from **`java.lang.Throwable`**.

**Branches:**
1. **Exception** → Checked & Unchecked
   - `IOException`, `RuntimeException`, `NullPointerException`
2. **Error** → System-level errors
   - `OutOfMemoryError`, `StackOverflowError`

**Explanation:** Catch **subclasses before superclasses** to handle exceptions correctly.

---

### 9️⃣ Question: Difference between **Error** and **Exception**.

| Aspect | Exception | Error |
|--------|-----------|-------|
| Recoverable? | Usually yes | Usually no |
| Checked / Unchecked | Checked & Unchecked | Unchecked only |
| Example | `IOException`, `NullPointerException` | `OutOfMemoryError`, `StackOverflowError` |
| Purpose | Program-level problems | System-level failures |

**Explanation:** Exceptions are **part of normal application flow**; Errors indicate **serious system failures**.

---

### 🔟 Question: Why should we avoid catching **Throwable**?

**Answer:**
- `Throwable` includes both **`Error`** and **`Exception`**.
- Catching it may intercept serious system-level issues which should **not be handled programmatically**.
- Best practice: **catch specific exceptions**,