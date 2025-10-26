# 🎯 Section 1: Conceptual / Short Answers — Exception Handling in Java

---

### 1️⃣ What is an Exception in Java? How is it different from an Error?

- **Exception:** An event that occurs during program execution that disrupts the normal flow.  
- **Error:** Serious problems usually beyond the control of the application (e.g., `OutOfMemoryError`, `StackOverflowError`).

| Aspect | Exception | Error |
|:--|:--|:--|
| Recoverable? | Often recoverable | Usually unrecoverable |
| Package | `java.lang.Exception` | `java.lang.Error` |
| Example | `IOException`, `NullPointerException` | `OutOfMemoryError`, `StackOverflowError` |

---

### 2️⃣ Checked vs Unchecked Exceptions

- **Checked Exceptions:** Verified at **compile time**. Must be handled with `try–catch` or declared with `throws`.  
  *Examples:* `IOException`, `SQLException`

- **Unchecked Exceptions:** Verified at **runtime**. Not checked by the compiler.  
  *Examples:* `ArithmeticException`, `NullPointerException`

---

### 3️⃣ Purpose of `try`, `catch`, `finally`, `throw`, and `throws`

| Keyword | Purpose |
|:--|:--|
| `try` | Defines a block of code to monitor for exceptions |
| `catch` | Handles a specific type of exception |
| `finally` | Executes regardless of whether an exception occurred (used for cleanup) |
| `throw` | Explicitly throws an exception object |
| `throws` | Declares that a method may throw exceptions to its caller |

---

### 4️⃣ What happens if an exception occurs in the `finally` block?

If a `finally` block throws an exception, it **overrides** any exception thrown in `try` or `catch`, meaning the original exception is lost.

---

### 5️⃣ Can we have multiple `catch` blocks for a single `try`?

✅ Yes.  
A single `try` block can have **multiple `catch`** blocks.  
They are evaluated **top-to-bottom**, and the **first matching type** is executed.  
Always catch **subclasses first**, then **superclasses**.

---

### 6️⃣ What is the superclass of all exceptions in Java?

`java.lang.Throwable`

- Subclasses:  
  - `java.lang.Exception`  
  - `java.lang.Error`

---

### 7️⃣ Can constructors throw exceptions? Give an example.

Yes, constructors can declare or throw exceptions.

```java
class Test {
    Test() throws IOException {
        throw new IOException("Error in constructor");
    }
}
```

---

### 8️⃣ Why should you never catch the `Throwable` class directly?

Because `Throwable` includes both **`Error`** and **`Exception`** types.  
Catching it may intercept serious system-level issues (like `OutOfMemoryError`) that should **not** be handled programmatically.

---

### 9️⃣ Explain the concept of exception propagation in Java.

When an exception is **not caught** in the current method, it is **propagated up the call stack** to the caller until some method handles it or the JVM terminates the program.

---

### 🔟 What is the difference between `throw new Exception()` and `throws Exception`?

| Keyword | Meaning |
|:--|:--|
| `throw` | Used inside a method to **throw** an actual exception instance |
| `throws` | Used in the method declaration to **declare** possible exceptions |

**Example:**
```java
void test() throws IOException {
    throw new IOException("File error");
}
```

---

