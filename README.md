# MiniJava to LLVM-IR Compiler

This project implements a compiler for the MiniJava language in Java.
It performs lexical analysis, parsing, semantic checks, and generates
LLVM intermediate representation files that can be compiled with tools
like Clang to produce executable binaries.

This was a semester project for the University of Athens Compilers course.

### Compilation:
- Run `make` for compiling all files
- Run `make clean` for cleaning all generated files

### Execution: 
- Run `java Main <file1> <file2>... ` to run for multiple files

### Features

- **Semantic analysis with detailed error reporting**  
  The compiler detects semantic errors and reports the exact source line
  and error description. If no errors are found, it computes and prints
  memory offsets for all classes, methods, and variables.

- **Global symbol table for class information**  
  A central data structure stores all class metadata and is shared across
  compiler visitors. This symbol table is used to compute offsets and
  enforce semantic correctness.

- **Virtual table (vtable) construction with inheritance support**  
  Method dispatch is implemented using virtual tables. For subclasses,
  inherited methods are placed first, followed by methods defined in the
  subclass, preserving correct overriding behaviour.

### Compiler Visitors

The compiler is implemented using the **Visitor design pattern** and is
structured into four main visitors, each responsible for a distinct
compilation phase:

- **ClassNameVisitor**  
  Collects all class declarations and their formal parameters.

- **MethodNameVisitor**  
  Collects class fields, method declarations, and method parameters.

- **MethodsBodyVisitor**  
  Performs semantic checks and type checking on method bodies using the
  information gathered by previous visitors.

- **IRGenerator**  
  Generates the corresponding LLVM intermediate representation (LLVM-IR)
  for the input program.
