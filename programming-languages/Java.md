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

### User Input

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

### Conditional Statements

#### If, else-if, else blocks

##### Relational Operators

| Operator | Symbol |
| --- | --- |
| greater than | > |
| greater than or equal to | >= |
| less than | < |
| less than or equal to | <= |
| equal to | == |
| strict equal to| === |
| or |  |
| and | && |

##### If statement

```java
public class Main {

    public static void main(String[] args) {

        if (9 > 3) {
            System.out.println("Nine is always greater than three!");
        }
    }
}
```

##### If, else statement

```java
public class Main {

    public static void main(String[] args) {

        if (18 < 14) {
            System.out.println("Is this number bigger?");
        } else {
            System.out.println("This number is not bigger.");
        }
    }
}
```

##### If, else if, else statement

```java
public class Main {

    public static void main(String[] args) {

        if (9 > 12) {
            System.out.println("This line will never print.")
        } else if (9 < 12) {
            System.out.println("This is the answer!")
        } else {
            System.out.println("No need for this, but good to have a catch statement.")
        }
    }
}
```

##### String Comparison

```java
public class Main {

    public static void main(String[] args) {

        System.out.println("Monkey".equals("Monkey"));
        // The above code will print out true because both strings are identical

        System.out.println("Dog".equals("Cat"));
        // The above code will print out false because both strings are not identical
    }
}
```

##### Nesting If statements

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner keyboardInput = new Scanner(System.in);

        System.out.println("Legal Driver Check");

        System.out.print("What is your age?");
        Int age = keyboardInput.nextInt();

        System.out.print("Do you have valid insurance?");
        String validInsurance = keyboardInput.next();

        if (age < 16) {
            System.out.println("Sorry, you are not of legal age.")
        } else {
            if (validInsurance.equals("yes")) {
                System.out.println("Thank you. Go about your day.");
            } else {
                System.out.println("I'm sorry. Your insurance is expired. Please do not drive.");
            }
        }

        // The above conditional checks the answers of the user and responds with the appropriate answer to if they are able to drive legally.
    }
}
```

##### Lexical Scope

- Any code that is derived inside a class can be access globally inside that class.
- Code created in conditionals, nested conditionals or nested classes can only be accessed inside of the code in which they were created.

Example: 
```java
public class Main {

    public static void(String[] args) {

        int numOfPeople = 12;

        if (numOfPeople > 10) {
            System.out.println("Wow! It is crowded in here.")
            int numOfPeopleToLeave = numOfPeople - 10;
        } else {
            System.out.println("This party is great!")
        }

        int peopleWhoAreStillHere = numOfPeople - numOfPeopleToLeave;

        System.out.println("%f people need to leave, now!", numOfPeopleToLeave);

        // The above code will give several errors because the numOfPeopleToLeave variable was initialized inside the if statement and we are trying to access it in the global space of the class.
    }
}
```

##### Switch Statement

- Switch statements are a more dynamic way of using conditionals.
- The syntax for switch statements is easier to read and control.

Example:
```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner keyboardInput = new Scanner(System.in);

        System.out.println("Type a number between 1 and 3?")
        int num = keyboardInput.nextInt();

        switch (num) {
            case 1:
                System.out.println("You entered one.");
                break;
            case 2:
                System.out.println("You entered two.");
                break;
            case 3:
                System.out.println("You entered three.");
                break;
            default:
                System.out.println("Invalid number.");
                break;
        }

        // Switch statements are a great way of cleaning up messy conditionals. Each case is checked to see if it matches the input and responds with the appropriate code.
    }
}
```

