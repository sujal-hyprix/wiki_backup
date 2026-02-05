---
title: Coding standards
description: 
published: true
date: 2026-01-29T06:42:16.337Z
tags: 
editor: markdown
dateCreated: 2026-01-23T09:28:40.599Z
---

# NASA/GSFC C Style Guide (SEL-94-003)

# 1. Introduction

"Good programming style begins with the effective organization of code. By using a clear and consistent organization of the components of your programs, you make them more efficient, readable, and maintainable." — Steve Oualline, *C Elements of Style*.

## 1.1 Purpose
This document describes the Software Engineering Laboratory (SEL) recommended style for writing C programs, where code with "good style" is defined as that which is:
*   Organized
*   Easy to read
*   Easy to understand
*   Maintainable
*   Efficient

## 1.2 Audience
This document was written specifically for programmers in the SEL environment, although the majority of these standards are generally applicable to all environments. We assume that you have a working knowledge of C; we focus on pointing out good practices that will enhance the effectiveness of your C code.

## 1.3 Approach
This document provides guidelines for organizing the content of C programs, files, and functions. It discusses the structure and placement of variables, statements, and comments.
*   Software engineering principles are discussed and illustrated.
*   Key concepts are highlighted.
*   Code examples are provided to illustrate good practices.

***

# 2. Readability and Maintainability

This section summarizes general principles that maximize the readability and maintainability of C code:
*   Organize programs using encapsulation and information hiding techniques.
*   Enhance readability through the use of white space.
*   Add comments to help others understand your program.
*   Create names that are meaningful and readable.
*   Follow ANSI C standards, when available.

## 2.1 Encapsulation and Information Hiding
Encapsulation and information hiding techniques can help you write better organized and maintainable code. **Encapsulation** means grouping related elements. You can encapsulate on many levels:
*   Organize a program into files (e.g., using header files).
*   Organize files into data sections and function sections.
*   Organize functions into logically related groups within individual files.
*   Organize data into logical groups (data structures).

**Information hiding** refers to controlling the visibility (or scope) of program elements.
*   Encapsulate related information in header files, and then include those header files only where needed.
*   Use `static` for external definitions used only in the current file to limit scope.
*   Use `extern` only as needed in individual functions.

## 2.2 White Space
Write code that is as easy as possible to read and maintain. Adding white space in the form of blank lines, spaces, and indentation will significantly improve the readability of your code.

### 2.2.1 Blank Lines
A careful use of blank lines between code "paragraphs" can greatly enhance readability by making the logical structure of a sequence of lines more obvious. Use a single blank line to separate parts of your program from one another; overuse can defeat the purpose of grouping.

### 2.2.2 Spacing
Appropriate spacing enhances the readability of lexical elements such as variables and operators.
*   Put one space after a comma.
*   Put spaces around binary operators (e.g., `total / count`).

### 2.2.3 Indentation
Use indentation to show the logical structure of your code. Research has shown that **four spaces** is the optimum indent for readability and maintainability. Use four spaces unless other circumstances make it unworkable (e.g., highly nested code with long variable names).

## 2.3 Comments
Judiciously placed comments in the code can provide information that a person could not discern simply by reading the code.
*   **Program level:** Include a README file describing the program and organization.
*   **File level:** Include a file prolog explaining the purpose of the file.
*   **Function level:** A comment can serve as a function prolog.
*   **Variable level:** Add comments to explain the purpose of variables where declared.

**Styles:**
*   **Boxed comments:** Use for prologs or section separators.
*   **Block comments:** Use at the beginning of major code sections for narrative descriptions.
*   **Short comments:** Write on the same line as the code or data definition.
*   **Inline comments:** Write at the same level of indentation as the code they describe.

*Note:* If more than one short comment appears in a block, start all of them at the same tab position. Do not paraphrase the code.

## 2.4 Meaningful Names
Choose names for files, functions, constants, or variables that are meaningful and readable.
*   Choose names with precise meanings and use them consistently.
*   Follow a uniform scheme when abbreviating names (e.g., `dr_` prefix for "data refresher").
*   Avoid misleading abbreviations (e.g., `in_char` is better than `inch`).
*   Use underscores to improve readability (e.g., `get_best_fit_model`).
*   Assign unique names.
*   Names more than four characters in length should differ by at least two characters.
*   Do not rely on letter case to make a name unique (C is case sensitive, but mixed case names with same spelling are confusing).
*   Do not assign a variable and a typedef/struct the same name.

### 2.4.1 Standard Names
While standard short names (e.g., `c` for characters, `i,j,k` for indices, `p` for pointers) are acceptable if their meaning is clear, longer explicit names are recommended (e.g., `buffer_index`).

### 2.4.2 Variable Names
Do not duplicate global variable names with internal variable names (creates hidden variables). Use unique names to avoid confusion.

### 2.4.3 Capitalization
*   **Variables:** Lower-case words separated by underscores (e.g., `open_database`).
*   **Function names:** Capitalize the first letter of each word; no underscores (e.g., `ProcessError`).
*   **Constants:** Upper-case words separated by underscores (e.g., `MAX_COUNT`).
*   **C bindings:** Use the letter "c" followed by an underscore (e.g., `c_ephemrd`).

### 2.4.4 Type and Constant Names
*   **Typedefs:** Follow naming standards for global variables.
*   **Enumeration types/Constants:** Follow naming conventions for constants.

***

# 3. Program Organization

This section discusses organizing program code into files, grouping logically related functions and data, and controlling visibility.

## 3.1 Program Files
A C program consists of one or more program files. One contains the `main()` function, acting as the driver. Group the main function with other logically related functions in a program file.

## 3.2 README File
A README file should be used to explain what the program does, how it is organized, machine dependencies, and compilation flags.

## 3.3 Standard Libraries
Include only those libraries that contain functions your program needs. Standard libraries include `stdio.h` (I/O) and `math.h` (math functions).

## 3.4 Header Files
Header files encapsulate logically related ideas (defines, typedefs, structures, function declarations).
*   Use `#include <system_name>` for system files.
*   Use `#include "user_file"` for user files.
*   Organize header files by function.
*   Do not nest header files; use explicit includes in the program file.
*   Include header files in the file that defines the function/variable to ensure the declaration agrees with the definition.

## 3.5 Module Files
A module file contains logically related functions, constants, types, and data without the `main()` function.

## 3.6 Makefiles
Makefiles provide a mechanism for efficiently recompiling C code. They list all files included in the program, contain comments documenting library contents, and demonstrate dependencies.

## 3.7 Standard Filename Suffixes
*   `.c`: C source file
*   `.s`: Assembler source
*   `.o`: Relocatable object
*   `.h`: Include header
*   `.mak`: Makefile.

***

# 4. File Organization

The organization of information within a file is critical for readability.

**Standard Order:**
1.  File Prolog
2.  Header File Includes
3.  Defines and Typedefs
4.  External Data Declarations
5.  Functions (Prolog, Body)

## 4.1 File Prolog
Every file must have a prolog introduced by a boxed comment. It should include:
*   File Name and Purpose.
*   File References (I/O).
*   External Variables (Source, Name, Type, I/O, Description).
*   External References (Unit called).
*   Abnormal Termination Conditions/Error Messages.
*   Assumptions, Constraints, Restrictions.
*   Development History (Date, Author, Change ID, Release, Description).
*   Algorithm (PDL).

## 4.2 Program Algorithm and PDL
The prolog describes the algorithm using Program Design Language (PDL).
*   Indent by four spaces within control structures.
*   Align keywords (IF, ELSE).

### 4.2.1 Sequence Statements
Declarative English sentences (verb + object). Assignment statements used only for math formulas.
*   `CALL <unit name>`
*   `RETURN`

### 4.2.2 Selection Control Statements
*   **4.2.2.1 IF THEN ELSE:** `IF condition THEN ... ELSE ... ENDIF`.
*   **4.2.2.2 IF THEN:** `IF condition THEN ... ENDIF`.
*   **4.2.2.3 CASE:** `DO CASE of (name) ... CASE 1 condition: ... ENDDO CASE`.

### 4.2.3 Iteration Control Statements
*   **4.2.3.1 DO WHILE:** `DO WHILE condition true ... ENDDO WHILE`.
*   **4.2.3.2 DO FOR:** `DO FOR specified items ... ENDDO FOR`.
*   **4.2.3.3 DO UNTIL:** `DO UNTIL exit condition true ... ENDDO UNTIL`.

### 4.2.4 Severe Error and Exception Handling Statements
*   **4.2.4.1 ABORT:** `ABORT to (label)`. Used to jump to error processing at the end of a routine.
*   **4.2.4.2 UNDO:** Terminate current loop immediately (jumps to statement following ENDDO).

## 4.3 Include Directive
Include only necessary headers. Suggested order: `<stdio.h>`, other system headers, "user header files".

## 4.4 Defines and Typedefs
Define constants, types, and macros available to the rest of the file in this sequence: Enums, Typedefs, Constant macros, Function macros.

## 4.5 External Data Declarations and Definitions
Sequence:
1.  Extern declarations (from other files).
2.  Non-static external definitions (global to program).
3.  Static external definitions (local to file).

## 4.6 Sequence of Functions
*   `main()` should be first if present.
*   Place logically related functions in the same file.
*   Use breadth-first approach (abstraction levels) or alphabetical order for utility functions.
*   Place functions last in the file unless data hiding requires variables between them.

***

# 5. Function Organization

## 5.1 Function Prologs
Every function should have a prolog containing:
*   Function Name.
*   Arguments (Type, I/O, Description).
*   Return value description.
*   *Naming:* Imperative verb phrase (e.g., `obtain_next_token`) or predicate-clause for boolean (e.g., `stack_is_empty`).

## 5.2 Function Arguments
Declare arguments when the function is defined, beginning in column 1.

## 5.3 External Variable Declarations
Declare external variables immediately after the opening brace of the function block.

## 5.4 Internal Variable Declarations
*   Define after external variables.
*   Align first letters of names.
*   One variable per line with a comment (except loop indices).
*   Avoid hidden variables (overriding higher-level names).

## 5.5 Statement Paragraphing
Use blank lines to separate groups of related statements.

## 5.6 Return Statement
*   Any expression can follow return.
*   Prefer a single return statement at the end of the function.
*   Always declare return type (use `void` if none).
*   Parenthesize the return expression: `return (found);`.

***

# 6. Data Types, Operators, and Expressions

## 6.1 Variables
*   Define one variable per line with a comment.
*   Group related variables.

## 6.2 Constants
*   Capitalize constant names.
*   **6.2.1 Const Modifier:** Preferred for simple constants (allows type checking).
*   **6.2.2 #define Command:** Avoid for simple constants; use for string tokens.
*   **6.2.3 Enumeration Types:** Use for associated constant names/values.

## 6.3 Variable Definitions and Declarations
*   **6.3.1 Numbers:** Floating point must have digits on both sides (e.g., `0.5`). Hex starts with `0x` and uses uppercase `A-F`. Long constants end in `L`.
*   **6.3.2 Qualifiers:** Always associate qualifiers (short, long, unsigned) with basic types.
*   **6.3.3 Structures:** Use `typedef` to define structures. Common structures enhance efficiency.
*   **6.3.4 Automatic Variables:** Initialize where declared if used nearby.

## 6.4 Type Conversions and Casts
Use explicit casts rather than implicit conversions.

## 6.5 Pointer Types
Put the pointer qualifier (`*`) with the variable name, not the type (e.g., `char *s;`).

## 6.6 Pointer Conversions
Avoid, except for `NULL` (0), allocation (`malloc`), and size changes (pointer-to-char conversions).

## 6.7 Operator Formatting
*   No space around `->`, `.`, `[]`.
*   No space before parentheses following function names.
*   No space between unary operators and operands (`!p`, `++i`).
*   Space between cast and operand: `(long) m`.
*   Space around assignment (`=`) and conditional (`? :`) operators.
*   Space after commas and semicolons.
*   Space around binary operators (`+`, `<`, etc.).

## 6.8 Assignment Operators and Expressions
*   Avoid side-effect operators in relational expressions.
*   Use parentheses liberally to indicate precedence.
*   Use embedded assignments sparingly.

## 6.9 Conditional Expressions
Use conditional expressions (`z = (a>b) ? a : b;`) only if readable. Do not use for complex algorithms.

## 6.10 Precedence and Order of Evaluation
Remember: `* % /` come before `+ -`. Put `()` around everything else.

***

# 7. Statements and Control Flow

## 7.1 Sequence Statements
### 7.1.1 Statement Placement
Put only one statement per line. Avoid side-effects (`++`) in other statements.

### 7.1.2 Braces
*   Use the **Braces-Stand-Alone** method (braces on separate lines, aligned).
*   Use braces even for single statements in loops/conditionals to improve readability.
*   Comment closing braces on large blocks.

## 7.2 Selection Control Statements
### 7.2.1 If
Indent single statements one level. Use braces for blocks.

### 7.2.2 If Else
Indent the `else` statement. Use braces if the body is compound.

### 7.2.3 Else If
Format as:
```c
if (expression)
    statement;
else if (expression)
    statement;
else
    statement;
```


### 7.2.4 Nested If Statements
*   **7.2.4.1 If/If/If:** Use nested ifs for alternative actions or undoing actions. Avoid inappropriate nesting.
*   **7.2.4.2 If/If/Else:** Always use braces to associate the `else` with the correct `if` to avoid ambiguity.

### 7.2.5 Switch
Indent cases. Always include a `default` case. Comment fall-throughs.

## 7.3 Iteration Control Statements
### 7.3.1 While
Format:
```c
while (expression)
{
    statement;
}
```


### 7.3.2 For
Split into three lines if it does not fit on one.

### 7.3.3 Do While
Format:
```c
do
{
    statement;
} while (expression);
```


## 7.4 Severe Error and Exception Handling
### 7.4.1 Gotos and Labels
Use very sparingly. Useful primarily for breaking out of deep nesting.

### 7.4.2 Break
Use to exit a loop at a logical breaking point. Avoid if possible.

***

# 8. Portability and Performance

## 8.1 Guidelines for Portability
*   Use ANSI C whenever available.
*   Write portable code first; optimize only when necessary.
*   Isolate machine-dependent code in separate files.
*   Do not assume word sizes (use `sizeof` or typedefs like `int32`).
*   Avoid code relying on two's complement or byte ordering.
*   Use `#ifdef` to conceal non-portable quirks.

## 8.2 Guidelines for Performance
*   Write readable code first.
*   Minimize opens/closes and I/O.
*   Free memory as soon as possible.
*   Pass structures by pointer to save stack space and time.
*   Use ANSI C structure assignment instead of copying fields.

***

# 9. C Code Examples

This section in the document contains full code listings illustrating the principles.
*   **9.1 Makefile:** Demonstrates building multiple executables and dependencies.
*   **9.2 C Program File (`RF_GetReference.c`):** Illustrates file prologs, function prologs, PDL, headers, and spacing.
*   **9.3 Include File (`HD_reference.h`):** Illustrates definition and organization of constants, structures, and external variables.