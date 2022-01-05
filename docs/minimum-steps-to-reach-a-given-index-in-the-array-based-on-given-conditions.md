# 根据给定条件达到数组中给定索引的最小步数

> 原文:[https://www . geeksforgeeks . org/基于给定条件到达给定阵列索引的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-reach-a-given-index-in-the-array-based-on-given-conditions/)

给定一个由整数 **-1** 、 **0** 、 **1** 组成的大小为 **N** 的[数组**arr[]【T3]，以及一个由查询组成的**](https://www.geeksforgeeks.org/array-data-structure/)**[数组](https://www.geeksforgeeks.org/array-data-structure/)**q[**。在[数组](https://www.geeksforgeeks.org/array-data-structure/) **中，arr[ ]，-1** 表示它左边的任何索引都是可达的， **1** 表示它右边的任何索引都是从该索引可达的。特定查询中的索引不是直接可达的，但是所有其他索引都是可达的。为每个查询找到从其相邻索引(取最近的一个)到达任何索引所需的最小步骤数，并最终返回结果数组。如果无法到达任何索引，返回 **-1** 。**

**示例:**

> **输入:** arr[ ] = {0，0，-1，0，1，0，1，1，-1，0}，q[ ] = {3，6}
> **输出:**结果[ ] = {6，2}
> **说明:**到达指标 3 只有 1 条路，即从指标 9 开始。因此最小距离= 9-3=6
> 到达索引 6 的最短路径是通过索引 4。因此最小距离=6-4=2
> 结果[ ]={6，2}
> 
> **输入** : arr[ ] = {-1，0，0，0，1}，q[ ] = {2，0}
> **输出**:结果[ ] = {-1，0}

**方法:**思想是存储左侧最近的 **1** 和右侧最近的 **-1** 的索引，然后在[遍历数组](https://www.geeksforgeeks.org/tag/array-traversal-question/) **q[]** 的同时，对于每个查询 **q[i]，**检查两侧的距离并存储最小的一个。按照以下步骤解决问题:

*   [初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **结果【】，v1【】**和**v2【】**来存储每个查询的结果，以及最近的 **1** 和 **-1。**
*   将变量 **last_1** 和 **last_m1** 初始化为 **-1** ，存储最新的 **1** 和 **-1。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   [将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **中**最后 _1** 的值推至 v2[]。**
    *   如果**arr【I】**等于 **1，**则将 **last_1** 的值设置为 **i.**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**，并执行以下任务:
    *   [将](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **中**最后 _m1** 的值推至 v2[]。**
    *   如果**arr【I】**等于 **-1，**则将 **last_m1** 的值设置为 **i.**
*   [反转向量](https://www.geeksforgeeks.org/how-to-reverse-a-vector-using-stl-in-c/) **v1[]。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
    *   如果 **v1[q[i]]** 和 **v2[q[i]]** 不等于 **-1，**则将**结果[i]** 的值设置为**ABS(v1[q[I]]–q[I])**或**ABS(v2[q[I]–q[I])的最小值。**
    *   否则，如果 **v1[q[i]]** 不等于 **-1，**则将值**结果[i]** 设置为**ABS(v1[q[I]]–q[I])。**
    *   否则，如果 **v2[q[i]]** 不等于 **-1，**则将值**结果[i]** 设置为**ABS(v2[q[I]]–q[I])。**
    *   否则，将**结果【I】**的值设置为 **-1。**
*   执行上述步骤后，打印矢量**结果[]** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the min distance
// from neighboring index
vector<int> res(int arr[], int q[], int n, int m)
{
    // Vectors result, v1 and v2 to
    // store the minimum distance, index
    // of -1 and 1 respectively
    vector<int> result, v1, v2;

    // Variables to store the last
    // position of -1 and 1
    int last_m1 = -1, last_1 = -1;

    // Traverse over the array arr[]
    // to store the index of 1
    for (int i = 0; i < n; i++) {
        v2.push_back(last_1);
        if (arr[i] == 1)
            last_1 = i;
    }

    // Traverse over the array arr[]
    // to store the index of -1
    for (int i = n - 1; i >= 0; i--) {
        v1.push_back(last_m1);
        if (arr[i] == -1)
            last_m1 = i;
    }

    // Reverse v1 to get the original order
    reverse(v1.begin(), v1.end());

    // Traverse over the array q[]
    for (int i = 0; i < m; i++) {

        if (v1[q[i]] != -1 and v2[q[i]] != -1)
            result.push_back(
                min(abs(v1[q[i]] - q[i]),
                    abs(v2[q[i]] - q[i])));
        else if (v1[q[i]] != -1)
            result.push_back(
                abs(v1[q[i]] - q[i]));
        else if (v2[q[i]] != -1)
            result.push_back(
                abs(v2[q[i]] - q[i]));
        else
            result.push_back(-1);
    }

    // Finally return the vector of result
    return result;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { -1, 0, 0, 1, -1, 1,
                  1, 0, 0, 1, -1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Query
    int q[] = { 1, 5, 10 };
    int m = sizeof(q) / sizeof(q[0]);

    // Function call to find the minimum distance
    vector<int> x = res(arr, q, n, m);

    // Print the resultant vector
    for (auto y : x)
        cout << y << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the min distance
// from neighboring index
static Vector<Integer> res(int arr[], int q[], int n, int m)
{

    // Vectors result, v1 and v2 to
    // store the minimum distance, index
    // of -1 and 1 respectively
    Vector<Integer> result = new Vector<Integer>(),
            v1= new Vector<Integer>(),
            v2= new Vector<Integer>();

    // Variables to store the last
    // position of -1 and 1
    int last_m1 = -1, last_1 = -1;

    // Traverse over the array arr[]
    // to store the index of 1
    for (int i = 0; i < n; i++) {
        v2.add(last_1);
        if (arr[i] == 1)
            last_1 = i;
    }

    // Traverse over the array arr[]
    // to store the index of -1
    for (int i = n - 1; i >= 0; i--) {
        v1.add(last_m1);
        if (arr[i] == -1)
            last_m1 = i;
    }

    // Reverse v1 to get the original order
    Collections.reverse(v1);

    // Traverse over the array q[]
    for (int i = 0; i < m; i++) {

        if (v1.get(q[i]) != -1 && v2.get(q[i]) != -1)
            result.add(
                Math.min(Math.abs(v1.get(q[i]) - q[i]),
                    Math.abs(v2.get(q[i]) - q[i])));
        else if (v1.get(q[i]) != -1)
            result.add(
                Math.abs(v1.get(q[i]) - q[i]));
        else if (v2.get(q[i]) != -1)
            result.add(
                Math.abs(v2.get(q[i]) - q[i]));
        else
            result.add(-1);
    }

    // Finally return the vector of result
    return result;
}

// Driver Code
public static void main(String[] args)
{
    // Input
    int arr[] = { -1, 0, 0, 1, -1, 1,
                  1, 0, 0, 1, -1, 0 };
    int n = arr.length;

    // Query
    int q[] = { 1, 5, 10 };
    int m = q.length;

    // Function call to find the minimum distance
    Vector<Integer> x = res(arr, q, n, m);

    // Print the resultant vector
    for (int y : x)
        System.out.print(y+ " ");

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to return the min distance
# from neighboring index
def res(arr, q, n, m):

        # Vectors result, v1 and v2 to
        # store the minimum distance, index
        # of -1 and 1 respectively
    result = []
    v1 = []
    v2 = []

    # Variables to store the last
    # position of -1 and 1
    last_m1 = -1
    last_1 = -1

    # Traverse over the array arr[]
    # to store the index of 1
    for i in range(0, n):
        v2.append(last_1)
        if (arr[i] == 1):
            last_1 = i

        # Traverse over the array arr[]
        # to store the index of -1
    for i in range(n-1, -1, -1):
        v1.append(last_m1)
        if (arr[i] == -1):
            last_m1 = i

        # Reverse v1 to get the original order
    v1.reverse()

    # Traverse over the array q[]
    for i in range(0, m):
        if (v1[q[i]] != -1 and v2[q[i]] != -1):
            result.append(min(abs(v1[q[i]] - q[i]), abs(v2[q[i]] - q[i])))
        elif (v1[q[i]] != -1):
            result.append(abs(v1[q[i]] - q[i]))
        elif (v2[q[i]] != -1):
            result.append(abs(v2[q[i]] - q[i]))
        else:
            result.push_back(-1)
    # Finally return the vector of result
    return result

# Driver Code
if __name__ == "__main__":

        # Input
    arr = [-1, 0, 0, 1, -1, 1, 1, 0, 0, 1, -1, 0]
    n = len(arr)

    # Query
    q = [1, 5, 10]
    m = len(q)

    # Function call to find the minimum distance
    x = res(arr, q, n, m)

    # Print the resultant vector
    for y in x:
        print(y, end=" ")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to return the min distance
    // from neighboring index
    static List<int> res(int[] arr, int[] q, int n, int m)
    {

        // Vectors result, v1 and v2 to
        // store the minimum distance, index
        // of -1 and 1 respectively
        List<int> result = new List<int>();
        List<int> v1 = new List<int>();
        List<int> v2 = new List<int>();

        // Variables to store the last
        // position of -1 and 1
        int last_m1 = -1, last_1 = -1;

        // Traverse over the array arr[]
        // to store the index of 1
        for (int i = 0; i < n; i++) {
            v2.Add(last_1);
            if (arr[i] == 1)
                last_1 = i;
        }

        // Traverse over the array arr[]
        // to store the index of -1
        for (int i = n - 1; i >= 0; i--) {
            v1.Add(last_m1);
            if (arr[i] == -1)
                last_m1 = i;
        }

        // Reverse v1 to get the original order
        v1.Reverse();

        // Traverse over the array q[]
        for (int i = 0; i < m; i++) {

            if (v1[q[i]] != -1 && v2[q[i]] != -1)
                result.Add(
                    Math.Min(Math.Abs(v1[q[i]] - q[i]),
                             Math.Abs(v2[q[i]] - q[i])));
            else if (v1[q[i]] != -1)
                result.Add(Math.Abs(v1[q[i]] - q[i]));
            else if (v2[q[i]] != -1)
                result.Add(Math.Abs(v2[q[i]] - q[i]));
            else
                result.Add(-1);
        }

        // Finally return the vector of result
        return result;
    }

    // Driver Code
    public static void Main()
    {

        // Input
        int[] arr
            = { -1, 0, 0, 1, -1, 1, 1, 0, 0, 1, -1, 0 };
        int n = arr.Length;

        // Query
        int[] q = { 1, 5, 10 };
        int m = q.Length;

        // Function call to find the minimum distance
        List<int> x = res(arr, q, n, m);

        // Print the resultant vector
        foreach(int y in x) Console.Write(y + " ");
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to return the min distance
       // from neighboring index
       function res(arr, q, n, m) {
           // Vectors result, v1 and v2 to
           // store the minimum distance, index
           // of -1 and 1 respectively
           let result = [], v1 = [], v2 = [];

           // Variables to store the last
           // position of -1 and 1
           let last_m1 = -1, last_1 = -1;

           // Traverse over the array arr[]
           // to store the index of 1
           for (let i = 0; i < n; i++) {
               v2.push(last_1);
               if (arr[i] == 1)
                   last_1 = i;
           }

           // Traverse over the array arr[]
           // to store the index of -1
           for (let i = n - 1; i >= 0; i--) {
               v1.push(last_m1);
               if (arr[i] == -1)
                   last_m1 = i;
           }

           // Reverse v1 to get the original order
           v1.reverse();

           // Traverse over the array q[]
           for (let i = 0; i < m; i++) {

               if (v1[q[i]] != -1 && v2[q[i]] != -1)
                   result.push(
                       Math.min(Math.abs(v1[q[i]] - q[i]),
                           Math.abs(v2[q[i]] - q[i])));
               else if (v1[q[i]] != -1)
                   result.push(
                       Math.abs(v1[q[i]] - q[i]));
               else if (v2[q[i]] != -1)
                   result.push(
                       Math.abs(v2[q[i]] - q[i]));
               else
                   result.push_back(-1);
           }

           // Finally return the vector of result
           return result;
       }

       // Driver Code

       // Input
       let arr = [-1, 0, 0, 1, -1, 1,
           1, 0, 0, 1, -1, 0];
       let n = arr.length;

       // Query
       let q = [1, 5, 10];
       let m = q.length;

       // Function call to find the minimum distance
       let x = res(arr, q, n, m);

       // Print the resultant array
       for (let i = 0; i < x.length; i++)
           document.write(x[i] + " ");

    // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
3 2 1 
```

***时间复杂度:** O(N+M)其中 N 是 **arr[ ]** 的大小，M 是 **q[ ]***
***的大小辅助空间:** O(N)*