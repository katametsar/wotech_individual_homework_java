# Individual homework java 
## 15.05.2024 tic-tac-toe
```java
# Welcome to my homework repository

## 15.05.2024 ##
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

```
