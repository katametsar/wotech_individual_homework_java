# Individual homework java 
## 13.06.2024 cheese shop
```java
    import java.util.Scanner;

public class Main {
    public static CheeseShop shop = new CheeseShop();
    public static CheeseService cheeseService = new CheeseService();
    public static Customer customer = new Customer(100);

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the cheese shop! We have the best selection of cheeses in the Baltic states. This is a serious shop so identify yourself before going forward");

        while (true) {
            System.out.println("Press 1 if you are the owner of this great establishment.");
            System.out.println("Press 2 if you just want to buy some cheese.");
            System.out.println("Press 3 to leave this shop.");
            System.out.println();
            String userInput = scanner.nextLine();

            if (userInput.equals("1")) {
                    ownerMenu(scanner);
                } else if (userInput.equals("2")) {
                    customerMenu(scanner);
                } else if (userInput.equals("3")) {
                    break;
                } else {
                    System.out.println("Invalid input. Please try again.");
                }
            }

            scanner.close();
        }

    public static void ownerMenu(Scanner scanner) {
        while (true) {
            System.out.println("Dear owner, here you can add and remove cheeses to the shop and see the items we have in store.");
            System.out.println("Press 1 to insert a cheese to the list.");
            System.out.println("Press 2 to get the list of cheeses.");
            System.out.println("Press 3 to remove a cheese from the list.");
            System.out.println("Press 4 to go back.");
            System.out.println();
            String userInput = scanner.nextLine();

            if (userInput.equals("1")) {
                    createItem(scanner);
                } else if (userInput.equals("2")) {
                    showItemList();
                } else if (userInput.equals("3")) {
                    showItemList();
                    System.out.println("Enter the ID of the cheese you want to remove:");
                    int itemId = scanner.nextInt();
                    scanner.nextLine();
                    shop.removeItem(itemId);
                    cheeseService.removeItem(itemId);
                } else if (userInput.equals("4")) {
                    break;
                } else {
                    System.out.println("Invalid input. Please try again.");
                }
            }
        }

    public static void customerMenu(Scanner scanner) {
            while (true) {
                System.out.println("Press 1 to view available cheeses.");
                System.out.println("Press 2 to buy a cheese.");
                System.out.println("Press 3 to view your cart.");
                System.out.println("Press 4 to remove a cheese from your cart.");
                System.out.println("Press 5 to checkout and see the total price of your items.");
                System.out.println("Press 6 to go back.");
                System.out.println();

                String userInput = scanner.nextLine();

                if (userInput.equals("1")) {
                    showItemList();
                } else if (userInput.equals("2")) {
                    showItemList();
                    System.out.println("Enter the ID of the cheese you want to buy:");
                    int itemId = scanner.nextInt();
                    scanner.nextLine();
                    Item item = shop.getItemById(itemId);
                    if (item != null) {
                        customer.buyItem(item);
                        shop.addItemToCart(item);
                    } else {
                        System.out.println("Cheese not found.");
                    }
                } else if (userInput.equals("3")) {
                    showCartItems();
                } else if (userInput.equals("4")) {
                    showCartItems();
                    System.out.println("Enter the ID of the cheese you want to remove from the cart:");
                    int itemId = scanner.nextInt();
                    scanner.nextLine();
                    shop.removeItemFromCart(itemId);
                } else if (userInput.equals("5")) {
                    showCheckOut();
                } else if (userInput.equals("6")) {
                    break;
                } else {
                    System.out.println("Invalid input. Please try again.");
                }
            }
        }

    public static void createItem(Scanner scanner) {
            System.out.println("Enter the ID of the cheese: ");
            int id = scanner.nextInt();
            scanner.nextLine();
            System.out.println("Enter the name of the cheese: ");
            String name = scanner.nextLine();
            System.out.println("Enter the cost: ");
            int cost = scanner.nextInt();
            scanner.nextLine();
            Item item = new Item(id, name, cost);
            shop.addItem(item);
            cheeseService.addItem(item);
        }

    public static void showItemList() {
            for (Item item : shop.getItems()) {
                System.out.println("ID: " + item.getId() + ", Name: " + item.getName() + ", Cost: " + item.getCost());
            }
        }

    public static void showCartItems() {
            for (Item item : shop.getCartItems()) {
                System.out.println("ID: " + item.getId() + ", Name: " + item.getName() + ", Cost: " + item.getCost());
            }
        }

    public static void showCheckOut() {
            int total = shop.checkOut();
            System.out.println("Total price of your cheese-cart is: " + total);
        }
    }
```
```java
public class Item {
    private int id;
    private String name;
    private int cost;

    public Item(int id, String name, int cost) {
        this.id = id;
        this.name = name;
        this.cost = cost;
    }

    public int getId() {
        return id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setCost(int cost) {
        this.cost = cost;
    }

    public int getCost() {
        return cost;
    }
}
```
```java
import java.util.ArrayList;

public class CheeseShop {
    private ArrayList<Item> items = new ArrayList<Item>();
    private ArrayList<Item> cart = new ArrayList<Item>();

    public ArrayList<Item> getItems() {
        return items;
    }

    public void addItem(Item item) {
        items.add(item);
    }

    public void removeItem(int id) {
        items.removeIf(item -> item.getId() == id);
        cart.removeIf(item -> item.getId() == id);
    }

    public Item getItemById(int id) {
        for (Item item : items) {
            if (item.getId() == id) {
                return item;
            }
        }
        return null;
    }

    public void addItemToCart(Item item) {
        cart.add(item);
    }

    public void removeItemFromCart(int id) {
        cart.removeIf(item -> item.getId() == id);
    }

    public ArrayList<Item> getCartItems() {
        return cart;
    }

    public int checkOut() {
        int sum = 0;
        for (Item item : cart) {
            sum += item.getCost();
        }
        return sum;
    }
}
```
```java
import java.util.ArrayList;

public class CheeseService {
    private ArrayList<Item> items = new ArrayList<Item>();

    public ArrayList<Item> getItems() {
        return items;
    }

    public void addItem(Item item) {
        items.add(item);
    }

    public void removeItem(int id) {
        items.removeIf(item -> item.getId() == id);
    }

    public void updateItem(int id, String name, int cost) {
        for (Item item : items) {
            if (item.getId() == id) {
                item.setName(name);
                item.setCost(cost);
                return;
            }
        }
    }
}
```
```java
import java.util.ArrayList;

public class Customer {
    private int money;
    private ArrayList<Item> ownedItems = new ArrayList<Item>();

    public Customer(int money) {
        this.money = money;
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }

    public ArrayList<Item> getOwnedItems() {
        return ownedItems;
    }

    public void buyItem(Item item) {
        if (money >= item.getCost()) {
            money -= item.getCost();
            ownedItems.add(item);
        } else {
            System.out.println("You don't have enough money to buy " + item.getName());
        }
    }
}
```

## 29.05.2024 book manager
```java
import java.util.Scanner;
import java.util.ArrayList;

public class Main {
    public static BookManager bookManager = new BookManager();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("Press 1 to insert a book");
            System.out.println("Press 2 to show the list of books");
            System.out.println("Press 3 to remove a book from the list");
            System.out.println("Press x to stop.");
            String userInput = scanner.nextLine();

            if (userInput.equals("1")) {
                createBook(scanner);
            } else if (userInput.equals("2")) {
                showBookList();
            } else if (userInput.equals("3")) {
                showBookList();
                System.out.println("Enter the name of the book you want to remove:");
                String bookName = scanner.nextLine();
                bookManager.removeBook(bookName);
            } else if (userInput.equalsIgnoreCase("x")) {
                break;
            }
        }
    }

    public static void createBook(Scanner scanner) {
        System.out.println("Enter the book name:");
        String name = scanner.nextLine();
        System.out.println("Enter the book author:");
        String author = scanner.nextLine();

        Book book = new Book(name, author);
        bookManager.addBook(book);
    }

    public static void showBookList() {
        ArrayList<Book> books = bookManager.getBooks();
        if (books.isEmpty()) {
            System.out.println("No books in the list.");
        } else {
            System.out.println("These books have been added to the list:");
            for (Book book : books) {
                System.out.println(book.getName() + " by  " + book.getAuthor());
            }
        }
    }
}
```
```java
public class Book{

  public String name; 
  public String author;

  public Book(String name, String author){
    this.name = name;
    this.author = author;
    
  }
  public String getName(){
  return name;
}
  public String getAuthor(){
    return author;
  }
}
```
```java
import java.util.ArrayList;
import java.util.stream.Collectors;

public class BookManager {
    private ArrayList<Book> books = new ArrayList<>();

    public void addBook(Book book) {
        books.add(book);
    }

    public ArrayList<Book> getBooks() {
        return books;
    }

    public void removeBook(String bookName) {
        books.removeIf(book -> book.name.equals(bookName));
    }
}
```
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
        for (int i = 0; i < 3; i++) {
            if (board[i][0] != 0 && board[i][0] == board[i][1] && board[i][0] == board[i][2]) {
                return true;
            }
        }
        for (int i = 0; i < 3; i++) {
            if (board[0][i] != 0 && board[0][i] == board[1][i] && board[0][i] == board[2][i]) {
                return true;
            }
        }
        return false;
    }
}
```


