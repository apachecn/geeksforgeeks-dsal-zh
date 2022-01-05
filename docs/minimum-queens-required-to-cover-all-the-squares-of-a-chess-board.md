# 覆盖棋盘所有方格所需的最小皇后数

> 原文:[https://www . geeksforgeeks . org/最小皇后区-需要覆盖棋盘上的所有方块/](https://www.geeksforgeeks.org/minimum-queens-required-to-cover-all-the-squares-of-a-chess-board/)

给定棋盘的尺寸(N×M)，确定覆盖棋盘所有方块所需的最小皇后数。女王可以攻击其行、列或对角线上的任何方块。

示例:

```
Input : N = 8, M = 8
Output : 5
Layout : Q X X X X X X X 
         X X Q X X X X X 
         X X X X Q X X X 
         X Q X X X X X X 
         X X X Q X X X X 
         X X X X X X X X 
         X X X X X X X X 
         X X X X X X X X 

Input : N = 3, M = 5
Output : 2
Layout : Q X X X X 
         X X X X X 
         X X X Q X 

```

本文试图以一种非常简单的方式解决这个问题，而不需要太多的优化。

> 第一步:从棋盘的任何一个角方块开始，找到一个“未覆盖”的方块(未覆盖的方块是没有被任何已经放置的皇后攻击的方块)。如果没有找到，请转到步骤 4。
> 第二步:在这个方块上放置一个皇后，并将变量“计数”增加 1。
> 第三步:重复第一步。
> 第四步:现在，你已经有了一个布局，每个方块都被覆盖了。因此，“计数”的值可以是答案。然而，你可能会做得更好，因为可能会有一个更好的布局与较少数量的皇后。因此，将这个“计数”存储为目前的最佳值，并继续寻找更好的解决方案。
> 第五步:取出最后一个放置的皇后，放入下一个“未盖”的牢房。
> 第六步:递归进行，尝试所有可能的布局。最后，皇后数量最少的那个就是答案。

为了更好地理解，试运行以下代码。

```
// Java program to find minimum number of queens needed
// to cover a given chess board.

public class Backtracking {

    // The chessboard is represented by a 2D array.
    static boolean[][] board;

    // N x M is the dimension of the chess board.
    static int N, M;

    // The minimum number of queens required.
    // Initially, set to MAX_VAL.
    static int minCount = Integer.MAX_VALUE;

    static String layout; // Stores the best layout.

    // Driver code
    public static void main(String[] args)
    {
        N = 8;
        M = 8;
        board = new boolean[N][M];
        placeQueen(0);

        System.out.println(minCount);
        System.out.println("\nLayout: \n" + layout);
    }

    // Finds minimum count of queens needed and places them.
    static void placeQueen(int countSoFar)
    {
        int i, j;

        if (countSoFar >= minCount)

            // We've already obtained a solution with lesser or
            // same number of queens. Hence, no need to proceed.
            return;

        // Checks if there exists any unattacked cells.
        findUnattackedCell : {
        for (i = 0; i < N; ++i)
            for (j = 0; j < M; ++j)
                if (!isAttacked(i, j))

                    // Square (i, j) is unattacked.
                    break findUnattackedCell;

        // All squares all covered. Hence, this 
        // is the best solution till now.
        minCount = countSoFar;
        storeLayout();

        return;
        }

        for (i = 0; i < N; ++i)
            for (j = 0; j < M; ++j) {
                if (!isAttacked(i, j)) {

                    // Square (i, j) is unattacked.
                    // Therefore, place a queen here.
                    board[i][j] = true; 

                    // Increment 'count' and proceed recursively.
                    placeQueen(countSoFar + 1);

                    // Remove this queen and attempt to
                    // find a better solution.
                    board[i][j] = false; 
                }
            }
    }

    // Returns 'true' if the square (row, col) is 
    // being attacked by at least one queen.
    static boolean isAttacked(int row, int col) 
    {
        int i, j;

        // Check the 'col'th column for any queen.
        for (i = 0; i < N; ++i)
            if (board[i][col])
                return true;

        // Check the 'row'th row for any queen.
        for (j = 0; j < M; ++j)
            if (board[row][j])
                return true;

        // Check the diagonals for any queen.
        for (i = 0; i < Math.min(N, M); ++i)
            if (row - i >= 0 && col - i >= 0 && 
                        board[row - i][col - i])
                return true;
            else if (row - i >= 0 && col + i < M &&
                           board[row - i][col + i])
                return true;
            else if (row + i < N && col - i >= 0 && 
                            board[row + i][col - i])
                return true;
            else if (row + i < N && col + i < M &&
                            board[row + i][col + i])
                return true;

        // This square is unattacked. Hence return 'false'.
        return false;
    }

    // Stores the current layout in 'layout' 
    // variable as String.
    static void storeLayout()
    {
        StringBuilder sb = new StringBuilder();
        for (boolean[] row : board) {
            for (boolean cell : row)
                sb.append(cell ? "Q " : "X ");
            sb.append("\n");
        }
        layout = sb.toString();
    }
}
```

**Output:**

```
5

Layout: 
Q X X X X X X X 
X X Q X X X X X 
X X X X Q X X X 
X Q X X X X X X 
X X X Q X X X X 
X X X X X X X X 
X X X X X X X X 
X X X X X X X X

```