# Structural Patterns

List of Structural Design Patterns, ordered from the most straightforward to those that require more architectural overhead (increasing complexity).
These patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

* Adapter
* Complexity: Low
   * Description: Allows objects with incompatible interfaces to collaborate. It acts as a wrapper between two different interfaces.
   
   // Target interface
interface EuropeanSocket { void supply230V(); }

// Adaptee (Incompatible)
class USDevice { void supply110V() { System.out.println("Using 110V..."); } }

// Adapter
class SocketAdapter implements EuropeanSocket {
    private USDevice device = new USDevice();
    public void supply230V() { 
        System.out.print("Converting 230V to 110V: ");
        device.supply110V(); 
    }
}

* Facade
* Complexity: Low
   * Description: Provides a simplified interface to a library, a framework, or any other complex set of classes.
   
   class ComputerFacade {
    private CPU cpu = new CPU();
    private HardDrive hd = new HardDrive();

    public void start() {
        cpu.freeze();
        hd.read();
        cpu.execute();
    }
}
// Usage: new ComputerFacade().start(); // Hide all internal logic

   
* Proxy
* Complexity: Medium
   * Description: Provides a substitute or placeholder for another object. A proxy controls access to the original object, allowing you to perform something either before or after the request reaches the original object (e.g., logging or caching).
   interface Image { void display(); }

class RealImage implements Image {
    public RealImage(String filename) { loadFromDisk(filename); }
    private void loadFromDisk(String f) { System.out.println("Loading " + f); }
    public void display() { System.out.println("Displaying image"); }
}

class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String f) { this.filename = f; }
    public void display() {
        if (realImage == null) realImage = new RealImage(filename); // Lazy Loading
        realImage.display();
    }
}

* Decorator
* Complexity: Medium
   * Description: Lets you attach new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.
   
interface Coffee { double getCost(); }

class SimpleCoffee implements Coffee { public double getCost() { return 1.0; } }

// Decorator
class MilkDecorator implements Coffee {
    private Coffee coffee;
    public MilkDecorator(Coffee c) { this.coffee = c; }
    public double getCost() { return coffee.getCost() + 0.5; }
}
// Usage: Coffee myCoffee = new MilkDecorator(new SimpleCoffee());

   
* Composite
* Complexity: Medium/High
   * Description: Lets you compose objects into tree structures and then work with these structures as if they were individual objects.
   interface FileSystemItem { void showDetails(); }

class File implements FileSystemItem {
    private String name;
    public File(String n) { this.name = n; }
    public void showDetails() { System.out.println("File: " + name); }
}

class Folder implements FileSystemItem {
    private List<FileSystemItem> children = new ArrayList<>();
    public void add(FileSystemItem item) { children.add(item); }
    public void showDetails() { 
        for (FileSystemItem item : children) item.showDetails(); 
    }
}

* Bridge
* Complexity: High
   * Description: Lets you split a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently.

interface Color { void apply(); }
class Red implements Color { public void apply() { System.out.println("Red"); } }

abstract class Shape {
    protected Color color;
    protected Shape(Color c) { this.color = c; }
    abstract void draw();
}

class Circle extends Shape {
    public Circle(Color c) { super(c); }
    void draw() { System.out.print("Drawing Circle in "); color.apply(); }
}
// Usage: Shape redCircle = new Circle(new Red());
   
* Flyweight
* Complexity: High
   * Description: Lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.
   
class TreeType { // Intrinsic state (shared)
    private String name, color;
    public TreeType(String n, String c) { this.name = n; this.color = c; }
}

class TreeFactory {
    private static Map<String, TreeType> types = new HashMap<>();
    public static TreeType getType(String name, String color) {
        if (!types.containsKey(name)) types.put(name, new TreeType(name, color));
        return types.get(name);
    }
}
// Only one TreeType object is created for 1000s of "Oak" trees.

