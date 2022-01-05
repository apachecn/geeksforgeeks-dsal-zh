# Q 查询更新后所有可能的非空子阵列的逐位“与”的逐位“或”

> 原文:[https://www . geeksforgeeks . org/按位或所有可能的非空子数组-q 查询后更新/](https://www.geeksforgeeks.org/bitwise-or-of-bitwise-and-of-all-possible-non-empty-subarrays-after-q-query-updates/)

给定由正整数 **N** 和类型为**【L，R】**的查询数组**Q【】**组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在为每个查询更新索引 **L** 到 **R** 处的数组元素后，找到数组的所有可能的非空子数组的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[ ] = {1，2，3}，Q[ ] = {{1，4}，{3，0}}
> **输出:** 7 6
> **解释:**
> 所有子阵都是{1}、{2}、{3}、{1，2}、{2，3}和{1，2，3}
> **对于查询 1:** 更新 arr[1] = 4，那么新数组就是{4，2}所有子阵列的按位&为 4、2、3、0、2、0，按位“或”({4、2、3、0、2、0})等于 7。
> **对于查询 2:** 更新 arr[3] = 0，则新数组为{4，2，0}。所有子阵列的按位&为 4、2、0、0、0、0，按位“或”({4、2、0、0、0、0})等于 6。
> 
> **输入:** arr[ ] = {1，2，1}，Q[ ] = {{2，1}}
> **输出:** 1

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[]** 并为每个查询更新数组元素**arr【L】**到 **R** 和[找到所有子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)及其按位 and，并将它们存储在新数组中。存储按位“与”后，找到新形成的数组的按位“或”。

***时间复杂度:**O(N<sup>2</sup>Q)*
*T8】辅助空间: O(N <sup>2</sup> )*

**有效方法:**上述方法也可以通过使用以下事实进行优化:所有生成的子阵列的结果按位“与”的按位“或”与阵列中所有元素的结果“T2”按位“或”相同。

因此，想法是在每次更新数组后，执行查询并打印所有数组元素的按位或值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

    // Function to find the Bitwise OR
    // of Bitwise AND of all possible
    // subarrays after performing the
    // every query
  void performQuery(vector<int> arr,
                             vector<vector<int>> Q)
    {
        // Traversing each pair
        // of the query
        for (int i = 0; i < Q.size(); i++) {

            // Stores the Bitwise OR
            int or1 = 0;

            // Updating the array
            int x = Q[i][0];
            arr[x - 1] = Q[i][1];

            // Find the Bitwise OR of
            // new updated array
            for (int j = 0; j < arr.size(); j++) {
                or1 = or1 | arr[j];
            }

            // Print the ans
            cout<<or1<<" ";
        }
    }

    // Driver Code
   int main()
    {
        vector<int> arr({ 1, 2, 3 });
        vector<int> v1({1,4});
        vector<int> v2({3,0});
        vector<vector<int>> Q;
        Q.push_back(v1);
        Q.push_back(v2);
        performQuery(arr, Q);
    }

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find the Bitwise OR
    // of Bitwise AND of all possible
    // subarrays after performing the
    // every query
    static void performQuery(int arr[],
                             int Q[][])
    {
        // Traversing each pair
        // of the query
        for (int i = 0; i < Q.length; i++) {

            // Stores the Bitwise OR
            int or = 0;

            // Updating the array
            int x = Q[i][0];
            arr[x - 1] = Q[i][1];

            // Find the Bitwise OR of
            // new updated array
            for (int j = 0; j < arr.length; j++) {
                or = or | arr[j];
            }

            // Print the ans
            System.out.print(or + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3 };
        int Q[][] = { { 1, 4 }, { 3, 0 } };
        performQuery(arr, Q);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to find the Bitwise OR
# of Bitwise AND of all possible
# subarrays after performing the
# every query
def performQuery(arr, Q):

    # Traversing each pair
    # of the query
    for i in range (0, len(Q)):

        # Stores the Bitwise OR
        orr = 0

        # Updating the array
        x = Q[i][0]
        arr[x - 1] = Q[i][1]

        # Find the Bitwise OR of
        # new updated array
        for j in range(0,len(arr)):
            orr = orr | arr[j]

        # Print the ans
        print(orr ,end= " ")

# Driver Code
arr = [1, 2, 3]
Q = [[1, 4] , [3, 0]]
performQuery(arr, Q)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to find the Bitwise OR
    // of Bitwise AND of all possible
    // subarrays after performing the
    // every query
    static void performQuery(int []arr, int [,]Q)
    {
        // Traversing each pair
        // of the query
        for (int i = 0; i < Q.Length; i++) {

            // Stores the Bitwise OR
            int or = 0;

            // Updating the array
            int x = Q[i,0];
            arr[x - 1] = Q[i,1];

            // Find the Bitwise OR of
            // new updated array
            for (int j = 0; j < arr.Length; j++) {
                or = or | arr[j];
            }

            // Print the ans
            Console.Write(or + " ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 1, 2, 3 };
        int [,]Q = { { 1, 4 }, { 3, 0 } };
        performQuery(arr, Q);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        // Function to find the Bitwise OR
        // of Bitwise AND of all possible
        // subarrays after performing the
        // every query
        function performQuery(arr, Q)
        {

            // Traversing each pair
            // of the query
            for (let i = 0; i < Q.length; i++) {

                // Stores the Bitwise OR
                let or = 0;

                // Updating the array
                let x = Q[i][0];
                arr[x - 1] = Q[i][1];

                // Find the Bitwise OR of
                // new updated array
                for (let j = 0; j < arr.length; j++) {
                    or = or | arr[j];
                }

                // Print the ans
                document.write(or + " ");
            }
        }

        // Driver Code
        let arr = [1, 2, 3];
        let Q = [[1, 4], [3, 0]];
        performQuery(arr, Q);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
7 6
```

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*