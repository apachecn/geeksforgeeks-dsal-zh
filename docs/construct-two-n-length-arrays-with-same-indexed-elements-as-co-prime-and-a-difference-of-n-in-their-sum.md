# 构造两个 N 长度的数组，其中相同索引的元素作为同素，并且它们的和相差 N

> 原文:[https://www . geeksforgeeks . org/construct-两个 n 长度数组，具有相同的索引元素作为同素和 n 之差/](https://www.geeksforgeeks.org/construct-two-n-length-arrays-with-same-indexed-elements-as-co-prime-and-a-difference-of-n-in-their-sum/)

给定一个正整数 **N** ，任务是生成两个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)，使得两个数组的相同索引元素为[同素](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)，数组元素之和的绝对差为 **N** 。

**示例:**

> **输入:** N = 5
> **输出:**
> {1，3，5，7，9}
> {2，4，6，8，10}
> **说明:**成对的同索引元素为(1，2)，(3，4)，(5，6)，(7，8)，(9，10)。可以观察到所有的对都是互质的，两个数组之和的绝对差是 5。
> 
> **输入:** N = 3
> **输出:**
> {2，4，7}
> {1，3，6}

**方法:**这个想法是基于这样的观察:[两个连续的自然数总是同素的](https://www.geeksforgeeks.org/group-all-co-prime-numbers-from-1-to-n/)，它们之间的区别是 **1** 。按照以下步骤解决问题:

*   初始化两个大小为 **N** 的数组 **A[]** 和 **B[]** 。
*   使用变量 **i** 迭代范围**【1，2 * N】**。对于范围内的每个元素，检查 **i** 是否能被 **2** 整除。如果发现为真，则将 **i** 插入数组 **A[]** 。否则，将 **i** 插入阵列 **B[]** 。
*   完成上述步骤后，打印两个阵列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate two arrays
// satisfying the given conditions
void printArrays(int n)
{
    // Declare the two arrays A and B
    vector<int> A, B;

    // Iterate from range [1, 2*n]
    for (int i = 1; i <= 2 * n; i++) {

        // Assign consecutive numbers to
        // same indices of the two arrays
        if (i % 2 == 0)
            A.push_back(i);
        else
            B.push_back(i);
    }

    // Print the first array
    cout << "{ ";
    for (int i = 0; i < n; i++) {
        cout << A[i];

        if (i != n - 1)
            cout << ", ";
    }
    cout << " }\n";

    // Print the second array, B
    cout << "{ ";
    for (int i = 0; i < n; i++) {
        cout << B[i];

        if (i != n - 1)
            cout << ", ";
    }
    cout << " }";
}

// Driver Code
int main()
{
    int N = 5;

    // Function Call
    printArrays(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Satisfying the given conditions
static void printArrays(int n)
{

    // Declare the two arrays A and B
    ArrayList<Integer> A = new ArrayList<Integer>();
    ArrayList<Integer> B = new ArrayList<Integer>();

    // Iterate from range [1, 2*n]
    for(int i = 1; i <= 2 * n; i++)
    {

        // Assign consecutive numbers to
        // same indices of the two arrays
        if (i % 2 == 0)
            A.add(i);
        else
            B.add(i);
    }

    // Print the first array
    System.out.print("{ ");
    for(int i = 0; i < n; i++)
    {
        System.out.print(A.get(i));

        if (i != n - 1)
            System.out.print(", ");
    }
    System.out.print(" }\n");

    // Print the second array, B
    System.out.print("{ ");
    for(int i = 0; i < n; i++)
    {
        System.out.print(B.get(i));

        if (i != n - 1)
            System.out.print(", ");
    }
    System.out.print(" }");
}

// Driver code
public static void main (String[] args)
{
    int N = 5;

    // Function Call
    printArrays(N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to generate two arrays
# satisfying the given conditions
def printArrays(n) :

    # Declare the two arrays A and B
    A, B = [], [];

    # Iterate from range [1, 2*n]
    for i in range(1, 2 * n + 1):

        # Assign consecutive numbers to
        # same indices of the two arrays
        if (i % 2 == 0) :
            A.append(i);
        else :
            B.append(i);

    # Print the first array
    print("{ ", end="");
    for i in range(n) :
        print(A[i], end="");

        if (i != n - 1) :
            print(", ", end="");

    print("}");

    # Print the second array, B
    print("{ ", end="");

    for i in range(n) :
        print(B[i], end="");

        if (i != n - 1) :
            print(",", end=" ");

    print(" }", end="");

# Driver Code
if __name__ == "__main__" :

    N = 5;

    # Function Call
    printArrays(N);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Satisfying the given conditions
static void printArrays(int n)
{

    // Declare the two arrays A and B
    List<int> A = new List<int>();
    List<int> B = new List<int>();

    // Iterate from range [1, 2*n]
    for(int i = 1; i <= 2 * n; i++)
    {

        // Assign consecutive numbers to
        // same indices of the two arrays
        if (i % 2 == 0)
            A.Add(i);
        else
            B.Add(i);
    }

    // Print the first array
    Console.Write("{ ");
    for(int i = 0; i < n; i++)
    {
        Console.Write(A[i]);

        if (i != n - 1)
            Console.Write(", ");
    }
    Console.Write(" }\n");

    // Print the second array, B
    Console.Write("{ ");
    for(int i = 0; i < n; i++)
    {
        Console.Write(B[i]);

        if (i != n - 1)
            Console.Write(", ");
    }
    Console.Write(" }");
}

// Driver Code
public static void Main()
{
    int N = 5;

    // Function Call
    printArrays(N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Satisfying the given conditions
    function printArrays(n)
    {

        // Declare the two arrays A and B
        let A = [];
        let B = [];

        // Iterate from range [1, 2*n]
        for(let i = 1; i <= 2 * n; i++)
        {

            // Assign consecutive numbers to
            // same indices of the two arrays
            if (i % 2 == 0)
                A.push(i);
            else
                B.push(i);
        }

        // Print the first array
        document.write("{ ");
        for(let i = 0; i < n; i++)
        {
            document.write(A[i]);

            if (i != n - 1)
                document.write(", ");
        }
        document.write(" }" + "</br>");

        // Print the second array, B
        document.write("{ ");
        for(let i = 0; i < n; i++)
        {
            document.write(B[i]);

            if (i != n - 1)
                document.write(", ");
        }
        document.write(" }");
    }

    let N = 5;

    // Function Call
    printArrays(N);

</script>
```

**Output:** 

```
{ 2, 4, 6, 8, 10 }
{ 1, 3, 5, 7, 9 }
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)