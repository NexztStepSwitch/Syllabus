# ☕ Core Java – Detailed Syllabus

### ⭐ Importance: ★★★★★ (5/5)

---

## 1. **Java Basics**
- **History & Features**
  - JVM, JRE, JDK
  - WORA (Write Once, Run Anywhere)
- **Java program structure**
  - Class, main method, identifiers
  - Compilation & execution flow
- **Data Types**
  - Primitive types
  - Reference types
- **Operators**
  - Arithmetic, Logical, Bitwise
  - Ternary, instanceof

---

## 2. **Control Flow Statements**
- **Decision-making**
  - if, if-else, switch
- **Loops**
  - for, while, do-while
  - Enhanced for-loop (for-each)
- **Jump statements**
  - break, continue, return

---

## 3. **OOP Concepts in Java**
- **Class & Objects**
  - Fields, methods, constructors
  - Object lifecycle
- **Encapsulation**
  - Access modifiers (public, private, protected, default)
  - Getters & Setters
- **Inheritance**
  - extends keyword
  - Multilevel & hierarchical inheritance
  - Method overriding
- **Polymorphism**
  - Compile-time (method overloading)
  - Runtime (method overriding)
- **Abstraction**
  - Abstract classes
  - Interfaces (Java 8 default & static methods)
- **Composition vs Inheritance**
- **Association, Aggregation, Composition**

---

## 4. **Memory Management**
- **Stack vs Heap**
- **Garbage Collection**
  - finalize() method
  - JVM Garbage Collectors (Serial, Parallel, G1, ZGC)
- **Memory leaks in Java**
- **Escape analysis & object allocation**

---

## 5. **Strings & Wrapper Classes**
- **String handling**
  - String, StringBuffer, StringBuilder
  - String Pool (interning)
- **Wrapper classes**
  - Autoboxing & Unboxing
- **Immutable objects**

---

## 6. **Exception Handling**
- **Types of exceptions**
  - Checked vs Unchecked
  - Error vs Exception
- **Keywords**
  - try, catch, finally, throw, throws
- **Custom exceptions**
- **Best practices**
  - Exception hierarchy
  - Avoid swallowing exceptions

---

## 7. **Java Collections Framework (JCF)**
- **Collection Interfaces**
  - List, Set, Queue, Map
- **Implementations**
  - ArrayList, LinkedList
  - HashSet, TreeSet, LinkedHashSet
  - HashMap, TreeMap, LinkedHashMap
  - PriorityQueue, ArrayDeque
- **Utility classes**
  - Collections, Arrays
- **Comparable vs Comparator**
- **Fail-fast vs Fail-safe iterators**
- **Concurrent collections**
  - ConcurrentHashMap
  - CopyOnWriteArrayList

---

## 8. **Generics**
- **Generic classes & methods**
- **Bounded type parameters**
- **Wildcards**
  - `?`, `? extends T`, `? super T`
- **Type erasure**
- **Generics best practices**

---

## 9. **Multithreading & Concurrency**
- **Thread lifecycle**
  - Thread class vs Runnable interface
  - Thread states
- **Synchronization**
  - synchronized methods & blocks
  - Intrinsic locks (monitor)
- **Inter-thread communication**
  - wait(), notify(), notifyAll()
- **Executor framework**
  - ThreadPoolExecutor
  - Callable & Future
- **Concurrency utilities**
  - Locks (ReentrantLock, ReadWriteLock)
  - Semaphores, CountDownLatch, CyclicBarrier
  - Concurrent collections
- **Fork/Join framework**
- **Volatile & Atomic classes**

---

## 10. **Java I/O (Input/Output)**
- **Byte Streams vs Character Streams**
- **File I/O**
  - FileInputStream, FileOutputStream
  - FileReader, FileWriter
- **Buffered I/O**
  - BufferedReader, BufferedWriter
- **Serialization**
  - Serializable interface
  - Externalizable
- **NIO (New I/O)**
  - Channels, Buffers, Selectors
  - Path & Files API (Java 7+)

---

## 11. **Java 8 Features**
- **Functional Interfaces**
  - `@FunctionalInterface`
  - Common ones: Runnable, Callable, Comparator
- **Lambda Expressions**
  - Syntax & use cases
- **Streams API**
  - Intermediate vs Terminal operations
  - Map, Filter, Reduce
  - Collectors
- **Optional**
  - Avoiding NullPointerExceptions
- **Default & Static methods in interfaces**
- **Date & Time API**
  - LocalDate, LocalTime, LocalDateTime
  - Duration, Period, ZonedDateTime

---

## 12. **Advanced Java Features**
- **Reflection API**
  - Accessing classes, fields, methods at runtime
- **Annotations**
  - Built-in annotations (`@Override`, `@Deprecated`, `@FunctionalInterface`)
  - Custom annotations
- **Inner Classes**
  - Static, non-static, anonymous
- **Enums**
  - Enum with methods
- **Var keyword (Java 10+)**
- **Records (Java 14+)**
- **Sealed Classes (Java 17+)**

---

## 13. **JVM Internals**
- **JVM Architecture**
  - ClassLoader subsystem
  - Runtime Data Areas (Heap, Stack, Method Area, PC Register, Native Method Stack)
  - Execution Engine
- **Class loading**
  - Loading, Linking, Initialization
  - ClassLoader types (Bootstrap, Extension, Application, Custom)
- **JIT Compiler**
- **Performance tuning basics**

---

## 14. **Best Practices**
- **Effective Java principles**
- **Immutability**
- **Thread-safety practices**
- **Coding standards**
- **Design principles (SOLID) applied in Java**

---

## 15. **Testing in Java**
- **JUnit (4 & 5)**
- **Mockito (Basics)**
- **TestNG**
- **Best practices in unit testing**

---

## 16. **Tools & Ecosystem**
- **Build tools**
  - Maven, Gradle
- **IDEs**
  - IntelliJ IDEA, Eclipse
- **Code Quality**
  - SonarLint, Checkstyle
- **Logging**
  - Log4j, SLF4J, Logback
