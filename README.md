# Individual homework java 
## 15.05.2024 tic-tac-toe
```java
/* Easy: Ask user for row and column and write in the two dimensional array a value "1" in the correct place.
Check whether or not the row chosen by user contains all 1.
If all elements in row contain 1, then let player know they won. */

import java.util.Scanner;

class HelloWorld {
    public static void main(String[] args) {
        int[][] array = new int[3][3];
        array[1][0]=1;
        array[1][1]=1;
        array[1][2]=1;
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to a simple game of tic-tac-toe! You have to choose, in which row and column you would like your number 1 to be. If you find the row filled with number 1, you win!");
       
        outerloop: 
        while (true)
        for(int i = 0; i < array.length; i++){
            for(int j=0; j < array[i].length; j++){
            System.out.println("From 1-3, which row do you want to insert your number 1: ");
            int userGuessRow = scanner.nextInt();
            System.out.println("From 1-3, which column do you want to insert your number 1: ");
            int userGuessColumn = scanner.nextInt();
            
            int adjustedRow = userGuessRow - 1;
            int adjustedColumn = userGuessColumn - 1;
        
            if (userGuessRow > 3 || userGuessColumn > 3){
                System.out.println("Choose a number between 1-3");
            }
            else if (adjustedRow == 1){
                System.out.println("You win!");
                break outerloop;
            }
            else {
                System.out.println("You loose, try again.");
            }
        }
    }
}
}
```
## Tic-tac-toe medium
```java
/*Medium: Ask for row and column and write in the two dimensional array a value "1" or "2" in the correct place, depending on which players turn it is. Switch the turn after every move.

Check whether or not the row chosen by user contains all 1, or all 2.

Check whether or not the column chosen by user contains all 1, or all 2.

(1 represents X, 2 represents O, 0 represents empty)*/

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        int[][] board = new int[3][3];
        boolean firstPlayerTurn = true;
        boolean win = false;
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to the game of tic-tac-toe. We have two users and winner is the one, who gets a row or column filled first.");
        System.out.println("What is the name of first player: ");
        String firstPlayer = scanner.nextLine();
        System.out.println("What is the name of second player: ");
        String secondPlayer = scanner.nextLine();
        System.out.println("Welcome " + firstPlayer + " and " + secondPlayer + ". " + firstPlayer + " uses number 1 and " + secondPlayer + " uses 2, let's begin the game and see, who gets a row or a column first.");

        while (!win && !boardFull(board)) {
            if (firstPlayerTurn) {
                System.out.println(firstPlayer + "'s turn");
            } else {
                System.out.println(secondPlayer + "'s turn");
            }

            int row = playerInput(scanner, "row") - 1;
            int column = playerInput(scanner, "column") - 1;

            if (isValidMove(board, row, column)) {
                board[row][column] = firstPlayerTurn ? 1 : 2;
                printBoard(board);

                win = checkWin(board);

                if (win) {
                    System.out.println((firstPlayerTurn ? firstPlayer : secondPlayer) + " wins!");
                } else {
                    firstPlayerTurn = !firstPlayerTurn;
                }
            } else {
                System.out.println("Invalid move. Try again.");
            }
        }

        if (!win) {
            System.out.println("The game is a draw!");
        }

        scanner.close();
    }

    public static void printBoard(int[][] board) {
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[i].length; j++) {
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    public static int playerInput(Scanner scanner, String type) {
        System.out.print("Enter " + type + " (1-3): ");
        while (!scanner.hasNextInt()) {
            System.out.print("Invalid input. Enter " + type + " (1-3): ");
            scanner.next();
        }
        return scanner.nextInt();
    }

    public static boolean isValidMove(int[][] board, int row, int column) {
        return row >= 0 && row < 3 && column >= 0 && column < 3 && board[row][column] == 0;
    }

    public static boolean boardFull(int[][] board) {
        for (int[] row : board) {
            for (int cell : row) {
                if (cell == 0) {
                    return false;
                }
            }
        }
        return true;
    }

    public static boolean checkWin(int[][] board) {
        // Check rows
        for (int i = 0; i < 3; i++) {
            if (board[i][0] != 0 && board[i][0] == board[i][1] && board[i][0] == board[i][2]) {
                return true;
            }
        }
        // Check columns
        for (int i = 0; i < 3; i++) {
            if (board[0][i] != 0 && board[0][i] == board[1][i] && board[0][i] == board[2][i]) {
                return true;
            }
        }
        return false;
    }
}
```


