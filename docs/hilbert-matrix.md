# 希尔伯特矩阵

> 原文:[https://www.geeksforgeeks.org/hilbert-matrix/](https://www.geeksforgeeks.org/hilbert-matrix/)

希尔伯特矩阵 是一个正方形矩阵，它的每个元素都是一个单位分数。
**属性:**

1.  它是一个对称矩阵。
2.  Its determinant value is always positive.

    **示例:**

    ```
    Input : N = 2
    Output : 1    0.5
             0.5  0.33                   

    Input : N = 3
    Output : 1.0000    0.5000    0.3333
             0.5000    0.3333    0.2500
             0.3333    0.2500    0.2000

    ```

    数学上，希尔伯特矩阵可以由给定的公式形成:

    ```

    Let H be a Hilbert Matrix of NxN.
    Then
    H(i, j) = 1/(i+j-1)

    ```

    下面是上述公式的基本实现。

    ## C++

    ```
    // C++ program for Hilbert Matrix
    #include <bits/stdc++.h>
    using namespace std;

    // Function that generates a Hilbert matrix
    void printMatrix(int n)
    {
        float H[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // using the formula to generate
                // hilbert matrix
                H[i][j] = (float)1.0 / 
                         ((i + 1) + (j + 1) - 1.0);
            }
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) 
                cout << H[i][j] << " ";        
            cout << endl;
        }
    }

    // driver function
    int main()
    {
        int n = 3;
        printMatrix(n);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program for
    // Hilbert Matrix
    import java.io.*;

    class GFG 
    {

    // Function that generates 
    // a Hilbert matrix
    static void printMatrix(int n)
    {
        float H[][] = new float[n][n];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++) 
            {

                // using the formula 
                // to generate
                // hilbert matrix
                H[i][j] = (float)1.0 / 
                          ((i + 1) + (j + 1) - 
                          (float)1.0);
            }
        }

        for (int i = 0; i < n; i++) 
        {
            for (int j = 0; j < n; j++) 
                System.out.print(H[i][j] + " "); 
            System.out.println();
        }
    }

    // Driver code
    public static void main (String[] args) 
    {
        int n = 3;
        printMatrix(n);
    }
    }

    // This code is contributed 
    // by anuj_67.
    ```

    ## C#

    ```
    // C# program for Hilbert Matrix
    using System;

    class GFG 
    {

    // Function that generates 
    // a Hilbert matrix
    static void printMatrix(int n)
    {
        float[,] H = new float[n, n];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++) 
            {

                // using the formula to generate
                // hilbert matrix
                H[i, j] = (float)1.0 / 
                         ((i + 1) + (j + 1) - 
                          (float)1.0);
            }
        }

        for (int i = 0; i < n; i++) 
        {
            for (int j = 0; j < n; j++) 
                Console.Write(H[i, j] + " "); 
            Console.WriteLine("");
        }
    }

    // Driver code
    public static void Main() 
    {
        int n = 3;
        printMatrix(n);
    }
    }

    // This code is contributed 
    // by mits
    ```

    **Output:**

    ```
    1 0.5 0.333333 
    0.5 0.333333 0.25 
    0.333333 0.25 0.2

    ```