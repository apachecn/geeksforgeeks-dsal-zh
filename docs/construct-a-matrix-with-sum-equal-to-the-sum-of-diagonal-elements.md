# 构造一个和等于对角元素之和的矩阵

> 原文:[https://www . geeksforgeeks . org/construct-a-sum 等于对角线元素之和的矩阵/](https://www.geeksforgeeks.org/construct-a-matrix-with-sum-equal-to-the-sum-of-diagonal-elements/)

给定一个整数 **N** ，任务是使用正负整数并排除 **0** 来构造一个大小为 N <sup>2</sup> 的矩阵，使得矩阵的和等于矩阵对角线的和。

**示例:**

> **输入:** N = 2
> **输出:**
> 1 -2
> 2 4
> **说明:**
> 对角线总和= (1 + 4) = 5
> 矩阵总和=(1–2+2+4)= 5
> 
> **输入:** N = 5
> **输出:**
> 1 2 3 5 10
> 3 1 4-9 1
> -19 6 1 5-8
> 4-7 2 1 12
> -17 1 1 1
> **解释:**
> 对角线总和= (1 + 1 + 1 + 1 + 1) = 5
> 矩阵总和= 5

**方法:**
解决问题的方法是遍历矩阵的所有索引，在 **N** 对角位置打印一个正元素(比如说 **y** ，在剩余的**N<sup>2</sup>–N**位置平均分配一个单值的正负整数(比如说 **x** 和 **-x** )。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct matrix with
// diagonal sum equal to matrix sum
void constructmatrix(int N)
{
    bool check = true;

    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // If diagonal position
            if (i == j) {
                cout << 1 << " ";
            }

            else if (check) {

                // Positive element
                cout << 2 << " ";
                check = false;
            }
            else {

                // Negative element
                cout << -2 << " ";
                check = true;
            }
        }

        cout << endl;
    }
}

// Driver Code
int main()
{
    int N = 5;

    constructmatrix(5);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
public class Main {

    // Function to construct matrix with
    // diagonal sum equal to matrix sum
    public static void constructmatrix(int N)
    {
        boolean check = true;

        for (int i = 0; i < N; i++) {

            for (int j = 0; j < N; j++) {

                // If diagonal position
                if (i == j) {
                    System.out.print("1 ");
                }
                else if (check) {

                    // Positive element
                    System.out.print("2 ");
                    check = false;
                }
                else {
                    // Negative element
                    System.out.print("-2 ");
                    check = true;
                }
            }

            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;

        constructmatrix(5);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to construct matrix with
# diagonal sum equal to matrix sum
def constructmatrix(N):

    check = bool(True)

    for i in range(N):
        for j in range(N):

            # If diagonal position
            if (i == j):
                print(1, end = " ")

            elif (check):

                # Positive element
                print(2, end = " ")
                check = bool(False)

            else:

                # Negative element
                print(-2, end = " ")
                check = bool(True)

        print()

# Driver code
N = 5
constructmatrix(5)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to construct matrix with
// diagonal sum equal to matrix sum
public static void constructmatrix(int N)
{
    bool check = true;

    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // If diagonal position
            if (i == j)
            {
                Console.Write("1 ");
            }
            else if (check)
            {

                // Positive element
                Console.Write("2 ");
                check = false;
            }
            else
            {

                // Negative element
                Console.Write("-2 ");
                check = true;
            }
        }
        Console.WriteLine();
    }
}

// Driver Code
static public void Main ()
{
    int N = 5;

    constructmatrix(N);
}
}

// This code is contributed by piyush3010
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to construct matrix with
    // diagonal sum equal to matrix sum
    function constructmatrix(N)
    {
        let check = true;

        for (let i = 0; i < N; i++) {

            for (let j = 0; j < N; j++) {

                // If diagonal position
                if (i == j) {
                    document.write("1 ");
                }
                else if (check) {

                    // Positive element
                    document.write("2 ");
                    check = false;
                }
                else {
                    // Negative element
                    document.write("-2 ");
                    check = true;
                }
            }

            document.write("<br/>");
        }
    }

    // Driver Code

    let N = 5;

    constructmatrix(5);

</script>
```

**Output:** 

```
1 2 -2 2 -2 
2 1 -2 2 -2 
2 -2 1 2 -2 
2 -2 2 1 -2 
2 -2 2 -2 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*