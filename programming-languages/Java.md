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
| string | "ABCDEFGHIJKLMNOPQRSTUVWXYZ" |
| array | [2,5,6,7] |

## Variable Naming Conventions

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

## User Input

### Scanner

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

### Format Specifier

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

### Tokens and nextLine() Method

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

## Conditional Statements

### If, else-if, else blocks

#### Relational Operators

| Operator | Symbol |
| --- | --- |
| greater than | > |
| greater than or equal to | >= |
| less than | < |
| less than or equal to | <= |
| equal to | == |
| or | &#124; |
| and | && |
| increment | ++ |
| decrement | -- |
| modulo | % |

#### If statement

```java
public class Main {

    public static void main(String[] args) {

        if (9 > 3) {
            System.out.println("Nine is always greater than three!");
        }
    }
}
```

#### If, else statement

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

#### If, else if, else statement

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

#### String Comparison

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

#### Nesting If statements

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

#### Lexical Scope

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

#### Switch Statement

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

## Loops

### While Loop

- The while loop takes a condition as an argument and runs the code until the argument returns false

```java
public class Main

    public static void main(String[] args) {

        int i = 0;

        while (i < 5) {
            System.out.println("Test")
            i++;
        }
        // The above loop will run until the i variable become 5.
    }
```

### For Loop

- The For loop takes in three arguments. An initialized counter variable, a condition to tell the loop when to stop and an increment or decrement to the counter variable.
- These arguments tell the For loop how you want it to run and for how long. It will run any code inside it for the predetermined amount of time based off of the counter variable.

```java
public class Main {

    public static void main(String[] args) {

        for(int i = 0; i < 8; i++) {
            System.out.println(i);
        }
        // This loop will continuously run printing the current value of the i variable.
    }
}
```

### Break & Continue

- The break and continue keywords are used to tell the loop what behavior to take on depending on when they are put into the loop.
- Break stops the loop and continues on in the program.
- Continue stops the current cycle of the loop and moves on to the next cycle of the loop.

```java
public class Main {

    public static void main(String[] args) {

        for(int i = 1; i < 7; i++) {
            if(i == 3) {
                continue;
            }

            System.out.println(i);

            if(i == 6) {
                break;
            }
        }
    }
    // The above loop will print out each value of that i variable except for when i equals 3. The loop will break once i is equal to 6 which is before the input argument.
}
```

### Do While Loop

- The Do While Loop is similar to the while loop except the Do While Loop will always run the code once before checking its condition.
- This can be helpful if you want a piece of code to always run at the start.

```java
public class Main {

    public static void main(String[] args) {

        int i = 0;

        do {
            System.out.println("I ran!")
        } while (i < 2);
    }
    // This Do While Loop will print out I ran! until i becomes equal to the number 2.
    // The initial print statment is ran before the condition is checked.
}
```

## Arrays

### Basics of Arrays

- Arrays are containers that store values
- Arrays can hold a collection of data
- The data inside an array is identified by their index starting with 0
- Arrays will always have a set length upon its creation which cannot be changed after it is created

Example:

| Index | Element |
|-|-|
| 0 | "Charles" |
| 1 | 75 |
| 2 | "Steven" |
| 3 | 48 |
| 4 | "ABC" |

```java
public class Main {

    public static void main(Stringp[] args) {

        int[] nums = {75, 29, 350, 7, 4192};
        // The above variable is an array of numbers

        String[] names = {"Bob", "Charles", "Steven"};
        // The above variable is an array of strings.
    }
}
```

### Adaptive Iteration

- When iterating through an array we usually use loops
- Using loops we should set the conditional to be the length of the element. This way the loop is more dynamic and can adapt to the length of the array we are iterating through
- We do this because Arrays are 0-indexed so setting the condition to end when the variable is the same value as the length of the array, the loop will end appropriately

```java
public class Main {

    public static void main(String[] args) {

        int[] numbers = {1,2,3,4,5,6,7,8,9};

        for (int i = 0; i < numbers.length; i++) {

        }
        // The above loop will iterate through the array using the length of the array as the condition in which the loop should stop.
        // If I change the length of the array, the for loop will still work appropriately because of its adaptive nature.
    }
}
```

### Simple Processing

- We can use conditionals inside loops to process arrays in different ways
- This is helpful in many cases because it allows us to set conditions to utilize the array in ways we choose

```java
public class Main {

    public static void main(String[] args) {

        int[] numbers = {2,4,5,7,1,0};

        for(int i = 0; i < numbers.length; i++) {

            if(numbers[i] > 4) {
                System.out.println("Found a high number!")
            }
        }
        // The above loop will iterate through the array and only print out numbers that match our conditional.
    }
}
```

### Sizes and Types

- The proper way to create an array of elements is by giving it an initial length
- We do this because once we create the array, the length cannot be changed
- Arrays can be created using any data type

```java
public class Main {

    public static void main(String[] args) {

        String[] names = new String[10];
        // The above array will be initialized with 10 elements that are default to empty strings.
        // The elements will be indexed from 0 to 9;

        names[0] = "George";
        names[7] = "Nancy";
        // We have changed the value of the 0 indexed element to George and the 7th indexed to Nancy;

        int[] numbers = new int[4];
        // The above array of numbers is initialized with 4 0's.
        // The indexes are from 0 to 3;

        numbers[1] = 9;
        numbers[3] = 10;
        // We have changed the 1st indexed element to the number 9 and the 3rd indexed element to the number 10;
    }
}
```

### For Each Loop

- A For Each loop can be used to iterate through a list with simpler syntax
- For Each loops are only used for lists and not basic data types

```java
public class Main {

    public static void main(String[] args) {

        String[] names = {"Steve", "Charles", "Rebecca", "Robert"};

        for(String e : names) {
            System.out.println(e);
        }
        // The above for each loop will print out each name in the names list.
    }
}
```

## Methods (Functions)

### Basics of Methods

- Methods are pieces of code that are run for a specific purpose
- They can be called within other methods and ran at anytime we invoke them
- They can be invoked with or without parameters or arguments
- Methods can be given any name just like variables
- It is best practice to name the first method "main"

```java
public class Main {

    public static void main(String[] args) {
        System.out.println("I am the first method!")
        main2();
    }

    public static void main2() {
        System.out.println("I am the second method.");
    }
}
// Running the above code will result in printing two lines. One for the main method and one for the main2 method.
```

### Passing data to methods

- Data can be passed into methods using arguments
- Arguments are variables that hold data that are passed down into methods for use inside those methods

```java
public class Main {

    public static void main(String[] args) {

        int var;
        var = 5;
        main2(var);
    }

    public static void main2(int number) {
        System.out.println(number);
    }
}
// The main method creates the var variable and assigns it the value of 5.
// The main2 method gets passed the var variable and then prints that variables value.
```

### Returning data from methods

- Data can be returned from methods using the return keyword

```java
public class Main {

    public static void main(String[] args) {
        System.out.println(main2());
    }

    public static int main2() {
        return 9;
    }
}
// This program will print out the number 9.
// The integer is returned from the main2 function and passed into the print statement of the main method.
```

### Passing and Returning data

- Data can be passed and returned from methods
- This allows data to flow throughout the program to be utilized in different places

```java
public class Main {

    public static void main(String[] args) {
        System.out.println(add(5,7), add(9,4));
    }

    public static int add(int a, int b) {
        return a + b;
    }
}
// The add method is created to be utilized many times because it is built to be adaptive and reuseable.
// The main method is calling the add method twice in a print statement. So the result will print -> 12, 13.
```

### References

- Primitive data types are passed by the value that they hold.
- Reference data types like arrays are passed by reference. Where they are stored in memory is their reference.

```java
public class Main{

    public static void main(String[] args) {
        int[] x = {1,2,3,4};
        int[] y = x;

        System.out.println(x, y);
    }
}
// This print statement will print out two arrays that look like this -> [1,2,3,4] because y has been assigned the reference array that was assigned to the x variable. So they are both pinting at the same array in memory.
```

### Class/Static members

- Class variables are "global" variables that can be utilized in any method inside the parent class
- Static members are pieces of data that can only be used in the methods they are created in

```java
public class Main {

    static int x = 6;

    public static void main(String[] args) {
        main2();
    }

    static void main2() {
        System.out.println(x);
        main3();
    }

    static void main3() {
        int y = 10;
        System.out.println(y);
        main4();
    }

    static void main4() {
        System.out.println(y);
    }
}
// The program above will result in an error and will not compile because the main4 method is trying to utilize a variable that was created inside the main3 method.
```

## OOP (Object-oriented Programming)

### Data Structures

- Data Structures are a collection of variables under a specific name
- These data structures can be reused and duplicated throughout the program
- This is how modern programming languages make code bases manageable and easier to read
- These data structures create bundles of code that are easier to debug and modify

```java
public class Car {
    String color;
    int numOfWheels;
    int numOfDoors;
    String make;
    String model;
}

public class Main {

    public static void main(String[] args) {

        Car myCar = new Car;

        myCar.color = "blue";
        myCar.numOfWheels = 4;
        myCar.numOfDoors = 2;
        myCar.make = "Ford";
        myCar.model = "Mustang";
    }
}
```

### State and Behavior

- State is the different attributes of a given or created object
- This mirrors what attributes objects have in real life
- Behavior is the code that deals with the actions an object can take

```java
public class Door {
    boolean isOpen;
    boolean isLocked;
    String color = brown;

    void open() {
        isOpen = true;
    }

    void close() {
        isOpen = false;
    }

    void lock() {
        isLocked = true;
    }

    void unlock() {
        isLocked = false;
    }

    void get color() {
        System.out.println(this.color);
    }
}
```

### Encapsulation

- This is the term we use to explain the process of containers of code that hold certain pieces that are held from other parts of the program
- Encapsulation enables us to bundle code for easier debugging and development
- Objects use encapsulation to hold their state and behavior in a way so that only the object itself can change its state
- Outside code shouldn't be able to affect a piece of state inside an object without using a method or a "behavior" from the object

```java
public class Rectangle {
    private int height = 1;
    private int width = 1;

    public void setHeight(int h) {
        if (h > 0) {
            height = h;
        }
    }

    public void getHeight() {
        return height;
    }

    public void setWidth(int w) {
        if (w > 0) {
            width = w;
        }
    }

    public void getHeight() {
        return width;
    }

    public int getArea() {
        return height * width;
    }
}

public class Main {

    public static void main(String[] args) {

        Rectangle r1 = new Rectangle();
        r1.setHeight(5);
        r1.setWidth(9);

        System.out.println(r1.printArea());
    }
}
```

### Constructors

- Constructors use the same name as the class
- It does not return any value 
- Constructors run their code automatically when instances are created

```java
public class Rectangle {
    private int height = 1;
    private int width = 1;

    public Rectangle(int h, int w) {
        setHeight(h);
        setWidth(w);
    }
}

public class Main {
    public static void main(String[] args) {
        Rectangle r1 = new Rectangle(7, 9);

        Rectangle r2 = new Rectangle(8, 4);

    }
}
```

### ArrayList

- ArrayList should always be used instead of arrays
- They are more dynamic and less fixed than normal arrays
- ArrayLists will shrink and grow depending on the data they hold
- The length of the ArrayList does not need to be specified
- ArrayLists have built in methods to manipulate their data

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> stringArrayList = new ArrayList<String>();

        stringArrayList.add("toaster"); // -> adds the given element
        stringArrayList.add("fridge"); // -> adds the given element
        stringArrayList.add("kettle"); // -> adds the given element

        stringArrayList.remove("fridge"); // -> removes the given element
        stringArrayList.remove(0); // -> removes the given element at the given index

        stringArrayList.indexOf("kettle"); // -> returns the index of the given element

        stringArrayList.contains("fridge"); // -> returns a boolean if the ArrayList contains the given element

        stringArrayList.get(1); // -> Gets the element at the given index

        stringArrayList.set(1, "microwave"); // -> Changes the element at the given index

        stringArrayList.size(); // -> Gets the size of the ArrayList

        stringArrayList.clear(); // -> Clears theArrayList
    }
}
```

### Enums

- Enums are a data type that we can use to specify a fixed set of values
- Enums hold constant values that cannot be changed
- Enums handle values that are not contained inside the Enum by throwing a compile error

```java
public enum Month {
    JANUARY,
    FEBRUARY,
    MARCH,
    APRIL,
    MAY,
    JUNE,
    JULY,
    AUGUST,
    SEPTEMBER,
    OCTOBER,
    NOVEMBER,
    DECEMBER,
}

public class Main {
    public static void main(String[] args) {
        whichSeason(Month.March);
    }

    public static void whichSeason(Month month) {
        switch(month) {
            case DECEMBER, JANUARY, FEBRUARY:
                System.out.printf("%s is in the winter season.\n", month);
                break;
            case MARCH, APRIL, MAY:
                System.out.printf("%s is in the spring season.\n", month);
                break;
            case JUNE, JULY, AUGUST:
                System.out.printf("%s is in the summer season.\n", month);
                break;
            case SEPTEMBER, OCTOBER, NOVEMBER:
                System.out.printf("%s is in the autumn season.\n", month);
                break;
        }
    }
}
```

## OOP: Inheritance and Polymorphism

### Inheritance and Access Level Modifiers

- Inheritance is where one class inherits certain properties from another class
- Parent classes usually pass their properties down to their child classes
- We can extend the properties from one class to another using the extend keyword
- Constructors are not inherited, each class needs its own constructor or call the super keyword which runs the parent class constructor
- An empty constructor with zero arguments is called if you do not create a constructor

```java
// Main class
package p1;

public class Main {
    public static void main(String[] args) {
        B b = new B();
        System.out.println(b.v5);
        System.out.println(b.v3);
    }
}

// Superclass A or Parent class A
package p2;

public class A {
    public int v1 = 5;
    protected int v2 = 10; // class B inherits, but is inaccessible by any other class
    int v3 = 15; // Only inherited by classes that are in the same package, It is a private package variable
    private int v4 = 20; // cannot be inherited or accessed by any other class

    protected void m1() {
        System.out.println("something");
    }
}

// Subclass B or Child class B
package p3;

import p2.a;

public class B extends A {
    public int v5 = 100;
    public int v6 = 101;

    public void someMethod() {
        v2 = 40;
    }
}
```

### The Bank Account Program

- Account
    - CheckingAccount -> Inherits from Account
        - SilverCheckingAccount -> Inherits from Account and CheckingAccount
        - GoldCheckingAccount -> Inherits from Account and CheckingAccount
        - DiamondCheckingAccount -> Inherits from Account and CheckingAccount
    - SavingsAccount -> Inherits from Account


```java
// Main class
public class Main {
    public static void main(String[] args) {
        Account account = new Account(100, 0.025);
        account.status();
        account.withdrawal(45.86);
        account.status();
        account.withdrawal(62.96);
        account.status();        
        account.deposit(32.50);
        account.status();
    }
}

// Account class
package account;

public class Account {
    private double balance;
    private double interestRate;

    public Account(double balance, double interestRate) {
        this.balance = balance;
        this.interestRate = interestRate;
    }

    public boolean = withdrawal(double account) {
        if (amount > balance) {
            return false;
        }

        balance -= amount;
        return true;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public double getBalance() {
        return balance;
    }

    public double getInterestRate() {
        return interestRate;
    }

    public void status() {
        System.out.printf("Balance: %.2f\n", balance);
    }
}
```

### Constructors and Inheritance

```java
// Main class
import accounts.CheckingAccount;

public class Main {
    public static void main(String[] args) {
        CheckingAccount checkingAccount = new CheckingAccount(100, 0.042);
        checkingAccount.status();
        checkingAccount.deposit(20);
        checkingAccount.status();
    }
}

// Account class
package accounts;

public class Account {
    private double balance;
    private double interestRate;

    public Account(double balance, double interestRate) {
        this.balance = balance;
        this.interestRate = interestRate;
    }

    public boolean = withdrawal(double account) {
        if (amount > balance) {
            return false;
        }

        balance -= amount;
        return true;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public double getBalance() {
        return balance;
    }

    public double getInterestRate() {
        return interestRate;
    }

    public void status() {
        System.out.printf("Balance: %.2f\n", balance);
    }
}

// CheckingAccount class
package accounts;

public class CheckingAccount extends Account {
    public CheckingAccount(double balance, double interestRate) {
        super(balance, interestRate);
        
    }
}

// SavingsAccount class
package accounts;

public class SavingsAccount extends Account {
    public SavingsAccount(double balance, double interestRate) {
        super(balance, interestRate);
    }
}
```


### Method Overriding

```java
// Main class
import accounts.CheckingAccount;
import accounts.SilverCheckingAccount;

public class Main {
    public static void main(String[] args) {
        CheckingAccount checkingAccount = new CheckingAccount(100, 0.042, 700);
        checkingAccount.status();

        SavingsAccount savingsAccount = new SavingsAccount(100, 0.045);
        savingsAccount.status();
        savingsAccount.withdrawal(10);
        savingsAccount.status();

        SilverCheckingAccount silveraccount = new SilverCheckingAccount(250, 0.026, 765);
        silverAccount.status();


    }
}

// Account class
package accounts;

public class Account {
    protected double balance;
    private double interestRate;

    public Account(double balance, double interestRate) {
        this.balance = balance;
        this.interestRate = interestRate;
    }

    public boolean = withdrawal(double account) {
        if (amount > balance) {
            return false;
        }

        balance -= amount;
        return true;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public double getBalance() {
        return balance;
    }

    public double getInterestRate() {
        return interestRate;
    }

    public void status() {
        System.out.printf("Balance: %.2f\n", balance);
    }
}

// CheckingAccount class
package accounts;

public class CheckingAccount extends Account {
    public int rewardsPoints;

    public CheckingAccount(double balance, double interestRate, int rewardsPoints) {
        super(balance, interestRate);
        this.rewardsPoints = rewardPoints;
    }

    public boolean purchase(double cost) {
        if (cost > balance) {
            return false;
        } 

        balance -= cost;
        rewardPoints += calculateRewardPoints(cost);
        return true;
    }

    public int calculateRewardPoints(double cost) {
        return (int) (cost * 10);
    }

    public getRewardPoints() {
        return rewardPoints;
    }
}

// SilverCheckingAccount class
package account;

public class silverCheckingAccount extends CheckingAccount {
    public silverCheckingAccount(double balance, double interestRate, int rewardPoints) {
        super(balance, interestRate, rewardPOints);
    }

    @override
    public int calculateRewardPoints(double cost) {
        return (int) (cost * 25);
    }
}

// GoldCheckingAccount class
package account;

public class GoldCheckingAccount extends CheckingAccount {
    public GoldCheckingAccount(double balance, double interestRate, int rewardPoints) {
        super(balance, interestRate, rewardPOints);
    }

    @override
    public int calculateRewardPoints(double cost) {
        return (int) (Math.min(cost, 4000 *50));
    }
}

// DiamondCheckingAccount class
package account;

public class DiamondCheckingAccount extends CheckingAccount {
    public DiamondCheckingAccount(double balance, double interestRate, int rewardPoints) {
        super(balance, interestRate, rewardPOints);
    }

    @override
    public int calculateRewardPoints(double cost) {
        int rewards = 0;

        if (cost > 500) {
            rewards += (cost - 500) * 80;
        }
        if (cost > 100) {
            rewards += (cost - 100) * 65;
        }
        rewards += cost * 40;
        return rewards;
    }
}

// SavingsAccount class
package accounts;

public class SavingsAccount extends Account {
    public SavingsAccount(double balance, double interestRate) {
        super(balance, interestRate);
    }

    @override
    public boolean withdrawal(double amount) {
        double fee = 0.025 * amount;
        amount += fee;

        return super.withdrawal(amount); // calls the parent class version of this method
    }

    @override
    public void deposit(double amount) {
        super.deposit(amount);
    }
}
```

### Polymorphism

- The variable type determines what methods are available to be called 
- The object type determines which version of the method is called
- We can store multiple objects in one variable such as an ArrayList and affect them in the same manner

### Abstract Classes

- Abstract classes cannot be instantiated, the purpose of the class is to be extended

- Vehicle class -> Abstract class
    - int speed
    - abstract void move()
        - Car class -> Subclass extended from Vehicle class
            - int speed
            - @override void move()
        - Boat class -> Subclass extended from Vehicle class
            - int speed
            - @override void move()
        - Plane class -> Subclass extended from Vehicle class
            - int speed
            - @override void move()
        - Helicopter class -> Subclass extended from Vehicle class
            - int speed
            - @override void move()

```java
public class Main {
    public static void main(String[] args) {

    }
}

public abstract class Vehicle {
    protected int speed;

    public Vehicle(int speed) {
        this.speed = speed;
    }
    public abstract move ();
}

public class Car extends Vehicle {
    super(90);

    @override
    public move() {
        System.out.println("Moving on land!")
    }
}

public class Boat extends Vehicle {
    super(50);

    @override
    public move() {
        System.out.println("Moving on the sea!")
    }
}

public class Plane extends Vehicle {
    super(200);

    @override
    public move() {
        System.out.println("Moving high in the air!")
    }
}

public class Helicopter extends Vehicle {
    super(70);

    @override
    public move() {
        System.out.println("Moving through the air!")
    }
}
```

### Interfaces

- A way in which two things interact
- The way we create our classes will depend on how other classes interface with others
- Typically interfaces only contain abstract methods
- Interfaces do not need the keyword abstract or public
- Interfaces are designed to be implemented by classes
- Interfaces are similar to abstract classes
- We use interfaces because we can only extend one other class for each class
- Classes can implement multiple interfaces

```java
public class Main {
    public static void main(String[] args) {
        Foo foo = new foo();
        foo.m1();
    }
}
public interface Baz {
    void m1();
    boolean m2();
    String m3(int pos, String tag);
}

public class Foo implements Baz {
    public void m1() {

    }
    public boolean m2() {
        return false;
    }
    public String m3(int pos, String tag) {
        return null;
    }
}
```

### Shape Interface

- Shape Interface
    - getName()
    - getSideCount()
    - draw()

- Square class -> Implements Shape Interface
- Triangle class -> Implements Shape Interface
- Circle class -> Implements Shape Interface

```java
public class Main {
    public static void main(String[] args) {
        displayShape(new Square());
        displayShape(new Circle());
        displayShape(new Triangle());
    }

    static void displayShape(Shape shape) {
        System.out.println(shape.getName());
        shape.draw();
        System.out.println("Sides: " + shape.getSideCount());
    }
}

public interface Shape {
    String getName();
    int getSideCount();
    void draw();
}

public class Square implements Shape {
    @override
    public String getName() {
        return "Square";
    }

    @override
    public int getSideCount() {
        return 4;
    }

    @override
    public void draw() {
        System.out.println("-------------");
        System.out.println("|           |");
        System.out.println("|           |");
        System.out.println("|           |");
        System.out.println("-------------");
    }
}

public class Triangle implements Shape{
    @override
    public String getName() {
        return "Triangle";
    }

    @override
    public int getSideCount() {
        return 3;
    }

    @override
    public void draw() {
        System.out.println("    -     ");
        System.out.println("   / \\   ");
        System.out.println("  /   \\  ");
        System.out.println(" /     \\ ");
        System.out.println("/-------\\");
    }
}

public class Cirlce implements Shape {
    @override
    public String getName() {
        return "Cirlce";
    }

    @override
    public int getSideCount() {
        return 1;
    }

    @override
    public void draw() {
        System.out.println("  . ```` .   ");
        System.out.println(" /        \\ ");
        System.out.println("|          |");
        System.out.println(" \\        / ");
        System.out.println("  `- ___ -`  ");
    }
}
```

### Type Conversion

- We can use type conversion can convert variables, instances and classes into others of another type

### Instance of

- We can check the instance type by using the instanceof keyword
- If we need to run a certain piece of code ony for certain instances, we can use a conditional along with the instanceof keyword to check the type of instance we are working with
- Polymorhpism is a better practice to use then the instanceof keyword