# Java Loops

---

## While Loops

The easiest looping structure is `while()`.  It takes a conditional statement between the '(' and ')'.

```Java
while ( true ) {
  // do something
}
```

---

### While example

```Java
public class WhileLoopExample {
  public static void main(String[] args) {
    int numDinosaurs = 10;
    int count = 1;
    while (count <= numDinosaurs) {
      System.out.println(count + " little dinosaur(s)");
      count++;
    }
  }
}
```

```no-highlight
1 little dinosaur(s)
2 little dinosaur(s)
3 little dinosaur(s)
4 little dinosaur(s)
5 little dinosaur(s)
6 little dinosaur(s)
7 little dinosaur(s)
8 little dinosaur(s)
9 little dinosaur(s)
10 little dinosaur(s)
```

---

## Recall the Racetrack Analogy

This will keep looping until the conditional resolves to `false`.

---

```java
public class WhileLoopExample {
  public static void main(String[] args) {
    int numDinosaurs = 10;
    int count = 11;
    while (count <= numDinosaurs) {
      System.out.println(count + " little dinosaur(s)");
      count++;
    }
  }
}
```

What is the output of this routine?

---

## The Body of a While Doesn't Always Execute

If the condition is initially false, the body is not evaluated

---

## Do...While() Loops

Want to run at least once? Use `do...while`

```Java
do {
  // do something
} while (true);
```

As with `while()`, its conditional test has to be true to keep looping.  It is just like the `while()` loop but it runs once before the condition is checked.

---

### Do...While() example

```Java
public class DoWhileExample {
  public static void main(String[] args) {
    int numDinosaurs = 10;
    int count = 1;
    do {
      System.out.println(count + " little dinosaur(s)");
      count++;
    } while (count <= numDinosaurs);
  }
}
```

```no-highlight
1 little dinosaur(s)
2 little dinosaur(s)
3 little dinosaur(s)
4 little dinosaur(s)
5 little dinosaur(s)
6 little dinosaur(s)
7 little dinosaur(s)
8 little dinosaur(s)
9 little dinosaur(s)
10 little dinosaur(s)
```

---

## When would you use While() and Do...While()?

Use `do...while()` when you want to process something *before* the test is run.

---

## Use Do...While for Prompts

```java
import java.util.Scanner;

public class WhileInput {

  public static void main(String[] args) {
    String response;
    Scanner scanner = new Scanner(System.in);
    do {
      System.out.println("Do you like pizza?");
      response = scanner.next();
      if (!response.toLowerCase().equals("yes")) {
        System.out.println("Inconceivable");
      }
    } while (!response.toLowerCase().equals("yes"));
  }
}
```

---

## For Loops

A `while` loop shortcut

```Java
for (initialization; conditionToCheckWithEachLoop; actionToPerformAtEnd) {
  // do something
}
```

- `initialization` is done before the loop
- `conditionToCheckWithEachLoop` is loop conditional
- `actionToPerformAtEnd` is what is done before the end of the loop

- The semi-colons are important here.
- Ensure your `actionToPerformAtEnd` affects the `conditionToCheckWithEachLoop`

---

## For example

```Java
public class ForLoopExample {
  public static void main(String[] args) {
    int numDinosaurs = 10;
    for (int count = 1; count <= numDinosaurs; count++) {
      System.out.println(count + " little dinosaur(s)");
    }
  }
}
```
