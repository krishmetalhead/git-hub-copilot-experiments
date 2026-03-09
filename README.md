# Java821Features - Fibonacci Series Generator

## Overview
Java821Features is a simple Java project that demonstrates fundamental programming concepts through a Fibonacci sequence generator. The project is built and managed using Eclipse IDE with Java Development Tools (JDT).

## Project Structure
```
Java821Features/
├── src/
│   └── com/github/
│       └── copilot.java          # Main Fibonacci series implementation
├── bin/                           # Compiled class files
├── docs/
│   └── JAVA_CODING_STANDARDS.md  # Java coding guidelines
├── .project                       # Eclipse project configuration
├── .classpath                     # Eclipse classpath configuration
└── .settings/                     # Eclipse IDE settings
```

## Features
- **Fibonacci Series Generation**: Generates and prints the first N terms of the Fibonacci sequence
- **Iterative Approach**: Uses an efficient loop-based implementation with minimal memory overhead
- **Simple Output**: Displays terms separated by commas for easy readability

## How to Run
1. **Using Eclipse IDE**:
   - Open Eclipse and import the project
   - Navigate to `src/com/github/copilot.java`
   - Right-click and select "Run As" → "Java Application"

2. **Via Command Line**:
   ```bash
   cd src
   javac com/github/copilot.java
   java com.github.copilot
   ```

## Configuration
- **Default Terms**: Generates 10 terms of the Fibonacci sequence
- **Starting Values**: Begins with 0 and 1 (classic Fibonacci)
- **To Modify**: Edit the `n` variable in the `main()` method to generate a different number of terms

## Dependencies
- **Java Version**: Compatible with Java 8 and later
- **Build Tool**: Eclipse IDE with JDT (Java Development Tools)
- **External Libraries**: None

## Coding Standards
The project adheres to Java coding standards as documented in `docs/JAVA_CODING_STANDARDS.md`. Follow these guidelines when extending or modifying the codebase.

## Example Output
```
Fibonacci Series till 10 terms:
0, 1, 1, 2, 3, 5, 8, 13, 21, 34,
```

## Future Enhancements
- Add recursive implementation option
- Support for dynamic user input
- Memoization for performance optimization
- Unit tests for validation

---
**Last Updated**: March 9, 2026
