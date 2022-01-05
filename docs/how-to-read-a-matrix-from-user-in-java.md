# 如何用 Java 从用户那里读取矩阵？

> 原文:[https://www . geesforgeks . org/如何从 java 用户那里读取矩阵/](https://www.geeksforgeeks.org/how-to-read-a-matrix-from-user-in-java/)

给定的任务是从用户那里读取矩阵。矩阵元素的大小和数量将从键盘上读取。

```
// Java program to read a matrix from user

import java.util.Scanner;

public class MatrixFromUser {

    // Function to read matrix
    public static void readMatrixByUser()
    {
        int m, n, i, j;
        Scanner in = null;
        try {
            in = new Scanner(System.in);
            System.out.println("Enter the number "
                               + "of rows of the matrix");
            m = in.nextInt();
            System.out.println("Enter the number "
                               + "of columns of the matrix");
            n = in.nextInt();

            // Declare the matrix
            int first[][] = new int[m][n];

            // Read the matrix values
            System.out.println("Enter the elements of the matrix");
            for (i = 0; i < m; i++)
                for (j = 0; j < n; j++)
                    first[i][j] = in.nextInt();

            // Display the elements of the matrix
            System.out.println("Elements of the matrix are");
            for (i = 0; i < m; i++) {
                for (j = 0; j < n; j++)
                    System.out.print(first[i][j] + "  ");
                System.out.println();
            }
        }
        catch (Exception e) {
        }
        finally {
            in.close();
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        readMatrixByUser();
    }
}
```

**Output:**

```
Enter the number of rows of the matrix 2
Enter the number of columns of the matrix 2
Enter the elements of the matrix
1
2
3
4
Elements of the matrix are
1 2 
3 4 

```