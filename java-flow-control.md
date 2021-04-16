# Java Fundamentals and Flow Control

---

# More Fundamentals

---

## Variables

```java
public class Fundamentals {
  public static void main(String[] args) {
    String name = "Sam";
    System.out.println("Hi " + name);
  }
}
```

- We must declare the type of the variable

---

## Variable Assignment

```java
int counter = 0;
char answer = 'y'
boolean isDone = false;
```

- we use `'` for characters
- lower-camelcase convention for re-assignable variables

---

## Constants

```java
public class Fundamentals {
  public static final NAME = "Sam"
  public static void main(String[] args) {
    System.out.println("Hi " + NAME);
  }
}
```


- `NAME` cannot be reassigned
- `NAME` available to all `static` methods
- Use all upper-case, underscores for constants

---

## Primitive "Wrappers"

```java
int myNum = new Integer(34);
char myChar = new Character('a');
```

- All primitives have more Object Oriented Counterparts
- We conventionally still do direct assignment

---

## Dealing with Types

```java
public class Fundamentals {
  public static void main(String[] args) {
    int num = 97;
    char theChar = (char)num;
    System.out.println(theChar);
    System.out.println((int)theChar);
    System.out.println((short)num);
    System.out.println((double)num);
  }
}
```

```no-highlight
a
97
97
97.0
```

---

## Parsing

```java
public class Fundamentals {
  public static void main(String[] args) {
    int thirtyFour = Integer.parseInt("34");
    System.out.println(thirtyFour + 1);

    double myDouble = Double.parseDouble("34.01");
    System.out.println(myDouble + 1);

    // causes an exception
    int notNumber = Integer.parseInt("thirty four");
  }
}
```

---

## Runtime Exceptions

- Compilers and static typing afford us some protection
- Stuff can still go wrong at runtime
- We must handle for exceptions like `NumberFormatException` or `IOException`

---

## Exception Handling

```java
public class Fundamentals {
  public static void main(String[] args) {
    int thirtyFour = Integer.parseInt("34");
    System.out.println(thirtyFour + 1);

    double myDouble = Double.parseDouble("34.01");
    System.out.println(myDouble + 1);

    // causes an exception
    try {
      int notNumber = Integer.parseInt("thirty four");
    }
    catch(Exception error) {
      //this is bad
      System.out.println("ERROR!");
    }
  }
}
```

---

## Better Exception Handling

```java
public class Fundamentals {
  public static void main(String[] args) {
    int thirtyFour = Integer.parseInt("34");
    System.out.println(thirtyFour + 1);

    double myDouble = Double.parseDouble("34.01");
    System.out.println(myDouble + 1);

    try {
      // causes an exception
      int notNumber = Integer.parseInt("thirty four");
    }
    catch(NumberFormatException error) {
      System.out.println("ERROR!");
    }
  }
}
```

---

## Alternative

```java
public class Fundamentals {
  public static void main(String[] args) throws NumberFormatException {
    int thirtyFour = Integer.parseInt("34");
    System.out.println(thirtyFour + 1);

    double myDouble = Double.parseDouble("34.01");
    System.out.println(myDouble + 1);

    // causes an exception
    int notNumber = Integer.parseInt("thirty four");
  }
}
```

---

# Conditionals and Flow Control

---

## If / Else in Java

```java
if(booleanExpression) {
  //perform this logic if true
}
else {
  //preform this logic if false
}
```

---

## Else If

```java
if(booleanExpression) {
  //perform this logic if true
}
else if(anotherBooleanExpression) {

}
else {
  //preform this logic if false
}
```

---

## A Brief Re-visitation of Boolean Expressions

```java
3 > 4  //false
3 < 4  //true
3 == 4 //false
3 != 4 //true
```

---

## Compound Boolean Expressions

- `&&` - logical **and**
- `||` - logical **or**

---

## Short Circuit Evaluation

```java
true || isNeverEvaluated
false && isNeverEvaluated
```

- Once a logical true is found with an `||`, there is no need to evaluate further
- Once a logical false is found with a `&&`, there is no need to evaluate further

---

## Ternary Operator

```java
Scanner scanner = new Scanner(System.in);
char continueInput = scanner.next().charAt(0);
String continuingMsg = continueInput == 'y' ? "Onward!" : "Ok. Exiting.";
System.out.println(continuingMsg);
```

---

## Switch Statement

```java
switch(userInput) {
  case 'a':
    System.out.println("The student scored a 90 or better");
    break;
  case 'b':
    System.out.println("The student scored somewhere between an 80 and an 89");
    break;
  case 'c':
    System.out.println("The student scored somewhere between an 70 and an 79");
    break;
  case 'd':
    System.out.println("The student scored somewhere between an 60 and an 69");
    break;
  case 'f':
    System.out.println("The student scored lower than a 60");
    break;
  default:
    System.out.println(userInput + " is not a valid letter grade");
}
```

---

## Switch Statements

- We generally avoid using them
- Use an `if...else if...else` instead