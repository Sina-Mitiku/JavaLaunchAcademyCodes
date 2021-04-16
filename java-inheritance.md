# Inheritance and Polymorphism

---

## Inheritance to Advance Metaphor

- The _is a_ test
- Considering composition instead of inheritance

---

## The Quintessential Inheritance Example

```java
public class Rectangle {
  private double length;
  private double width;

  public Rectangle(double length, double width) {
    this.length = length;
    this.width = width;
  }

  public double area() {
    return length * width;
  }

  public double perimeter() {
    return 2 * length + 2 * width;
  }
}
```

---

## A Square is a Rectangle

```java
public class Square {
  private double length;

  public Square(double length) {
    this.length = length;
  }

  public double area() {
    return length * length;
  }

  public double perimeter() {
    return 4 * length;
  }
}
```

What's wrong with these two classes?

---

## Inheritance Reduces Duplication

- Children can **inherit** the behavior of their parents

---

## Inheritance in Java

```java
public class Shape {
}

public class Rectangle extends Shape {
}

public class Square extends Rectangle {
}
```

---

## Inheritance in English

- A `Rectangle` is a `Shape`
- A `Square` is a `Rectangle`

- A `Rectangle` behaves as a `Shape`
- A `Square` behaves as a `Rectangle`

This is the essence of **polymorphism**.

---

## Polymorphism is a Fancy Way to Say...

All children can behave exactly like its parent.

---

## Constructors and Inheritance

- Constructors must be explicit
- The `super` keyword can be called to call parent constructors

```java
public class Rectangle extends Shape {
  private double width;
  private double length;

  public Rectangle(double width, double length) {
    this.width = width;
    this.length = length;
  }
}

public class Square extends Rectangle {
  public Square(double length) {
    super(length, length);
  }
}
```

---

## We can Override the Methods that are Different

```java
public class Rectangle extends Shape {
  ...

  public void printInformation() {
    System.out.println("This is a RECTANGLE object");
  }
}

public class Square extends Rectangle {
  ...

  @Override
  public void printInformation() {
    System.out.println("This is a SQUARE object");
  }
}
```

---

## Reducing Duplication

- With this setup, we can implement `area` and `perimeter` behaviors in `Rectangle`
- `Square` will get those behaviors for free
- We can Override anything we need to

---

## Private data is private to the class

Private state and behavior is _not_ accessible from the child

```java
public class Rectangle extends Shape {
  private double length;
  private double width;
}

public class Square extends Rectangle {
  public void output(){
    //Nope - can't be done
    System.out.println(this.width);
  }
}
```

---

## Private Data Can't be Seen From the Outside

Private state and behavior is _not_ accessible from the child

```java
public class Rectangle extends Shape {
  private double length;
  private double width;

  public double getLength() {
    return this.length;
  }

  public double getWidth() {
    return this.width;
  }
}

public class Square extends Rectangle {
  public void output(){
    System.out.println(this.getWidth());
  }
}
```

---

## Abstract Classes

- Abstract classes cannot be instantiated
- Abstract classes define behaviors that must be implemented by inheritors

```java
public abstract class Shape {
  public abstract double perimeter();
  public abstract double area();
}
```

---
## Rectangle implements Shape..

```java
public class Rectangle extends Shape {
  private double length;
  private double width;

  public Rectangle(double length, double width) {
    this.length = length;
    this.width = width;
  }
  public double area() {
    return length * width;
  }
  public double perimeter() {
    return 2 * length + 2 * width;
  }

  public void setLength(int length) { this.length = length; }
  public double getLength() { return this.length; }

  public void setWidth(int width) { this.width = width; }
  public double getWidth() { return this.width; }
}
```
---
## And Square inherits Rectangle...

```java
public class Square extends Rectangle{

  public Square(double length) {
    super(length, length);
  }
  public double area() {
    return getLength() * getLength();
  }
  public double perimeter() {
    return 4 * getLength();
  }
}
```

---
## Circle also implements Shape, but in a different way!

```java
public class Circle extends Shape {
  private double radius;

  public Circle(double radius) {
    this.radius = radius;
  }

  @Override
  public double perimeter() {
    return 2 * Math.PI * this.radius;
  }

  @Override
  public double area() {
    return this.radius * this.radius * Math.PI;
  }
}
```

---

## It's all Hierarchical

- A Rectangle is a Shape
- A Square is a Rectangle

```java
public abstract class Shape {
  public abstract double perimeter();
  public abstract double area();
}

public class Rectangle extends Shape {
  private double length;
  private double width;

  ...
}

public class Square extends Rectangle {
  public void output(){
    System.out.println(this.getLength());
  }
}
```

---

## Polymorphism Illustrated

```java
public class ShapeStatPrinter {
  public static String printStats(Shape shape) {
    return "Area: " + shape.area() + "\nPerimeter: " + shape.perimeter();
  }

  public static main(String[] args) {
    Square square = new Square(4.0);
    Circle circle = new Circle(5.0);

    printStats(square);
    printStats(circle);
  }
}
```

---

## Polymorphism Illustrated Part II

```java
public class ShapeCollectionRunner {
  public static void main(String[] args) {
    ArrayList<Shape> shapeList = new ArrayList<Shape>();
    Rectangle twoByTwo = new Rectangle(2, 2);
    Rectangle threeByFour = new Rectangle(3, 4);
    Circle smallCircle = new Circle(2);

    shapeList.add(twoByTwo);
    shapeList.add(threeByFour);
    shapeList.add(smallCircle);

    for(Shape shape : shapeList) {
      System.out.println(shape.area());
    }
  }
}
```

---

## The Abstract Class Connects the Shapes

- `printStats` only cares that `area` and `perimeter` methods are defined
  - Both `Circle` and `Square` instances behave as a `Shape`, so the JVM allows for it
- Our `ArrayList` generic takes in `Shape` objects, so `Rectangle` and `Circle`s are allowed
  - This works in our `for` loop, and it's fairly able to assume that the `area` method exists
