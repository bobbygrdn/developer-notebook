# Java

## Data Types

### Primitive

| Data Type | Value Range |
|:------------|:-------------:|
| byte | -128 to 127 |
| short | -32768 to 32767 |
| int | -2147483648 to 2147483647 |
| long | -9223372036854775808 to 9223372036854775807 |
| float | varies |
| double | varies |
| boolean | true/false |
| char | 0 to 65535|

### Reference

| Data Type | Value |
|-|-|
|string|"ABCDEFGHIJKLMNOPQRSTUVWXYZ"|

### Variable Naming Conventions

| Variable Type | Convention |
|-|-|
| int, short, byte, long, float, double, char, string | camelCase |
| boolean | camelCase(starting with is or was) |

### Type Casting

Type casting can help with arithmatic and other use cases by changing the type of the variable to use in further code.

Example:
```java
    int foo = 17;
    int bar = 4;

    System.out.println(((double) foo) / bar);
    // The above code creates a new copy of the foo variable as a double variable so the division can work appropriately
    // Before casting the answer would print -> 4
    // After casting the answer would print -> 4.25
```

### Classes

#### Scanner

There are many built-in classes that can be used in java applications. One such class is called the "Scanner" class.

Example:
```java
// This will import the scanner util
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        // This code builds a new scanner to be used
        Scanner keyboardScanner = new Scanner(System.in);

        // This code is one of the methods that are built-in to the scanner that returns a string
        String input = keyboardScanner.next();
        System.out.println(input); // -> prints the user input
    }
}
```

Example Use Case:
```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner keyboardScanner = new Scanner(System.in);

        System.out.println("What is your name?");
        String userInput = keyboardScanner.next();
        System.out.println(userInput + " is a nice name.");
    }
}

// This simple program asks the user their name and returns their name along with the string
```

#### Format Specifier

Format specifiers use arguments to change the given argument with the second argument(s).

Example:

```java
System.out.format("I have %d cats, %d dogs, and 1 %s.", 7, 2, "panther");

// This will result in printing out the following string -> I have  7 cats, 2 dogs, and 1 panther.
```

Each argument inside the quotations is different depending on the variable type. Each input will format the argument in a different manner depending on the variable type.

| Variable Type | Input |
|-|-|
| Double | %d |
| Float | %f |
| String | %s |

#### Tokens and nextLine() Method

Each token is one part of the string. Most methods only return the first token that is input.

The nextLine method will return the entire input as one string as an accumulation of all tokens.

Example: 

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner keyboardScanner = new Scanner(System.in);

        System.out.println("What is your name?");
        String userName = keyboardScanner.nextLine();
        System.out.println("Hello %s! It is nice to meet you.", userName);
    }
}
// The above program takes in the users input and returns their name in its entirety as they typed it in the output string. This method is more diverse and flexible and will return the input as the user types it regardless of the number of tokens.
```

