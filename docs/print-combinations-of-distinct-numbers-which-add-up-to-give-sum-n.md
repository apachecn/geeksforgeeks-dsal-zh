# 打印不同数字的组合，相加得出总和 N

> 原文:[https://www . geeksforgeeks . org/print-distinct-numbers-that-add-to-sum-n/](https://www.geeksforgeeks.org/print-combinations-of-distinct-numbers-which-add-up-to-give-sum-n/)

给定一个正整数 **N** ，任务是找出所有的正整数组合加起来的给定整数 **N** 。程序应该只打印组合，而不是排列，并且组合中的所有整数必须是不同的。例如，对于输入 3，应该打印 1，2 或 2，1，而不能打印 1，1，1，1，因为整数是不同的。
**例:**

> **输入:** N = 3
> **输出:**
> 1 2
> 3
> **输入:** N = 7
> **输出:**
> 1 2 4
> 1 6
> 2 5
> 3 4
> 7

**方法:**该方法是这里[讨论的方法的扩展](https://www.geeksforgeeks.org/find-all-combinations-that-adds-upto-given-number-2/)。用来得到所有不同元素的想法是，首先我们找到所有相加得到总和的元素 **N** 。然后我们迭代每个元素并将元素存储到[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。将元素存储到集合中会删除所有重复的元素，然后我们将集合的元素之和相加，并检查它是否等于 **N** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

/* arr[] to store all the distinct elements
    index - next location in array
    num - given number
    reducedNum - reduced number */
void findCombinationsUtil(int arr[], int index,
                          int n, int red_num)
{

    // Set to store all the
    // distinct elements
    set<int> s;
    int sum = 0;

    // Base condition
    if (red_num < 0) {
        return;
    }

    if (red_num == 0) {

        // Iterate over all the elements
        // and store it into the set
        for (int i = 0; i < index; i++) {
            s.insert(arr[i]);
        }

        // Calculate the sum of all
        // the elements of the set
        for (auto itr = s.begin();
             itr != s.end(); itr++) {
            sum = sum + (*itr);
        }

        // Compare whether the sum is equal to n or not,
        // if it is equal to n print the numbers
        if (sum == n) {
            for (auto i = s.begin();
                 i != s.end(); i++) {
                cout << *i << " ";
            }
            cout << endl;
            return;
        }
    }

    // Find previous number stored in the array
    int prev = (index == 0) ? 1 : arr[index - 1];

    for (int k = prev; k <= n; k++) {

        // Store all the numbers recursively
        // into the arr[]
        arr[index] = k;
        findCombinationsUtil(arr, index + 1,
                             n, red_num - k);
    }
}

// Function to find all the
// distinct combinations of n
void findCombinations(int n)
{
    int a[n];
    findCombinationsUtil(a, 0, n, n);
}

// Driver code
int main()
{
    int n = 7;
    findCombinations(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

/* arr[] to store all the distinct elements
    index - next location in array
    num - given number
    reducedNum - reduced number */
static void findCombinationsUtil(int arr[], int index,
                        int n, int red_num)
{

    // Set to store all the
    // distinct elements
    HashSet<Integer> s = new HashSet<>();
    int sum = 0;

    // Base condition
    if (red_num < 0)
    {
        return;
    }

    if (red_num == 0)
    {

        // Iterate over all the elements
        // and store it into the set
        for (int i = 0; i < index; i++)
        {
            s.add(arr[i]);
        }

        // Calculate the sum of all
        // the elements of the set
        for (Integer itr : s)
        {

            sum = sum + itr;
        }

        // Compare whether the sum is equal to n or not,
        // if it is equal to n print the numbers
        if (sum == n)
        {
            for (Integer i : s)
            {
                System.out.print(i+" ");
            }
            System.out.println();
            return;
        }
    }

    // Find previous number stored in the array
    int prev = (index == 0) ? 1 : arr[index - 1];

    for (int k = prev; k <= n; k++)
    {

        // Store all the numbers recursively
        // into the arr[]
        if(index < n)
        {
            arr[index] = k;
            findCombinationsUtil(arr, index + 1,
                            n, red_num - k);

        }
    }
}

// Function to find all the
// distinct combinations of n
static void findCombinations(int n)
{
    int []a = new int[n];
    findCombinationsUtil(a, 0, n, n);
}

// Driver code
public static void main(String arr[])
{
    int n = 7;
    findCombinations(n);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# arr[] to store all the distinct elements
# index - next location in array
# num - given number
# reducedNum - reduced number
def findCombinationsUtil(arr, index, n, red_num):

    # Set to store all the
    # distinct elements
    s = set()
    sum = 0

    # Base condition
    if (red_num < 0):
        return

    if (red_num == 0):

        # Iterate over all the elements
        # and store it into the set
        for i in range(index):
            s.add(arr[i])

        # Calculate the sum of all
        # the elements of the set
        for itr in s:
            sum = sum + (itr)

        # Compare whether the sum is equal to n or not,
        # if it is equal to n print the numbers
        if (sum == n):
            for i in s:
                print(i, end = " ")
            print("\n", end = "")
            return

    # Find previous number stored in the array
    if (index == 0):
        prev = 1
    else:
        prev = arr[index - 1]

    for k in range(prev, n + 1, 1):

        # Store all the numbers recursively
        # into the arr[]
        arr[index] = k
        findCombinationsUtil(arr, index + 1,
                             n, red_num - k)

# Function to find all the
# distinct combinations of n
def findCombinations(n):
    a = [0 for i in range(n + 1)]
    findCombinationsUtil(a, 0, n, n)

# Driver code
if __name__ == '__main__':
    n = 7
    findCombinations(n)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

/* arr[] to store all the distinct elements
    index - next location in array
    num - given number
    reducedNum - reduced number */
static void findCombinationsUtil(int []arr, int index,
                        int n, int red_num)
{

    // Set to store all the
    // distinct elements
    HashSet<int> s = new HashSet<int>();
    int sum = 0;

    // Base condition
    if (red_num < 0)
    {
        return;
    }

    if (red_num == 0)
    {

        // Iterate over all the elements
        // and store it into the set
        for (int i = 0; i < index; i++)
        {
            s.Add(arr[i]);
        }

        // Calculate the sum of all
        // the elements of the set
        foreach (int itr in s)
        {

            sum = sum + itr;
        }

        // Compare whether the sum is equal to n or not,
        // if it is equal to n print the numbers
        if (sum == n)
        {
            foreach (int i in s)
            {
                Console.Write(i+" ");
            }
            Console.WriteLine();
            return;
        }
    }

    // Find previous number stored in the array
    int prev = (index == 0) ? 1 : arr[index - 1];

    for (int k = prev; k <= n; k++)
    {

        // Store all the numbers recursively
        // into the arr[]
        if(index < n)
        {
            arr[index] = k;
            findCombinationsUtil(arr, index + 1,
                            n, red_num - k);

        }
    }
}

// Function to find all the
// distinct combinations of n
static void findCombinations(int n)
{
    int []a = new int[n];
    findCombinationsUtil(a, 0, n, n);
}

// Driver code
public static void Main(String []arr)
{
    int n = 7;
    findCombinations(n);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach
      /* arr[] to store all the distinct elements
    index - next location in array
    num - given number
    reducedNum - reduced number */
      function findCombinationsUtil(arr, index, n, red_num) {
        // Set to store all the
        // distinct elements
        var s = new Set();
        var sum = 0;

        // Base condition
        if (red_num < 0) {
          return;
        }

        if (red_num === 0) {
          // Iterate over all the elements
          // and store it into the set
          for (var i = 0; i < index; i++) {
            s.add(arr[i]);
          }

          // Calculate the sum of all
          // the elements of the set
          for (const itr of s) {
            sum = sum + itr;
          }

          // Compare whether the sum is equal to n or not,
          // if it is equal to n print the numbers
          if (sum === n) {
            for (const i of s) {
              document.write(i + " ");
            }
            document.write("<br>");
            return;
          }
        }

        // Find previous number stored in the array
        var prev = index === 0 ? 1 : arr[index - 1];

        for (var k = prev; k <= n; k++) {
          // Store all the numbers recursively
          // into the arr[]
          if (index < n) {
            arr[index] = k;
            findCombinationsUtil(arr, index + 1, n, red_num - k);
          }
        }
      }

      // Function to find all the
      // distinct combinations of n
      function findCombinations(n) {
        var a = new Array(n).fill(0);
        findCombinationsUtil(a, 0, n, n);
      }

      // Driver code
      var n = 7;
      findCombinations(n);

</script>
```

**Output:** 

```
1 2 4 
1 6 
2 5 
3 4 
7
```