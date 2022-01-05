# 将 N^2 数放入矩阵中，使每行都有相等的和

> 原文:[https://www . geesforgeks . org/place-N2-numbers-in-matrix-这样每一行都有一个相等的总和/](https://www.geeksforgeeks.org/place-n2-numbers-in-matrix-such-that-every-row-has-an-equal-sum/)

给定一个数字 N，将范围[1，N <sup>2</sup> ]中的数字放入 NxN 矩阵中，使每行的总和相等。

**示例:**

```
Input: N = 3
Output: 1 5 9    
        2 6 7    
        3 4 8    
Sum in 1st row: 15
Sum in 2nd row: 15 
Sum in 2nd row: 15 

Input: N = 5
Output: 1 7 13 19 25    
        2 8 14 20 21    
        3 9 15 16 22    
        4 10 11 17 23    
        5 6 12 18 24
```

一种**贪婪方法**已经被用来填充矩阵，其中矩阵中元素的插入是逐行进行的。所需的矩阵可以通过以下步骤获得:

*   使用矩阵遍历，最初用范围[1，N <sup>2</sup> ]中的数字填充矩阵。
*   遍历矩阵，并通过**答案[i][j] = mat[j][(i+j)%n]将新矩阵中的每个位置视为答案矩阵进行更改。**

下面是上述方法的实现:

## C++

```
// C++ program to distribute n^2 numbers
// to n people
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> solve(vector<vector<int>> arr,
                          int n)
{

    // 2D array for storing the final result
    vector<vector<int>> ans(n, vector<int> (n, 0));

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Using modulo to go to the firs
            // column after the last column
            ans[i][j] = arr[j][(i + j) % n];
        }
    }
    return ans;
}

void show(vector<vector<int>> arr, int n)
{
    vector<vector<int>> res = solve(arr, n);
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            cout << res[i][j] << " ";
        }
        cout << endl;
    }
}

// Making a 2D array containing numbers
vector<vector<int>> makeArray(int n)
{
    vector<vector<int>> arr(n, vector<int>(n, 0));
    int c = 1;
    for (int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            arr[i][j] = c;
            c++;
        }
    }
    return arr;
}

// Driver code
int main()
{
    int n = 5;
    vector<vector<int>> arr = makeArray(n);

    show(arr, n);

    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to distribute n^2 numbers to n people
public class Numbers {
    public static int[][] solve(int[][] arr, int n)
    {
        // 2D array for storing the final result
        int[][] ans = new int[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                // using modulo to go to the firs
                // column after the last column
                ans[i][j] = arr[j][(i + j) % n];
            }
        }
        return ans;
    }
    public static void show(int[][] arr, int n)
    {
        int[][] res = solve(arr, n);
        for (int i = 0; i < n; i++) {

            for (int j = 0; j < n; j++) {
                System.out.print(res[i][j] + " ");
            }
            System.out.println();
        }
    }
    // making a 2D array containing numbers
    public static int[][] makeArray(int n)
    {
        int[][] arr = new int[n][n];
        int c = 1;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                arr[i][j] = c++;
        }
        return arr;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        int[][] arr = makeArray(n);
        show(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to distribute n^2
# numbers to n people
def solve(arr, n):

    # 2D array for storing the final result
    ans = [[0 for i in range(n)]
              for j in range(n)]

    for i in range(n):
        for j in range(n):

            # Using modulo to go to the firs
            # column after the last column
            ans[i][j] = arr[j][(i + j) % n]

    return ans

def show(arr, n):

    res = solve(arr, n)

    for i in range(n):
        for j in range(n):
            print(res[i][j], end = " ")

        print()

# Making a 2D array containing numbers
def makeArray(n):

    arr = [[0 for i in range(n)]
              for j in range(n)]

    c = 1

    for i in range(n):
        for j in range(n):
            arr[i][j] = c
            c += 1

    return arr

# Driver Code
n = 5
arr = makeArray(n)

show(arr, n)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to distribute n^2
// numbers to n people
using System;

class GFG{

static int[,] solve(int[,] arr, int n)
{

    // 2D array for storing the final result
    int[,] ans = new int[n, n];

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // Using modulo to go to the firs
            // column after the last column
            ans[i, j] = arr[j, (i + j) % n];
        }
    }
    return ans;
}

static void show(int[,] arr, int n)
{
    int[,] res = solve(arr, n);
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            Console.Write(res[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Making a 2D array containing numbers
static int[,] makeArray(int n)
{
    int[,] arr = new int[n, n];
    int c = 1;

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
            arr[i, j] = c++;
    }
    return arr;
}

// Driver code
static void Main()
{
    int n = 5;
    int[,] arr = makeArray(n);

    show(arr, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to distribute n^2 numbers to n people

function solve(arr, n)
    {
        // 2D array for storing the final result
        let ans = new Array(n);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < ans.length; i++) {
        ans[i] = new Array(2);
        }

        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {
                // using modulo to go to the firs
                // column after the last column
                ans[i][j] = arr[j][(i + j) % n];
            }
        }
        return ans;
    }
    function show(arr, n)
    {
        let res = solve(arr, n);
        for (let i = 0; i < n; i++) {

            for (let j = 0; j < n; j++) {
               document.write(res[i][j] + " ");
            }
            document.write("<br/>");
        }
    }
    // making a 2D array containing numbers
    function makeArray(n)
    {
        let arr = new Array(n);

        // Loop to create 2D array using 1D array
        for (var i = 0; i < arr.length; i++) {
        arr[i] = new Array(2);
        }

        let c = 1;
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++)
                arr[i][j] = c++;
        }
        return arr;
    }

// driver program   
        let  n = 5;
        let arr = makeArray(n);
        show(arr, n);

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1 7 13 19 25 
2 8 14 20 21 
3 9 15 16 22 
4 10 11 17 23 
5 6 12 18 24
```