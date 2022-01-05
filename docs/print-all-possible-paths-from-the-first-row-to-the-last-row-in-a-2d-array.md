# 打印 2D 数组中从第一行到最后一行的所有可能路径

> 原文:[https://www . geesforgeks . org/print-所有可能的路径-从 2d 数组中的第一行到最后一行/](https://www.geeksforgeeks.org/print-all-possible-paths-from-the-first-row-to-the-last-row-in-a-2d-array/)

给定一个具有 **M** 行和 **N** 列的 2D 字符数组。任务是打印从顶部(第一行)到底部(最后一行)的所有可能路径。

**示例:**

> **输入:**arr[]=
> {‘a’、【b】、【c】、
> 【d】、【e】、【f】、
> 【g】、【h】、【I’}
> **输出:**
> 【adg adad ADI AEG AEI afg】

**进场:**

1.  这个问题可以通过稍微修改一下数组的[深度优先遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来解决。
2.  这里的修改是只迭代数组中的列，直到到达目标行。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

void dfs(char inputchar[][2], string res,
                int i, int j, int R, int C)
{

    // If the current row index equals to R, it
    // indicates we have reached the bottom of
    // the array and hence we print the result
    if (i == R)
    {
        cout << res << " ";
        return;
    }

    res = res + (inputchar[i][j]);

    // Iterate over each of the columns
    // in the array
    for (int k = 0; k < C ; k++)
    {
        dfs(inputchar, res, i + 1, k, R, C);
        if (i + 1 == R)
            break;
    }
}

// Function to print all the possible paths
void printPaths(char inputchar[][2], int R, int C)
{
    for (int i = 0; i < C; i++)
    {
        dfs(inputchar, "", 0, i, R, C);
        cout<<endl;
    }

    /*
    * Depth first traversal of the array
    *
    * @param input array of characters
    * @param res to be printed in console
    * @param i current row index
    * @param j current column index
    * @param R number of rows in the input array
    * @param C number of rows in the output array
    *
*/
}

// Driver code
int main()
{

    char inputchar[][2] = {
            { 'a', 'b' },
            { 'd', 'e' }
            };

    int R = sizeof(inputchar)/sizeof(inputchar[0]);
    int C = sizeof(inputchar[0])/sizeof(char);

    printPaths(inputchar, R, C);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to print all the possible paths
    private static void printPaths(char[][] input,
                                   int R, int C)
    {
        for (int i = 0; i < C; i++) {
            dfs(input, "", 0, i, R, C);
            System.out.println();
        }
    }

    /**
    * Depth first traversal of the array
    *
    * @param input array of characters
    * @param res to be printed in console
    * @param i     current row index
    * @param j     current column index
    * @param R     number of rows in the input array
    * @param C     number of rows in the output array
    */
    private static void dfs(char[][] input, String res,
                            int i, int j, int R, int C)
    {
        // If the current row index equals to R, it
        // indicates we have reached the bottom of
        // the array and hence we print the result
        if (i == R) {
            System.out.print(res + " ");
            return;
        }

        res = res + input[i][j];

        // Iterate over each of the columns
        // in the array
        for (int k = 0; k < C; k++) {
            dfs(input, res, i + 1, k, R, C);
            if (i + 1 == R) {
                break;
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        char[][] input = {
            { 'a', 'b' },
            { 'd', 'e' }
        };
        int R = input.length;
        int C = input[0].length;
        printPaths(input, R, C);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print all the possible paths
def printPaths(inputchar, R, C) :
    for i in range(C) :
        dfs(inputchar, "", 0, i, R, C);
        print()

    """
    * Depth first traversal of the array
    *
    * @param input array of characters
    * @param res to be printed in console
    * @param i current row index
    * @param j current column index
    * @param R number of rows in the input array
    * @param C number of rows in the output array
    * """
def dfs(inputchar, res, i, j, R, C) :

    # If the current row index equals to R, it
    # indicates we have reached the bottom of
    # the array and hence we print the result
    if (i == R) :
        print(res, end = " ");
        return;

    res = res + inputchar[i][j];

    # Iterate over each of the columns
    # in the array
    for k in range(C) :
        dfs(inputchar, res, i + 1, k, R, C);
        if (i + 1 == R) :
            break;

# Driver code
if __name__ == "__main__" :

    inputchar = [
            [ 'a', 'b' ],
            [ 'd', 'e' ]
            ];

    R = len(inputchar);
    C = len(inputchar[0]);

    printPaths(inputchar, R, C);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print all the possible paths
    private static void printPaths(char[,] input,
                                int R, int C)
    {
        for (int i = 0; i < C; i++)
        {
            dfs(input, "", 0, i, R, C);
            Console.WriteLine();
        }
    }

    /**
    * Depth first traversal of the array
    *
    * @param input array of characters
    * @param res to be printed in console
    * @param i current row index
    * @param j current column index
    * @param R number of rows in the input array
    * @param C number of rows in the output array
    */
    private static void dfs(char[,] input, string res,
                            int i, int j, int R, int C)
    {
        // If the current row index equals to R, it
        // indicates we have reached the bottom of
        // the array and hence we print the result
        if (i == R)
        {
            Console.Write(res + " ");
            return;
        }

        res = res + input[i,j];

        // Iterate over each of the columns
        // in the array
        for (int k = 0; k < C; k++)
        {
            dfs(input, res, i + 1, k, R, C);
            if (i + 1 == R)
            {
                break;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        char[,] input = {
            { 'a', 'b' },
            { 'd', 'e' }
        };
        int R = input.GetLength(0);
        int C = input.GetLength(1);
        printPaths(input, R, C);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to print all the possible paths
     function printPaths( input , R , C) {
        for (i = 0; i < C; i++) {
            dfs(input, "", 0, i, R, C);
            document.write("<br/>");
        }
    }

     function dfs( input,  res , i , j , R , C) {
        // If the current row index equals to R, it
        // indicates we have reached the bottom of
        // the array and hence we print the result
        if (i == R) {
            document.write(res + " ");
            return;
        }

        res = res + input[i][j];

        // Iterate over each of the columns
        // in the array
        for (var k = 0; k < C; k++) {
            dfs(input, res, i + 1, k, R, C);
            if (i + 1 == R) {
                break;
            }
        }
    }

    // Driver code

        var input = [ [ 'a', 'b' ], [ 'd', 'e' ] ];
        var R = input.length;
        var C = input[0].length;
        printPaths(input, R, C);

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
ad ae 
bd be
```

**时间复杂度:**O(R * C)
T3】空间复杂度: O(1)