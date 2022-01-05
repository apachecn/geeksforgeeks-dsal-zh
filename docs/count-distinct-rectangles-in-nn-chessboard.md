# 计数 N*N 棋盘中不同的矩形

> 原文:[https://www . geesforgeks . org/count-distinct-矩形-in-nn-棋盘/](https://www.geeksforgeeks.org/count-distinct-rectangles-in-nn-chessboard/)

给定一个**N×N**棋盘。任务是计算棋盘上不同的矩形。例如，如果输入是 8，那么输出应该是 36。
**例:**

```
Input: N = 4 
Output: 10

Input: N = 6
Output: 21
```

**逼近:**
假设给定 N = 8，即 8×8 的棋盘，那么可以形成的不同矩形有:

```
1 x 1, 1 x 2, 1 x 3, 1 x 4, 1 x 5, 1 x 6, 1 x 7, 1 x 8 = 8
      2 x 2, 2 x 3, 2 x 4, 2 x 5, 2 x 6, 2 x 7, 2 x 8 = 7 
            3 x 3, 3 x 4, 3 x 5, 3 x 6, 2 x 7, 3 x 8 = 6 
                  4 x 4, 4 x 5, 4 x 6, 4 x 7, 4 x 8 = 5 
                        5 x 5, 5 x 6, 5 x 7, 5 x 8 = 4
                              6 x 6, 6 x 7, 6 x 8 = 3
                                    7 x 7, 7 x 8 = 2
                                          8 x 8 = 1
```

所以形成的唯一矩形总数= 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 = 36，这是前 8 个自然数的和。所以一般来说，可以在 N×N 棋盘上形成的不同矩形是:

```
Sum of the first N natural numbers = N*(N+1)/2
                                   = 8*(8+1)/2
                                   = 36
```

以下是上述方法的实现:

## C++

```
// C++ code to count distinct rectangle in a chessboard
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of distinct rectangles
int count(int N)
{
    int a = 0;
    a = (N * (N + 1)) / 2;
    return a;
}

// Driver Code
int main()
{
    int N = 4;
    cout<<count(N);
}

// This code is contributed by nidhi16bcs2007
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count unique rectangles in a chessboard
class Rectangle {

    // Function to count distinct rectangles
    static int count(int N)
    {
        int a = 0;

        a = (N * (N + 1)) / 2;

        return a;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 4;
        System.out.print(count(n));
    }
}
```

## 蟒蛇 3

```
    # Python code to count distinct rectangle in a chessboard

# Function to return the count
# of distinct rectangles
def count(N):
    a = 0;
    a = (N * (N + 1)) / 2;
    return int(a);

# Driver Code
N = 4;
print(count(N));

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# program to count unique rectangles in a chessboard
using System;

class Rectangle
{

    // Function to count distinct rectangles
    static int count(int N)
    {
        int a = 0;

        a = (N * (N + 1)) / 2;

        return a;
    }

    // Driver Code
    public static void Main()
    {
        int n = 4;
        Console.Write(count(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
// Javascript program to count unique rectangles in a chessboard

   // Function to count distinct rectangles
    function count(N)
    {
        var a = 0;

        a = (N * (N + 1)) / 2;

        return a;
    }

    // Driver Code
        var n = 4;
        document.write(count(n));

// This code is contributed by bunnyram19. 
```

**Output:** 

```
10
```