

## Creational - Factory Method Pattern (Definition)

- **Definition**
  - A creational design pattern that provides an interface for creating objects, allowing subclasses to decide which class to instantiate.
  - Defers instantiation to subclasses, encapsulating object creation logic.
  - Promotes loose coupling by separating the client code from specific class implementations.
  - **Key Idea**: Use a factory method to create objects without specifying their exact type, enabling flexibility and extensibility.
- **When to Use**
  - When a class cannot anticipate the type of objects it needs to create.
  - When you want subclasses to control object creation.
  - When you need to localize object creation logic.

---

## Creational - Factory Method Pattern (Problem)

- **Problem: Hardcoded Logger Creation**

  - Scenario: A logging system needs to create different loggers (e.g., File, Console) but uses hardcoded logic, making it rigid and hard to extend.
  - **Issues**:
    - Client code directly creates logger objects, leading to tight coupling.
    - Adding a new logger type requires modifying the client code.
    - Violates the open/closed principle, making maintenance difficult.

- **Bad Code Example**

  ```java
  public class LoggerApp {
      public static void main(String[] args) {
          String type = "file"; // Hardcoded or input
          if (type.equals("file")) {
              System.out.println("Logging to file: Error occurred");
          } else if (type.equals("console")) {
              System.out.println("Logging to console: Error occurred");
          } else {
              System.out.println("Unknown logger type");
          }
      }
  }
  ```

  - **Problems**:
    - Inflexible: Adding a new logger (e.g., Database) requires changing the `if-else` logic.
    - Tight coupling: Client code depends on specific logger implementations.
    - Error-prone: Manual type checking increases the risk of mistakes.


---

## Creational - Factory Method Pattern (Solution)

- **Solution: Use Factory Method**

  - Introduce a factory interface to encapsulate logger creation, allowing subclasses to define which logger to instantiate.
  - **Benefits**:
    - Decouples client code from specific logger classes.
    - Simplifies adding new logger types via new factory classes.
    - Follows the open/closed principle for easy extension.

- **Good Code Example**

  ```java
  // Product Interface
  interface Logger {
      void log(String message);
  }
  
  // Concrete Products
  class FileLogger implements Logger {
      public void log(String message) {
          System.out.println("Logging to file: " + message);
      }
  }
  
  class ConsoleLogger implements Logger {
      public void log(String message) {
          System.out.println("Logging to console: " + message);
      }
  }
  
  // Factory Interface
  interface LoggerFactory {
      Logger createLogger();
  }
  
  // Concrete Factories
  class FileLoggerFactory implements LoggerFactory {
      public Logger createLogger() {
          return new FileLogger();
      }
  }
  
  class ConsoleLoggerFactory implements LoggerFactory {
      public Logger createLogger() {
          return new ConsoleLogger();
      }
  }
  
  // Client Code
  public class LoggerApp {
      public static void main(String[] args) {
          LoggerFactory factory = new FileLoggerFactory();
          Logger logger = factory.createLogger();
          logger.log("Error occurred");
  
          factory = new ConsoleLoggerFactory();
          logger = factory.createLogger();
          logger.log("Error occurred");
      }
  }
  ```

---

## Creational - Factory Method Pattern (Pros and Cons)

- **Pros**
  - **Extensibility**: Add new logger types by creating new factory classes without modifying client code.
  - **Loose Coupling**: Client interacts with interfaces, reducing dependency on concrete classes.
  - **Encapsulation**: Hides creation logic, making client code cleaner and focused on usage.
  - **Reusability**: Factory logic can be reused across the application.
- **Cons**
  - **Added Complexity**: Introduces additional classes, which may be overkill for simple systems.
  - **Maintenance**: Changes to the logger interface require updates to all factory classes.
  - **Learning Curve**: Developers unfamiliar with the pattern may find it confusing initially.

---

## Structural - Decorator Pattern (Definition)

- **Definition**
  - A structural design pattern that allows dynamic addition of functionality to objects without modifying their code.
  - Uses decorator classes to wrap objects, extending behavior in a flexible and reusable way.
  - Adheres to the open/closed principle, enabling extensibility without altering existing classes.
  - **Key Idea**: Wrap an object with decorators to add features incrementally, supporting combinations at runtime.
- **When to Use**
  - When you need to add responsibilities to objects dynamically and transparently.
  - When subclassing is impractical due to many possible feature combinations.
  - When you want to keep classes open for extension but closed for modification.

---

## Structural - Decorator Pattern (Problem)

- **Problem: Fixed Ice Cream Customizations**

  - Scenario: An ice cream shop offers customizations (e.g., sprinkles, chocolate) but uses separate classes for each combination, leading to code bloat.
  - **Issues**:
    - Each customization combination requires a new class (e.g., SprinklesIceCream, ChocolateIceCream).
    - Adding new customizations creates exponentially more classes.
    - Violates the open/closed principle by requiring changes to existing code.

- **Bad Code Example**

  ```java
  class VanillaIceCream {
      public String getDescription() {
          return "Vanilla Ice Cream";
      }
      public double getCost() {
          return 3.0;
      }
  }
  
  class SprinklesIceCream {
      public String getDescription() {
          return "Vanilla Ice Cream, Sprinkles";
      }
      public double getCost() {
          return 3.5;
      }
  }
  
  class ChocolateIceCream {
      public String getDescription() {
          return "Vanilla Ice Cream, Chocolate";
      }
      public double getCost() {
          return 4.0;
      }
  }
  
  public class IceCreamShop {
      public static void main(String[] args) {
          VanillaIceCream vanilla = new VanillaIceCream();
          System.out.println(vanilla.getDescription() + ": $" + vanilla.getCost());
  
          SprinklesIceCream sprinkles = new SprinklesIceCream();
          System.out.println(sprinkles.getDescription() + ": $" + sprinkles.getCost());
      }
  }
  ```

  - **Problems**:
    - Cannot combine customizations (e.g., sprinkles + chocolate) without new classes.
    - Adding new customizations increases class count and maintenance effort.


---

## Structural - Decorator Pattern (Solution)

- **Solution: Use Decorator Pattern**

  - Wrap ice cream objects with decorators to add customizations dynamically, supporting flexible combinations without new classes.
  - **Benefits**:
    - Enables runtime addition of customizations (e.g., sprinkles, chocolate).
    - Reduces class proliferation by composing behavior.
    - Follows the open/closed principle for easy extension.

- **Good Code Example**

  ```java
  // Component Interface
  interface IceCream {
      String getDescription();
      double getCost();
  }
  
  // Concrete Component
  class VanillaIceCream implements IceCream {
      public String getDescription() {
          return "Vanilla Ice Cream";
      }
      public double getCost() {
          return 3.0;
      }
  }
  
  // Abstract Decorator
  abstract class IceCreamDecorator implements IceCream {
      protected IceCream iceCream;
      public IceCreamDecorator(IceCream iceCream) {
          this.iceCream = iceCream;
      }
  }
  
  // Concrete Decorators
  class SprinklesDecorator extends IceCreamDecorator {
      public SprinklesDecorator(IceCream iceCream) {
          super(iceCream);
      }
      public String getDescription() {
          return iceCream.getDescription() + ", Sprinkles";
      }
      public double getCost() {
          return iceCream.getCost() + 0.5;
      }
  }
  
  class ChocolateDecorator extends IceCreamDecorator {
      public SprinklesDecorator(IceCream iceCream) {
          super(iceCream);
      }
      public String getDescription() {
          return iceCream.getDescription() + ", Chocolate";
      }
      public double getCost() {
          return iceCream.getCost() + 1.0;
      }
  }
  
  // Client Code
  public class IceCreamShop {
      public static void main(String[] args) {
          IceCream iceCream = new VanillaIceCream();
          System.out.println(iceCream.getDescription() + ": $" + iceCream.getCost());
  
          iceCream = new SprinklesDecorator(iceCream);
          System.out.println(iceCream.getDescription() + ": $" + iceCream.getCost());
  
          iceCream = new ChocolateDecorator(iceCream);
          System.out.println(iceCream.getDescription() + ": $" + iceCream.getCost());
      }
  }
  ```

---

## Structural - Decorator Pattern (Pros and Cons)

- **Pros**
  - **Flexibility**: Add or remove customizations dynamically at runtime.
  - **Modularity**: Separates customizations into distinct classes, improving organization.
  - **Scalability**: Easily introduce new customizations without modifying existing code.
  - **Reduced Classes**: Avoids creating a class for every customization combination.
- **Cons**
  - **Complexity**: Multiple decorators can make the system harder to understand.
  - **Performance Overhead**: Adding many decorators may introduce slight delays.
  - **Debugging Challenges**: Tracing issues through decorator layers can be difficult.

---

## Behavioral - Template Method Pattern (Definition)

- **Definition**
  - A behavioral design pattern that defines the skeleton of an algorithm in a superclass, allowing subclasses to customize specific steps.
  - Preserves the overall algorithm structure while enabling flexibility in implementation details.
  - Encourages code reuse by centralizing common steps in the superclass.
  - **Key Idea**: Provide a fixed algorithm template with customizable steps, ensuring consistency and reusability.
- **When to Use**
  - When you have a common algorithm with variable steps across implementations.
  - When you want to enforce a specific process while allowing customization.
  - When you need to reduce code duplication in similar processes.

---

## Behavioral - Template Method Pattern (Problem)

- **Problem: Duplicated Data Export Logic**

  - Scenario: A data export tool exports data in different formats (e.g., JSON, XML) but duplicates the workflow logic in each class, leading to redundancy.
  - **Issues**:
    - Common steps (e.g., initialize, finalize) are repeated in each exporter.
    - Changes to the workflow require updates to multiple classes.
    - Increases maintenance effort and risks inconsistencies.

- **Bad Code Example**

  ```java
  class JsonExporter {
      void export() {
          System.out.println("Initializing JSON export");
          System.out.println("Exporting data as JSON");
          System.out.println("Finalizing JSON export");
      }
  }
  
  class XmlExporter {
      void export() {
          System.out.println("Initializing XML export");
          System.out.println("Exporting data as XML");
          System.out.println("Finalizing XML export");
      }
  }
  
  public class DataExportTool {
      public static void main(String[] args) {
          JsonExporter json = new JsonExporter();
          json.export();
  
          XmlExporter xml = new XmlExporter();
          xml.export();
      }
  }
  ```

  - **Problems**:
    - Duplicated code for initializing and finalizing exports.
    - No centralized structure to enforce a consistent process.


---

## Behavioral - Template Method Pattern (Solution)

- **Solution: Use Template Method**

  - Define a common export workflow in an abstract class, allowing subclasses to customize the data formatting step.
  - **Benefits**:
    - Eliminates code duplication by centralizing shared steps.
    - Ensures a consistent process across export formats.
    - Simplifies maintenance and supports new formats.

- **Good Code Example**

  ```java
  // Abstract Class
  abstract class DataExporter {
      // Template Method
      public final void export() {
          initialize();
          formatData();
          finalize();
      }
  
      void initialize() {
          System.out.println("Initializing export");
      }
      abstract void formatData();
      void finalize() {
          System.out.println("Finalizing export");
      }
  }
  
  // Concrete Subclasses
  class JsonExporter extends DataExporter {
      void formatData() {
          System.out.println("Exporting data as JSON");
      }
  }
  
  class XmlExporter extends DataExporter {
      void formatData() {
          System.out.println("Exporting data as XML");
      }
  }
  
  // Client Code
  public class DataExportTool {
      public static void main(String[] args) {
          DataExporter json = new JsonExporter();
          json.export();
  
          DataExporter xml = new XmlExporter();
          xml.export();
      }
  }
  ```

---

## Behavioral - Template Method Pattern (Pros and Cons)

- **Pros**
  - **Reusability**: Common steps are defined once, reducing duplication.
  - **Consistency**: Enforces a standard workflow across all export formats.
  - **Extensibility**: New formats can be added by creating new subclasses.
  - **Maintainability**: Workflow changes only require updates to the superclass.
- **Cons**
  - **Inflexibility**: Fixed algorithm structure may limit highly variable processes.
  - **Coupling**: Subclasses depend on the superclass, complicating major changes.
  - **Overuse Risk**: Applying to simple algorithms may add unnecessary complexity.

---

## Overview of Example Patterns

- **Creational: Factory Method**
  - **Definition**: Encapsulates object creation, letting subclasses decide the type.
  - **Problem**: Hardcoded logger creation, causing tight coupling.
  - **Solution**: Factory method enables flexible logger instantiation.
  - **Key Benefit**: Enhances extensibility and loose coupling.
  - **Source**: GeeksforGeeks (https://www.geeksforgeeks.org/factory-method-design-pattern-in-java/)
- **Structural: Decorator**
  - **Definition**: Dynamically adds functionality to objects without modification.
  - **Problem**: Separate classes for ice cream customizations, leading to class explosion.
  - **Solution**: Decorators add customizations dynamically, reducing classes.
  - **Key Benefit**: Supports flexible, runtime feature composition.
  - **Source**: GeeksforGeeks (https://www.geeksforgeeks.org/decorator-pattern/)
- **Behavioral: Template Method**
  - **Definition**: Defines an algorithm skeleton with customizable steps.
  - **Problem**: Duplicated data export logic, increasing maintenance.
  - **Solution**: Template method centralizes common steps, ensuring consistency.
  - **Key Benefit**: Promotes code reuse and maintainability.
