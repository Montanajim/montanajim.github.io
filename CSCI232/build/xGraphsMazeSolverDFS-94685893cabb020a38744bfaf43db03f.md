# DSF - Maze Solving



This program defines constants for different characters in the maze and implements two methods:

- **solveMaze**: Finds the starting point and calls the recursive solveMazeDFS method.
- **solveMazeDFS**: Uses depth-first search to explore the maze. It marks visited cells, checks all four directions (up, down, left, right) for a solution, and backtracks if necessary.

The main method demonstrates how to use the program with a sample maze. 



## Lecture Code

```java
/*
Programmer: James Goudy with JGEM
 */
package mazesolver;

import java.util.Scanner;

public class MazeSolver {

    public static final char START = 'S';
    public static final char END = 'E';
    public static final char WALL = 'W';
    public static final char OPEN = '.';
    public static final char VISITED = 'V';
    public static final char ROUTE = '*'; // New character to mark the route

    public static boolean solveMaze(char[][] maze) {
        int startRow = -1;
        int startCol = -1;

        // Find the starting point
        for (int row = 0; row < maze.length; row++) {
            for (int col = 0; col < maze[row].length; col++) {
                if (maze[row][col] == START) {
                    startRow = row;
                    startCol = col;
                    break;
                }
            }
        }

        if (startRow == -1 || startCol == -1) {
            System.out.println("Error: Starting point not found in maze");
            return false;
        }

        return solveMazeDFS(maze, startRow, startCol);
    }

    private static boolean solveMazeDFS(char[][] maze, int row, int col) {
        // Check if we reached the end or hit a wall/visited cell
        if (maze[row][col] == END) {
            return true;
        } else if (maze[row][col] == WALL || maze[row][col] == VISITED) {
            return false;
        }

        // Mark current cell as visited
        maze[row][col] = VISITED;

        // Try all four directions (up, down, left, right)
        if (row > 0 && solveMazeDFS(maze, row - 1, col)) {
            maze[row][col] = ROUTE; // Mark as part of the route on successful return
            return true; // Found solution going up
        }
        if (row < maze.length - 1 && solveMazeDFS(maze, row + 1, col)) {
            maze[row][col] = ROUTE;
            return true; // Found solution going down
        }
        if (col > 0 && solveMazeDFS(maze, row, col - 1)) {
            maze[row][col] = ROUTE;
            return true; // Found solution going left
        }
        if (col < maze[row].length - 1 && solveMazeDFS(maze, row, col + 1)) {
            maze[row][col] = ROUTE;
            return true; // Found solution going right
        }

        // Backtrack if no solution found in any direction
        maze[row][col] = OPEN; // Unmark cell as visited (backtracking)
        return false;
    }

    public static void printMaze(char[][] maze) {
        for (char[] row : maze) {
            for (char c : row) {
                System.out.print(c + " ");
            }
            System.out.println();
        }
    }
    
    public static void main(String[] args) {
        
        char[][] maze = new char[1][1];
        
        char[][] maze1 = {
            {'W', 'W', 'W', '.'},
            {'.', '.', 'S', '.'},
            {'W', 'W', 'W', '.'},
            {'W', '.', '.', 'E'}
        };

        char[][] maze2 = {
            {'W', 'W', 'W', 'W', 'W', 'W', 'W', 'W', 'W', 'W'},
            {'.', '.', '.', '.', 'W', '.', '.', '.', '.', '.'},
            {'W', 'W', '.', 'W', 'W', '.', 'W', 'W', 'W', 'W'},
            {'.', '.', 'S', '.', '.', '.', '.', '.', '.', '.'},
            {'W', 'W', '.', 'W', 'W', 'W', 'W', '.', 'W', 'W'},
            {'.', '.', '.', '.', '.', '.', '.', '.', '.', '.'},
            {'W', 'W', 'W', 'W', '.', 'W', 'W', 'W', 'W', 'W'},
            {'.', '.', '.', '.', '.', '.', '.', '.', '.', '.'},
            {'W', 'W', '.', 'W', '.', 'W', '.', 'W', 'W', 'W'},
            {'.', '.', '.', 'W', '.', '.', '.', '.', '.', '.'},
            {'.', 'W', 'W', '.', 'W', '.', '.', '.', '.', '.'},
            {'.', '.', '.', '.', '.', 'W', '.', '.', '.', '.'},
            {'.', '.', '.', '.', '.', 'W', 'E', 'W', '.', '.'}
        };
        
        char[][] maze3 = {
            {'W', 'W', 'W', 'W', 'W', 'W', 'W', 'W', 'W', 'W'},
            {'.', '.', '.', '.', 'W', '.', '.', '.', '.', '.'},
            {'W', 'W', '.', 'W', 'W', '.', 'W', 'W', 'W', 'W'},
            {'.', '.', 'S', '.', '.', '.', '.', 'W', '.', '.'},
            {'W', 'W', '.', 'W', 'W', 'W', 'W', 'W', 'W', 'W'},
            {'.', '.', '.', '.', '.', '.', '.', 'W', '.', 'E'},
            {'W', 'W', 'W', 'W', '.', 'W', 'W', 'W', '.', 'W'},
            {'.', '.', '.', '.', '.', '.', '.', 'W', '.', 'W'},
            {'W', 'W', '.', 'W', '.', 'W', '.', 'W', '.', 'W'},
            {'.', '.', '.', 'W', '.', '.', '.', 'W', '.', 'W'},
            {'.', 'W', 'W', '.', 'W', '.', '.', '.', '.', 'W'},
            {'.', '.', '.', '.', '.', 'W', '.', '.', '.', 'W'},
            {'.', '.', '.', '.', '.', 'W', 'W', 'W', 'W', 'W'}
        };
        
        char[][] maze4 = {
            {'W', 'W', 'W', 'W'},
            {'.', '.', 'S', '.'},
            {'W', 'W', 'W', '.'},
            {'W', 'W', '.', '.'},
            {'W', 'W', '.', '.'},
            {'W', 'W', 'W', 'W'},
            {'W', '.', '.', 'E'}
        };

        String choice;
        Scanner myScan = new Scanner(System.in);
        
        System.out.println("Choose maze 1,2 3 or 4");
        choice = myScan.nextLine();
        
        switch(choice){
           case "1" -> maze = maze1;
           case "2" -> maze = maze2;
           case "3" -> maze = maze3;
           case "4" -> maze = maze4;
           default ->  {System.out.println("Not a choice");}
        }
        
        
        printMaze(maze);
        System.out.println("\n");
        
        if (solveMaze(maze)) {
            System.out.println("Maze solved!");
            printMaze(maze); // Print the maze with the solved route
        } else {
            System.out.println("No solution found for the maze");
        }
    }
}
```





# Sample Output

```  
Choose maze 1,2 3 or 4
3
W W W W W W W W W W 
. . . . W . . . . . 
W W . W W . W W W W 
. . S . . . . W . . 
W W . W W W W W W W 
. . . . . . . W . E 
W W W W . W W W . W 
. . . . . . . W . W 
W W . W . W . W . W 
. . . W . . . W . W 
. W W . W . . . . W 
. . . . . W . . . W 
. . . . . W W W W W 


Maze solved!
W W W W W W W W W W 
. . . . W . . . . . 
W W . W W . W W W W 
. . * . . . . W . . 
W W * W W W W W W W 
. . * * * . . W * E 
W W W W * W W W * W 
. . . . * . . W * W 
W W . W * W . W * W 
. . . W * * . W * W 
. W W . W * * * * W 
. . . . . W * * . W 
. . . . . W W W W W 
```

