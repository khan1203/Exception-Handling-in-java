# 🎯 Section 2: Analytical Questions — Exception Handling in Java

---


### 1️⃣ Predict the output:

```java
try {
    int a = 5 / 0;
    System.out.println("After division");
} catch (ArithmeticException e) {
    System.out.println("Caught ArithmeticException");
} finally {
    System.out.println("Finally block executed");
}
System.out.println("End of main");
```

**Answer:**
```
Caught ArithmeticException
Finally block executed
End of main
```

---

### 2️⃣ If an exception is not handled anywhere in the program, what happens?

**Answer:**
- The exception **propagates up the call stack** to the caller method.
- If no method handles it, the **JVM prints a stack trace** and the program terminates abnormally.

---

### 3️⃣ What happens to the return value if finally has a return statement?

```java
try {
    return 10;
} catch (Exception e) {
    return 20;
} finally {
    return 30;
}
```

**Answer:** `30`  
**Explanation:** The `finally` block **overrides any return** value from `try` or `catch`.

---

### 4️⃣ Is it a good practice to have an empty catch block? Why or why not?

**Answer:** ❌ No  
- Empty `catch` blocks **hide exceptions silently**.
- Always **log** or **handle** exceptions properly.

---

### 5️⃣ Write a custom exception example:

```java
class InvalidAgeException extends Exception {
    InvalidAgeException(String msg) {
        super(msg);
    }
}

class Test {
    static void checkAge(int age) throws InvalidAgeException {
        if (age < 18)
            throw new InvalidAgeException("Age < 18 not allowed");
        else
            System.out.println("Allowed to vote");
    }
}
```

**Answer:**
- `InvalidAgeException` is a **user-defined exception**.
- It is **thrown** when age < 18.

---

### 6️⃣ Handle multiple exceptions in a program:

```java
import java.util.*;

public class Division {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        try {
            System.out.print("Enter two integers: ");
            int a = sc.nextInt();
            int b = sc.nextInt();
            System.out.println("Result: " + (a / b));
        } catch (ArithmeticException e) {
            System.out.println("Error: Division by zero!");
        } catch (InputMismatchException e) {
            System.out.println("Error: Invalid input type!");
        } catch (Exception e) {
            System.out.println("General Exception: " + e.getMessage());
        } finally {
            sc.close();
            System.out.println("Program finished.");
        }
    }
}
```

**Answer:**
- Handles **ArithmeticException**, **InputMismatchException**, and **general Exception**.
- `finally` ensures scanner is **always closed**.

---

### 7️⃣ Nested try blocks example:

```java
public class NestedTry {
    public static void main(String[] args) {
        try {
            String str = null;
            try {
                int[] arr = new int[3];
                System.out.println(arr[5]);
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Inner: Array index out of bounds");
            }
            System.out.println(str.length());
        } catch (NullPointerException e) {
            System.out.println("Outer: Null pointer exception");
        }
    }
}
```

**Answer:**
```
Inner: Array index out of bounds
Outer: Null pointer exception
```

---

### 8️⃣ Re-throwing an exception:

```java
public class ReThrow {
    static void method1() throws Exception {
        try {
            throw new Exception("Error in method1");
        } catch (Exception e) {
            System.out.println("Caught inside method1, rethrowing...");
            throw e;
        }
    }

    public static void main(String[] args) {
        try {
            method1();
        } catch (Exception e) {
            System.out.println("Caught in main: " + e.getMessage());
        }
    }
}
```

**Answer:**
```
Caught inside method1, rethrowing...
Caught in main: Error in method1
```

---

### 9️⃣ File handling with exceptions:

```java
import java.io.*;

public class FileRead {
    public static void main(String[] args) {
        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader("data.txt"));
            String line;
            while ((line = br.readLine()) != null)
                System.out.println(line);
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        } catch (IOException e) {
            System.out.println("I/O error: " + e.getMessage());
        } finally {
            try {
                if (br != null) br.close();
            } catch (IOException e) {
                System.out.println("Error closing file");
            }
        }
    }
}
```

**Answer:**
- `FileNotFoundException` if the file doesn't exist.
- `IOException` if read error occurs.
- `finally` ensures file **is closed**.

---

### 🔟 Predict the output with multiple exceptions:

```java
try {
    int[] arr = new int[2];
    arr[5] = 10;
} catch (ArithmeticException e) {
    System.out.println("Arithmetic Exception");
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Array Index Out Of Bounds Exception");
} catch (Exception e) {
    System.out.println("General Exception");
} finally {
    System.out.println("Finally executed");
}
```

**Answer:**
```
Array Index Out Of Bounds Exception
Finally exe
