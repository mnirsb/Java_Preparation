# Class
## Introduction

A **class** in Java is like a blueprint or template that defines what an object is and what it can do.

Imagine you're designing a new type of car. The **class** would be the blueprint for that car, specifying things like:

- **Attributes** (what the car has): color, model, engine type, number of doors, etc.
- **Methods** (what the car can do): start the engine, accelerate, brake, turn, etc.

When you create an actual car using this blueprint, you're creating an **object**. Each car you make from this blueprint can have its own specific attributes (like one car being red and another blue), but they all follow the same general design.

In Java, a class is a way to define the properties (called fields) and behaviors (called methods) that objects created from the class will have. Here’s a simple example:

```java
// Defining a class named Car
public class Car {
    // Attributes (fields)
    String color;
    String model;

    // Behavior (method)
    void startEngine() {
        System.out.println("Engine started!");
    }
}
```

From this **Car** class, you can create objects (instances of the class):

```java
// Creating an object from the Car class
Car myCar = new Car();
myCar.color = "Red";  // Setting an attribute
myCar.model = "Sedan";
myCar.startEngine();  // Calling a method
```

In this example:
- `Car` is the class (the blueprint).
- `myCar` is an object (an instance of the Car class).
- `color` and `model` are attributes of the object.
- `startEngine()` is a method that describes what the object can do.

So, a class is just a way to define a group of related attributes and behaviors that will be shared by all the objects created from that class.
## But how java recognises class?
Java recognizes a class through its syntax and structure in the code. Here's how it works:

### 1. **Class Definition**
- A class in Java is defined using the `class` keyword followed by the class name.
- The class name must follow Java naming conventions (usually starting with an uppercase letter).
- The class body is enclosed in curly braces `{}`.

Example:
   ```java
   public class Car {
       // Fields and methods go here
   }
   ```

### 2. **Compilation Process**
- When you write Java code in a `.java` file, the Java compiler (`javac`) reads the file and looks for the class definitions.
- Each class is compiled into a separate `.class` file containing bytecode, which the Java Virtual Machine (JVM) can execute.
- If the file is named `Car.java`, it should contain a class named `Car`, and the compiled bytecode will be in `Car.class`.

### 3. **Naming and File Structure**
- The name of the `.java` file should match the name of the public class inside it. For example, if your class is named `Car`, the file should be named `Car.java`.
- The compiler recognizes the class by this name and expects the filename and class name to be the same.

### 4. **Classpath**
- The JVM uses the **classpath** to locate classes. The classpath is a parameter that tells the JVM where to find the compiled `.class` files (in directories or JAR files).
- When you run a Java program, the JVM searches the classpath for the required classes, loads them, and executes the code.

### 5. **Access Modifiers**
- The visibility of a class is controlled by access modifiers like `public`, `protected`, and default (no modifier).
- A `public` class is accessible from any other class, while a default (package-private) class is only accessible from classes within the same package.

### 6. **Main Method (Entry Point)**
- Java recognizes a class that can be run as a program by looking for a special method called `main`.
- The `main` method has a specific signature:
  ```java
  public static void main(String[] args) {
      // Code to be executed
  }
  ```
- When you execute a Java program, the JVM looks for the `main` method in the specified class and starts executing the code from there.

### Example:
Let's say you have a file named `Car.java`:
```java
public class Car {
    // Fields and methods
    String model;

    public void startEngine() {
        System.out.println("Engine started!");
    }

    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.model = "Sedan";
        myCar.startEngine();
    }
}
```

- The compiler (`javac Car.java`) will generate `Car.class`.
- The JVM (`java Car`) will recognize the `Car` class because it's in `Car.class`.
- The JVM will then look for the `main` method to start the program.

So, Java recognizes a class by the way it's defined, named, compiled, and located on the classpath. The class structure, along with the correct file and method names, allows the compiler and JVM to correctly interpret and run your Java code.
## Easy Level Questions
1. What is a class in Java, and how is it different from an object?
2. How do you define a class in Java? Write a simple example.
3. What is the purpose of the public keyword when defining a class?
4. How can you create an instance (object) of a class in Java? Write a code snippet to demonstrate.
5. What is the significance of the new keyword in Java when creating objects?
6. Explain the concept of a constructor in a Java class. How is it different from a regular method?
7. What happens if you don't explicitly define a constructor in a class?
8. How can you use the this keyword inside a class, and what is its purpose?
9. In Java 17 (or most recent version), what is a sealed class, and how does it differ from a regular class?
10. What are access modifiers in Java? How do public, private, and protected differ when applied to class members?

## Medium Level Questions
1. What is the difference between a static method and an instance method in a Java class? Provide an example where both are used.
2. Explain method overloading in Java. How does the compiler differentiate between overloaded methods in a class?
3. How does inheritance work in Java? Create a base class and a derived class, and show how methods and fields are inherited.
4. What is the purpose of the final keyword when applied to a class? Can a final class be extended? Explain with an example.
5. Describe the concept of encapsulation in Java. How can you achieve encapsulation in a class? Provide a code example.
6. How does the super keyword work in Java? Provide an example where it is used to call a superclass constructor and method.
7. Explain what an abstract class is in Java. How does it differ from an interface? Provide an example where an abstract class might be more appropriate than an interface.
8. In Java 17 (or the latest version), what are record classes, and how do they differ from regular classes? Write a simple record class and explain its use.
9. How does the Java garbage collector manage objects created from classes? Explain the role of strong, weak, and phantom references in this context.
10. What are inner classes in Java? Explain the difference between static inner classes and non-static inner classes with examples.

## Hard Level Questions
1. How does the Java memory model handle the allocation and deallocation of objects created from classes? Discuss the roles of the heap, stack, and method area, and explain how object references are managed.
2. Explain the concept of polymorphism in Java. How do method overriding and dynamic method dispatch work? Provide an example demonstrating how the JVM resolves method calls at runtime.
3. Discuss the implications of using a finalize() method in a Java class. Why is it considered deprecated in modern Java versions, and what alternatives are recommended for resource management?
4. Describe the process of creating a custom class loader in Java. What are the potential use cases for a custom class loader, and how does it interact with the JVM’s built-in class loaders?
5. How does the transient keyword work in the context of serialization in Java? Provide an example where the transient keyword is used, and explain how it affects the serialization process.
6. In Java 17 (or the latest version), how do sealed classes enhance the design of class hierarchies? Provide a detailed example of a sealed class, and discuss its advantages and limitations compared to traditional inheritance.
7. Explain the concept of reflection in Java. How can reflection be used to dynamically inspect or modify a class at runtime? What are the potential risks and performance implications of using reflection extensively?
8. Discuss the role of the volatile keyword in multi-threaded Java applications. How does it affect the visibility of changes to class fields across threads? Provide an example that demonstrates the correct usage of volatile.
9. What are synthetic classes and methods in Java? How and why does the Java compiler generate synthetic elements, and what are the potential challenges when dealing with them in frameworks or tools that perform bytecode manipulation?
10. How does Java's module system (introduced in Java 9) affect the design and structure of classes within an application? Explain the use of exports, opens, and requires keywords in the context of modular class design, and discuss how they impact encapsulation and dependency management.

## Extreme Level Questions
1. Explain the concept of Metaspace in the Java HotSpot VM. How does it differ from the older PermGen space, and what is the impact of Metaspace on class loading and unloading? Discuss how improper management of Metaspace can lead to memory leaks in large applications.
2. In Java, the Unsafe class allows for low-level operations, including direct memory access. How can you use Unsafe to allocate memory for a class outside of the JVM’s managed heap? Discuss the potential risks and benefits of using Unsafe for managing objects.
3. Describe the internals of the Java Class file format. How are fields, methods, and attributes represented in the bytecode? Explain how tools like javap can be used to inspect the bytecode and provide an example of decoding a class file to analyze its structure.
4. What are hidden classes in Java (introduced in Java 15), and how do they differ from regular classes? Discuss their use cases, particularly in dynamic language runtimes or frameworks, and explain how they can be utilized in conjunction with the MethodHandles API.
5. Java's support for Nest-Based Access Control (introduced in Java 11) allows nested classes to access each other's private members more efficiently. Explain the bytecode-level changes introduced to support this feature, and discuss how it impacts the design of nested class hierarchies.
6. Discuss the concept of Escape Analysis in the JVM. How does it allow the JVM to optimize object allocation on the stack instead of the heap? Provide an example where escape analysis can lead to significant performance improvements by avoiding heap allocations in a class-heavy application.
7. Java supports method handles via the java.lang.invoke.MethodHandle class. Explain the difference between method handles and reflection, and describe how method handles can be used for dynamic method invocation. What are the performance implications of using method handles over traditional reflection?
8. How does the JVM implement class redefinition and retransforming at runtime, particularly in the context of tools like java.lang.instrument.Instrumentation? Discuss the challenges and limitations of redefining classes dynamically, especially in a production environment.
9. In the context of multi-module applications, explain the role of split packages and the challenges they introduce in class loading. Discuss how to avoid split package issues in complex applications, especially when using third-party libraries or modular JARs.
10. Java's GraalVM introduces the concept of SubstrateVM for ahead-of-time (AOT) compilation. How does AOT compilation impact the design and initialization of classes, especially considering static initializers and class loading? Discuss how developers need to adapt their classes for optimal performance and compatibility with GraalVM’s native image generation.


# Let's find out each Questions in detailed solution with cross questions.