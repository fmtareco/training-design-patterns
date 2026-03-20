# Gang of Four (GoF) patterns

 Categorizes the 23 Gang of Four (GoF) patterns by their Intent and Core Keyword.

This One-Page Cheat Sheet is designed for a quick "mental warm-up" 5 minutes before your interview. It categorizes the 23 Gang of Four (GoF) patterns by their Intent and Core Keyword.
------------------------------
🚀 Design Patterns Cheat Sheet (GoF)🏗️ Creational: "How to Create"

| Pattern | Core Keyword | Use Case |
|---|---|---|
| Singleton | Global | Shared resources (DB connection, Config). |
| Factory Method | Interface | Let subclasses decide which class to instantiate. |
| Abstract Factory | Family | Creating sets of related objects (Windows vs Mac UI). |
| Builder | Step-by-Step | Complex objects with many optional parameters. |
| Prototype | Clone | Creating objects is expensive; copy an existing one. |

📐 Structural: "How to Assemble"

| Pattern | Core Keyword | Use Case |
|---|---|---|
| Adapter | Translator | Connect two incompatible interfaces. |
| Facade | Entry-Point | Simple interface for a complex library/subsystem. |
| Proxy | Placeholder | Access control, Lazy loading, Logging. |
| Decorator | Wrapper | Add behavior to an object without inheritance. |
| Composite | Tree | Treat single objects and collections the same way. |
| Bridge | Decouple | Separate Abstraction from Implementation (Platform vs UI). |
| Flyweight | Cache | Shared state to save RAM (1,000s of small objects). |

⚙️ Behavioral: "How to Communicate"

| Pattern | Core Keyword | Use Case |
|---|---|---|
| Strategy | Interchangeable | Swap algorithms at runtime (Payment methods). |
| Observer | Pub-Sub | Notify multiple objects of a state change. |
| Command | Object-Request | Queue, log, or undo actions. |
| State | Mode | Object behaves differently based on internal state. |
| Chain of Resp. | Relay | Pass a request through a series of handlers. |
| Template Method | Skeleton | Define steps in superclass; details in subclasses. |
| Iterator | Traversal | Move through a collection without knowing its type. |
| Mediator | Tower | Centralize communication between complex components. |
| Memento | Snapshot | Save/Restore object state (Undo functionality). |
| Visitor | Operation | Add new functionality to classes without changing them. |

------------------------------
💡 Tips:

   1. Don't over-engineer: Only use a pattern if it solves a real problem. Patterns add complexity.
   2. Know your "Triplets":
      * Adapter changes an interface.
      * Proxy provides the same interface.
      * Decorator enhances the interface.
   3. The "Strategy" Default: If you don't know which behavioral pattern to use, Strategy is the safest guess for most logic-swapping scenarios.


