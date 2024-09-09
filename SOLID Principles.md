# Software-Development-Principles
Learning how to apply Design principles in Java Applications.

"_It's not enough for code to work_" - Robert C. Martin (Clean Code)

- Clean & Maintainable architectures are very important.

# Problems
- Change Request can cause
  - Code Fragility
  - Code Rigidity
  - The above two are symptoms of Technical Debt.
# Technical Debt
- Cost of prioritizing fast delivery over code quality for long periods of time.
- Choices of developer
  - Fast delivery (Easiest fix/change, Fast, Poor written code)
  - Code Quality (Takes more time, adds a bit of complexity but maintainable)
# SOLID Principles
## Single Responsibility Principle (SRP)
  - Every function, class or module should have only one reason to change.
  - Examples: Business Logic,UI, Persistence, Logging, Orchestration, Users etc.,
  - Always identify the reasons to change that your components have and reduce them to a single one.
  - Easier to understand, fix and maintain.
  - Classes are less coupled and more resilient to change.
  - More Testable design.
  - **Identifying multiple reasons to change**
    - If-else statements
    - switch statements
    - Monster methods (large lines of code, mix levels of abstraction within implementation)
    - God Classes (Helper, Shared, Utils Methods)
    - People Roles (ex: Report generation)
  - **Dangers of Multiple Responsibilities**
    - Code is more difficult to read and reason about
    - Decreased Quality due to testing difficulty
    - Side effects
    - High Coupling (interdependency between various software components)
  - "_We want to design components that are self-contained, independent,and with a single well-defined principle_" - Andrew Hunt & David Thomas
## Open Closed Principle (OCP)
- Classes,Functions and Modules should be closed for modification and open for extension.
- Why OCP is needed?
  - New features can be added easily with minimal cost.
  - Minimizes the risk of regression bugs.
  - Enforces Decoupling by isolating changes in specific components and works along with SRP.
  - Most effective when used along with SRP.
- OCP Implementation
  - Inheritance (only downside is coupling in the derived classes)
  - **Strategy Design Pattern** (Better approach than inheritance)
    - Use of interfaces to declare capabilities and implementation classes for the features required further.
- Do not use OCP for small Bug fixes.
- Applying OCP for APIs and Frameworks
  - Changes can break the Public APIs for clients.
  - Best Practices
    - Do not change existing public contracts: data classes, method signatures.
    - Expose the abstractions to the customers and let them add new features on top of your framework.
    - If breaking change is inevitable, give your clients time to adapt (make use of deprecated concept).
## Liskov Substitution Principle 
- If S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without modifying the functionality of the program.
- Any object of a type must be _substitutable_ by objects of a derived typed without altering the correctness of the program.
- This principle is all about relationships (not is-a but **is-substitutable-by**).
- Incorrect relationships can cause side effects and unexpected bugs.
- Violations:
  - Empty Methods/Functions. (ex: Is Ostrich substitutable by a Bird which can fly?)
  - Hardened Preconditions. (ex: Is Rectangle fully substitutable by a Square?)
  - Partial Implemented Interfaces.
  - Type Checking
  - Also applies for interfaces and not just for class inheritance.
- Fixing the Violations
  - Eliminate the incorrect relationships between objects.
  - Use 'Tell don't ask!' principle to eliminate type checking and casting.
  - Make sure that a derived type can substitute its base type completely.
  - Keep base classes small and focused.
  - Keep interfaces lean.
- **_If it looks like a duck, quacks like a duck, but needs batteries - you probably have the wrong abstraction._**
## Interface Segregation Principle (ISP)
- Clients should not be forced to depend on methods that they do not use.
- This ISP reinforces other principles,
  - ISP --> LSP (By keeping interfaces small, the classes that implement them have a higher chance to fully substitute the interface).
  - ISP --> SRP (Classes that implement small interfaces are more focused and tend to have single purpose).
- Benefits
  - Lean interfaces minimize dependencies and reduce code coupling.
  - Code becomes more cohesive and focused.
  - **It reinforces the use of LSP and SRP.**
- Identifying _Fat_ Interfaces
  - Interfaces with many methods.
  - Client throws exception instead of implementing methods.
  - Interfaces with low cohesion. (methods that do not align with the overall purpose of interface are called cohesive). This causes increased coupling.
  - It's not just about interfaces but also abstract classes. This can cause Empty methods.
- Fixing Interface Pollution
  - Breaking interfaces.
  - Use design patterns like _**Adapter**_ (when you have legacy interface code you can't control).
  - Interface Reuse.
- **_Many Client specific interfaces are better than one general purpose interface._**
## Dependency Inversion Principle (DIP)
- High level modules (real problems) should not depend on low level modules (various tasks);  both should depend on abstractions.
- Abstractions should not depend on details. Details should depend upon abstraction.
- Example: Payment (HLM) --> Networking (LLM), Notification System(LLM to Payment) (HLM) --> Email Service (LLM)
- Another: User Management (HLM) --> Data Access, Security (LLM).
- Dependency Injection
  - A technique that allows the creation of dependent objects outside a class and provides those objects to a class.
  - Constructor injection
- Inversion of Control (IoC)
  - IoC is a design principle in which the control of object creation, configuration and lifecycle is passed to a container or framework.
  - You don't "new" up objects.
  - Control of Object creation is inverted.
  - Recommended to use it for service, data access, controller objects and **not** entities, value objects.
  - Benefits:
    - Switch between different implementations at run time.
    - Increases program modularity.
    - Manages the lifecycle of the objects and their configuration.
  - Example: Spring Beans
- The DIP, DI, and IoC are most effective in eliminating the code coupling.
- **_New is glue. - Steve Smith_**
## Pyramid of Clean Code (bottom up)
  - Constant Refactoring
  - Unit Testing (TDD)
  - Design Patterns
  - SOLID Principles