# Java Coding Standards Review Guide

**Version:** 1.0  
**Last Updated:** March 9, 2026  
**Target Java Version:** Java 8+  
**Project:** Java Learning & Experimentation Workspace

---

## 1. Overview

This document defines the Java coding standards for code review within this project. It can be used as a guide for manual code reviews and as instruction set for custom AI code review agents.

### Objectives
- Maintain consistent code style and structure across the project
- Ensure code readability and maintainability
- Promote Java best practices and design patterns
- Establish clear documentation standards
- Improve code quality and reduce technical debt

---

## 2. Naming Conventions

### 2.1 Package Naming
**Standard:** All lowercase, reverse domain notation, no underscores  
**Format:** `com.organization.project.module`

✅ **CORRECT:**
```java
package com.github.learn.java8.streams;
package com.kb.utils;
```

❌ **INCORRECT:**
```java
package com.github.Learn.java8.Streams;  // Mixed case
package github_utilities;                 // Underscore, no domain
```

---

### 2.2 Class Naming
**Standard:** PascalCase (UpperCamelCase)  
**Rules:**
- Start with uppercase letter
- Use whole words, avoid abbreviations
- Interfaces may use descriptive nouns or adjectives
- Exception classes should end with "Exception"
- Abstract classes may be prefixed with "Abstract"

✅ **CORRECT:**
```java
public class UserService { }
public class DataProcessor { }
public class InvalidInputException extends Exception { }
public interface Comparable { }
public abstract class BaseService { }
```

❌ **INCORRECT:**
```java
public class userService { }           // Lowercase start
public class UserServ { }              // Abbreviated
public class UserException { }         // Should end with Exception
public class user_service { }          // Underscore
```

---

### 2.3 Method Naming
**Standard:** camelCase (lowerCamelCase)  
**Rules:**
- Start with lowercase letter
- Use verbs for action methods
- Use "get", "set", "is", "has" prefixes for getters/setters/boolean methods
- Private methods should not be prefixed with underscores

✅ **CORRECT:**
```java
public void processData() { }
public String getUserName() { }
public void setUserName(String name) { }
public boolean isActive() { }
public boolean hasPermission() { }
private void validateInput() { }
```

❌ **INCORRECT:**
```java
public void ProcessData() { }          // Uppercase start
public String get_user_name() { }      // Underscore
public void _validateInput() { }       // Underscore prefix
public boolean getUserActive() { }     // Should use "isActive"
```

---

### 2.4 Variable and Field Naming
**Standard:** camelCase, meaningful names  
**Rules:**
- Use descriptive names that convey purpose
- Avoid single letters except for loop counters and coordinates
- Use uppercase for constants (CONSTANT_NAME)
- Avoid abbreviations unless universally understood (e.g., URL, ID)

✅ **CORRECT:**
```java
private String userName;
public static final int MAX_RETRIES = 3;
int itemCount = 0;
for (int i = 0; i < items.length; i++) { }  // Loop counter OK
boolean isValidated;
```

❌ **INCORRECT:**
```java
private String un;                     // Too abbreviated
private String userName2;              // Numbered suffix
public static final int max_retries;   // Underscore, not all caps
private String u_name;                 // Underscore
boolean valid;                         // Vague purpose
```

---

### 2.5 Constant Naming
**Standard:** ALL_CAPS_WITH_UNDERSCORES  
**Rules:**
- Only for truly static final values
- Use underscores to separate words
- Must be declared as `static final`

✅ **CORRECT:**
```java
public static final int DEFAULT_TIMEOUT = 5000;
private static final String API_KEY = "default";
public static final double PI = 3.14159;
```

❌ **INCORRECT:**
```java
public static final int defaultTimeout = 5000;  // Should be all caps
public int DEFAULT_VALUE = 10;                   // Not static/final
```

---

## 3. Code Structure & Organization

### 3.1 Class Organization
**Standard Order:**
1. Package declaration
2. Import statements (organized: static, then others, alphabetically)
3. Class documentation (Javadoc)
4. Class declaration
5. Static constants
6. Static variables
7. Instance constants
8. Instance variables
9. Constructors
10. Public methods (grouped by functionality)
11. Protected methods
12. Package-private methods
13. Private methods
14. Inner classes

✅ **CORRECT:**
```java
package com.github.learn;

import java.util.*;
import java.io.*;

/**
 * UserService handles user-related operations.
 */
public class UserService {
    private static final int MAX_USERS = 1000;
    private List<User> users;
    
    public UserService() {
        this.users = new ArrayList<>();
    }
    
    public void addUser(User user) {
        // implementation
    }
    
    private void validateUser(User user) {
        // implementation
    }
}
```

---

### 3.2 File Length
**Standard:** Maximum 500 lines per file  
**Guideline:** 
- Single responsibility per class
- If file exceeds 300 lines, consider refactoring
- Extract inner classes, interfaces, or helper classes

---

### 3.3 Method Length
**Standard:** Maximum 50 lines per method  
**Guideline:**
- Ideally under 30 lines
- Each method should do one thing
- Extract complex logic into helper methods

✅ **CORRECT:**
```java
public boolean processOrder(Order order) {
    if (!validateOrder(order)) {
        return false;
    }
    chargePayment(order);
    shipOrder(order);
    return true;
}

private boolean validateOrder(Order order) {
    return order != null && order.hasItems();
}
```

❌ **INCORRECT:**
```java
public boolean processOrder(Order order) {
    // 80+ lines of validation, payment, shipping logic all mixed
}
```

---

### 3.4 Line Length
**Standard:** Maximum 120 characters per line  
**Guideline:** Aim for 100 characters for better readability

---

## 4. Documentation Standards

### 4.1 Class Documentation
**Requirement:** All public classes must have Javadoc

✅ **CORRECT:**
```java
/**
 * Represents a user in the system.
 * 
 * This class handles user profile information including name,
 * email, and status.
 * 
 * @author Development Team
 * @version 1.0
 */
public class User {
    // ...
}
```

---

### 4.2 Method Documentation
**Requirement:** All public methods must have Javadoc

✅ **CORRECT:**
```java
/**
 * Retrieves a user by their ID.
 * 
 * @param userId the unique identifier of the user
 * @return the User object if found, null otherwise
 * @throws IllegalArgumentException if userId is negative
 */
public User getUserById(int userId) {
    // implementation
}
```

---

### 4.3 Field Documentation
**Requirement:** Public and protected fields must have Javadoc comments

✅ **CORRECT:**
```java
/** The maximum number of retry attempts. */
public static final int MAX_RETRIES = 3;

/** List of active users in the system. */
private List<User> activeUsers;
```

---

### 4.4 Complex Logic Comments
**Requirement:** Explain "why", not "what"  
**Guidelines:**
- Comments should explain business logic or non-obvious implementation
- Avoid commenting obvious code
- Use // for single-line comments, /* */ for multi-line

✅ **CORRECT:**
```java
// Sort by creation date descending, as newer entries have higher priority
Collections.sort(entries, (a, b) -> b.getCreatedDate().compareTo(a.getCreatedDate()));
```

❌ **INCORRECT:**
```java
// Loop through items
for (Item item : items) {
    // Check if item is active
    if (item.isActive()) {
        // Print item
        System.out.println(item);
    }
}
```

---

## 5. Formatting & Style

### 5.1 Indentation
**Standard:** 4 spaces per indentation level  
**Rule:** Never use tabs; use spaces only

---

### 5.2 Braces
**Standard:** Opening braces on same line (Java style)

✅ **CORRECT:**
```java
public void method() {
    if (condition) {
        doSomething();
    }
}
```

❌ **INCORRECT:**
```java
public void method()
{
    if (condition)
    {
        doSomething();
    }
}
```

---

### 5.3 Spacing
**Rules:**
- One blank line between methods
- One blank line between logical sections within a method
- Space after keywords: `if`, `for`, `while`, `catch`
- Space around binary operators: `+`, `-`, `==`, `!=`
- No space after method/function names

✅ **CORRECT:**
```java
public void calculate() {
    int result = a + b;
    
    if (result > 0) {
        process(result);
    }
    
    return result;
}
```

---

### 5.4 Import Organization
**Standard:** 
1. All static imports
2. All java.* imports
3. All javax.* imports
4. All other imports
5. All project-specific imports
Each group separated by blank line, alphabetically sorted within groups

✅ **CORRECT:**
```java
import static java.lang.Math.*;

import java.util.*;
import java.io.*;

import javax.persistence.*;

import com.github.learn.models.*;
import com.github.learn.utils.*;
```

---

## 6. Exception Handling

### 6.1 Exception Catching
**Rules:**
- Catch specific exceptions, never catch generic Exception
- Always handle caught exceptions (log or re-throw)
- Use try-with-resources for AutoCloseable resources

✅ **CORRECT:**
```java
try (FileInputStream fis = new FileInputStream(file)) {
    // process file
} catch (FileNotFoundException e) {
    logger.error("File not found", e);
} catch (IOException e) {
    logger.error("IO error occurred", e);
}
```

❌ **INCORRECT:**
```java
try {
    // code
} catch (Exception e) {  // Too generic
    e.printStackTrace();  // Bad practice
}
```

---

### 6.2 Custom Exceptions
**Standard:** Create specific exception classes for your domain

✅ **CORRECT:**
```java
/**
 * Thrown when user validation fails.
 */
public class UserValidationException extends Exception {
    public UserValidationException(String message) {
        super(message);
    }
    
    public UserValidationException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

---

### 6.3 Exception Messages
**Rule:** Provide clear, actionable error messages

✅ **CORRECT:**
```java
throw new IllegalArgumentException("User ID must be positive integer, received: " + userId);
```

❌ **INCORRECT:**
```java
throw new Exception("Error");
throw new IllegalArgumentException("Invalid");
```

---

## 7. Type Safety & Generics

### 7.1 Raw Types
**Rule:** Never use raw types; always specify generic parameters

✅ **CORRECT:**
```java
List<String> names = new ArrayList<>();
Map<Integer, User> userMap = new HashMap<>();
```

❌ **INCORRECT:**
```java
List names = new ArrayList();  // Raw type
Map userMap = new HashMap();   // Raw type
```

---

### 7.2 Wildcard Usage
**Rule:** Use bounded wildcards when appropriate

✅ **CORRECT:**
```java
public void printList(List<? extends Number> list) {
    for (Number num : list) {
        System.out.println(num);
    }
}

public void addNumbers(List<? super Integer> list) {
    list.add(10);
}
```

---

## 8. Object-Oriented Design

### 8.1 Encapsulation
**Rule:** Fields should be private; expose through public methods only

✅ **CORRECT:**
```java
public class User {
    private String name;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = Objects.requireNonNull(name);
    }
}
```

❌ **INCORRECT:**
```java
public class User {
    public String name;  // Direct access
}
```

---

### 8.2 Immutability
**Rule:** Prefer immutable objects; mark constants as `final`

✅ **CORRECT:**
```java
public final class Point {
    private final int x;
    private final int y;
    
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

---

### 8.3 Inheritance vs Composition
**Rule:** Favor composition over inheritance

✅ **CORRECT:**
```java
public class Engine {
    private String type;
}

public class Car {
    private Engine engine;  // Composition
}
```

❌ **QUESTIONABLE:**
```java
public class Car extends Engine {  // Inheritance without clear "is-a" relationship
}
```

---

## 9. Performance & Best Practices

### 9.1 Null Checking
**Rule:** Use Objects.requireNonNull() or Optional for null-safety

✅ **CORRECT:**
```java
public void setName(String name) {
    this.name = Objects.requireNonNull(name, "Name cannot be null");
}

public Optional<User> findUser(int id) {
    return userRepository.findById(id);
}
```

---

### 9.2 String Operations
**Rule:** Use StringBuilder for concatenation in loops

✅ **CORRECT:**
```java
StringBuilder sb = new StringBuilder();
for (String item : items) {
    sb.append(item).append(",");
}
```

❌ **INCORRECT:**
```java
String result = "";
for (String item : items) {
    result += item + ",";  // Creates new String each iteration
}
```

---

### 9.3 Collections
**Rule:** Use appropriate collection types; initialize with capacity

✅ **CORRECT:**
```java
List<String> names = new ArrayList<>(100);
Set<Integer> ids = new HashSet<>(50);
```

❌ **INCORRECT:**
```java
List<String> names = new ArrayList<>();
List<String> ids = new ArrayList<>();  // Wrong type for unique IDs
```

---

### 9.4 Streams (Java 8+)
**Rule:** Use streams for functional operations, not side effects

✅ **CORRECT:**
```java
List<Integer> even = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
```

❌ **INCORRECT:**
```java
numbers.stream()
    .forEach(n -> {
        if (n % 2 == 0) {
            results.add(n);  // Side effect in stream
        }
    });
```

---

## 10. Security Considerations

### 10.1 Input Validation
**Rule:** Always validate external input

✅ **CORRECT:**
```java
public void processUserInput(String input) {
    if (input == null || input.trim().isEmpty()) {
        throw new IllegalArgumentException("Input cannot be empty");
    }
    // process
}
```

---

### 10.2 SQL Injection Prevention
**Rule:** Use PreparedStatements, never concatenate SQL strings

✅ **CORRECT:**
```java
PreparedStatement ps = connection.prepareStatement("SELECT * FROM users WHERE id = ?");
ps.setInt(1, userId);
```

❌ **INCORRECT:**
```java
String query = "SELECT * FROM users WHERE id = " + userId;  // SQL injection risk
```

---

### 10.3 Sensitive Data
**Rule:** Don't log sensitive information (passwords, tokens, PII)

✅ **CORRECT:**
```java
logger.info("User login attempted for email: {}.", maskedEmail);
```

---

## 11. Code Review Severity Levels

When using this guide for automated code review, categorize findings as:

### CRITICAL 🔴
- Security vulnerabilities (SQL injection, hard-coded credentials)
- Missing null checks for nullability violations
- Raw types usage
- Resource leaks (unclosed streams, connections)
- Catch generic Exception

### WARNING 🟡
- Violation of naming conventions
- Missing Javadoc for public methods/classes
- Methods exceeding 50 lines
- Files exceeding 500 lines
- Inconsistent code style

### INFO ℹ️
- Suggestions for improvement
- Use of immutability opportunities
- Stream vs loop optimization suggestions
- Code clarity improvements

---

## 12. Checklist for Code Review

### Pre-Submission Review Checklist
- [ ] Class and method names follow PascalCase/camelCase conventions
- [ ] All public classes and methods have Javadoc
- [ ] No raw types used in generics
- [ ] No catch(Exception) blocks
- [ ] Resources properly closed (try-with-resources)
- [ ] No null pointer dereferences without null checks
- [ ] Methods under 50 lines
- [ ] No hardcoded values (use constants)
- [ ] Input validation present for external data
- [ ] No console.log/println in production code (use logging framework)
- [ ] Code follows 4-space indentation
- [ ] Imports organized and no unused imports
- [ ] Meaningful variable names used
- [ ] No commented-out code blocks

---

## 13. Agent Directives for Automated Review

### When using this guide as a custom agent instruction:

1. **Scope:** Review Java files in src/ directory
2. **Report Format:** 
   - File: [path/to/file.java]
   - Line: [line number]
   - Issue: [violation description]
   - Severity: CRITICAL | WARNING | INFO
   - Suggestion: [recommended fix]

3. **Output Format:**
   ```
   JAVA CODE REVIEW REPORT
   =======================
   File: src/com/github/copilot.java
   
   [CRITICAL] Line 5: Class name 'copilot' violates PascalCase convention. 
   Suggestion: Rename to 'Copilot'
   
   [WARNING] Line 10-15: Method missing Javadoc documentation.
   Suggestion: Add Javadoc describing method purpose, parameters, and return value.
   ```

4. **Agent Behavior:**
   - Flag all violations with severity level
   - Provide specific line numbers
   - Suggest concrete fixes
   - Prioritize CRITICAL issues
   - Group by file and severity

---

## 14. Exceptions to Standards

Circumstances where standards may be relaxed:
- Legacy code migration (temporary waivers)
- Performance-critical code sections (with explicit justification)
- Third-party code or generated code (may have different standards)
- Experimental/prototype code (should migrate to standards before production)

All exceptions must be documented with justification in code comments.

---

## Revision History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | March 9, 2026 | Initial comprehensive standard guide |

---

## References

- [Java Code Style Guide - Google](https://google.github.io/styleguide/javaguide.html)
- [Oracle Java Code Conventions](https://www.oracle.com/java/technologies/)
- [Effective Java by Joshua Bloch](https://www.oreilly.com/library/view/effective-java-third/9780134685991/)
- [Java 21 Documentation](https://docs.oracle.com/en/java/javase/21/)

---

**Note:** This document should be reviewed and updated quarterly or whenever significant changes to project standards are decided.
