<h1 align="center">☕ Exception Handling in Java</h1>

<p align="center">
  <b>A comprehensive hands-on guide and code repository covering fundamental to advanced Java Exception Handling concepts.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Java-17%2B-orange?style=for-the-badge&logo=openjdk" alt="Java Version" />
  <img src="https://img.shields.io/badge/Eclipse-IDE-purple?style=for-the-badge&logo=eclipseide" alt="Eclipse IDE" />
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License" />
</p>

---

## 📖 Overview

Exception handling is a critical mechanism in Java that ensures applications handle unexpected runtime conditions gracefully without crashing. This repository provides step-by-step code demonstrations (**Demo0** through **Demo8**), illustrating how exceptions occur, how they propagate, and how to effectively catch, handle, throw, and manage resources using modern Java best practices.

---

## 📂 Repository Structure & Modules Breakdown

The project is structured into incremental demo projects, each highlighting a specific aspect of exception handling:

| Module | Topic / Focus | Description |
| :--- | :--- | :--- |
| **`Demo0`** | **Scenario Without Exception Handling** | Demonstrates abrupt program termination when unhandled exceptions (e.g., division by zero) occur. |
| **`Demo1`** | **Basic Try-Catch Blocks** | Introduces basic exception catching using `try` and `catch` blocks to prevent crashes. |
| **`Demo2`** | **Printing Exception Messages** | Demonstrates different techniques for extracting error details: `getMessage()`, `toString()`, and `printStackTrace()`. |
| **`Demo3`** | **Multiple Catch & Multi-Catch** | Explains handling multiple specific exceptions separately vs using Java 7+ multi-catch syntax (`catch (ExA \| ExB e)`). |
| **`Demo4`** | **Exception Propagation** | Shows how unchecked exceptions automatically travel up the call stack to parent methods. |
| **`Demo5`** | **The `throw` Keyword** | Explains explicit exception throwing using the `throw` keyword. |
| **`Demo6`** | **The `throws` Keyword** | Demonstrates method signature declarations using `throws` to delegate exception handling to caller methods. |
| **`Demo7`** | **`finally` & Try-With-Resources** | Compares classic resource cleanup in `finally` blocks with Java 7+ Automatic Resource Management (`AutoCloseable`). |
| **`Demo8`** | **Custom Exceptions** | Guides you through building user-defined application exception classes (e.g., `ScaleUpIndiaException`). |

---

## 💡 Key Exception Handling Concepts

### 1. Throwable Hierarchy

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

![Checked vs Unchecked Exceptions](Checked-and-Unchecked-exceptions-in-jaa.jpg)

### 2. Core Keywords Summary

- **`try`**: Defines a block of code to monitor for exceptions.
- **`catch`**: Handles specific exceptions caught from the corresponding `try` block.
- **`finally`**: Guarantees code execution regardless of whether an exception was thrown or caught (ideal for cleanup).
- **`throw`**: Used to explicitly throw an exception object from any method or block.
- **`throws`**: Used in method signatures to declare exceptions that may be propagated to the caller.

---

## 🎓 Summary of Module Demos

### 🔴 Demo0: Scenario Without Exception Handling
```java
// Division without try-catch results in abrupt program crash if denominator is 0
int quotient = array[0] / array[1]; 
```

### 🟢 Demo1 & Demo2: Try-Catch & Exception Details
```java
try {
    int quotient = array[0] / array[1];
} catch (ArithmeticException e) {
    System.out.println("Message: " + e.getMessage());
    System.out.println("String representation: " + e.toString());
    e.printStackTrace();
}
```

### 🟡 Demo3: Multi-Catch Block (Java 7+)
```java
try {
    int quotient = array[0] / array[1];
} catch (ArithmeticException | ArrayIndexOutOfBoundsException e) {
    System.out.println("Handling arithmetic or array index error: " + e.getMessage());
}
```

### 🔵 Demo7: Try-With-Resources (AutoCloseable)
```java
// Automatic resource cleanup without explicit finally block
try (CustomResource resource = new CustomResource()) {
    resource.doOperation();
} catch (Exception e) {
    System.out.println("Error: " + e.getMessage());
}
```

### 🟣 Demo8: Custom Exceptions
```java
// User-defined Exception class
public class ScaleUpIndiaException extends Exception {
    public ScaleUpIndiaException(String message) {
        super(message);
    }
}
```

---

## ⚙️ Prerequisites & Setup

- **Java Development Kit (JDK):** Version 17 or higher (JDK 21 recommended)
- **IDE:** Eclipse IDE, IntelliJ IDEA, VS Code, or Spring Tool Suite (STS)
- **Git:** Installed on your local machine

---

## 🚀 How to Run

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/aashiqui2/Exception-Handling.git
   ```
2. **Open in IDE:**
   - Open Eclipse / IntelliJ / VS Code / STS.
   - Import the project or sub-modules (`Demo0` to `Demo8`).
3. **Execute Demos:**
   - Navigate to `src/com/main/Demo.java` in any demo folder.
   - Right-click `Demo.java` ➡️ **Run As** ➡️ **Java Application**.

---

## 📝 Learning Materials

- Check out **[Notes.md](Notes.md)** for exhaustive theoretical notes, comparative tables, and exception handling best practices.

---

## 🎥 Video Tutorials & Social Links

Detailed video walkthroughs are featured on the YouTube channel:  
📺 **[@CodeWithAashiq](https://www.youtube.com/@codewithaashiq)**

### 🌐 Connect with Me

<div align="left">
  <a href="https://github.com/aashiqui2" target="_blank">
    <img src="https://img.shields.io/static/v1?message=GitHub&logo=github&label=&color=181717&logoColor=white&style=for-the-badge" height="35" alt="GitHub" />
  </a>
  <a href="https://www.linkedin.com/in/aashiqui" target="_blank">
    <img src="https://img.shields.io/static/v1?message=LinkedIn&logo=linkedin&label=&color=0A66C2&logoColor=white&style=for-the-badge" height="35" alt="LinkedIn" />
  </a>
  <a href="mailto:ashikmail2747@gmail.com">
    <img src="https://img.shields.io/static/v1?message=Gmail&logo=gmail&label=&color=EA4335&logoColor=white&style=for-the-badge" height="35" alt="GMail" />
  </a>
</div>

---

<p align="center"><b>🚀 Keep coding, keep learning, and build resilient Java applications!</b></p>
<p align="center">Copyright © 2025 <b>Aashiq</b> — All Rights Reserved</p>
