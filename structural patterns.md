# Structural Patterns

List of Structural Design Patterns, ordered from the most straightforward to those that require more architectural overhead (increasing complexity).
These patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

* Adapter
* Complexity: Low
   * Description: Allows objects with incompatible interfaces to collaborate. It acts as a wrapper between two different interfaces.
* Facade
* Complexity: Low
   * Description: Provides a simplified interface to a library, a framework, or any other complex set of classes.
* Proxy
* Complexity: Medium
   * Description: Provides a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request reaches the original object (e.g., logging or caching).
* Decorator
* Complexity: Medium
   * Description: Lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.
* Composite
* Complexity: Medium/High
   * Description: Lets you compose objects into tree structures and then work with these structures as if they were individual objects.
* Bridge
* Complexity: High
   * Description: Lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently.
* Flyweight
* Complexity: High
   * Description: Lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.

