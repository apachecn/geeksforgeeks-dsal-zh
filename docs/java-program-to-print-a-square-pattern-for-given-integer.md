# 给定整数打印方形图案的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序打印给定整数的正方形图案/](https://www.geeksforgeeks.org/java-program-to-print-a-square-pattern-for-given-integer/)

编写一个 java 程序，通过命令行输入一个整数来打印给定的正方形模式。

示例:

```
Input : 3
Output :1 2 3.
        7 8 9
        4 5 6
Input :4
Output :1  2  3  4 
        9  10 11 12
        13 14 15 16
        5  6  7  8 

```

```
// Java program to print a square pattern with command
// line one argument
import java.util.*;
import java.lang.*;

public class SquarePattern {
    public static void main(String[] args)
    {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter a number");
        int number = sc.nextInt();
        int arr[][] = PrintSquarePattern(number);

        // int num = 3;
        int k = 0, m = number - 1, n = number;
        int l = 0;
        if (number % 2 == 0)
            m = number - 1;
        else
            m = number;

        for (int i = 0; i < n / 2; i++) {
            for (int j = 0; j < n; j++) {
                System.out.format("%3d", arr[k][j]);
            }
            System.out.println("");
            l = l + 2;
            k = l;
            // System.out.println("");
        }
        k = number - 1;
        for (int i = n / 2; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.format("%3d", arr[k][j]);
            }
            m = m - 2;
            k = m;
            System.out.println("");
        }
    }

    public static int[][] PrintSquarePattern(int n)
    {
        int arr[][] = new int[n][n];
        int k = 1;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                arr[i][j] = k;
                k++;
            }
        }
        return arr;
    }
}
```

输入:

```
5
```

输出:

```
Enter a number
  1  2  3  4  5
 11 12 13 14 15
 21 22 23 24 25
 16 17 18 19 20
  6  7  8  9 10

```