# 按 X 除时数组元素商的非递减顺序打印索引

> 原文:[https://www . geeksforgeeks . org/print-indexes-in-非递减顺序-按 x 除的数组元素商/](https://www.geeksforgeeks.org/print-indices-in-non-decreasing-order-of-quotients-of-array-elements-on-division-by-x/)

给定一个由 **N** 个整数和一个整数 **X** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是通过 **X** 对数组元素执行整数除法，并按照获得的商的非递减顺序打印数组的索引。

**示例:**

> ***输入:** N = 3，X = 3，顺序[] = {2，7，4}*
> ***输出:*** 1 3 2
> **解释:**
> 将数组元素除以 3 后，数组修改为{0，2，1}。因此，所需的输出顺序是 1 3 2。
> 
> ***输入:** N = 5，X = 6，顺序[] = {9，10，4，7，2}*
> ***输出:*** 3 5 1 2 4
> **解释:**
> 将数组元素除以 6 后，将数组元素修改为 1 1 0 1 0。因此，所需的序列是 3 5 1 2 4。

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
*   初始化[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。
*   对于每个数组元素，将除以 **X** 得到的商的值存储为[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的第一个元素，将第二个元素存储为所需顺序中整数的位置。
*   遍历结束后，[对向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序，最后打印出对的所有第二个元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the order of array
// elements generating non-decreasing
// quotient after division by X
void printOrder(int order[], int N, int X)
{

    // Stores the quotient and the order
    vector<pair<int, int> > vect;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        if (order[i] % X == 0) {

            vect.push_back({ order[i] / X,
                             i + 1 });
        }
        else {

            vect.push_back({ order[i] / X + 1,
                             i + 1 });
        }
    }

    // Sort the vector
    sort(vect.begin(), vect.end());

    // Print the order
    for (int i = 0; i < N; i++) {
        cout << vect[i].second << " ";
    }

    cout << endl;
}

// Driver Code
int main()
{

    int N = 3, X = 3;
    int order[] = { 2, 7, 4 };
    printOrder(order, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
class GFG {

    // Function to print the order of array
    // elements generating non-decreasing
    // quotient after division by X
    static void printOrder(int order[], int N, int X)
    {

        // Stores the quotient and the order
        ArrayList<int[]> vect = new ArrayList<>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            if (order[i] % X == 0) {

                vect.add(new int[] { order[i] / X, i + 1 });
            }
            else {

                vect.add(
                    new int[] { order[i] / X + 1, i + 1 });
            }
        }

        // Sort the vector
        Collections.sort(vect, (a, b) -> a[0] - b[0]);

        // Print the order
        for (int i = 0; i < N; i++) {
            System.out.print(vect.get(i)[1] + " ");
        }

        System.out.println();
    }

    // Driver Code
    public static void main(String args[])
    {

        int N = 3, X = 3;
        int order[] = { 2, 7, 4 };
        printOrder(order, N, X);
    }
}
// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the order of array
# elements generating non-decreasing
# quotient after division by X
def printOrder(order, N, X):

    # Stores the quotient and the order
    vect = []

    # Traverse the array
    for i in range(N):

        if (order[i] % X == 0):
            vect.append([order[i] // X, i + 1])
        else:
            vect.append([order[i] // X + 1,i + 1])

    # Sort the vector
    vect = sorted(vect)

    # Print the order
    for i in range(N):
        print(vect[i][1], end = " ")

        # Driver Code
if __name__ == '__main__':

    N, X = 3, 3
    order = [2, 7, 4]
    printOrder(order, N, X)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to print the order of array
// elements generating non-decreasing
// quotient after division by X
static void printOrder(int[] order, int N, int X)
{

    // Stores the quotient and the order
    List<Tuple<int,
               int>> vect = new List<Tuple<int,
                                          int>>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        if (order[i] % X == 0)
        {
            vect.Add(new Tuple<int,int>((order[i] / X), i + 1));
        }
        else
        {
            vect.Add(new Tuple<int,int>((order[i] / X + 1), i + 1));
        }
    }

    // Sort the vector
    vect.Sort();

    // Print the order
    for (int i = 0; i < N; i++)
    {
        Console.Write(vect[i].Item2 + " ");
    }

    Console.WriteLine();
}

// Driver Code
public static void Main()
{
    int N = 3, X = 3;
    int[] order = { 2, 7, 4 };
    printOrder(order, N, X);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the order of array
// elements generating non-decreasing
// quotient after division by X
function printOrder(order, N, X)
{

    // Stores the quotient and the order
    let vect = [];

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        if (order[i] % X == 0)
        {
            vect.push([ order[i] / X, i + 1 ]);
        }
        else
        {
            vect.push([ order[i] / X + 1, i + 1 ]);
        }
    }

    // Sort the vector
    vect.sort(function(a, b){return a[0] - b[0]});

    // Print the order
    for(let i = 0; i < N; i++)
    {
        document.write(vect[i][1] + " ");
    }

    document.write();
}

// Driver Code
let N = 3, X = 3;
let order = [ 2, 7, 4 ];

printOrder(order, N, X);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
1 3 2
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)