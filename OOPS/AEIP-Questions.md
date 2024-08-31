## Level-1
### **1. Encapsulation**

**Question:** What is encapsulation in object-oriented programming and why is it important?

**Cross-Questions:**
- How does encapsulation improve the maintainability of a codebase?
- Can you explain how encapsulation helps in data hiding?
- What are some common challenges when implementing encapsulation in a large system?

### **2. Access Modifiers**

**Question:** Describe the roles of `private`, `protected`, and `public` access modifiers in Java. How do they contribute to encapsulation?

**Cross-Questions:**
- What access modifier would you use for a method that should only be accessible within its own package? Why?
- How does the `protected` access modifier affect subclasses in different packages?
- Can you provide an example of how improper use of access modifiers can lead to issues in a system?

### **3. Getters and Setters**

**Question:** What are getters and setters? Why are they used, and what are some best practices for their implementation?

**Cross-Questions:**
- How would you handle a situation where a field should be read-only?
- What are the potential drawbacks of using getters and setters excessively?
- Can you discuss a scenario where direct field access might be preferable to using getters and setters?

### **4. Inheritance**

**Question:** What is inheritance in object-oriented programming, and when would you use it?

**Cross-Questions:**
- How does the `extends` keyword work in Java to create subclass relationships?
- Can you explain the difference between inheritance and composition? When might you choose one over the other?
- What are some common problems associated with inheritance, such as the fragile base class problem?

### **5. Method Overriding**

**Question:** What is method overriding, and what is the purpose of the `@Override` annotation in Java?

**Cross-Questions:**
- How does method overriding support runtime polymorphism in Java?
- What are the rules for overriding methods in terms of return types and access modifiers?
- Can you give an example of a situation where method overriding might cause issues?

### **6. Polymorphism**

**Question:** Explain compile-time and runtime polymorphism in Java. How are they achieved?

**Cross-Questions:**
- How does method overloading differ from method overriding in terms of polymorphism?
- Can you provide an example of how polymorphism can be leveraged using interfaces and abstract classes?
- What are some limitations of polymorphism, and how can they be addressed?

### **7. Dynamic Method Dispatch**

**Question:** What is dynamic method dispatch, and how does the JVM use it to determine which method to call at runtime?

**Cross-Questions:**
- How does dynamic method dispatch enable runtime polymorphism?
- Can you discuss a scenario where dynamic method dispatch might lead to unexpected behavior?
- How would you debug issues related to dynamic method dispatch in a Java application?

### **8. Abstract Classes**

**Question:** What are abstract classes, and when should you use them? How do they differ from interfaces?

**Cross-Questions:**
- How do abstract classes provide partial implementation for subclasses?
- When might it be more appropriate to use an interface rather than an abstract class?
- Can you give an example of a situation where using an abstract class might be problematic?

### **9. Abstract Methods**

**Question:** What are abstract methods, and how do they differ from concrete methods? Why are they important in object-oriented design?

**Cross-Questions:**
- What happens if a subclass does not implement all of the abstract methods from its superclass?
- How do abstract methods help in designing flexible and extensible systems?
- Can you provide an example of a case where abstract methods would be preferred over concrete methods?

### **10. Designing for Abstraction**

**Question:** How does focusing on "what" rather than "how" support effective design and abstraction?

**Cross-Questions:**
- How does designing for abstraction improve code flexibility and maintainability?
- Can you provide an example where focusing on "what" rather than "how" led to a better design solution?
- What are some potential pitfalls of over-abstraction, and how can they be avoided?

--- 

## Level-2


### **1. Encapsulation and Access Modifiers**

**Question:** How does encapsulation enhance the security and maintainability of an application? Discuss the impact of access modifiers (`private`, `protected`, `public`) on encapsulation and provide examples where each access level is appropriate.

**Cross-Questions:**
- How would you refactor code to improve encapsulation in a legacy system?
- What potential issues might arise if access modifiers are used incorrectly, particularly with `protected` and `public`?
- How do you balance between exposing necessary information and maintaining encapsulation in complex systems?

### **2. Getters and Setters**

**Question:** Analyze the trade-offs of using getters and setters extensively in a class. How do they impact encapsulation, and what are some best practices for their usage in large-scale systems?

**Cross-Questions:**
- How would you design getters and setters for immutable objects?
- What problems might occur if getters and setters are not used properly, and how can these be mitigated?
- Can you describe a scenario where exposing fields directly might be justified over using getters and setters?

### **3. Inheritance vs. Composition**

**Question:** Compare and contrast inheritance and composition in terms of their advantages and disadvantages. When would you choose one over the other, and how does each approach impact the flexibility and maintainability of the system?

**Cross-Questions:**
- How can improper use of inheritance lead to the fragile base class problem, and what strategies can be employed to avoid it?
- Can you provide a real-world example where composition is preferred over inheritance?
- How do you decide when to use composition instead of inheritance for a given design problem?

### **4. Method Overriding and `@Override` Annotation**

**Question:** Discuss the role of the `@Override` annotation in method overriding. How does it enhance the correctness of method overriding, and what are the potential issues if the annotation is omitted?

**Cross-Questions:**
- What are some common pitfalls in method overriding that the `@Override` annotation helps to prevent?
- How do you handle method overriding in a complex class hierarchy where multiple classes may override the same method?
- Can you provide an example where overriding a method without using `@Override` might lead to unexpected behavior?

### **5. Polymorphism: Compile-Time vs. Runtime**

**Question:** Explain the difference between compile-time (method overloading) and runtime polymorphism (method overriding). How does each form of polymorphism contribute to a flexible and extensible design?

**Cross-Questions:**
- How does method overloading differ from method overriding in terms of method resolution and binding?
- Can you provide an example where compile-time polymorphism enhances code readability and maintainability?
- What challenges arise when combining compile-time and runtime polymorphism in a single system?

### **6. Dynamic Method Dispatch**

**Question:** Describe how dynamic method dispatch works in the Java Virtual Machine (JVM). How does it support runtime polymorphism, and what are some performance considerations associated with it?

**Cross-Questions:**
- How can you optimize the performance of dynamic method dispatch in a high-performance application?
- What are the potential pitfalls of dynamic method dispatch, and how can they be mitigated?
- How does dynamic method dispatch interact with other JVM features like Just-In-Time (JIT) compilation?

### **7. Covariant Return Types**

**Question:** What are covariant return types, and how do they allow for more flexible method overriding? Discuss the benefits and limitations of using covariant return types in method overrides.

**Cross-Questions:**
- How does the concept of covariant return types affect class design and maintainability?
- Can you provide an example where covariant return types are used effectively in an application?
- What limitations or potential issues should be considered when using covariant return types?

### **8. Abstract Classes vs. Interfaces**

**Question:** Compare and contrast abstract classes and interfaces in terms of their use cases and design implications. How do you decide when to use an abstract class versus an interface in a complex system?

**Cross-Questions:**
- What are some scenarios where using an abstract class might lead to design limitations compared to using interfaces?
- How can interfaces and abstract classes be combined effectively in a single design?
- Can you provide an example of a situation where choosing between an abstract class and an interface significantly impacted the system’s architecture?

### **9. Designing for Abstraction**

**Question:** How does focusing on "what" rather than "how" lead to more effective system design? Discuss how this principle can be applied in designing APIs and libraries.

**Cross-Questions:**
- How do you ensure that your abstractions remain relevant and useful as the system evolves?
- Can you provide a real-world example where focusing on "what" rather than "how" led to a better design outcome?
- What are the risks of over-abstraction, and how can they be managed?

### **10. Advanced Encapsulation Issues**

**Question:** Discuss some advanced issues related to encapsulation, such as exposing internal state through methods and the impact of reflection on encapsulation. How can these issues be addressed in a robust system design?

**Cross-Questions:**
- How do you prevent unintended exposure of internal state while still providing necessary functionality?
- What strategies can be employed to handle the impact of reflection on encapsulation and security?
- Can you describe a scenario where encapsulation was compromised due to reflection, and how you addressed it?

