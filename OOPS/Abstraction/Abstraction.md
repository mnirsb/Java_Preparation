### **Abstraction in Object-Oriented Programming (OOP)**

#### **Definition:**
Abstraction in OOP is a fundamental concept that focuses on exposing only the necessary and relevant details of an object while hiding its internal complexities. It allows developers to work with high-level ideas and interactions, rather than getting bogged down by the intricate details of how something is implemented.

#### **Purpose of Abstraction:**

1. **Simplification:**
    - Abstraction simplifies the interaction with complex systems by providing a clear and easy-to-understand interface. This makes it easier to design, implement, and manage large software systems, as you can work with a simplified view of the objects and their relationships.

2. **Separation of Concerns:**
    - Abstraction helps separate what an object does from how it does it. This separation allows developers to change the internal implementation of an object without affecting other parts of the system that rely on the abstracted interface.

3. **Code Reusability:**
    - By abstracting common behaviors into base classes or interfaces, you can create reusable components that can be extended or implemented by various other classes. This promotes reuse and reduces code duplication.

4. **Security:**
    - Abstraction can also protect sensitive information by hiding the internal implementation details that shouldn't be exposed to users or other parts of the system. Only the relevant and necessary parts of an object are made accessible.

5. **Improved Maintenance:**
    - Abstracting complex logic into simpler interfaces makes it easier to update and maintain the code. When changes are required, you only need to modify the underlying implementation without altering the abstracted interface, minimizing the risk of breaking other parts of the system.

### **How Abstraction Works:**

1. **Interfaces and Abstract Classes:**
    - Abstraction is typically achieved through the use of interfaces and abstract classes. An interface defines a contract that implementing classes must follow, while an abstract class provides a partially implemented base class that other classes can extend.

2. **Hiding Implementation Details:**
    - In abstraction, the focus is on hiding the "how" and only exposing the "what." For example, when you use a method to save a file, you don't need to know the exact steps the method takes to save the file—you only need to know how to call the method and what parameters it needs.

### **Edge Cases in Abstraction:**

1. **Over-Abstraction:**
    - While abstraction is useful, over-abstraction can lead to unnecessary complexity. If too many layers of abstraction are introduced, it can make the system harder to understand and maintain. This often happens when developers abstract too early or without a clear understanding of the requirements.

2. **Leaky Abstractions:**
    - A leaky abstraction is when the underlying complexity "leaks" through the abstraction, making it difficult for users to ignore the hidden details. This can happen if the abstraction is not well-designed, leading to situations where users are forced to deal with the complexities the abstraction was supposed to hide.

3. **Inadequate Abstraction:**
    - On the other hand, if abstraction is too minimal, it might not effectively hide the complexity it was intended to. This can result in a system where users need to understand too much about the internal workings to use it correctly, defeating the purpose of abstraction.

4. **Interface Fatigue:**
    - If an interface becomes too broad or complex, implementing it can become cumbersome. This is especially true if an interface defines too many methods, leading to classes that need to implement methods they don't actually need, resulting in unnecessary and bloated code.

5. **Abstract Class vs. Interface Dilemma:**
    - Deciding whether to use an abstract class or an interface can sometimes be tricky. Abstract classes allow you to define some behavior (with concrete methods), but a class can only extend one abstract class. Interfaces, on the other hand, are more flexible as a class can implement multiple interfaces, but they can't contain implementation details (at least in traditional OOP languages).

### **Conclusion:**

Abstraction is a key concept in OOP that helps manage complexity by allowing developers to focus on high-level operations without worrying about the underlying details. It plays a crucial role in creating modular, maintainable, and reusable code. However, like any tool, abstraction needs to be applied thoughtfully. Over-abstraction, leaky abstractions, and interface fatigue are potential pitfalls that can undermine the benefits of abstraction. Understanding and carefully applying abstraction can lead to cleaner, more efficient, and more manageable code.

### Industry-Oriented Use Case: Payment Processing System

#### **Scenario:**
You are tasked with designing a payment processing system for an e-commerce platform. The system needs to support multiple payment methods such as credit card payments, PayPal, and bank transfers. Each payment method has its own specific details and validation requirements. Additionally, the system should be extensible to support future payment methods without requiring major changes to the existing code.

#### **Abstraction Implementation:**

1. **Abstract Class** `PaymentProcessor`: This will serve as the base class for all payment processors. It defines the common interface and some shared functionality.
2. **Concrete Classes**: Implement specific payment methods like `CreditCardProcessor`, `PayPalProcessor`, and `BankTransferProcessor` that extend `PaymentProcessor`.
3. **Edge Cases**: Handle scenarios such as invalid payment details, unsupported currencies, and null inputs.

### **Code Implementation:**

```java
// Abstract Class
abstract class PaymentProcessor {
    protected String currency;

    public PaymentProcessor(String currency) {
        this.currency = currency;
    }

    // Abstract method to process payment
    public abstract void processPayment(double amount);

    // Method to validate the currency (common functionality)
    protected void validateCurrency() {
        if (!"USD".equals(currency)) {
            throw new UnsupportedOperationException("Currency not supported: " + currency);
        }
    }

    // Edge case handling: Invalid amount
    protected void validateAmount(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException("Invalid payment amount: " + amount);
        }
    }
}

// Concrete Class for Credit Card Processing
class CreditCardProcessor extends PaymentProcessor {
    private String cardNumber;

    public CreditCardProcessor(String currency, String cardNumber) {
        super(currency);
        this.cardNumber = cardNumber;
    }

    @Override
    public void processPayment(double amount) {
        validateCurrency();
        validateAmount(amount);
        // Edge Case: Null or invalid card number
        if (cardNumber == null || cardNumber.length() != 16) {
            throw new IllegalArgumentException("Invalid card number.");
        }
        System.out.println("Processing credit card payment of " + amount + " " + currency);
    }
}

// Concrete Class for PayPal Processing
class PayPalProcessor extends PaymentProcessor {
    private String email;

    public PayPalProcessor(String currency, String email) {
        super(currency);
        this.email = email;
    }

    @Override
    public void processPayment(double amount) {
        validateCurrency();
        validateAmount(amount);
        // Edge Case: Null or invalid email
        if (email == null || !email.contains("@")) {
            throw new IllegalArgumentException("Invalid PayPal email.");
        }
        System.out.println("Processing PayPal payment of " + amount + " " + currency);
    }
}

// Concrete Class for Bank Transfer Processing
class BankTransferProcessor extends PaymentProcessor {
    private String bankAccountNumber;

    public BankTransferProcessor(String currency, String bankAccountNumber) {
        super(currency);
        this.bankAccountNumber = bankAccountNumber;
    }

    @Override
    public void processPayment(double amount) {
        validateCurrency();
        validateAmount(amount);
        // Edge Case: Null or invalid bank account number
        if (bankAccountNumber == null || bankAccountNumber.length() != 10) {
            throw new IllegalArgumentException("Invalid bank account number.");
        }
        System.out.println("Processing bank transfer of " + amount + " " + currency);
    }
}
```

### **Usage Example:**

```java
public class PaymentProcessingDemo {
    public static void main(String[] args) {
        try {
            PaymentProcessor creditCardProcessor = new CreditCardProcessor("USD", "1234567812345678");
            creditCardProcessor.processPayment(150.0);

            PaymentProcessor payPalProcessor = new PayPalProcessor("USD", "user@example.com");
            payPalProcessor.processPayment(200.0);

            PaymentProcessor bankTransferProcessor = new BankTransferProcessor("USD", "1234567890");
            bankTransferProcessor.processPayment(300.0);

            // Edge Cases
            PaymentProcessor invalidCurrencyProcessor = new CreditCardProcessor("EUR", "1234567812345678");
            invalidCurrencyProcessor.processPayment(100.0); // Throws UnsupportedOperationException

        } catch (Exception e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

### **Explanation:**

1. **Abstraction**:
   - The `PaymentProcessor` abstract class provides a high-level abstraction for different payment methods. Each specific payment processor (CreditCard, PayPal, BankTransfer) extends this class and implements the `processPayment` method.

2. **Separation of Concerns**:
   - The concrete classes (`CreditCardProcessor`, `PayPalProcessor`, `BankTransferProcessor`) handle the specific details of each payment method, allowing the `PaymentProcessor` to focus on the general process of payment validation and processing.

3. **Code Reusability**:
   - Shared validation logic, such as currency validation and amount validation, is centralized in the abstract class, making the code more reusable and reducing duplication.

4. **Security**:
   - The abstraction hides the internal details of how each payment method is processed, exposing only the necessary interfaces (`processPayment` method).

5. **Edge Case Handling**:
   - The code handles various edge cases like invalid currency, null inputs, and incorrect payment details (e.g., invalid card number, email, or bank account number).
   - This ensures that the system can gracefully handle unexpected inputs and errors, providing meaningful error messages.

### **Conclusion:**

This example demonstrates how abstraction can be effectively used in an industry-oriented, real-life scenario to build a flexible, maintainable, and robust payment processing system. By abstracting the common logic and exposing only what is necessary, the system becomes easier to extend and maintain, while also handling potential edge cases in a consistent manner.

---

### Abstract Classes: When and How to Use Them

#### **What Are Abstract Classes?**

An abstract class in object-oriented programming is a class that cannot be instantiated on its own and serves as a blueprint for other classes. It may contain both abstract methods (methods without a body) and concrete methods (methods with a body). The purpose of an abstract class is to provide a common definition of a base class that multiple derived classes can share.

#### **When to Use Abstract Classes**

1. **Shared Behavior with Flexibility:**
   - Use an abstract class when you have a group of related classes that share common behavior but also require flexibility to implement or override certain functionalities. The abstract class defines the shared behavior, while subclasses provide specific implementations.

2. **Partial Implementation:**
   - If you want to provide some default behavior or common utility methods while forcing subclasses to implement certain methods, an abstract class is the right choice. This allows you to avoid code duplication while still giving subclasses control over specific behaviors.

3. **Hierarchical Relationships:**
   - Abstract classes are useful when there is a clear hierarchical relationship between classes, where the base class defines a generic template and the derived classes represent more specific instances of that template.

4. **When Interfaces Alone Aren't Enough:**
   - Interfaces define a contract that classes must follow but can't provide any implementation. If you need to provide some implementation along with the contract, an abstract class is better suited than an interface. This is particularly important when some methods have a common implementation that shouldn't be duplicated across classes.

5. **Controlled Instantiation:**
   - If you want to prevent the creation of objects from the base class itself but still allow instantiation of its derived classes, an abstract class should be used. This enforces that the abstract class is only used as a foundation for other classes.

#### **How to Use Abstract Classes**

1. **Define the Abstract Class:**
   - Start by defining an abstract class with both abstract methods (methods that must be implemented by subclasses) and concrete methods (methods that provide shared functionality).

2. **Create Subclasses:**
   - Create subclasses that extend the abstract class. These subclasses must implement all abstract methods from the base class. They can also override concrete methods if needed.

3. **Instantiation of Subclasses:**
   - Remember that you cannot create an instance of an abstract class directly. You can only create instances of the subclasses that have fully implemented the abstract class’s abstract methods.

4. **Polymorphism:**
   - Use abstract classes to achieve polymorphism, allowing objects of different subclasses to be treated as objects of the abstract class type. This enables flexibility and reusability in your code.

#### **Edge Cases and Considerations**

1. **Too Much Abstraction:**
   - Be cautious not to make your abstract classes too generic. Over-abstraction can lead to a design where the base class is too broad, making it difficult for subclasses to implement the required behavior in a meaningful way. This can result in subclasses implementing methods that don’t quite fit their purpose, leading to awkward or confusing code.

2. **Lack of Abstraction:**
   - Conversely, if the abstract class does not provide enough abstraction, you may end up with a base class that closely resembles one of its subclasses, limiting the benefits of using an abstract class in the first place. It’s important to strike a balance between shared functionality and flexibility.

3. **Choosing Between Abstract Class and Interface:**
   - Sometimes, it’s not clear whether to use an abstract class or an interface. Use an abstract class when you want to provide shared code and state (fields). Use an interface when you want to define a contract for other classes to implement without imposing any state or behavior.

4. **Multiple Inheritance Issues:**
   - Some languages don’t support multiple inheritance of classes, meaning a class can only inherit from one abstract class. If you need to inherit behaviors from multiple sources, you might need to use interfaces or a combination of abstract classes and interfaces to achieve the desired design.

5. **Handling Changes:**
   - When you modify an abstract class (e.g., adding new abstract methods), you may inadvertently force all existing subclasses to implement the new methods. This can lead to extensive refactoring in large codebases. It’s important to carefully consider the impact of changes to an abstract class.

6. **Final Methods:**
   - Be mindful of the use of final methods (methods that cannot be overridden) in abstract classes. While they can ensure certain behaviors remain unchanged in subclasses, overuse of final methods can reduce the flexibility that abstract classes are supposed to provide.

#### **Conclusion**

Abstract classes are a powerful tool in object-oriented programming that allow you to create flexible and reusable code. They are particularly useful when you need to define a common structure with shared behavior across multiple related classes. However, they should be used thoughtfully to avoid over-complicating your design or making your code difficult to maintain. Understanding when and how to use abstract classes will help you build robust, maintainable, and scalable systems.

### Real-Life Industry Use Case: Abstract Classes in a Payment Processing System

#### **Scenario:**
Imagine you're developing a payment processing system for an e-commerce platform. The system needs to handle payments through various methods such as credit cards, PayPal, and cryptocurrency. Each payment method has different processing logic, but they share some common steps, such as validating the payment details and logging the transaction.

#### **Abstract Class Design:**
We can use an abstract class to represent the common behaviors of all payment methods and allow each specific payment method to implement its unique processing logic.

#### **Abstract Class: `PaymentProcessor`**
This abstract class defines the common structure that all payment methods must follow. It includes both concrete methods (for shared functionality) and abstract methods (for unique implementations).

```java
public abstract class PaymentProcessor {

    // Concrete method for validating payment details
    public boolean validatePaymentDetails(String paymentDetails) {
        // Common validation logic, e.g., checking for null or empty values
        if (paymentDetails == null || paymentDetails.isEmpty()) {
            System.out.println("Invalid payment details.");
            return false;
        }
        System.out.println("Payment details validated.");
        return true;
    }

    // Abstract method to process the payment, to be implemented by subclasses
    public abstract void processPayment(double amount);

    // Concrete method to log the transaction
    public void logTransaction(String transactionDetails) {
        // Common logic for logging transactions
        System.out.println("Logging transaction: " + transactionDetails);
    }
}
```

#### **Subclasses: Implementing Different Payment Methods**

1. **Credit Card Payment Processor:**
   - Implements the `processPayment` method for handling credit card payments.

```java
public class CreditCardProcessor extends PaymentProcessor {

    @Override
    public void processPayment(double amount) {
        // Specific logic for processing credit card payments
        System.out.println("Processing credit card payment of $" + amount);
        // Assume payment is processed and logged
        logTransaction("Credit card payment of $" + amount);
    }
}
```

2. **PayPal Payment Processor:**
   - Implements the `processPayment` method for handling PayPal payments.

```java
public class PayPalProcessor extends PaymentProcessor {

    @Override
    public void processPayment(double amount) {
        // Specific logic for processing PayPal payments
        System.out.println("Processing PayPal payment of $" + amount);
        // Assume payment is processed and logged
        logTransaction("PayPal payment of $" + amount);
    }
}
```

3. **Cryptocurrency Payment Processor:**
   - Implements the `processPayment` method for handling cryptocurrency payments.

```java
public class CryptoProcessor extends PaymentProcessor {

    @Override
    public void processPayment(double amount) {
        // Specific logic for processing cryptocurrency payments
        System.out.println("Processing cryptocurrency payment of $" + amount);
        // Assume payment is processed and logged
        logTransaction("Cryptocurrency payment of $" + amount);
    }
}
```

#### **Usage in the System:**

```java
public class PaymentService {

    public void processTransaction(PaymentProcessor processor, String paymentDetails, double amount) {
        // Validate payment details
        if (processor.validatePaymentDetails(paymentDetails)) {
            // Process payment
            processor.processPayment(amount);
        } else {
            System.out.println("Payment failed due to invalid details.");
        }
    }

    public static void main(String[] args) {
        PaymentService service = new PaymentService();

        // Process a credit card payment
        PaymentProcessor creditCard = new CreditCardProcessor();
        service.processTransaction(creditCard, "1234-5678-9876-5432", 150.0);

        // Process a PayPal payment
        PaymentProcessor paypal = new PayPalProcessor();
        service.processTransaction(paypal, "user@example.com", 75.0);

        // Process a cryptocurrency payment
        PaymentProcessor crypto = new CryptoProcessor();
        service.processTransaction(crypto, "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa", 0.01);
    }
}
```

#### **Edge Cases and Considerations in the Code:**

1. **Null or Empty Payment Details:**
   - The `validatePaymentDetails` method checks if the payment details are null or empty. This prevents processing invalid payment details, which could lead to errors.

2. **Overriding Concrete Methods:**
   - If a subclass needs to customize how a transaction is logged, it can override the `logTransaction` method. This flexibility allows subclasses to modify shared behavior while still benefiting from the base implementation.

3. **Multiple Payment Processors:**
   - The `PaymentService` class demonstrates polymorphism by treating different payment processors as instances of the `PaymentProcessor` abstract class. This allows the system to handle various payment methods uniformly without needing to know the specifics of each method.

4. **Leaky Abstraction:**
   - In this design, care is taken to avoid leaky abstractions. For example, the `processPayment` method in each subclass should fully encapsulate the details of how that specific payment method works, without exposing unnecessary implementation details to the outside world.

5. **Extensibility:**
   - The system is easily extensible. If a new payment method is introduced (e.g., bank transfers), you can simply create a new subclass of `PaymentProcessor` and implement the `processPayment` method without modifying existing code.

#### **Conclusion:**
This example illustrates how abstract classes can be used effectively in a real-world scenario to manage shared behavior, enforce a common structure, and provide flexibility for specific implementations. By carefully designing the abstract class and its subclasses, you can create a system that is both robust and maintainable, while also being flexible enough to handle future changes or extensions.

---

### Abstract Methods: Declaration vs. Implementation

#### **What Are Abstract Methods?**

Abstract methods are methods declared in an abstract class or interface that do not have a body (i.e., no implementation). These methods only have a signature—essentially a method name and its parameters. An abstract method acts as a placeholder, indicating that any class that inherits from the abstract class or implements the interface must provide its own implementation of the method.

#### **Declaration of Abstract Methods:**

1. **Method Signature Without Implementation:**
   - An abstract method is declared with a method signature (method name, return type, and parameters) but without a body. This means that the method doesn’t perform any action by itself. Instead, it serves as a contract, specifying that any subclass or implementing class must define how the method works.

2. **Purpose of Declaration:**
   - The declaration of an abstract method in an abstract class or interface sets the expectation that subclasses or implementing classes will provide specific behavior. It enforces a structure where certain methods must be implemented, ensuring consistency across different classes that share the same abstract base or interface.

3. **Syntax and Rules:**
   - Abstract methods can only be declared in abstract classes or interfaces. If you try to declare an abstract method in a non-abstract class, the compiler will throw an error because non-abstract classes are supposed to have fully defined methods.
   - If a class has even one abstract method, the class itself must be declared as abstract.

4. **Use Cases for Declaration:**
   - Abstract methods are used when you want to ensure that all subclasses of a class provide specific behaviors. For instance, if you have an abstract class `Shape`, you might declare an abstract method `calculateArea()` to ensure every specific shape (like `Circle`, `Rectangle`, etc.) provides its own way of calculating its area.

#### **Implementation of Abstract Methods:**

1. **Concrete Implementation:**
   - The implementation of an abstract method occurs in a subclass or an implementing class. Here, the method body is provided, defining what the method actually does. This is where the behavior specified by the abstract method is concretely realized.

2. **Binding Declaration to Action:**
   - When a subclass implements an abstract method, it takes the method declaration from the abstract class or interface and binds it to specific actions. This gives the subclass the flexibility to define how the method should behave in the context of that specific class.

3. **Mandatory Implementation:**
   - If a subclass or implementing class does not provide an implementation for an inherited abstract method, it too must be declared abstract. This rule ensures that any concrete class (a class that can be instantiated) has fully defined methods.

4. **Customization in Subclasses:**
   - Different subclasses can implement the same abstract method in different ways. This allows each subclass to define its unique behavior while still adhering to a common interface or abstract base class.

#### **Edge Cases and Considerations:**

1. **Multiple Abstract Methods:**
   - If a class implements an interface or extends an abstract class that has multiple abstract methods, it must provide implementations for all of them. Failing to do so will result in the subclass itself becoming abstract.

2. **Conflicting Method Signatures:**
   - When a class implements multiple interfaces or extends a class with an abstract method and implements an interface with a method of the same name but different signatures, conflicts can arise. The developer must carefully handle these cases, either by providing distinct implementations or by using techniques like method overloading.

3. **Unintended Abstract Methods:**
   - A method might unintentionally be left unimplemented in a subclass. In such cases, the subclass might still compile if it’s declared abstract, but it cannot be instantiated, potentially leading to unexpected limitations in the code’s usability.

4. **Inheritance Chain:**
   - In complex inheritance hierarchies, a method may remain abstract through several layers of classes. In such cases, it’s crucial to ensure that the method is eventually implemented in a concrete subclass. Missing an implementation could break the intended functionality.

5. **Abstract vs. Default Methods in Interfaces:**
   - In some languages (like Java 8 and beyond), interfaces can have default methods—methods with a body. This provides an alternative to abstract methods when you want to provide a default implementation that can be overridden. Understanding when to use an abstract method versus a default method is key to designing flexible and reusable code.

6. **Impact on Instantiation:**
   - Since abstract classes cannot be instantiated, declaring a method as abstract and having it unimplemented in subclasses might inadvertently prevent object creation. This is especially problematic if a concrete implementation was expected but not provided.

#### **Conclusion:**

Abstract methods play a crucial role in object-oriented programming by enforcing that certain methods are implemented in derived classes, ensuring consistency across different subclasses. They represent a powerful tool for designing flexible and extensible systems, but they must be used thoughtfully. Understanding the distinction between the declaration of abstract methods (which sets expectations) and their implementation (which fulfills those expectations) is key to effectively using abstract methods in your code. This balance allows developers to create robust, maintainable, and scalable software architectures.

### Industry-Oriented Use Case for Abstract Methods: Declaration vs. Implementation

#### **Scenario: Payment Processing System**

Imagine you're working on a payment processing system for an e-commerce platform. The system needs to handle different types of payments, such as credit cards, PayPal, and bank transfers. Each payment method has a distinct way of processing transactions, but all must follow a basic set of steps, like validating the payment and processing the transaction.

#### **Step 1: Define an Abstract Class**

First, you create an abstract class `PaymentProcessor` to serve as a blueprint for all payment methods. This class will contain abstract methods that must be implemented by any subclass, ensuring that all payment processors follow a common interface.

```java
public abstract class PaymentProcessor {
    
    // Abstract method for validating the payment
    public abstract boolean validatePayment();

    // Abstract method for processing the payment
    public abstract void processPayment();

    // Concrete method for logging the payment
    public void logPayment(String paymentId) {
        System.out.println("Logging payment with ID: " + paymentId);
    }
}
```

#### **Explanation:**

- **Abstract Methods:**
   - `validatePayment()` and `processPayment()` are abstract methods with no implementation. They must be defined by any class that extends `PaymentProcessor`.

- **Concrete Method:**
   - `logPayment()` is a concrete method with an implementation that can be used by all subclasses. It logs payment details and doesn't need to be redefined unless necessary.

#### **Step 2: Implementing Subclasses**

Now, you create subclasses for different payment methods, each providing its own implementation of the abstract methods.

**CreditCardProcessor.java**

```java
public class CreditCardProcessor extends PaymentProcessor {

    @Override
    public boolean validatePayment() {
        // Specific validation logic for credit cards
        System.out.println("Validating credit card payment.");
        return true; // Simplified for this example
    }

    @Override
    public void processPayment() {
        // Specific processing logic for credit cards
        System.out.println("Processing credit card payment.");
    }
}
```

**PayPalProcessor.java**

```java
public class PayPalProcessor extends PaymentProcessor {

    @Override
    public boolean validatePayment() {
        // Specific validation logic for PayPal
        System.out.println("Validating PayPal payment.");
        return true; // Simplified for this example
    }

    @Override
    public void processPayment() {
        // Specific processing logic for PayPal
        System.out.println("Processing PayPal payment.");
    }
}
```

#### **Explanation:**

- **Concrete Implementations:**
   - Both `CreditCardProcessor` and `PayPalProcessor` provide specific implementations for `validatePayment()` and `processPayment()`. This fulfills the contract set by the abstract class.

- **Shared Behavior:**
   - Both classes can use the `logPayment()` method from the abstract class without reimplementing it, promoting code reuse.

#### **Step 3: Using the Payment Processors**

You might then use these processors in your application like this:

```java
public class PaymentService {

    public void processTransaction(PaymentProcessor processor, String paymentId) {
        if (processor.validatePayment()) {
            processor.processPayment();
            processor.logPayment(paymentId);
        } else {
            System.out.println("Payment validation failed.");
        }
    }

    public static void main(String[] args) {
        PaymentService service = new PaymentService();
        
        PaymentProcessor creditCardProcessor = new CreditCardProcessor();
        service.processTransaction(creditCardProcessor, "CC123");

        PaymentProcessor payPalProcessor = new PayPalProcessor();
        service.processTransaction(payPalProcessor, "PP456");
    }
}
```

#### **Explanation:**

- **Polymorphism:**
   - The `PaymentService` class doesn’t need to know the specifics of each payment method. It simply calls the methods defined by the `PaymentProcessor` abstract class, allowing you to easily switch between different payment methods.

#### **Edge Cases Considered:**

1. **Unimplemented Abstract Methods:**
   - If a subclass fails to implement all abstract methods from the `PaymentProcessor` class, it must also be declared abstract, preventing it from being instantiated directly. This enforces that all necessary methods are defined before the class can be used.

2. **Adding New Payment Methods:**
   - If you introduce a new payment method, say `BankTransferProcessor`, you simply extend `PaymentProcessor` and provide implementations for the abstract methods. This makes the system easily extensible without altering the existing codebase.

3. **Changing the Abstract Class:**
   - If you decide to add a new abstract method to `PaymentProcessor`, all existing subclasses must be updated to implement this new method. This ensures that all payment methods remain consistent with the new requirements but might require refactoring across the codebase.

4. **Default Implementations:**
   - Suppose you realize that some payment methods might share the same validation logic. Instead of making `validatePayment()` abstract, you could provide a default implementation in `PaymentProcessor`. Subclasses could then override it only if they require a different validation approach.

   ```java
   public boolean validatePayment() {
       // Default validation logic
       System.out.println("Default payment validation.");
       return true;
   }
   ```

   This approach can reduce duplication and make the system more maintainable.

#### **Conclusion:**

This use case illustrates how abstract methods help enforce a common structure across different subclasses while allowing each subclass to define its specific behavior. By using abstract classes and methods, you can create a flexible and maintainable system that is easy to extend and modify as new requirements arise. The considerations for edge cases ensure that your design remains robust and adaptable in the face of change.

---

### Interfaces as a Contract for Implementation

#### **What Are Interfaces?**

An interface in object-oriented programming is a way to define a contract that classes must adhere to. An interface specifies a set of methods that a class must implement, but it does not provide the implementation of these methods. Essentially, it defines "what" methods a class should have, but not "how" these methods work.

#### **Purpose of Interfaces**

1. **Defining a Contract:**
   - Interfaces serve as a contract or a promise that a class will provide certain functionalities. When a class implements an interface, it agrees to implement all the methods declared in that interface. This ensures that the class adheres to a specific contract and provides the expected behaviors.

2. **Decoupling Code:**
   - Interfaces help decouple code by defining methods that can be used without knowing the details of their implementation. This allows different parts of a program to interact with objects through their interfaces rather than their specific classes, promoting flexibility and reducing dependencies.

3. **Supporting Multiple Inheritance:**
   - In languages that do not support multiple inheritance (i.e., a class cannot inherit from more than one class), interfaces allow a class to implement multiple interfaces. This provides a way for a class to inherit behaviors from multiple sources, combining different sets of functionality.

4. **Polymorphism:**
   - Interfaces enable polymorphism by allowing objects to be treated as instances of their interfaces rather than their specific classes. This means you can write code that operates on the interface type and works with any class that implements that interface.

5. **Enforcing Consistency:**
   - By defining an interface, you ensure that all implementing classes follow the same structure. This enforces consistency across different classes and ensures that they provide the required methods.

#### **How Interfaces Work**

1. **Defining an Interface:**
   - An interface defines a set of method signatures (name, return type, and parameters) without providing the actual implementation. It acts as a blueprint for other classes.

2. **Implementing an Interface:**
   - A class that implements an interface must provide concrete implementations for all the methods declared in the interface. This class is responsible for defining how these methods work.

3. **Using Interfaces:**
   - Code that interacts with objects through their interfaces can work with any class that implements the interface, regardless of the class’s specific implementation. This promotes flexibility and allows for easier code maintenance and extension.

4. **Interface Inheritance:**
   - Interfaces can extend other interfaces, allowing for more complex contracts. A new interface can inherit methods from one or more existing interfaces, combining their contracts.

#### **Edge Cases and Considerations**

1. **Multiple Inheritance of Interfaces:**
   - While a class can implement multiple interfaces, if two interfaces define methods with the same name and parameters, the class must provide a single implementation. This can be a source of confusion if not handled carefully.

2. **Default Methods in Interfaces:**
   - In some languages (like Java 8 and later), interfaces can include default methods—methods with a body. This allows interfaces to provide common implementations, reducing the need for every implementing class to duplicate code. However, it can complicate the contract if not used judiciously.

3. **Abstract Classes vs. Interfaces:**
   - Deciding between an abstract class and an interface can be tricky. Use interfaces when you want to define a contract without imposing a specific class hierarchy. Use abstract classes when you want to provide some common behavior or state along with the contract.

4. **Interface Segregation:**
   - Avoid creating "fat" interfaces that include too many methods. This violates the Interface Segregation Principle, which suggests that clients should not be forced to implement interfaces they do not use. Instead, create smaller, more focused interfaces.

5. **Implementation Conflicts:**
   - If a class implements multiple interfaces that contain methods with the same name but different signatures, it must provide implementations that handle these methods consistently. This can lead to implementation conflicts and requires careful design.

6. **Legacy Code:**
   - When integrating new interfaces into existing codebases, ensure that the interface contract does not break existing functionality. This might involve adapting or refactoring existing code to fit the new contract.

### Real-Life Use Case Example: Payment Processing System

#### **Use Case Overview:**

Imagine you're developing a payment processing system for an e-commerce platform. The system needs to support multiple payment methods like Credit Card, PayPal, and Bank Transfer. Each payment method has its own specific implementation for processing payments, but they all follow a common set of operations like authorizing and completing a payment.

In this case, you can use an interface to define a contract for all payment methods. Each payment method will implement this interface to provide its own specific behavior while adhering to the common contract.

#### **Interface Definition:**

Here’s how you might define an interface for payment methods:

```java
public interface PaymentMethod {
    boolean authorizePayment(double amount);
    boolean completePayment();
}
```

**Explanation:**
- **authorizePayment(double amount):** This method is intended to authorize the payment of a given amount. The implementation will vary depending on the payment method.
- **completePayment():** This method completes the payment process. Its implementation will also vary.

#### **Implementing the Interface:**

1. **Credit Card Payment:**

```java
public class CreditCardPayment implements PaymentMethod {
    private double amount;
    
    @Override
    public boolean authorizePayment(double amount) {
        // Implement authorization logic specific to credit cards
        this.amount = amount;
        System.out.println("Credit Card payment authorized for amount: " + amount);
        return true; // Assume authorization is successful
    }
    
    @Override
    public boolean completePayment() {
        // Implement completion logic specific to credit cards
        System.out.println("Credit Card payment completed for amount: " + amount);
        return true; // Assume completion is successful
    }
}
```

2. **PayPal Payment:**

```java
public class PayPalPayment implements PaymentMethod {
    private double amount;
    
    @Override
    public boolean authorizePayment(double amount) {
        // Implement authorization logic specific to PayPal
        this.amount = amount;
        System.out.println("PayPal payment authorized for amount: " + amount);
        return true; // Assume authorization is successful
    }
    
    @Override
    public boolean completePayment() {
        // Implement completion logic specific to PayPal
        System.out.println("PayPal payment completed for amount: " + amount);
        return true; // Assume completion is successful
    }
}
```

3. **Bank Transfer Payment:**

```java
public class BankTransferPayment implements PaymentMethod {
    private double amount;
    
    @Override
    public boolean authorizePayment(double amount) {
        // Implement authorization logic specific to bank transfer
        this.amount = amount;
        System.out.println("Bank Transfer payment authorized for amount: " + amount);
        return true; // Assume authorization is successful
    }
    
    @Override
    public boolean completePayment() {
        // Implement completion logic specific to bank transfer
        System.out.println("Bank Transfer payment completed for amount: " + amount);
        return true; // Assume completion is successful
    }
}
```

#### **Using the Interface:**

In the payment processing system, you might use the interface to interact with different payment methods without needing to know the specifics of each:

```java
public class PaymentProcessor {
    public void processPayment(PaymentMethod paymentMethod, double amount) {
        if (paymentMethod.authorizePayment(amount)) {
            paymentMethod.completePayment();
        } else {
            System.out.println("Payment authorization failed.");
        }
    }
}
```

**Explanation:**
- The `PaymentProcessor` class uses the `PaymentMethod` interface to process payments. It does not need to know whether the payment is made via credit card, PayPal, or bank transfer. It just calls the methods defined in the interface.

#### **Edge Cases and Considerations:**

1. **Multiple Implementations:**
   - If the `authorizePayment` method has different signatures across implementations (e.g., one accepts different parameters), ensure consistent method signatures in the interface to avoid conflicts.

2. **Default Methods in Interfaces:**
   - If default methods are used in the interface (e.g., to provide a common logging mechanism), ensure that they don’t conflict with or override methods in implementing classes. For example, adding default implementations for logging should be done carefully to avoid unintended consequences.

3. **Interface Segregation:**
   - Avoid creating a large, monolithic interface with too many methods. Instead, break down the interface into smaller, more focused interfaces if needed. For instance, you might have separate interfaces for authorization and completion if they are used independently.

4. **Legacy Code Integration:**
   - When introducing new interfaces into existing systems, ensure backward compatibility. Existing code using older methods should still function correctly or be refactored to fit the new interface contract.

5. **Method Conflicts:**
   - If a class implements multiple interfaces with methods that have the same name but different signatures, resolve conflicts by providing a single implementation that handles the method consistently.

#### **Conclusion:**

Using interfaces as contracts for implementation in a payment processing system allows for flexibility, extensibility, and decoupling of code. By defining common methods in an interface and providing specific implementations for each payment method, you can create a system that easily accommodates new payment methods without altering existing code. Handling edge cases, such as method conflicts and interface segregation, ensures that your system remains robust and maintainable.

---

### Differences Between Interfaces and Abstract Classes

#### **1. Definition and Purpose:**

- **Abstract Classes:**
   - An abstract class is a class that cannot be instantiated on its own. It is used to define common behavior and state that can be shared by subclasses. Abstract classes can have both abstract methods (methods without implementation) and concrete methods (methods with implementation).
   - **Purpose:** Abstract classes provide a partial implementation and a foundation for subclasses to build upon. They are useful when you want to share code among multiple related classes while also allowing for specific implementations in those subclasses.

- **Interfaces:**
   - An interface is a contract that defines a set of methods that a class must implement. It does not provide any implementation for these methods, only their signatures. Interfaces can also include constants but no instance fields or constructors.
   - **Purpose:** Interfaces define what a class should do, but not how it should do it. They are used to enforce that certain classes provide specific behaviors without dictating how those behaviors are implemented.

#### **2. Key Characteristics:**

- **Abstract Classes:**
   - **Instantiation:** Cannot be instantiated directly. They must be subclassed.
   - **Methods:** Can include both abstract methods (which must be implemented by subclasses) and concrete methods (which have a defined implementation).
   - **Fields:** Can have fields (instance variables) and maintain state.
   - **Constructors:** Can have constructors to initialize fields.
   - **Inheritance:** A class can inherit from only one abstract class due to single inheritance constraints in many languages.

- **Interfaces:**
   - **Instantiation:** Cannot be instantiated. They must be implemented by classes.
   - **Methods:** Only define method signatures (names, return types, and parameters). Methods in interfaces are typically abstract, but some modern languages allow default methods with implementation.
   - **Fields:** Can have constants (static final variables), but no instance fields.
   - **Constructors:** Cannot have constructors.
   - **Inheritance:** A class can implement multiple interfaces, allowing it to inherit behaviors from multiple sources.

#### **3. Use Cases and Design Considerations:**

- **Abstract Classes:**
   - **When to Use:**
      - When you want to provide a common base with some shared functionality that other classes can extend.
      - When you need to define a common interface and share code, but also want to provide some default behavior.
   - **Considerations:**
      - Abstract classes should be used when you have a clear hierarchy of classes and some common behavior or state that should be shared.
      - Be cautious of the single inheritance constraint; if you need to inherit behavior from multiple sources, consider using interfaces.

- **Interfaces:**
   - **When to Use:**
      - When you want to define a set of methods that can be implemented by any class, regardless of its position in the class hierarchy.
      - When you need to support multiple inheritance of behavior (i.e., a class should be able to implement multiple sets of functionalities).
   - **Considerations:**
      - Interfaces should be used to define capabilities or contracts that are not tied to a specific class hierarchy.
      - Ensure interfaces are focused and not overloaded with too many methods. Smaller, specific interfaces adhere to the Interface Segregation Principle.

#### **4. Edge Cases and Potential Issues:**

- **Abstract Classes:**
   - **Overhead:** Adding too much functionality to an abstract class can make it bulky and complex. Be mindful of what should be shared among subclasses and what should remain specific to each subclass.
   - **Single Inheritance Limitation:** A class can only extend one abstract class, which can be restrictive if you need multiple sources of functionality.

- **Interfaces:**
   - **Method Conflicts:** If a class implements multiple interfaces that have methods with the same name but different parameters, it needs to provide a single, consistent implementation.
   - **Default Methods:** Modern languages like Java allow interfaces to have default methods with implementation. This can create complexity if interfaces evolve and introduce new methods, affecting all implementing classes.
   - **No State or Constructor:** Since interfaces cannot maintain state or have constructors, they rely on the implementing classes to handle instance-specific details.

#### **5. Example Scenarios:**

- **Abstract Class Example:** Imagine a base class `Vehicle` that provides common properties like `speed` and methods like `accelerate()`. Specific types of vehicles (e.g., `Car`, `Motorcycle`) extend `Vehicle` and provide their own implementations for certain methods.

- **Interface Example:** Consider an interface `Drivable` with a method `drive()`. Different types of objects (e.g., `Car`, `Bicycle`) that can be driven would implement `Drivable` and provide their own version of the `drive()` method, regardless of their class hierarchy.

### Real-Life Use Case: Abstract Classes vs. Interfaces

Let’s explore a real-life scenario where both abstract classes and interfaces are used. We’ll consider a system for managing various types of user notifications in an application. This system includes different methods of sending notifications, such as via email and SMS.

#### **Scenario Overview**

You need to design a notification system where different types of notifications (like Email and SMS) must be sent using various methods. You also want to ensure that any new notification methods you add in the future adhere to a common set of requirements.

### Using Abstract Classes and Interfaces

#### **Abstract Class Example:**

**Scenario:** You have a common set of functionalities that all notification types share, such as tracking notification history and logging.

**Design:**
1. **Abstract Class:** `Notification`
   - **Purpose:** Provides shared behavior and state for different types of notifications.
   - **Common Functionality:** Tracks notification history and provides default implementations for logging.

2. **Concrete Subclasses:** `EmailNotification`, `SMSNotification`
   - **Purpose:** Implement specific details for sending notifications via email or SMS.

**Code Example:**

```java
abstract class Notification {
    // Common state for all notifications
    private String history;

    // Constructor
    public Notification() {
        this.history = "";
    }

    // Abstract method that must be implemented by subclasses
    public abstract void send(String message);

    // Concrete method with shared functionality
    public void log(String message) {
        history += message + "\n";
        System.out.println("Log: " + message);
    }

    // Get history of notifications
    public String getHistory() {
        return history;
    }
}

class EmailNotification extends Notification {
    @Override
    public void send(String message) {
        // Implementation for sending email
        System.out.println("Sending email: " + message);
        log("Email sent: " + message);
    }
}

class SMSNotification extends Notification {
    @Override
    public void send(String message) {
        // Implementation for sending SMS
        System.out.println("Sending SMS: " + message);
        log("SMS sent: " + message);
    }
}
```

**Edge Cases:**
- **Overhead:** If you add too many methods to `Notification`, it could become bloated. Ensure that only common functionalities are included.
- **Single Inheritance Limitation:** If a new type of notification needs to extend another class, it cannot extend `Notification` due to single inheritance constraints.

#### **Interface Example:**

**Scenario:** You want to define a contract for sending notifications, which can be applied to various types of notifications (e.g., email, SMS, push notifications).

**Design:**
1. **Interface:** `Sendable`
   - **Purpose:** Defines the contract for sending notifications without specifying how the notifications should be sent.

2. **Concrete Implementations:** `EmailSender`, `SMSSender`, `PushNotificationSender`
   - **Purpose:** Provide specific implementations for the `send()` method defined by the `Sendable` interface.

**Code Example:**

```java
interface Sendable {
    void send(String message);
}

class EmailSender implements Sendable {
    @Override
    public void send(String message) {
        // Implementation for sending email
        System.out.println("Sending email: " + message);
    }
}

class SMSSender implements Sendable {
    @Override
    public void send(String message) {
        // Implementation for sending SMS
        System.out.println("Sending SMS: " + message);
    }
}

class PushNotificationSender implements Sendable {
    @Override
    public void send(String message) {
        // Implementation for sending push notification
        System.out.println("Sending push notification: " + message);
    }
}
```

**Edge Cases:**
- **Method Conflicts:** If multiple interfaces have methods with the same name but different parameters, the implementing class must provide a consistent implementation.
- **Default Methods:** If you add default methods to the `Sendable` interface, ensure that they do not conflict with existing implementations.

---

### Designing for Abstraction: Focusing on "What" Rather Than "How"

#### **What Is Abstraction?**

Abstraction in software design is the concept of hiding the complex implementation details and showing only the essential features of an object or system. It focuses on "what" an object does rather than "how" it does it. This helps in simplifying interactions with objects and promotes a clearer separation between the interface and the implementation.

#### **Why Focus on "What" Rather Than "How"?**

1. **Simplification:**
   - By concentrating on what an object does (its behaviors and properties) rather than how it performs those actions, you simplify the way you interact with it. This makes the system easier to use and understand, as users only need to know the purpose and functionality of the object, not its internal workings.

2. **Flexibility and Change Management:**
   - Focusing on "what" allows you to change the underlying implementation without affecting the parts of the system that use the object. This separation makes the system more adaptable to changes and easier to maintain or extend over time.

3. **Code Reusability:**
   - Abstraction encourages designing systems with general-purpose components that can be reused in different contexts. By defining clear interfaces for what these components do, you ensure they can be integrated into various parts of your application without needing to understand their internal workings.

4. **Enhanced Modularity:**
   - Abstraction promotes modular design by allowing you to develop and test components independently based on their interfaces. This modularity helps in managing complexity and enhances the scalability of your system.

#### **How to Design for Abstraction:**

1. **Define Clear Interfaces:**
   - Start by defining what your objects or components should do. Identify the essential functions or behaviors they must provide. This is done by creating clear and well-defined interfaces or abstract classes that specify the methods and properties required.

2. **Separate Interface from Implementation:**
   - Ensure that the interface (the "what") is separate from the implementation (the "how"). The interface should provide methods and properties that define what the object does, while the implementation provides the details of how these functionalities are achieved.

3. **Use Abstract Classes and Interfaces:**
   - Use abstract classes to define common behaviors and properties that multiple subclasses can share. Use interfaces to define contracts that any class can implement, regardless of its inheritance hierarchy. This helps in creating flexible and interchangeable components.

4. **Encapsulate Details:**
   - Encapsulate the internal workings of an object within its implementation. This means that the details of how methods are executed or how data is managed are hidden from the users of the object. Users interact with the object through its interface without needing to understand its internal complexity.

5. **Focus on Purpose:**
   - When designing a component or system, focus on its purpose and how it will be used rather than on its implementation details. Define what the component should accomplish and leave the specifics of how it achieves its goals to the implementation.

#### **Edge Cases and Considerations:**

1. **Over-Abstraction:**
   - Be careful not to over-abstract your design. Too many layers of abstraction can lead to confusion and make the system harder to understand. Strive for a balance where abstraction provides clarity and flexibility without becoming overly complex.

2. **Performance Considerations:**
   - While abstraction simplifies design and development, it can sometimes introduce performance overhead due to additional layers of indirection. Be mindful of performance implications and optimize where necessary, especially in performance-critical applications.

3. **Compatibility Issues:**
   - When abstracting existing code, ensure that the new abstraction layer is compatible with the current system and that it does not break existing functionality. Gradual migration and thorough testing are essential to avoid compatibility issues.

4. **Documentation and Communication:**
   - Proper documentation is crucial when focusing on abstraction. Ensure that the purpose, functionality, and usage of abstract components are well-documented. This helps in communicating the design to other developers and stakeholders.

5. **Testing and Debugging:**
   - Abstraction can sometimes make testing and debugging more challenging because the details are hidden. Develop comprehensive tests for the abstract interfaces to ensure they behave as expected, and use debugging tools to trace issues in the implementation.

6. **Evolving Requirements:**
   - Requirements might evolve over time, requiring changes to the abstraction layers. Be prepared to adjust your abstractions and interfaces as new requirements emerge, while still maintaining a clear separation between what and how.

#### **Conclusion:**

Designing for abstraction involves focusing on "what" an object or system does rather than "how" it achieves its goals. This approach simplifies interactions, enhances flexibility, and promotes modularity. By defining clear interfaces, encapsulating implementation details, and managing edge cases carefully, you can create systems that are easier to maintain, extend, and understand. Balancing abstraction with practical considerations will help you build robust and adaptable software systems.

---


### **1. Easy: Define an Abstract Class and Subclass**

**Problem:**
Define an abstract class named `Employee` with the following abstract method:
- `public abstract double calculateSalary();`

Create two subclasses, `FullTimeEmployee` and `PartTimeEmployee`, that extend `Employee`.
- `FullTimeEmployee` should have a constructor that takes a base salary and override the `calculateSalary` method to return the base salary.
- `PartTimeEmployee` should have a constructor that takes hourly wage and hours worked, and override the `calculateSalary` method to return the total salary based on these values.

**Objective:**
Write code that demonstrates creating instances of both subclasses and calculates their salaries.

### **2. Medium: Interface Implementation with Default Methods**

**Problem:**
Define an interface `Shape` with the following methods:
- `double getArea();`
- `double getPerimeter();`
- A default method `void printDetails()` that prints "Area: [area], Perimeter: [perimeter]" using the `getArea` and `getPerimeter` methods.

Create two classes, `Circle` and `Rectangle`, that implement the `Shape` interface.
- `Circle` should have a constructor that takes the radius and override the methods to calculate the area and perimeter.
- `Rectangle` should have a constructor that takes width and height and override the methods to calculate the area and perimeter.

**Objective:**
Write code that demonstrates creating instances of `Circle` and `Rectangle`, and use the `printDetails` method to print their details.

### **3. Medium: Abstract Class vs. Interface Design**

**Problem:**
Design an abstract class `Vehicle` and an interface `Drivable`.
- The `Vehicle` class should have an abstract method `void startEngine()` and a concrete method `void stopEngine()`.
- The `Drivable` interface should declare a method `void drive()`.

Create a concrete class `Car` that extends `Vehicle` and implements `Drivable`.
- `Car` should provide implementations for `startEngine`, `stopEngine`, and `drive`.

**Objective:**
Write code that demonstrates creating an instance of `Car`, starting the engine, driving, and stopping the engine.

### **4. Hard: Interface Segregation Principle**

**Problem:**
Define an interface `Machine` with the following methods:
- `void start();`
- `void stop();`
- `void reset();`

Due to changes in requirements, the `reset` method is no longer needed for all machines. Refactor the `Machine` interface into multiple smaller interfaces to adhere to the Interface Segregation Principle:
- Create `Startable` with `void start();`
- Create `Stoppable` with `void stop();`
- Create `Resettable` with `void reset();`

Then, create a class `Printer` that implements `Startable` and `Stoppable`, but not `Resettable`. Create another class `Server` that implements all three interfaces.

**Objective:**
Write code that demonstrates using both `Printer` and `Server`, showing how the refactored interfaces align with the new requirements.

### **5. Hard: Abstract Methods and Multiple Inheritance**

**Problem:**
Define an abstract class `Animal` with an abstract method `makeSound()`. Define another abstract class `Mammal` that extends `Animal` and adds an abstract method `nurseYoung()`.

Create an interface `Domestic` with a method `isFriendly()`.

Create a class `Dog` that extends `Mammal` and implements `Domestic`.
- `Dog` should provide implementations for `makeSound`, `nurseYoung`, and `isFriendly`.

Create another class `Cat` that extends `Mammal` and implements `Domestic`.
- `Cat` should provide implementations for `makeSound`, `nurseYoung`, and `isFriendly`.

**Objective:**
Write code that demonstrates creating instances of `Dog` and `Cat`, calling their methods, and displaying their behaviors.
