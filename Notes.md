# ☕ Java Exception Handling - Detailed Notes

---

## 📌 1. What is an Exception?

An **Exception** is an unexpected or abnormal event that occurs during the execution of a program (at runtime) and disrupts the normal flow of instruction execution.

### Common Causes of Exceptions:
- Dividing a number by zero (`ArithmeticException`)
- Accessing an invalid array index (`ArrayIndexOutOfBoundsException`)
- Dereferencing a `null` object reference (`NullPointerException`)
- Trying to open a non-existent file (`FileNotFoundException`)
- Passing invalid method inputs (`IllegalArgumentException`)

### What happens when an Exception occurs?
1. The Java Virtual Machine (JVM) creates an **Exception Object** containing error details (exception type, message, stack trace).
2. JVM searches the **call stack** for an appropriate exception handler.
3. If no handler is found, the default JVM Exception Handler terminates the program abruptly and prints the stack trace.

---

## 📌 2. What is Exception Handling?

**Exception Handling** is a programming technique used to handle runtime errors gracefully, preserving the normal execution flow of the application instead of causing abrupt crashes.

### Objectives of Exception Handling:
- **Graceful Degradation:** Prevent abnormal program termination.
- **User-Friendly Error Messages:** Provide meaningful feedback to users instead of raw stack traces.
- **Resource Management:** Ensure critical resources (files, database connections, sockets) are properly closed even when errors occur.

---

## 📌 3. Java Exception Hierarchy

In Java, all exception and error types are subclasses of the root class `java.lang.Throwable`.

```
                    ┌─────────────────────────┐
                    │    java.lang.Throwable  │
                    └────────────┬────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
    ┌────────────┴───────────┐       ┌───────────┴────────────┐
    │   java.lang.Exception  │       │    java.lang.Error     │
    └────────────┬───────────┘       └────────────────────────┘
                 │                      (OutOfMemoryError,
      ┌──────────┴───────────┐           StackOverflowError)
      │                      │
┌─────┴──────────────┐ ┌─────┴────────────────────────┐
│ Checked Exceptions │ │ Unchecked Exceptions         │
└────────────────────┘ │ (java.lang.RuntimeException) │
 (IOException,         └──────────────────────────────┘
  SQLException)         (ArithmeticException,
                         NullPointerException,
                         ArrayIndexOutOfBoundsException)
```

![Checked and Unchecked Exceptions](Checked-and-Unchecked-exceptions-in-jaa.jpg)

### Core Components:
1. **`Throwable`**: The root class of the Java exception hierarchy. Only objects of this class (or its subclasses) can be thrown or caught.
2. **`Error`**: Represents severe conditions that reasonable applications should not try to catch (e.g., `OutOfMemoryError`, `StackOverflowError`). Usually caused by the environment or JVM failure.
3. **`Exception`**: Represents conditions that a reasonable application might want to catch and recover from.

---

## 📌 4. Checked vs Unchecked Exceptions

| Feature | Checked Exceptions | Unchecked Exceptions |
| :--- | :--- | :--- |
| **Inheritance** | Directly extends `java.lang.Exception` (excluding `RuntimeException`). | Extends `java.lang.RuntimeException`. |
| **Checking Time** | Checked at **compile time** by the compiler. | Occurs at **runtime**. |
| **Compiler Enforcement** | Compiler forces you to handle (`try-catch`) or declare (`throws`). | Compiler does not force handling or declaration. |
| **Cause** | External factors (file missing, network down, DB connection failed). | Programming logic errors (null references, bad indexing, math errors). |
| **Examples** | `IOException`, `SQLException`, `ClassNotFoundException`, `FileNotFoundException` | `ArithmeticException`, `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException` |

---

## 📌 5. Essential Keywords in Java Exception Handling

Java provides **five key keywords** to handle exceptions:

| Keyword | Description |
| :--- | :--- |
| **`try`** | Wraps the block of code that might throw an exception. Must be followed by `catch` or `finally`. |
| **`catch`** | Catches and handles specific exceptions thrown by the associated `try` block. |
| **`finally`** | Defines a block of code that is **always executed**, whether an exception occurs or not. Used for cleanup. |
| **`throw`** | Used to explicitly throw an exception object manually from a method or block. |
| **`throws`** | Used in a method signature to declare exceptions that the method might propagate caller-side. |

### Summary Code Example:
```java
public void processFile(String fileName) throws IOException {
    if (fileName == null) {
        throw new IllegalArgumentException("File name cannot be null");
    }
    
    try {
        // Code that might throw IOException
        FileReader reader = new FileReader(fileName);
    } catch (FileNotFoundException e) {
        System.err.println("File not found: " + e.getMessage());
    } finally {
        System.out.println("Processing attempt finished.");
    }
}
```

---

## 📌 6. Control Flow & Advanced Concepts

### A. Multiple Catch & Multi-Catch Blocks
- **Specific to General Rule:** Subclass exception types must be caught **before** superclass exception types.
- **Multi-Catch (Java 7+):** Catch multiple unrelated exceptions in a single `catch` block using the pipe (`|`) operator.

```java
// Multi-Catch Block Example
try {
    int result = array[0] / array[1];
} catch (ArithmeticException | ArrayIndexOutOfBoundsException e) {
    System.err.println("Invalid operation: " + e.getMessage());
}
```

### B. Exception Propagation
- Unchecked exceptions automatically propagate up the call stack until caught.
- If an exception reaches the `main()` method without being caught, the JVM terminates the thread.

### C. Try-With-Resources (Java 7+)
- Automatically closes resources implementing `java.lang.AutoCloseable` or `java.io.Closeable`.
- Eliminates boilerplate `finally` blocks for closing streams/readers.

```java
try (CustomResource resource = new CustomResource()) {
    resource.doOperation();
} catch (Exception e) {
    System.err.println("Error handling resource: " + e.getMessage());
}
// resource.close() is automatically called here
```

### D. Custom Exceptions
User-defined exceptions are created by extending `Exception` (for checked) or `RuntimeException` (for unchecked).

```java
public class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```

---

## 📌 7. Best Practices for Exception Handling

1. **Don't Swallow Exceptions:** Never leave catch blocks empty (`catch (Exception e) {}`). Always log or handle the error.
2. **Catch Specific Exceptions:** Catch specific exceptions (e.g., `FileNotFoundException`) instead of generic `Exception` or `Throwable`.
3. **Clean Up Resources:** Use **Try-With-Resources** or `finally` blocks to close file handles, DB connections, and network streams.
4. **Preserve Stack Traces:** When re-throwing exceptions, pass the original exception as the cause (`new CustomException("Failed", cause)`).
5. **Use Custom Exceptions Wisely:** Create custom exceptions for domain-specific errors to improve code readability and maintainability.