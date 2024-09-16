// 15-Number-Puzzle
//to play the 15 number puzzle
import java.util.Random;
import java.util.Scanner;

public class numberPuzzle {
    
    private static final int SIZE = 4;
    private static int[][] puzzle = new int[SIZE][SIZE];
    private static int emptyX = SIZE - 1, emptyY = SIZE - 1;

    // Initializing
    private static void Initializing() {
        int num = 1;
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                if (i == SIZE - 1 && j == SIZE - 1) {
                    puzzle[i][j] = 0;  // Empty space
                } else {
                    puzzle[i][j] = num++;
                }
            }
        }
    }
 
    // Shuffling
    private static void shuffling() {
        Random rand = new Random();
        for (int i = 0; i < 50; i++) {
            int direction = rand.nextInt(4);  
            switch (direction) {
                case 0: movement('W'); break; //up
                case 1: movement('S'); break; //down
                case 2: movement('A'); break; //left
                case 3: movement('D'); break; //right
            }
        }
    }
    
    //displaying
    private static void displayPuzzle() {
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                if (puzzle[i][j] == 0) {
                    System.out.print("   ");  // Empty space
                } else {
                    System.out.printf("%3d", puzzle[i][j]);
                }
            }
            System.out.println();
        }
        System.out.println();
    }
    
    // Movement
    private static boolean movement(char direction) {
        int newX = emptyX, newY = emptyY;
        
        switch (Character.toUpperCase(direction)) {
            case 'W': newX--; break;  // Move up
            case 'S': newX++; break;  // Move down
            case 'A': newY--; break;  // Move left
            case 'D': newY++; break;  // Move right
            default: return false;    // Invalid input
        }
        
        if (validation(newX, newY)) {
            swaping(emptyX, emptyY, newX, newY);
            emptyX = newX;
            emptyY = newY;
            return true;
        } else {
            return false;  
        }
    }
    
    // validation
    private static boolean validation(int x, int y) {
        return x >= 0 && x < SIZE && y >= 0 && y < SIZE;
    }
    
    // Swaping
    private static void swaping(int x1, int y1, int x2, int y2) {
        int temp = puzzle[x1][y1];
        puzzle[x1][y1] = puzzle[x2][y2];
        puzzle[x2][y2] = temp;
    }
    
    // puzzle status
    private static boolean status() {
        int num = 1;
        for (int i = 0; i < SIZE; i++) {
            for (int j = 0; j < SIZE; j++) {
                if (i == SIZE - 1 && j == SIZE - 1) {
                    return puzzle[i][j] == 0; 
                }
                if (puzzle[i][j] != num++) {
                    return false;
                }
            }
        }
        return true;
    }


    public static void main(String[] args) {
        Initializing();
        shuffling();
        Scanner scanner = new Scanner(System.in);
        
        while (true) {
            displayPuzzle();
            System.out.println("Use the keys W (up), S (down), A (left), D (right) to move tiles:");
            char key = scanner.next().charAt(0);
            
            if (movement(key)) {
                if (status()) {
                    displayPuzzle();
                    System.out.println("Congratulations! You've solved the puzzle!");
                    break;
                }
            } else {
                System.out.println("Invalid key. Try again.");
            }
        }
        
        scanner.close();
    }
}
