**1 – Why we need to use OOP ? Some major OOP languages ?**
 
Object-Oriented Programming (OOP) is a popular programming paradigm that helps in organizing and managing complex software systems. Here’s why it is essential:
 

📌 1. Modularity (Code Reusability)
    · Why? Write code once and reuse it across different parts of your application.
    · Example: You can create a Vehicle class and reuse it for Car, Bike, and Truck objects without rewriting code.
 

📌 2. Maintainability (Easier to Update and Debug)
    · Why? Changes in one part of the code can be localized and easier to maintain.
    · Example: If you update a method in a parent class, all child classes automatically inherit the change.
 

📌 3. Scalability (Handle Large Systems)
    · Why? OOP allows you to break complex systems into smaller, manageable objects.
    · Example: In a banking system, you can have classes like Account, Customer, and Transaction to represent different components.
 

📌 4. Abstraction (Hide Complex Implementation)
    · Why? Focus on what an object does rather than how it does it.
    · Example: A Payment class may have different implementations (Credit Card, PayPal) without exposing the internal details.
 

📌 5. Encapsulation (Data Security)
    · Why? Protect object data by restricting direct access.
    · Example: Private fields in a User class ensure sensitive data (like passwords) cannot be modified directly.
 

📌 6. Polymorphism (Flexibility & Extensibility)
    · Why? Use the same interface for different data types.
    · Example: A draw() method can be used to render circles, rectangles, or polygons without changing the calling code.
 

📌 7. Inheritance (Code Efficiency)
    · Why? Create a new class from an existing class, reducing code duplication.
    · Example: A Bird class can inherit properties from an Animal class and add specific behaviors like fly().
 
✅ Some Major OOP Languages

Language	    Key Features
--------------------------------------------------------------------------
Java	        Pure OOP, platform-independent (Write Once, Run Anywhere)
Python	        Multi-paradigm (OOP + Procedural), dynamic typing
C++	            High-performance, supports both OOP and procedural
C#	            OOP-centric, commonly used for .NET applications
Ruby	        Everything is an object, dynamic and flexible
Swift	        OOP + Protocol-Oriented, used for iOS/macOS development
JavaScript	    Prototype-based OOP, dominant in web development
Kotlin	        Modern OOP + Functional, used for Android development
 

🎯 In Short:
    · Why OOP? For better structure, reusability, and scalability.
    · Major OOP Languages: Java, Python, C++, C#, and more.
 
**2 – Interface vs Abstract class ?**

When deciding between an interface and an abstract class, understanding their differences is key. Here's a breakdown:
 

✅ 1. Definition
    · Interface: A contract that defines a set of abstract methods (no implementation) that a class must implement.
    · Abstract Class: A class that may contain both abstract methods (without implementation) and concrete methods (with implementation).
 

✅ 2. Key Differences
Feature	           Interface	                                Abstract Class
------------------------------------------------------------------------------------------------------------
Methods	         | Only abstract methods (before Java 8)	  | Can have both abstract and concrete methods
Fields	         | Only public, static, and final (constants) | Can have instance variables (non-final)
Access Modifiers | Methods are public by default	          | Can have methods with any visibility
Inheritance	     | A class can implement multiple interfaces  |	A class can extend only one abstract class
Default Methods	 | Supported (since Java 8)	                  | Supported (via concrete methods)
Constructor	     | No constructors allowed	                  | Can have constructors
Use Case	     | Define a contract for multiple classes	  | Provide a base class with shared code
Performance	     | Slightly faster (no inheritance hierarchy) | Slightly slower due to inheritance
 

✅ 3. When to Use What?

Use an Interface	                                            Use an Abstract Class
----------------------------------------------------------------------------------------------------
When you want to define a contract	                          | When you want to provide common behavior
For multiple inheritance needs	                              | If future changes are expected
To achieve loose coupling	                                  | When methods have a default behavior
Ideal for defining capabilities (e.g., Flyable, Serializable) |	For hierarchical relationships (e.g., Animal -> Dog)
 

✅ 4. Example Code
Interface Example:
````java
interface Animal {
    void makeSound(); // Abstract method (no body)
}
 
class Dog implements Animal {
    public void makeSound() {
        System.out.println("Woof!");
    }
}
Abstract Class Example:
````java
abstract class Animal {
    abstract void makeSound(); // Abstract method
    void sleep() {             // Concrete method
        System.out.println("Sleeping...");
    }
}
 
class Dog extends Animal {
    void makeSound() {
        System.out.println("Woof!");
    }
}
 

✅ 5. Summary
    · Interfaces: Ideal for defining a contract for unrelated classes.
    · Abstract Classes: Best for defining shared behavior in a class hierarchy.
 
3 – Why wee need equals and hashcode ? When to override ?
 
 
✅ Why Do We Need equals() and hashCode() in Java?
In Java, the equals() and hashCode() methods play a crucial role in comparing objects and ensuring the correct functioning of collections like HashMap, HashSet, and HashTable.
 

📌 1. equals() Method
    · Purpose: To compare the contents of two objects for equality.
    · Default Behavior (from Object class): Compares memory addresses (reference equality), not the actual data.
✅ Why Override equals()?
When you want to compare object values rather than memory locations.
Example Without Overriding equals():
````java
class Person {
    String name;
    Person(String name) {
        this.name = name;
    }
}
 
Person p1 = new Person("Alice");
Person p2 = new Person("Alice");
 
System.out.println(p1.equals(p2)); // Output: false (different memory locations)
Example With Overridden equals():
````java
class Person {
    String name;
    Person(String name) {
        this.name = name;
    }
 
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true; // Same reference
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return name.equals(person.name);
    }
}
 
System.out.println(p1.equals(p2)); // Output: true (compares values)
 

📌 2. hashCode() Method
    · Purpose: Generates a unique integer (hash code) representing an object.
    · Default Behavior (from Object class): Returns the object`s memory address as a hash code.
✅ Why Override hashCode()?
If you override equals(), you must override hashCode() to maintain consistency when using hash-based collections (e.g., HashMap, HashSet).
Example of HashMap Without Overriding hashCode():
````java
Map<Person, String> map = new HashMap<>();
map.put(new Person("Alice"), "Developer");
 
System.out.println(map.get(new Person("Alice"))); // Output: null (hashes differ)
Fixed by Overriding hashCode():
````java
@Override
public int hashCode() {
    return Objects.hash(name); // Generates a hash from the name
}
 

📌 3. When to Override equals() and hashCode()?
You should override these methods when:
✅ You want to compare object values instead of references.
✅ You plan to use the object in hash-based collections (e.g., HashMap, HashSet, HashTable).
✅ You want to ensure logical equality between two objects.
 

📌 4. Key Rules for Overriding
    1. Consistency Rule: If two objects are equal using equals(), they must return the same hash code.
    2. Symmetry Rule: If a.equals(b) is true, then b.equals(a) must also be true.
    3. Transitivity Rule: If a.equals(b) and b.equals(c) are both true, then a.equals(c) must also be true.
 

📌 5. Best Practice: Use Objects Utility
Java provides a convenient Objects class for null-safe comparison and hashing.
Example:
````java
@Override
public boolean equals(Object obj) {
    if (this == obj) return true;
    if (obj == null || getClass() != obj.getClass()) return false;
    Person person = (Person) obj;
    return Objects.equals(name, person.name);
}
 
@Override
public int hashCode() {
    return Objects.hash(name);
}
 

🎯 Summary
    · equals() checks for content equality (override when comparing by value).
    · hashCode() provides a unique identifier (override when using hash collections).
    · Always override both together to maintain collection integrity.
 
 4 – Diamond problem in Java ? How to fix it?
 
✅ What is the Diamond Problem in Java?
The diamond problem occurs in languages that support multiple inheritance, where a class inherits from two classes that have a common ancestor. This leads to ambiguity in method resolution.

📌 1. Understanding the Diamond Problem
Consider the following inheritance structure:
      A
     / \
    B   C
     \ /
      D
    · B and C both inherit from A.
    · D inherits from both B and C.
    · If A has a method (display()), and both B and C override it, then D does not know which version of display() to inherit.

❌ Does Java Support Multiple Inheritance?
    · Java does not allow multiple inheritance with classes (i.e., class D extends B, C is not allowed).
    · This restriction prevents the diamond problem at the class level.
 

✅ How to Fix the Diamond Problem?
🔹 1. Use Interfaces (Multiple Inheritance with Interfaces)
Java allows multiple inheritance through interfaces, but to resolve the diamond problem, default methods must be explicitly handled.
Example with Default Methods (Causing Diamond Problem)

````java
interface A {
    default void show() {
        System.out.println("A's show()");
    }
}
 
interface B extends A {
    default void show() {
        System.out.println("B's show()");
    }
}
 
interface C extends A {
    default void show() {
        System.out.println("C's show()");
    }
}
 
class D implements B, C {
    // Compilation Error: show() method is ambiguous
}
✅ Solution: Override the Method in Class D
````java
class D implements B, C {
    @Override
    public void show() {
        // Explicitly choose which interface method to call
        B.super.show(); // or C.super.show();
    }
}
 
public class Main {
    public static void main(String[] args) {
        D obj = new D();
        obj.show();  // Output: "B's show()"
    }
}

🔹 How This Fix Works:
    · Java forces D to override show() and explicitly specify which version to use (B.super.show() or C.super.show()).
    · This removes the ambiguity.
 

✅ Summary
Approach	    Fix for Diamond Problem
---------------------------------------------------------------------------------------------------------
Classes	   |    Java does not allow multiple inheritance with classes.
Interfaces |	Multiple inheritance is allowed, but methods must be resolved explicitly using super.
Solution   |	Override the method in the subclass (D) and specify which parent’s method to use.
💡 Java prevents the diamond problem at the class level but requires explicit resolution in interfaces.
 
 5 – Why we need Garbagge Collector ? How does it run ?


✅ Why Do We Need a Garbage Collector in Java?
In languages like C and C++, developers must manually allocate and deallocate memory. This can lead to issues like:
    1. Memory Leaks: Memory that is no longer used but not released.
    2. Dangling Pointers: Accessing memory that has already been freed.
    3. Double Free Errors: Trying to free the same memory twice.
Java solves these problems by using the Garbage Collector (GC), which automatically manages memory by reclaiming unused objects.
 

📌 1. What is Garbage Collection (GC)?
Garbage Collection is the process by which Java automatically identifies and removes unused objects to free up memory.
    · Unused Objects: Objects that are no longer referenced and can’t be accessed by the application.
Example:
````java
public class Example {
    public static void main(String[] args) {
        Example obj = new Example(); // Object created
        obj = null; // Object is now eligible for GC
    }
}
When obj is set to null, there are no references to the object, making it eligible for garbage collection.
 

📌 2. How Does the Garbage Collector Work?
The Java Virtual Machine (JVM) manages garbage collection in several steps:
🟢 Step 1: Object Allocation
    · Objects are created in the heap memory.
    · JVM keeps track of live and unused objects.
🔵 Step 2: Object Reachability
An object is considered reachable if:
    1. It is referenced by active threads or static fields.
    2. It is accessible via the stack or global references.
Objects not reachable are eligible for garbage collection.
🟠 Step 3: Garbage Collection Process
    1. Mark: Identify and mark all reachable objects.
    2. Sweep: Remove unreachable (garbage) objects from memory.
    3. Compact: Optional step to defragment memory for efficient allocation.
 

📌 3. Types of Garbage Collectors in Java
Java provides different types of Garbage Collectors:

Garbage Collector	             Description	                                             Use Case
----------------------------------------------------------------------------------------------------------------------
Serial GC	                |    Uses a single thread (simple and slow).	            |    Suitable for small applications.
Parallel GC (Throughput GC)	|    Uses multiple threads for better performance.	        |    Best for multi-core CPUs.
G1 GC (Garbage First)	    |    Splits the heap into regions and cleans incrementally.	|    Low-latency apps (e.g., web servers).
ZGC	                        |    Ultra-low-pause GC for large heaps (up to 16 TB).	    |    Large-scale and real-time systems.
Shenandoah GC	            |    Concurrent, low-pause GC.	                            |    Ideal for low-latency applications.

You can specify the collector using JVM options, e.g.:
bash
java -XX:+UseG1GC MyApp
 

📌 4. When Does the Garbage Collector Run?
The JVM triggers the GC under these conditions:
    1. Low Memory: When free memory is insufficient for new objects.
    2. Explicit Request: Using System.gc() (not guaranteed but suggests GC).
    3. Idle Time: JVM may trigger GC during application downtime.
 

📌 5. How to Optimize Garbage Collection?
    · Use appropriate GC (e.g., G1 for low-latency apps).
    · Avoid creating unnecessary or large objects.
    · Use Weak References for cache objects (via WeakReference, SoftReference).
    · Profile memory using tools like: 
            o VisualVM
            o Eclipse Memory Analyzer (MAT)
            o Java Flight Recorder (JFR)
 

📌 6. Common Misconceptions
❌ "GC frees everything immediately." → GC works asynchronously.
❌ "System.gc() forces GC." → It only suggests GC but does not guarantee it.
❌ "GC means no memory leaks." → Strong references prevent GC if you forget to clear them.
 

🎯 Summary
    · Why GC?: Automatic memory management, prevents memory leaks and dangling pointers.
    · How it works?: Mark objects, sweep garbage, and compact memory.
    · Types of GC: Serial, Parallel, G1, ZGC, and Shenandoah.
    · When?: JVM automatically decides, but you can request with System.gc().
 
 6 – Java ‘static’ keyword usage ?
 
static Keyword in Java – Usage and Examples
The static keyword in Java is used for memory management and allows members (variables, methods, blocks, and nested classes) to belong to the class rather than to specific instances of the class. It means these members are shared across all instances of the class.
 

📌 1. static Variables (Class Variables)
A static variable is shared by all instances of a class. It is initialized once when the class is loaded into memory.
✅ Example:
````java
class Employee {
    static int count = 0; // Static variable
    String name;
 
    Employee(String name) {
        this.name = name;
        count++; // Increment count for each object
    }
 
    void display() {
        System.out.println(name + " - Total Employees: " + count);
    }
}
 
public class Main {
    public static void main(String[] args) {
        Employee e1 = new Employee("Alice");
        Employee e2 = new Employee("Bob");
 
        e1.display(); // Output: Alice - Total Employees: 2
        e2.display(); // Output: Bob - Total Employees: 2
    }
}
🔎 Why use static variables?
    · Shared across all objects (e.g., counters, constants).
    · Saves memory because it’s created only once.
 

📌 2. static Methods (Class Methods)
A static method belongs to the class and can be called without creating an object.
✅ Example:
````java
class MathUtils {
    static int add(int a, int b) {
        return a + b;
    }
}
 
public class Main {
    public static void main(String[] args) {
        int sum = MathUtils.add(5, 10);
        System.out.println("Sum: " + sum); // Output: Sum: 15
    }
}
🔎 Why use static methods?
    · For utility methods (e.g., Math.max(), Arrays.sort()).
    · No need to create an object to use the method.
⚠️ Rules for static methods:
    1. Cannot access non-static (instance) members directly.
    2. Cannot use this or super keywords.
 

📌 3. static Blocks (Static Initialization Block)
A static block is executed once when the class is loaded. It is commonly used to initialize static variables.
✅ Example:
````java
class Config {
    static String appName;
 
    static {
        appName = "MyApp";
        System.out.println("Static Block Executed!");
    }
 
    static void display() {
        System.out.println("App Name: " + appName);
    }
}
 
public class Main {
    public static void main(String[] args) {
        Config.display();
        // Output:
        // Static Block Executed!
        // App Name: MyApp
    }
}
🔎 Why use static blocks?
    · To initialize complex static data.
    · For one-time setup (e.g., loading configuration).
 

📌 4. static Classes (Nested Static Class)
Java allows static nested classes inside another class. These are also known as static inner classes.
✅ Example:
````java
class Outer {
    static class Inner {
        void display() {
            System.out.println("Inside Static Inner Class");
        }
    }
}
 
public class Main {
    public static void main(String[] args) {
        Outer.Inner innerObj = new Outer.Inner();
        innerObj.display(); // Output: Inside Static Inner Class
    }
}
🔎 Why use static nested classes?
    · When a class is logically related to another but doesn’t need access to the outer class’s instance.
    · Better encapsulation and organization.
 

📌 5. static Imports (Importing Static Members)
You can use static imports to directly reference static methods or variables from another class without qualifying them.
✅ Example:
````java
import static java.lang.Math.*;
 
public class Main {
    public static void main(String[] args) {
        System.out.println(sqrt(64)); // Output: 8.0 (no Math.sqrt())
    }
}
🔎 Why use static imports?
    · Simplifies access to constants (e.g., PI) and utility methods.
    · Improves code readability.
 

📌 6. static with main() Method
The main() method in Java is static because:
    1. It allows the JVM to call main() without creating an object.
    2. It`s the entry point of every Java application.
✅ Example:
````java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
 

📌 7. static Final Constants
If you want to create a constant value, declare it as static final.
✅ Example:
````java
class Constants {
    static final double PI = 3.14159;
}
 
public class Main {
    public static void main(String[] args) {
        System.out.println(Constants.PI); // Output: 3.14159
    }
}
 

📌 Summary of static Usage
Feature	             Usage	                             Purpose
--------------------------------------------------------------------------------------------------
static Variable	 |   static int count;	             |   Share across all instances (e.g., counters).
static Method	 |   static void display()	         |   Call without an object (e.g., utility methods).
static Block	 |   static { /* init code */ }	     |   One-time static initialization (e.g., configs).
static Class	 |   static class Inner {}	         |   Nested class without outer class access.
static Import	 |   import static java.lang.Math.*; |	 Use static members without class name.
static Final	 |   static final int MAX = 100;	 |   Define constants.
 

🎯 When to Use static?
    · Use for shared data across instances.
    · For utility methods (e.g., Math.max()).
    · To manage constants with static final.
    · When a nested class doesn’t need to access the outer class.
 
 
7 – Immutability means ? Where, How and Why to use it ?


✅ What is Immutability?
Immutability means that an object’s state cannot be changed after it is created. Once an immutable object is constructed, its fields and properties are fixed and unchangeable.
 

📌 1. Characteristics of an Immutable Object:
    1. State cannot be modified after object creation.
    2. Thread-safe by design (no risk of concurrent modifications).
    3. No setters (modifying methods).
    4. Final fields to prevent reassignment.
 

📌 2. Examples of Immutable Objects in Java
✅ Built-in Immutable Classes:
    · String
    · Wrapper classes (e.g., Integer, Double, Boolean)
    · LocalDate, LocalTime, LocalDateTime (from java.time package)
 

📌 3. Why Use Immutability?
Benefit	                |    Explanation
----------------------------------------------------------------------------------------------------------------
Thread Safety	        |    Immutable objects cannot be modified, making them safe in concurrent environments.
Caching & Optimization	|    Java can cache immutable objects (e.g., String Pool), improving performance.
Security	            |    Immutable objects are inherently safer against unauthorized changes.
Simplified Debugging	|    No unexpected side effects from object modifications.
Safe Sharing	        |    Can be shared across classes and threads without cloning or defensive copying.
 

📌 4. How to Create Immutable Objects in Java
✅ Example: Creating a Custom Immutable Class
````java
final class Person {
    private final String name;
    private final int age;
 
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
 
    public String getName() {
        return name;
    }
 
    public int getAge() {
        return age;
    }
}
✅ Key Rules for Immutability:
    1. Declare the class final: Prevents subclass modification.
    2. Declare fields private and final: Prevents modification after construction.
    3. No setters: Avoid providing methods that change object state.
    4. Return copies: For mutable fields, return a defensive copy.
 

📌 5. Handling Mutable Fields in Immutable Classes
If a class contains mutable objects (e.g., List, Map), ensure you:
    1. Return a copy of the object.
    2. Create defensive copies in the constructor.
✅ Example with Mutable Field:
````java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
 
final class Employee {
    private final String name;
    private final List<String> tasks;
 
    public Employee(String name, List<String> tasks) {
        this.name = name;
        this.tasks = new ArrayList<>(tasks); // Defensive copy
    }
 
    public String getName() {
        return name;
    }
 
    public List<String> getTasks() {
        return Collections.unmodifiableList(tasks); // Immutable view
    }
}
 

📌 6. Where to Use Immutability
    1. Data Transfer Objects (DTOs): Pass data between layers in an application.
    2. Value Objects: Model values that represent data without an identity (e.g., Money, Date).
    3. Configuration Settings: Ensure constant settings are unmodifiable.
    4. Caching: Use immutable objects for safe and efficient caching.
    5. Concurrency: In multi-threaded applications to avoid synchronization issues.
 

📌 7. Immutability vs. Mutability

Feature	        Immutable Objects	                Mutable Objects
-----------------------------------------------------------------------------------------
State Change	Cannot be modified after creation	Can be changed after creation
Thread Safety	Naturally thread-safe	            Requires external synchronization
Performance	    May have better caching	            Higher memory overhead on changes
Example	        String, Integer, LocalDate	        StringBuilder, ArrayList, HashMap
 

📌 8. How Java Ensures Immutability Internally
✅ String Class Example:
    1. Declared as final – Cannot be extended.
    2. Character array is private final char[].
    3. Any operation (e.g., concat(), replace()) returns a new object.
Example:
````java
String str = "Java";
str.concat(" Rocks!");
System.out.println(str); // Output: "Java"
Explanation: concat() returns a new String, the original str is unchanged.
 

📌 9. Common Mistakes When Implementing Immutability
❌ Forgetting Defensive Copies: Directly exposing mutable fields.
❌ Providing Setters: Allowing modifications.
❌ Non-Final Fields: Allowing value reassignment.
 

📌 10. Best Practices for Immutability
    1. Prefer immutability for small objects and value types.
    2. Use immutable collections (List.of(), Collections.unmodifiableList()).
    3. Use record classes (from Java 14+) for concise immutable objects.
✅ Example Using record (Java 14+):
````java
public record Person(String name, int age) {}

This automatically provides:
    · final fields
    · A constructor
    · equals(), hashCode(), toString()
 

🎯 In Summary:
    · Immutability ensures that objects cannot be changed after creation.
    · Use immutability for safety, performance, and simplicity.
    · Follow best practices with final, defensive copying, and no setters.
 
 8 – Composition and Aggregation means and differences ?
 
✅ Composition vs. Aggregation in Java (Object-Oriented Programming)
Both Composition and Aggregation represent "Has-A" relationships between objects but differ in ownership and lifecycle management.
 

📌 1. What is Composition?
In Composition, one object is strongly dependent on another. If the parent object is destroyed, the child object is also destroyed.
✅ Key Characteristics:
    · Strong association (Whole-Part relationship).
    · Child cannot exist without the parent.
    · Tight coupling between objects.
✅ Example of Composition in Java:
````java
class Engine {
    private String type;
 
    public Engine(String type) {
        this.type = type;
    }
 
    public void start() {
        System.out.println("Engine started: " + type);
    }
}
 
class Car {
    private final Engine engine; // Composition (Car "has-a" Engine)
 
    public Car(String engineType) {
        this.engine = new Engine(engineType); // Engine created inside Car
    }
 
    public void drive() {
        engine.start();
        System.out.println("Car is driving");
    }
}
 
public class Main {
    public static void main(String[] args) {
        Car car = new Car("V8");
        car.drive();
        // Output:
        // Engine started: V8
        // Car is driving
    }
}

📌 Key Insight:
When the Car object is destroyed, its Engine object is also destroyed.
 

📌 2. What is Aggregation?
In Aggregation, one object is loosely dependent on another. The parent and child can exist independently.
✅ Key Characteristics:
    · Weak association (Has-A relationship).
    · Child can exist without the parent.
    · Loose coupling between objects.
✅ Example of Aggregation in Java:
````java
class Department {
    private String name;
 
    public Department(String name) {
        this.name = name;
    }
 
    public String getName() {
        return name;
    }
}
 
class University {
    private String universityName;
    private Department department; // Aggregation
 
    public University(String universityName, Department department) {
        this.universityName = universityName;
        this.department = department; // Injected from outside
    }
 
    public void display() {
        System.out.println(universityName + " has " + department.getName() + " Department");
    }
}
 
public class Main {
    public static void main(String[] args) {
        Department cs = new Department("Computer Science");
        University uni = new University("Tech University", cs);
        uni.display();
        
        // Output:
        // Tech University has Computer Science Department
    }
}
📌 Key Insight:
    · The Department object exists independently of the University.
    · Destroying the University object does not affect the Department.
 

📊 3. Key Differences: Composition vs. Aggregation

Feature	            |    Composition	Aggregation
-----------------------------------------------------------------------------------------------
Relationship Type	|    Strong (Part-Whole)	Weak (Association)
Dependency	        |    Child depends on parent	Child is independent of parent
Lifecycle	        |    Parent’s destruction destroys child	Parent’s destruction does not affect child
Example	            |    Car has-a Engine (Composition)	University has-a Department (Aggregation)
Coupling	        |    Tight coupling (High dependency)	Loose coupling (Low dependency)
Object Creation	    |    Child is created inside the parent	Child is passed from outside
 

📌 4. When to Use Composition vs. Aggregation

Scenario	                Use Composition	                        Use Aggregation
------------------------------------------------------------------------------------------------------------
Ownership	                Parent owns the child completely.	    Child can exist without the parent.
Lifecycle Dependency	    Child cannot exist without parent.	    Child can live independently.
Tight vs Loose Coupling	    When objects need close integration.	When you need flexibility between objects.
Example	                    Car and Engine, Human and Heart.	    University and Department, Team and Players.
 

📌 5. Advanced Example:
Let`s model a Library System using both Composition and Aggregation.
✅ Composition (Book and Pages):
A Book is composed of Pages. If you destroy the book, its pages also disappear.
````java
class Page {
    private int pageNumber;
 
    public Page(int pageNumber) {
        this.pageNumber = pageNumber;
    }
 
    public void printPage() {
        System.out.println("Page: " + pageNumber);
    }
}
 
class Book {
    private final List<Page> pages = new ArrayList<>();
 
    public Book(int pageCount) {
        for (int i = 1; i <= pageCount; i++) {
            pages.add(new Page(i)); // Creating pages (Composition)
        }
    }
 
    public void readBook() {
        pages.forEach(Page::printPage);
    }
}
 
public class Main {
    public static void main(String[] args) {
        Book book = new Book(3);
        book.readBook();
    }
}
 

✅ Aggregation (Library and Books):
A Library contains Books, but Books can exist independently.
````java
class Book {
    private String title;
 
    public Book(String title) {
        this.title = title;
    }
 
    public String getTitle() {
        return title;
    }
}
 
class Library {
    private String name;
    private List<Book> books;
 
    public Library(String name, List<Book> books) {
        this.name = name;
        this.books = books; // Aggregation (Books from outside)
    }
 
    public void showBooks() {
        for (Book b : books) {
            System.out.println(name + " has: " + b.getTitle());
        }
    }
}
 
public class Main {
    public static void main(String[] args) {
        Book b1 = new Book("Java Basics");
        Book b2 = new Book("Advanced Java");
        List<Book> books = Arrays.asList(b1, b2);
 
        Library library = new Library("City Library", books);
        library.showBooks();
    }
}
 

📌 6. Summary

Feature	        |     Composition	                     |       Aggregation
------------------------------------------------------------------------------------------------------------------
Dependency	    |    Strong – Child depends on Parent	 |   Weak – Child can exist without Parent
Lifecycle	    |    Parent’s removal destroys the child |	    Parent’s removal does not destroy the child
Object Creation	|    Created inside the parent	         |   Passed from outside
Coupling	    |    Tightly coupled (Highly dependent)	 |   Loosely coupled (Independent)
Example	        |    Car has-a Engine	                 |   University has-a Department
 
 
 9 – Cohesion and Coupling means and differences ?
 
✅ Cohesion vs. Coupling in Software Design (OOP Concepts)
Cohesion and Coupling are key principles of object-oriented programming that directly impact the maintainability, scalability, and readability of code.
 

📌 1. What is Cohesion?
Cohesion refers to how closely related and focused the responsibilities of a module, class, or method are. A highly cohesive module performs one well-defined task.
✅ Key Characteristics of Cohesion:
    · High cohesion = Focused and performs one specific responsibility.
    · Low cohesion = Does too many unrelated things, making it hard to maintain.
    · Improves code readability, reusability, and modularity.
 

✅ Example of High Cohesion (Good Practice)
A Student class with methods only related to student operations:
````java
class Student {
    private String name;
    private int id;
 
    public Student(String name, int id) {
        this.name = name;
        this.id = id;
    }
 
    public void displayDetails() {
        System.out.println("Student: " + name + ", ID: " + id);
    }
 
    public double calculateGrade(double marks) {
        return marks / 10.0;
    }
}
✅ Why is this high cohesion?
    · All methods are specific to the Student entity.
    · Each method performs a single responsibility.
 

❌ Example of Low Cohesion (Bad Practice)
A Student class doing unrelated tasks (like student info and database operations):
````java
class Student {
    private String name;
    private int id;
 
    public void displayDetails() {
        System.out.println("Student: " + name + ", ID: " + id);
    }
 
    // Database operation (unrelated responsibility)
    public void saveToDatabase() {
        System.out.println("Saving student to database...");
    }
 
    // Email sending (unrelated responsibility)
    public void sendEmail() {
        System.out.println("Sending email to student...");
    }
}
❌ Why is this low cohesion?
    · The class handles multiple responsibilities: 
            o Displaying student information
            o Database operations
            o Sending emails
    · Violates the Single Responsibility Principle (SRP).
 

📌 2. What is Coupling?
Coupling refers to the degree of dependency between two modules, classes, or components. It defines how interconnected or independent the components are.
✅ Key Characteristics of Coupling:
    · Tight coupling = High dependency between components.
    · Loose coupling = Low dependency between components (better).
    · Low coupling improves code flexibility, modularity, and testability.
 

✅ Example of Loose Coupling (Good Practice)
Using interfaces to decouple dependencies:
````java
interface Payment {
    void pay(double amount);
}
 
class CreditCardPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " via Credit Card");
    }
}
 
class Order {
    private Payment payment;
 
    public Order(Payment payment) {
        this.payment = payment; // Dependency Injection
    }
 
    public void processOrder(double amount) {
        payment.pay(amount);
    }
}
 
public class Main {
    public static void main(String[] args) {
        Payment payment = new CreditCardPayment();
        Order order = new Order(payment);
        order.processOrder(100.0);
    }
}
✅ Why is this loose coupling?
    · The Order class depends on the Payment interface, not a concrete class.
    · Easy to change the payment method (e.g., PayPal, BankTransfer) without modifying Order.
 

❌ Example of Tight Coupling (Bad Practice)
Directly hardcoding dependencies:
````java
class Order {
    private CreditCardPayment payment = new CreditCardPayment(); // Hard dependency
 
    public void processOrder(double amount) {
        payment.pay(amount);
    }
}
 
class CreditCardPayment {
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " via Credit Card");
    }
}
❌ Why is this tight coupling?
    · Directly creates a CreditCardPayment object.
    · Hard to change payment logic without modifying the Order class.
    · Reduces code flexibility and increases maintenance complexity.
 

📊 3. Key Differences: Cohesion vs. Coupling

Feature	                 |      Cohesion	                                    |         Coupling
-----------------------------------------------------------------------------------------------------------------------------
Definition	             |   How focused a class/module is on a single task.	|    Degree of dependency between classes/modules.
Goal	                 |   Ensure a single responsibility for each component.	|    Minimize dependencies between components.
High is Better?	         |   ✅ Yes – High cohesion means better code clarity.  |  ✅ No – Prefer loose (low) coupling for flexibility.
Example of Good Practice |	 A Student class only manages student data.	        |    Using an interface for payment methods.
Impact on Maintenance	 |   Easier to understand and modify.	                |    Easier to replace or extend functionality.
Testability	             |   Easier to unit-test (isolated logic).	            |    Easier to mock dependencies during testing.
Violation	             |   A class doing too many things.	                    |    Directly instantiating dependencies.
 

📌 4. How to Achieve High Cohesion & Low Coupling
✅ Best Practices:
    1. Follow SOLID Principles: 
            o Single Responsibility Principle (SRP) for cohesion.
            o Dependency Inversion Principle (DIP) for loose coupling.
    2. Use Interfaces & Abstract Classes: 
            o Depend on abstractions, not concrete implementations.
    3. Apply Dependency Injection (DI): 
            o Pass dependencies through constructors or methods.
    4. Separate Concerns: 
            o Keep business logic, presentation, and data access independent.
    5. Modular Design: 
            o Divide your system into small, independent modules.
 

📌 5. Example Combining Both:
High Cohesion + Loose Coupling Example
````java
// High Cohesion: Interface only handles payment
interface Payment {
    void pay(double amount);
}
 
// High Cohesion: Each class handles a specific payment method
class PayPalPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " via PayPal");
    }
}
 
// Low Coupling: Order depends on abstraction (Payment)
class Order {
    private Payment payment;
 
    public Order(Payment payment) {
        this.payment = payment;
    }
 
    public void processOrder(double amount) {
        payment.pay(amount);
    }
}
 
public class Main {
    public static void main(String[] args) {
        Payment payment = new PayPalPayment();
        Order order = new Order(payment);
        order.processOrder(150.0);
    }
}
 

📌 6. Summary

Concept	    Good Practice	                                Bad Practice
---------------------------------------------------------------------------------------------------------
Cohesion	One task per class (High Cohesion)	            Multiple responsibilities (Low Cohesion)
Coupling	Interface-based dependencies (Loose Coupling)	Direct class references (Tight Coupling)
 
 
 
 
10 - Heap and Stack means and differences ?
 
✅ Heap vs. Stack in Java (Memory Management)
In Java, memory is divided into Heap and Stack, each serving different purposes for storing objects, variables, and method calls.
 

📌 1. What is Stack Memory?
Stack memory is used for:
    · Method execution (local variables, method calls, parameters).
    · Primitive data types (e.g., int, char, boolean).
    · References to objects stored in the Heap.
✅ Key Characteristics of Stack Memory:
    · Fast access (LIFO – Last In, First Out).
    · Stores method calls and local variables.
    · Automatically managed (cleared when methods exit).
    · Thread-safe (each thread has its own stack).
 

✅ Example of Stack Memory in Java:
````java
public class StackExample {
    public static void main(String[] args) {
        int a = 10;              // Stored in Stack (primitive)
        int b = add(a, 5);       // Method call adds a new frame to Stack
        System.out.println(b);   // Output: 15
    }
 
    public static int add(int x, int y) {
        return x + y;            // x and y are local variables (Stack)
    }
}
Memory Layout:
    1. Main Method Stack Frame: 
            o a = 10
            o Method call to add(10, 5)
    2. Add Method Stack Frame: 
            o x = 10, y = 5
            o Returns 15 and stack frame is removed.
 

📌 2. What is Heap Memory?
Heap memory is used for:
    · Objects and instance variables.
    · Objects created with new keyword.
    · Garbage collection (GC) manages this area.
✅ Key Characteristics of Heap Memory:
    · Larger and slower than Stack.
    · Stores objects and their instance variables.
    · Shared across threads (not thread-safe by default).
    · Requires Garbage Collection to free unused objects.
 

✅ Example of Heap Memory in Java:
````java
class Person {
    String name;
 
    public Person(String name) {
        this.name = name;
    }
}
 
public class HeapExample {
    public static void main(String[] args) {
        Person p = new Person("Alice"); // Object in Heap, 'p' in Stack
        System.out.println(p.name);     // Output: Alice
    }
}
Memory Layout:
    1. Stack Memory: 
            o p (Reference to the Person object).
    2. Heap Memory: 
            o Person object with name = "Alice".
When the program ends, the Garbage Collector clears the Person object.
 

📊 3. Key Differences: Heap vs. Stack Memory

Feature	            Stack Memory	                            Heap Memory
----------------------------------------------------------------------------------------------------
Purpose	            Stores method calls, local variables	    Stores objects and instance variables
Storage Type	    Primitive types & object references	        Objects (created using new keyword)
Access Speed	    Faster (LIFO structure)	                    Slower (Dynamic memory allocation)
Memory Size	        Smaller (Limited to method scope)	        Larger (More memory for long-living objects)
Lifetime	        Temporary (Removed after method call)	    Persistent (Exists until GC removes it)
Management	        Automatically by JVM (when method exits)	Garbage Collection (by JVM)
Thread Safety	    Thread-safe (Each thread has its own stack)	Not thread-safe (Shared across threads)
Example Variables	Local variables, method parameters	        Objects created with new keyword
 

📌 4. How Stack and Heap Work Together
    1. Objects are always stored in the Heap.
    2. References to these objects are stored in the Stack.
    3. Primitives (like int, float, etc.) are stored directly in the Stack.
 

✅ Example of Stack and Heap Interaction:
````java
class Car {
    String model;
 
    Car(String model) {
        this.model = model;
    }
}
 
public class MemoryExample {
    public static void main(String[] args) {
        int x = 100;             // Stored in Stack (primitive)
        Car car = new Car("BMW"); // car reference: Stack, object: Heap
        System.out.println(car.model); // Output: BMW
    }
}
Memory Breakdown:
    1. Stack Memory: 
            o x = 100 (primitive)
            o car (reference to the Car object in Heap)
    2. Heap Memory: 
            o Car object with model = "BMW"
 

📌 5. Common Issues Related to Stack and Heap
Issue	                Cause	                                            Solution
------------------------------------------------------------------------------------------------------------------
Stack Overflow	        Too many nested method calls (infinite recursion).	Avoid deep recursion, use loops if possible.
Out of Memory (Heap)	Large objects or memory leaks.	                    Use Garbage Collection and manage memory wisely.
Memory Leak	            Unreferenced objects not cleaned by GC.	            Nullify unused references and use Weak References.
 

📌 6. When to Use Stack vs. Heap
Scenario	            Use Stack	                        Use Heap
--------------------------------------------------------------------------------------------------------
Method Execution	    Local variables, method parameters	Objects and instance variables
Temporary Data	        Small, short-lived data	            Large, persistent data
Performance-Critical	Fast execution (LIFO structure)	    For long-lasting objects (GC handles cleanup)
Multithreading	        Thread-specific storage (safe)	    Shared data across threads (requires synchronization)
 

📌 7. Example of Stack vs. Heap in Recursion
✅ Recursive Method (Stack Usage):
````java
public class RecursionExample {
    public static void main(String[] args) {
        int result = factorial(5);
        System.out.println("Factorial: " + result);
    }
 
    public static int factorial(int n) {
        if (n == 1) return 1;          // Base case
        return n * factorial(n - 1);   // Recursive call (new stack frame)
    }
}
Stack Behavior: Each recursive call creates a new stack frame. Deep recursion can cause a StackOverflowError.
 

📌 8. Summary
Feature	        Stack Memory	                                Heap Memory
-----------------------------------------------------------------------------------------------------
Speed	        Fast (LIFO – Last In, First Out)	            Slower (Dynamic allocation)
Storage	        Local variables, method calls, references	    Objects, instance variables
Lifetime	    Until method execution ends	                    Until Garbage Collection (GC) cleans up
Management	    Automatically managed by JVM	                Managed by Garbage Collector
Thread Safety	Each thread has its own stack (thread-safe)	    Shared between threads (not thread-safe)
Common Errors	StackOverflowError (deep recursion)	            OutOfMemoryError (large object usage)
 
 
 
 
11 – Exception means ? Type of Exceptions ?
 
✅ What is an Exception in Java?
An exception in Java is an unexpected event or error that occurs during the execution of a program, disrupting the normal flow of instructions.
Java provides a robust exception-handling mechanism to deal with runtime errors and maintain program stability using the try, catch, throw, throws, and finally keywords.
 

📌 1. Why Do Exceptions Occur?
Exceptions typically occur due to:
    · Invalid Input (e.g., dividing by zero).
    · Accessing Null Objects (e.g., NullPointerException).
    · File or Network Errors (e.g., IOException).
    · Array Out-of-Bounds (e.g., ArrayIndexOutOfBoundsException).
 

📌 2. Types of Exceptions in Java
Exceptions in Java are divided into checked, unchecked, and errors.
pgsql
Throwable (Superclass of all exceptions)
├── Exception (Recoverable Errors)
│    ├── Checked Exceptions (Compile-Time)
│    └── Unchecked Exceptions (Run-Time)
└── Error (Unrecoverable, System-Level)
 

📊 A. Checked Exceptions (Compile-Time Exceptions)
Checked exceptions are checked at compile-time—if not handled, the code will not compile. They represent anticipated issues that a program should handle.
✅ Examples of Checked Exceptions:

Exception	            When It Occurs
-------------------------------------------------------------
IOException	            Input/output failures (e.g., file not found).
SQLException	        Database access issues.
FileNotFoundException	File cannot be located.
ClassNotFoundException	Class not found during loading.
InterruptedException	Thread is interrupted.

✅ Example Code (Checked Exception Handling)
````java
import java.io.*;
 
public class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("file.txt");
            System.out.println("File opened successfully.");
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
 

📊 B. Unchecked Exceptions (Run-Time Exceptions)
Unchecked exceptions occur at runtime and are not checked during compilation. They usually stem from programming mistakes.
✅ Examples of Unchecked Exceptions:

Exception	                    When It Occurs
------------------------------------------------------------------
NullPointerException	        Accessing methods/fields of null.
ArrayIndexOutOfBoundsException	Accessing invalid array indices.
ArithmeticException	            Dividing by zero.
IllegalArgumentException	    Passing invalid arguments.
ClassCastException	            Invalid object typecasting.

✅ Example Code (Unchecked Exception Handling)
````java
public class UncheckedExceptionExample {
    public static void main(String[] args) {
        try {
            int result = 10 / 0; // ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
        }
    }
}
 

📊 C. Errors (System-Level Issues)
Errors are serious problems beyond the application`s control. Usually caused by JVM or system failures.
✅ Examples of Errors:

Error Type	            When It Occurs
------------------------------------------------------------------------
StackOverflowError	    Infinite recursion or deep method calls.
OutOfMemoryError	    Insufficient memory (heap overflow).
VirtualMachineError	    Critical JVM error.
NoClassDefFoundError	Class not found at runtime.

✅ Example Code (Error Demonstration)
````java
public class StackOverflowErrorExample {
    public static void recursiveMethod() {
        recursiveMethod(); // Infinite recursion
    }
 
    public static void main(String[] args) {
        recursiveMethod();
    }
}
🚨 Avoid handling errors directly—focus on fixing the root cause.
 

📌 3. How to Handle Exceptions in Java
Java provides five main exception-handling keywords:
    1. try: Defines a block where exceptions may occur.
    2. catch: Handles the specific exception.
    3. finally: Executes always (optional).
    4. throw: Manually throw an exception.
    5. throws: Declare exceptions a method can throw.
 

✅ Example of Exception Handling
````java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int num = Integer.parseInt("abc"); // NumberFormatException
        } catch (NumberFormatException e) {
            System.out.println("Invalid number format: " + e.getMessage());
        } finally {
            System.out.println("Program completed.");
        }
    }
}
Output:
Invalid number format: For input string: "abc"
Program completed.
 

📌 4. Custom (User-Defined) Exceptions
You can create your own exception by extending the Exception class.
✅ Example of a Custom Exception
````java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
 
public class CustomExceptionExample {
    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or above.");
        }
    }
 
    public static void main(String[] args) {
        try {
            validateAge(16);
        } catch (InvalidAgeException e) {
            System.out.println("Caught: " + e.getMessage());
        }
    }
}
 

📌 5. When to Use Checked vs. Unchecked Exceptions

Aspect	        Checked Exceptions	                    Unchecked Exceptions
------------------------------------------------------------------------------------------------------------------------
When to Use	    For expected issues (I/O, database).	For programming mistakes (null pointers, invalid array access).
Handling	    Mandatory (use try-catch or throws).	Optional (can be left unhandled).
Examples	    IOException, SQLException.	            NullPointerException, ArithmeticException.
Performance	    Slightly slower (due to checking).	    Faster (no compile-time checking).
 

📌 6. Common Exceptions in Java

Exception	                        When It Occurs
-----------------------------------------------------------------------------
NullPointerException	            Accessing methods/fields of a null object.
ArrayIndexOutOfBoundsException	    Accessing an invalid index in an array.
ArithmeticException	                Dividing by zero.
IOException	                        Input/output operations fail (file issues).
ClassCastException	                Invalid object typecasting.
IllegalArgumentException	        Passing illegal arguments to a method.
 

📌 7. Best Practices for Exception Handling
    1. Use Specific Exceptions – Catch specific exceptions rather than a generic Exception.
    2. Log Exceptions – Always log exceptions for debugging (e.printStackTrace() or logging frameworks).
    3. Never Suppress Exceptions – Avoid empty catch blocks.
    4. Custom Exceptions – Create custom exceptions for domain-specific errors.
    5. Resource Management – Use try-with-resources for closing resources (like files, sockets).
 
 
 
12 – How to summarize ‘clean code’ as short as possible ?
Clean Code means writing simple, readable, and maintainable code by following best practices. Key principles include:
    1. Readable – Use clear, meaningful names and keep functions small.
    2. Simple – Write straightforward logic and avoid over-engineering.
    3. Modular – Break code into small, reusable components.
    4. Consistent – Follow a uniform coding style and structure.
    5. Testable – Ensure code is easy to test with automated tests.
    6. Efficient – Prioritize performance without sacrificing clarity.
    7. Self-Documenting – Write code that explains itself without needing extra comments.
 
 
13 - What is the method of hiding in Java ?
 
In Java, method hiding occurs when a subclass defines a static method with the same name and signature as a static method in its superclass. This hides the superclass's method rather than overriding it.
 

✅ Key Points About Method Hiding:
    1. Static methods are hidden, not overridden.
    2. Method calls are resolved at compile time (not runtime).
    3. Instance methods cannot hide static methods.
    4. Access is based on the reference type, not the object type.
 

📌 Example of Method Hiding in Java:
````java
class Parent {
    static void display() {
        System.out.println("Parent static method");
    }
}
 
class Child extends Parent {
    static void display() { // Method Hiding
        System.out.println("Child static method");
    }
}
 
public class MethodHidingExample {
    public static void main(String[] args) {
        Parent obj1 = new Child();
        obj1.display(); // Calls Parent's display method (hiding)
 
        Child obj2 = new Child();
        obj2.display(); // Calls Child's display method
    }
}
🧠 Output:
sql
KopyalaDüzenle
Parent static method
Child static method
 

📊 Method Hiding vs. Method Overriding:

Feature	                Method Hiding	                Method Overriding
---------------------------------------------------------------------------------
Method Type	            Only static methods	            Only instance methods
Binding	                Compile-time (reference type)	Runtime (object type – polymorphism)
Keyword	                static (both parent and child)	@Override (optional annotation)
Inheritance	            Hides the parent method	        Overrides the parent method
Access	                Based on reference type	        Based on object type
 
 
 
 
14 - What is the difference between abstraction and polymorphism in Java ?
 
✅ Difference Between Abstraction and Polymorphism in Java
Feature	     Abstraction	                                                            Polymorphism
-----------------------------------------------------------------------------------------------------------------------------------------
Definition	 Hiding implementation details and showing only essential features.	            The ability of a method or object to take many forms.
Purpose	     Focuses on what a class does (not how it does it).	                            Allows different implementations of the same interface or method.
Types	     ✅ Abstract Class 	                                                          ✅ Compile-time (Method Overloading) 
             ✅ Interface	                                                              ✅ Runtime (Method Overriding)
How It Works	    By abstract classes and interfaces.	                                    By overloading (compile-time) or overriding (runtime).
Implementation	    Defined using abstract keyword or interface.	                        Achieved using method overloading or method overriding.
Example Use Case	Defining a template where subclasses must provide specific behavior.	Allowing different objects to respond differently to the same method call.
Key Benefit	Provides a blueprint for other classes and promotes loose coupling.	            Provides flexibility and supports code reusability through dynamic behavior.
 

📌 Example of Abstraction:
Using an abstract class to define a general shape:
Java
abstract class Shape {
    abstract void draw(); // Abstract method (no body)
}
 
class Circle extends Shape {
    void draw() {
        System.out.println("Drawing a circle.");
    }
}
 
public class Main {
    public static void main(String[] args) {
        Shape shape = new Circle();
        shape.draw(); // Output: Drawing a circle.
    }
}
 

📌 Example of Polymorphism:
Using method overriding (runtime polymorphism):
java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}
 
class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}
 
public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog(); // Polymorphism
        animal.sound(); // Output: Dog barks
    }
}
 

📊 Quick Summary:
    · Abstraction: Defines a contract for what should be done.
    · Polymorphism: Allows objects to behave differently while sharing a common interface.

