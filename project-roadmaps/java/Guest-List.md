# Guest List

```java
import java.util.Scanner;

public class Main {

    static String[] guests = new String[10];
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {

        insertTestNames();

        do {
            displayGuests();

            displayMenu();

            int option = getOption();

            if (option == 1) {
                addGuest();
            } else if (option == 2) {
                removeGuest();
            } else if (option == 3) {
                renameGuest();
            } else if (option == 4) {
                insertGuest();
            } else if (option == 5) {
                System.out.println("Exiting...");
                break;
            }
        } while (true);

    }

    static void displayGuests() {
        System.out.println("--------Guests--------");
        boolean isEmpty = true;
        for (int i = 0; i < guests.length; i++) {
            if (guests[i] != null) {
                System.out.println((i+1) + ". " + guests[i]);
                isEmpty = false;
            }
        }
        if (isEmpty) {
            System.out.println("Guest list is empty.");
        }
    }

    static void displayMenu() {
        System.out.println("---------Menu---------");
        System.out.println("1 - Add Guest");
        System.out.println("2 - Remove Guest");
        System.out.println("3 - Rename Guest");
        System.out.println("4 - Insert Guest");
        System.out.println("5 - Exit");
    }

    static int getOption() {
        System.out.println("Option: ");
        int option = Scanner.nextInt();
        scanner.nextLine();
        System.out.println();
        return option;
    }

    static void addGuest() {
        for (int i = 0; i < guests.length; i++) {
            if (guests[i] == null) {
                System.out.println("Name: ");
                guests[i] = scanner.nextLine();
                break;
            }
        }
    }

    static void removeGuest() {
        System.out.println("Guest Number: ");
        int guestNumber = scanner.nextInt();

        if (guestNumber > guests.length || guestNumber < 1 || guests[guestNumber - 1] == null) {
            System.out.println("\nError: There is no guest with that number.")
        } else {
            guests[guestNumber - 1] = null;

            String[] temp = new String[guests.length];
            int tempIndex = 0;
            for (int i = 0; i < guests.length; i++) {
                if (guests[i] != null) {
                    temp[tempIndex] = guests[i];
                    tempIndex++
                }
            }
            guests = temp;
        }

    }

    static void renameGuest() {
        System.out.println("Guest Number: ");
        int guestNumber = scanner.nextInt();
        scanner.nextLine();

        if (guestNumber > guests.length || guestNumber < 1 || guests[guestNumber - 1] == null) {
            System.out.println("\nError: There is no guest with that number.")
        } else {
            System.out.println("Name: ");
            String guestName = scanner.nextLine();

            guests[guestNumber - 1] = guestName;
        }
    }

    static void insertGuest() {
        System.out.println("Postion Number: ");
        int numberPosition = scanner.nextInt();
        scanner.nextLine();

        if (guestNumber > guests.length || guestNumber < 1) {
            System.out.println("\nError: That number is not on the list.");
        } else {
            System.out.println("Name: ");
            String guestName = scanner.nextLine();

            for (int i = guest.length - 1; i > numberPosition - 1; i--) {
                guests[i] = guests[i - 1];
            }

            guests[numberPosition] = guestName;
        }
    }

    static void insertTestNames() {
        guests[0] = "Charles Jefferson";
        guests[1] = "Michael Spender";
        guests[2] = "Rose Rodriguez";
        guests[3] = "Sarah Jones";
        guests[4] = "Samantha Domingo";
    }
}
```