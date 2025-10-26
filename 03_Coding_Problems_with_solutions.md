# 🎯 Section 3: Programming / Coding Questions — Exception Handling in Java

---

### 1️⃣ Question: Write a program to handle `ArrayIndexOutOfBoundsException`.

```java
public class ArrayExceptionDemo {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};
        try {
            System.out.println(arr[5]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index out of bounds!");
        } finally {
            System.out.println("End of program");
        }
    }
}
```

**Answer:**
```
Array index out of bounds!
End of program
```

---

### 2️⃣ Question: Program to handle multiple exceptions (`ArithmeticException` and `NullPointerException`).

```java
public class MultipleExceptionDemo {
    public static void main(String[] args) {
        try {
            int a = 5 / 0;   // ArithmeticException
            String str = null;
            System.out.println(str.length()); // NullPointerException
        } catch (ArithmeticException e) {
            System.out.println("Caught ArithmeticException");
        } catch (NullPointerException e) {
            System.out.println("Caught NullPointerException");
        } finally {
            System.out.println("Finally block executed");
        }
    }
}
```

**Answer:**
```
Caught ArithmeticException
Finally block executed
```

---

### 3️⃣ Question: Program to create and throw a **custom exception**.

```java
class MyException extends Exception {
    MyException(String msg) {
        super(msg);
    }
}

public class CustomExceptionDemo {
    static void checkNumber(int n) throws MyException {
        if (n < 0)
            throw new MyException("Negative number not allowed");
        else
            System.out.println("Number is: " + n);
    }

    public static void main(String[] args) {
        try {
            checkNumber(-5);
        } catch (MyException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
```

**Answer:**
```
Caught: Negative number not allowed
```

---

### 4️⃣ Question: Program demonstrating **re-throwing exceptions**.

```java
public class RethrowDemo {
    static void method() throws Exception {
        try {
            throw new Exception("Initial Exception");
        } catch (Exception e) {
            System.out.println("Caught in method, rethrowing...");
            throw e;
        }
    }

    public static void main(String[] args) {
        try {
            method();
        } catch (Exception e) {
            System.out.println("Caught in main: " + e.getMessage());
        }
    }
}
```

**Answer:**
```
Caught in method, rethrowing...
Caught in main: Initial Exception
```

---

### 5️⃣ Question: Program to read a file and handle `FileNotFoundException` and `IOException`.

```java
import java.io.*;

public class FileHandlingDemo {
    public static void main(String[] args) {
        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader("input.txt"));
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        } catch (IOException e) {
            System.out.println("Error reading file!");
        } finally {
            try {
                if (br != null) br.close();
            } catch (IOException e) {
                System.out.println("Error closing file!");
            }
        }
    }
}
```

**Answer:**
- Prints contents of `input.txt` if exists.  
- Otherwise prints "File not found!".  
- File is **always closed** in `finally`.

---

### 6️⃣ Question: Program demonstrating **nested try-catch**.

```java
public class NestedTryDemo {
    public static void main(String[] args) {
        try {
            try {
                int[] arr = new int[2];
                arr[5] = 10;
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Inner: Array Index Out Of Bounds");
            }

            String str = null;
            System.out.println(str.length());
        } catch (NullPointerException e) {
            System.out.println("Outer: Null Pointer Exception");
        }
    }
}
```

**Answer:**
```
Inner: Array Index Out Of Bounds
Outer: Null Pointer Exception
```

---

### 7️⃣ Question: Program demonstrating **finally overriding return value**.

```java
public class FinallyReturnDemo {
    static int testMethod() {
        try {
            return 10;
        } finally {
            return 20;
        }
    }

    public static void main(String[] args) {
        System.out.println(testMethod());
    }
}
```

**Answer:**
```
20
```

---

### 8️⃣ Question: Program demonstrating **unchecked vs checked exceptions**.

```java
import java.io.*;

public class CheckedUncheckedDemo {
    public static void main(String[] args) {
        // Unchecked exception
        int a = 5, b = 0;
        try {
            System.out.println(a / b); // ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Caught unchecked: " + e);
        }

        // Checked exception
        try {
            FileReader fr = new FileReader("test.txt"); // FileNotFoundException
        } catch (FileNotFoundException e) {
            System.out.println("Caught checked: " + e);
        }
    }
}
```

**Answer:**
```
Caught unchecked: java.lang.ArithmeticException: / by zero
Caught checked: java.io.FileNotFoundException: test.txt (No such file or directory)
```

---

### 9️⃣ Question: Program to demonstrate **throw keyword**.

```java
public class ThrowDemo {
    static void check(int n) {
        if (n < 0) {
            throw new ArithmeticException("Negative value not allowed");
        }
        System.out.println("Value: " + n);
    }

    public static void main(String[] args) {
        check(-10);
    }
}
```

**Answer:**
```
Exception in thread "main" java.lang.ArithmeticException: Negative value not allowed
    at ThrowDemo.check(ThrowDemo.java:4)
    ...
```

---

### 🔟 Question: Program demonstrating **throws keyword**.

```java
import java.io.*;

public class ThrowsDemo {
    static void readFile() throws IOException {
        FileReader fr = new FileReader("sample.txt");
        fr.close();
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("Exception caught: