# 打印给定数组的 k 个不同排序排列

> 原文:[https://www . geeksforgeeks . org/print-k-给定数组的不同排序排列/](https://www.geeksforgeeks.org/print-k-different-sorted-permutations-of-a-given-array/)

给定一个包含 **N** 整数的数组 **arr[]** ，任务是打印 **k** 不同的索引排列，使得这些索引处的值形成一个非递减序列。如果不可能，打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，3，3，1}，k = 3
> **输出:**
> 0 3 1 2
> 3 0 1 2
> 3 0 2 1
> 对于每个排列，索引处的值形成以下序列{1，1，3，3}
> **输入:** arr[] = {1，2，3，4}，k = 3
> **输出:**-1【T11

**方法:**对给定的数组进行排序，并跟踪每个元素的原始索引。这给出了一个必要的排列。如果任意两个连续的元素相等，那么它们可以交换，得到另一个排列。类似地，可以生成第三置换。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int next_pos = 1;
// Utility function to print the original indices
// of the elements of the array
void printIndices(int n, pair<int, int> a[])
{
    for (int i = 0; i < n; i++)
        cout << a[i].second << " ";
    cout << endl;
}

// Function to print the required permutations
void printPermutations(int n, int a[], int k)
{

    // To keep track of original indices
    pair<int, int> arr[n];
    for (int i = 0; i < n; i++)
    {
        arr[i].first = a[i];
        arr[i].second = i;
    }

    // Sort the array
    sort(arr, arr + n);

    // Count the number of swaps that can
    // be made
    int count = 1;
    for (int i = 1; i < n; i++)
        if (arr[i].first == arr[i - 1].first)
            count++;

    // Cannot generate 3 permutations
    if (count < k) {
        cout << "-1";
        return;
    }

    for (int i = 0; i < k - 1; i++)
    {
        // Print the first permutation
        printIndices(n, arr);

        // Find an index to swap and create
        // second permutation
        for (int j = next_pos; j < n; j++)
        {
            if (arr[j].first == arr[j - 1].first)
            {
                swap(arr[j], arr[j - 1]);
                next_pos = j + 1;
                break;
            }
        }
    }

    // Print the last permutation
    printIndices(n, arr);
}

// Driver code
int main()
{
    int a[] = { 1, 3, 3, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    int k = 3;

    // Function call
    printPermutations(n, a, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {
    static int next_pos = 1;
    static class pair {
        int first, second;
        pair()
        {
            first = 0;
            second = 0;
        }
    }

    // Utility function to print the original indices
    // of the elements of the array
    static void printIndices(int n, pair a[])
    {
        for (int i = 0; i < n; i++)
            System.out.print(a[i].second + " ");
        System.out.println();
    }
    static class sort implements Comparator<pair>
    {
        // Used for sorting in ascending order
        public int compare(pair a, pair b)
        {
            return a.first < b.first ? -1 : 1;
        }
    }

    // Function to print the required permutations
    static void printPermutations(int n, int a[], int k)
    {

        // To keep track of original indices
        pair arr[] = new pair[n];
        for (int i = 0; i < n; i++)
        {
            arr[i] = new pair();
            arr[i].first = a[i];
            arr[i].second = i;
        }

        // Sort the array
        Arrays.sort(arr, new sort());

        // Count the number of swaps that can
        // be made
        int count = 1;
        for (int i = 1; i < n; i++)
            if (arr[i].first == arr[i - 1].first)
                count++;

        // Cannot generate 3 permutations
        if (count < k)
        {
            System.out.print("-1");
            return;
        }

        for (int i = 0; i < k - 1; i++)
        {
            // Print the first permutation
            printIndices(n, arr);

            // Find an index to swap and create
            // second permutation
            for (int j = next_pos; j < n; j++)
            {
                if (arr[j].first == arr[j - 1].first)
                {
                    pair t = arr[j];
                    arr[j] = arr[j - 1];
                    arr[j - 1] = t;

                    next_pos = j + 1;
                    break;
                }
            }
        }

        // Print the last permutation
        printIndices(n, arr);
    }

    // Driver code
    public static void main(String arsg[])
    {
        int a[] = { 1, 3, 3, 1 };
        int n = a.length;

        int k = 3;

        // Function call
        printPermutations(n, a, k);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Utility function to print the original
# indices of the elements of the array

def printIndices(n, a):
    for i in range(n):
        print(a[i][1], end=" ")
    print("\n", end="")

# Function to print the required
# permutations

def printPermutations(n, a, k):

    # To keep track of original indices
    arr = [[0, 0] for i in range(n)]
    for i in range(n):
        arr[i][0] = a[i]
        arr[i][1] = i

    # Sort the array
    arr.sort(reverse=False)

    # Count the number of swaps that
    # can be made
    count = 1
    for i in range(1, n):
        if (arr[i][0] == arr[i - 1][0]):
            count += 1

    # Cannot generate 3 permutations
    if (count < k):
        print("-1", end="")
        return

    next_pos = 1
    for i in range(k - 1):

        # Print the first permutation
        printIndices(n, arr)

        # Find an index to swap and create
        # second permutation
        for j in range(next_pos, n):
            if (arr[j][0] == arr[j - 1][0]):
                temp = arr[j]
                arr[j] = arr[j - 1]
                arr[j - 1] = temp
                next_pos = j + 1
                break

    # Print the last permutation
    printIndices(n, arr)

# Driver code
if __name__ == '__main__':
    a = [1, 3, 3, 1]
    n = len(a)
    k = 3

    # Function call
    printPermutations(n, a, k)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG {
  static int next_pos = 1;
  public class pair {
    public int first, second;
    public pair()
    {
      first = 0;
      second = 0;
    }
  }

  class sortHelper : IComparer
  {
    int IComparer.Compare(object a, object b)
    {
      pair first = (pair)a;
      pair second = (pair)b;
      return first.first < second.first ? -1 : 1;
    }
  }

  // Utility function to print the original indices
  // of the elements of the array
  static void printIndices(int n, pair []a)
  {
    for (int i = 0; i < n; i++)
      Console.Write(a[i].second + " ");
    Console.WriteLine();
  }

  // Function to print the required permutations
  static void printPermutations(int n, int []a, int k)
  {

    // To keep track of original indices
    pair []arr = new pair[n];
    for (int i = 0; i < n; i++)
    {
      arr[i] = new pair();
      arr[i].first = a[i];
      arr[i].second = i;
    }

    // Sort the array
    Array.Sort(arr, new sortHelper());

    // Count the number of swaps that can
    // be made
    int count = 1;
    for (int i = 1; i < n; i++)
      if (arr[i].first == arr[i - 1].first)
        count++;

    // Cannot generate 3 permutations
    if (count < k)
    {
      Console.Write("-1");
      return;
    }

    for (int i = 0; i < k - 1; i++)
    {

      // Print the first permutation
      printIndices(n, arr);

      // Find an index to swap and create
      // second permutation
      for (int j = next_pos; j < n; j++)
      {
        if (arr[j].first == arr[j - 1].first)
        {
          pair t = arr[j];
          arr[j] = arr[j - 1];
          arr[j - 1] = t;

          next_pos = j + 1;
          break;
        }
      }
    }

    // Print the last permutation
    printIndices(n, arr);
  }

  // Driver code
  public static void Main(string []args)
  {
    int []a = { 1, 3, 3, 1 };
    int n = a.Length;

    int k = 3;

    // Function call
    printPermutations(n, a, k);
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var next_pos = 1;
// Utility function to print the original indices
// of the elements of the array
function printIndices(n, a)
{
    for (var i = 0; i < n; i++)
        document.write( a[i][1] + " ");
    document.write("<br>");
}

// Function to print the required permutations
function printPermutations(n, a, k)
{

    // To keep track of original indices
    var arr = Array.from(Array(n), ()=>Array(2));
    for (var i = 0; i < n; i++)
    {
        arr[i][0] = a[i];
        arr[i][1] = i;
    }

    // Sort the array
    arr.sort();

    // Count the number of swaps that can
    // be made
    var count = 1;
    for (var i = 1; i < n; i++)
        if (arr[i][0] == arr[i - 1][0])
            count++;

    // Cannot generate 3 permutations
    if (count < k) {
        document.write( "-1");
        return;
    }

    for (var i = 0; i < k - 1; i++)
    {
        // Print the first permutation
        printIndices(n, arr);

        // Find an index to swap and create
        // second permutation
        for (var j = next_pos; j < n; j++)
        {
            if (arr[j][0] == arr[j - 1][0])
            {
                [arr[j], arr[j - 1]] = [arr[j - 1], arr[j]];
                next_pos = j + 1;
                break;
            }
        }
    }

    // Print the last permutation
    printIndices(n, arr);
}

// Driver code
var a = [1, 3, 3, 1];
var n = a.length;
var k = 3;

// Function call
printPermutations(n, a, k);

// This code is contributed by famously.
</script>
```

**Output**

```
0 3 1 2 
3 0 1 2 
3 0 2 1 
```

**时间复杂度:** O(N log N + K N)