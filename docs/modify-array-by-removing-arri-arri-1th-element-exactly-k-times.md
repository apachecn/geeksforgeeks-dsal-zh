# 通过精确 K 次移除第(arr[i] + arr[i + 1])个元素来修改数组

> 原文:[https://www . geesforgeks . org/modify-array-by-remove-arri-1 th-element-just-k-times/](https://www.geeksforgeeks.org/modify-array-by-removing-arri-arri-1th-element-exactly-k-times/)

给定由第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **arr[i] = i** ( *基于 1 的索引*)和正整数 **K** ，任务是[打印在移除每个 **(arr[i] + arr[i + 1]) <sup>后获得的数组</sup>**](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]**

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8}，K = 2
> **输出:** 1 2 4 5 7
> **解释:**
> 最初，数组 arr[]为{1，2，3，4，5，6，7，8}。
> **操作 1:** 从数组 arr[]中删除每(A[1] + A[2]) <sup>个</sup>元素，即每 3 个<sup>个</sup>元素。现在数组修改为{1，2，4，5，7，8}。
> **操作 2:** 从数组 arr[]中删除每(A[2] + A[3]) <sup>个</sup>元素，即每 6 个<sup>个</sup>元素。现在数组修改为{1，2，4，5，7}。
> 执行上述操作后，得到的数组为{1，2，4，5，7}。
> 
> **输入:** N = 10，K = 3
> T3】输出: 1 2 4 5 7 10

**方法:**通过从每个**I**操作中的数组中删除每个 **(arr[i] + arr[i + 1]) <sup>第</sup>T7】项，精确地执行给定的操作 **K** 次，可以解决给定的问题。按照以下步骤解决问题:**

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/python-range-function/)**【0，K–1】**，并执行以下步骤:
    *   初始化一个辅助数组 **B[]** ，在每次删除操作后存储数组 **arr[]** 的元素。
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果当前索引不能被值 **(arr[i] + arr[i + 1])** 整除，则在数组 **B[]** 中插入该元素。
    *   完成上述步骤后，将数组 **B[]** 的所有元素插入到数组 **arr[]** 中。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 作为结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to modify array by removing
// every K-th element from the array
vector<int> removeEveryKth(vector<int> l, int k)
{

    for (int i = 0; i < l.size(); i++)
    {
        // Check if current element
        // is the k-th element
        if (i % k == 0)
            l[i] = 0;
    }

    // Stores the elements after
    // removing every kth element
    vector<int> arr;
    arr.push_back(0);

    for (int i = 1; i < l.size(); i++)
    {

        // Append the current element
        // if it is not k-th element
        if (l[i] != 0)
            arr.push_back(l[i]);
      }

    // Return the new array after
    // removing every k-th element
    return arr;
}

// Function to print the array
void printArray(vector<int> l)
{

    // Traverse the array l[]
    for (int i = 1; i < l.size(); i++)
        cout << l[i] << " ";
      cout << endl;
}

// Function to print the array after
// performing the given operations
// exactly k times
void printSequence(int n, int k)
{

    // Store first N natural numbers
    vector<int> l(n+1);

    for (int i = 0; i < n + 1; i++) l[i]=i;
    int x = 1;

    // Iterate over the range [0, k-1]
    for (int i = 0; i < k; i++)
    {

        // Store sums of the two
        // consecutive terms
        int p = l[x] + l[x + 1];

        // Remove every p-th
        // element from the array
        l = removeEveryKth(l, p);

        // Increment x by 1 for
        // the next iteration
        x += 1;
      }

    // Print the resultant array
    printArray(l);
}

// Driver Code
int main()
{
    // Given arrays
    int N = 8;
    int K = 2;

    //Function Call
    printSequence(N, K);

}

// This code is contributed by mohit kumar  29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to modify array by removing
    // every K-th element from the array
    static int[] removeEveryKth(int l[], int k)
    {

        for (int i = 0; i < l.length; i++) {
            // Check if current element
            // is the k-th element
            if (i % k == 0)
                l[i] = 0;
        }

        // Stores the elements after
        // removing every kth element
        ArrayList<Integer> list = new ArrayList<>();
        list.add(0);

        for (int i = 1; i < l.length; i++) {

            // Append the current element
            // if it is not k-th element
            if (l[i] != 0)
                list.add(l[i]);
        }

        // Return the new array after
        // removing every k-th element
        return list.stream().mapToInt(i -> i).toArray();
    }

    // Function to print the array
    static void printArray(int l[])
    {

        // Traverse the array l[]
        for (int i = 1; i < l.length; i++)
            System.out.print(l[i] + " ");
        System.out.println();
    }

    // Function to print the array after
    // performing the given operations
    // exactly k times
    static void printSequence(int n, int k)
    {

        // Store first N natural numbers
        int l[] = new int[n + 1];

        for (int i = 0; i < n + 1; i++)
            l[i] = i;
        int x = 1;

        // Iterate over the range [0, k-1]
        for (int i = 0; i < k; i++) {

            // Store sums of the two
            // consecutive terms
            int p = l[x] + l[x + 1];

            // Remove every p-th
            // element from the array
            l = removeEveryKth(l, p);

            // Increment x by 1 for
            // the next iteration
            x += 1;
        }

        // Print the resultant array
        printArray(l);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given arrays
        int N = 8;
        int K = 2;

        // Function Call
        printSequence(N, K);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python approach for the above approach

# Function to modify array by removing
# every K-th element from the array
def removeEveryKth(l, k):

    for i in range(0, len(l)):

        # Check if current element
        # is the k-th element
        if i % k == 0:
            l[i] = 0

    # Stores the elements after
    # removing every kth element
    arr = [0]

    for i in range(1, len(l)):

        # Append the current element
        # if it is not k-th element
        if l[i] != 0:
            arr.append(l[i])

    # Return the new array after
    # removing every k-th element
    return arr

# Function to print the array
def printArray(l):

    # Traverse the array l[]
    for i in range(1, len(l)):
        print(l[i], end =" ")

    print()

# Function to print the array after
# performing the given operations
# exactly k times
def printSequence(n, k):

    # Store first N natural numbers
    l = [int(i) for i in range(0, n + 1)]

    x = 1

    # Iterate over the range [0, k-1]
    for i in range(0, k):

        # Store sums of the two
        # consecutive terms
        p = l[x] + l[x + 1]

        # Remove every p-th
        # element from the array
        l = removeEveryKth(l, p)

        # Increment x by 1 for
        # the next iteration
        x += 1

    # Print the resultant array
    printArray(l)

# Driver Code
N = 8
K = 2

# Function Call
printSequence(N, K)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to modify array by removing
    // every K-th element from the array
    static List<int> removeEveryKth(List<int> l, int k)
    {

        for (int i = 0; i < l.Count; i++) {
            // Check if current element
            // is the k-th element
            if (i % k == 0)
                l[i] = 0;
        }

        // Stores the elements after
        // removing every kth element
        List<int> arr = new List<int>();
        arr.Add(0);

        for (int i = 1; i < l.Count; i++) {

            // Append the current element
            // if it is not k-th element
            if (l[i] != 0)
                arr.Add(l[i]);
        }

        // Return the new array after
        // removing every k-th element
        return arr;
    }

    // Function to print the array
    static void printArray(List<int> l)
    {

        // Traverse the array l[]
        for (int i = 1; i < l.Count; i++)
            Console.Write(l[i] + " ");
        Console.WriteLine();
    }

    // Function to print the array after
    // performing the given operations
    // exactly k times
    static void printSequence(int n, int k)
    {

        // Store first N natural numbers
        List<int> l = new List<int>();

        for (int i = 0; i < n + 1; i++)
            l.Add(i);
        int x = 1;

        // Iterate over the range [0, k-1]

        for (int i = 0; i < k; i++) {

            // Store sums of the two
            // consecutive terms
            int p = l[x] + l[x + 1];

            // Remove every p-th
            // element from the array
            l = removeEveryKth(l, p);

            // Increment x by 1 for
            // the next iteration
            x += 1;
        }

        // Print the resultant array
        printArray(l);
    }

    // Driver Code
    public static void Main()
    {

        // Given arrays
        int N = 8;
        int K = 2;

        // Function Call
        printSequence(N, K);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

       // Javascript program for the above approach

       // Function to modify array by removing
       // every K-th element from the array
       function removeEveryKth(l, k) {

           for (let i = 0; i < l.length; i++) {
               // Check if current element
               // is the k-th element
               if (i % k == 0)
                   l[i] = 0;
           }

           // Stores the elements after
           // removing every kth element
           let arr = [0];

           for (let i = 1; i < l.length; i++) {

               // Append the current element
               // if it is not k-th element
               if (l[i] != 0)
                   arr.push(l[i]);
           }

           // Return the new array after
           // removing every k-th element
           return arr;
       }

       // Function to print the array
       function printArray(l) {

           // Traverse the array l[]
           for (let i = 1; i < l.length; i++)
               document.write(l[i] + " ");

       }

       // Function to print the array after
       // performing the given operations
       // exactly k times
       function printSequence(n, k) {

           // Store first N natural numbers
           let l = [0];

           for (let i = 0; i < n + 1; i++) l[i] = i;
           let x = 1;

           // Iterate over the range [0, k-1]
           for (let i = 0; i < k; i++) {

               // Store sums of the two
               // consecutive terms
               let p = l[x] + l[x + 1];

               // Remove every p-th
               // element from the array
               l = removeEveryKth(l, p);

               // Increment x by 1 for
               // the next iteration
               x += 1;
           }

           // Print the resultant array
           printArray(l);
       }

       // Driver Code

       // Given arrays
       let N = 8;
       let K = 2;

       //Function Call
       printSequence(N, K);

       // This code is contributed by Hritik

   </script>
```

**Output:** 

```
1 2 4 5 7
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(N)*