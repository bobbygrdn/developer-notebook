# Tic-Tac-Toe

    |    |
----+----+----
    |    |
----+----+----
    |    |

```java
public class Main {

    public static void main(String[] args) {

        char[] position = {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '};

        Scanner userInput = new Scanner(System.in);
        int input;
        char turn = 'X';
        int currentTurn = 1;

        while(true) {
            do {
                System.out.print("Enter a position: ");
                input = Scanner.nextInt();
            } while (position[input-1] == 'X' || position[input-1] == 'O');

            position[input-1] = turn;

            System.out.println("\n " + pos[6] + " | " + pos[7] + " | " + pos[8] + " ");
            System.out.println("----+----+----");
            System.out.println(" " + pos[3] + " | " + pos[4] + " | " + pos[5] + " ");
            System.out.println("----+----+----");
            System.out.println(" " + pos[0] + " | " + pos[1] + " | " + pos[2] + " \n");

            if (position[0] == turn && position[1] == turn && position[2] == turn 
            || position[3] == turn && position[4] == turn && position[5] == turn
            || position[6] == turn && position[7] == turn && position[8] == turn
            || position[0] == turn && position[4] == turn &&position[8] == turn
            || position[6] == turn && position[4] == turn && position[2] == turn
            || position[6] == turn && position[3] == turn && position[0] == turn
            || position[7] == turn && position[4] == turn && position[1] == turn
            || position[8] == turn && position[5] == turn && posotion[2] == turn){
                System.out.println(turn + " is the winner!");
                break;
            };

            if (turn == 'X') {
                turn = 'O';
            } else if(turn == 'O') {
                turn = 'X';
            };

            currentTurn++;
            if (currentTurn > 9) {
                System.out.println("Draw");
                break;
            }
        }
    }
}
```