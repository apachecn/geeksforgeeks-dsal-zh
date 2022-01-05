# 构建最长递增子序列并打印最长递增子序列

> 原文:[https://www . geeksforgeeks . org/构造最长递增子序列-使用动态编程/](https://www.geeksforgeeks.org/construction-of-longest-increasing-subsequence-using-dynamic-programming/)

**Java 代码:**

> 最长递增子序列(LIS)问题是求给定序列的最长子序列的长度，使子序列的所有元素按递增顺序排序。
> 
> 例如，{10，22，9，33，21，50，41，60，80}的 LIS 长度为 6，LIS 长度为{10，22，33，50，60，80}。

## C++

```
#include <bits/stdc++.h>
using namespace std;

void LIS(int a[], int n)
{
    vector<int> list;
    vector<int> longestlist;

    // Highest count
    int hc = 0;

    // Current max
    int cm;
    for(int i = 0; i < n; i++)
    {
        cm = INT_MIN;
        for(int j = i; j < n; j++)
        {
            if (a[j] > cm)
            {
                list.push_back(a[j]);
                cm = a[j];
            }
        }

        // Compare previous highest subsequence
        if (hc < list.size())
        {
            hc = list.size();
            for(int k = 0; k < list.size(); k++)
            {
                longestlist.push_back(list[k]);
            }
        }
        list.clear();
    }

    for(int i = 0; i < longestlist.size(); i++)
    {
        cout << longestlist[i] << ' ';
    }
    cout << endl;
    cout << "length of longestlist is " << hc;
}

// Driver code
int main()
{
    int a[] = { 10, 22, 9, 33, 21,
                50, 41, 60, 80 };
    int n = sizeof(a) / sizeof(a[0]);
    LIS(a, n);

    return 0;
}

// This code is contributed by Harshit Srivastava
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
package BIT;

import java.util.ArrayList;
import java.util.Iterator;

public class LongestIncreasingSubsequence {
    public static void main(String[] args) {
//        int array[] = {10, 22, 9, 33, 21, 50, 41, 60, 80};
//        int array[] = {10, 2, 9, 3, 5, 4, 6, 8};
        int array[] = {10, 9, 8, 6, 5, 4};
        ArrayList list = new ArrayList();
        ArrayList longestList = new ArrayList();
        int currentMax;
        int highestCount = 0;
        for(int i = 0; i < array.length;i++)
        {
            currentMax = Integer.MIN_VALUE;
            for(int j = i;j < array.length; j++)
            {
                if(array[j] > currentMax)
                {
                    list.add(array[j]);
                    currentMax = array[j];
                }
            }

            //Compare previous highest subsequence
            if(highestCount < list.size())
            {
                highestCount = list.size();
                longestList = new ArrayList(list); 
            }  
            list.clear();
        }
        System.out.println();

        //Print list
        Iterator itr = longestList.iterator();
        System.out.println("The Longest subsequence");
        while(itr.hasNext())
        {
            System.out.print(itr.next() + " ");
        }
        System.out.println();
        System.out.println("Length of LIS: " + highestCount);
    }

}
```

## C#

```
using System;
using System.Collections.Generic;

class longestIncreasingSubsequence
{
    public static void Main(String[] args)
    {
        int []array = {10, 22, 9, 33, 21, 50, 41, 60, 80};
        // int []array = {10, 2, 9, 3, 5, 4, 6, 8};
        //int []array = {10, 9, 8, 6, 5, 4};
        List<int> list = new List<int>();
        List<int> longestList = new List<int>();
        int currentMax;
        int highestCount = 0;
        for(int i = 0; i < array.Length;i++)
        {
            currentMax = int.MinValue;
            for(int j = i;j < array.Length; j++)
            {
                if(array[j] > currentMax)
                {
                    list.Add(array[j]);
                    currentMax = array[j];
                }
            }

            // Compare previous highest subsequence
            if(highestCount < list.Count)
            {
                highestCount = list.Count;
                longestList = new List<int>(list);
            }
            list.Clear();
        }
        Console.WriteLine();

        // Print list
        Console.WriteLine("The longest subsequence");
        foreach(int itr in longestList)
        {
            Console.Write(itr + " ");
        }
        Console.WriteLine();
        Console.WriteLine("Length of LIS: " + highestCount);
    }
}

// This code is contributed by 29AjayKumar
```

最长递增子序列(LIS)问题是求给定序列的最长子序列的长度，使子序列的所有元素按递增顺序排序。

示例:

```
Input:  [10, 22, 9, 33, 21, 50, 41, 60, 80]
Output: [10, 22, 33, 50, 60, 80] 
OR [10 22 33 41 60 80] or any other LIS of same length.
```

在[之前的](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)帖子中，我们讨论了最长递增子序列问题。然而，这篇文章只涵盖了与 LIS 查询规模相关的代码，而没有涉及 LIS 的构建。在这篇文章中，我们将讨论如何使用前面讨论的类似 DP 解决方案打印 LIS。
让 arr[0..n-1]是输入数组。我们定义向量 L，使得 L[i]本身是一个存储以 arr[i]结束的 arr 列表的向量。例如，对于数组[3，2，6，4，5，1]，

```
L[0]: 3
L[1]: 2
L[2]: 2 6
L[3]: 2 4
L[4]: 2 4 5
L[5]: 1
```

因此，对于索引 I，L[i]可以递归地写成–

```
L[0] = {arr[O]}
L[i] = {Max(L[j])} + arr[i] 
where j < i and arr[j] < arr[i] and if there is no such j then L[i] = arr[i]
```

以下是上述想法的实现–

## C++

```
/* Dynamic Programming solution to construct Longest
   Increasing Subsequence */
#include <iostream>
#include <vector>
using namespace std;

// Utility function to print LIS
void printLIS(vector<int>& arr)
{
    for (int x : arr)
        cout << x << " ";
    cout << endl;
}

// Function to construct and print Longest Increasing
// Subsequence
void constructPrintLIS(int arr[], int n)
{
    // L[i] - The longest increasing sub-sequence
    // ends with arr[i]
    vector<vector<int> > L(n);

    // L[0] is equal to arr[0]
    L[0].push_back(arr[0]);

    // start from index 1
    for (int i = 1; i < n; i++)
    {
        // do for every j less than i
        for (int j = 0; j < i; j++)
        {
            /* L[i] = {Max(L[j])} + arr[i]
            where j < i and arr[j] < arr[i] */
            if ((arr[i] > arr[j]) &&
                    (L[i].size() < L[j].size() + 1))
                L[i] = L[j];
        }

        // L[i] ends with arr[i]
        L[i].push_back(arr[i]);
    }

    // L[i] now stores increasing sub-sequence of
    // arr[0..i] that ends with arr[i]
    vector<int> max = L[0];

    // LIS will be max of all increasing sub-
    // sequences of arr
    for (vector<int> x : L)
        if (x.size() > max.size())
            max = x;

    // max will contain LIS
    printLIS(max);
}

// Driver function
int main()
{
    int arr[] = { 3, 2, 6, 4, 5, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // construct and print LIS of arr
    constructPrintLIS(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach

// Dynamic Programming
// solution to conLongest
// Increasing Subsequence
import java.util.*;
class GFG{

// Utility function to print LIS
static void printLIS(Vector<Integer> arr)
{
  for (int x : arr)
    System.out.print(x + " ");
  System.out.println();
}

// Function to conand print
// Longest Increasing Subsequence
static void constructPrintLIS(int arr[],
                              int n)
{
  // L[i] - The longest increasing
  // sub-sequence ends with arr[i]
  Vector<Integer> L[] = new Vector[n];
  for (int i = 0; i < L.length; i++)
    L[i] = new Vector<Integer>();

  // L[0] is equal to arr[0]
  L[0].add(arr[0]);

  // Start from index 1
  for (int i = 1; i < n; i++)
  {
    // Do for every j less than i
    for (int j = 0; j < i; j++)
    {
      //L[i] = {Max(L[j])} + arr[i]
      // where j < i and arr[j] < arr[i]
      if ((arr[i] > arr[j]) &&
          (L[i].size() < L[j].size() + 1))
        L[i] = (Vector<Integer>) L[j].clone();  //deep copy
    }

    // L[i] ends with arr[i]
    L[i].add(arr[i]);
  }

  // L[i] now stores increasing sub-sequence of
  // arr[0..i] that ends with arr[i]
  Vector<Integer> max = L[0];

  // LIS will be max of all increasing sub-
  // sequences of arr
  for (Vector<Integer> x : L)
    if (x.size() > max.size())
      max = x;

  // max will contain LIS
  printLIS(max);
}

// Driver function
public static void main(String[] args)
{
  int arr[] = {3, 2, 4, 5, 1};
  int n = arr.length;

  // print LIS of arr
  constructPrintLIS(arr, n);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Dynamic Programming solution to construct Longest
# Increasing Subsequence

# Utility function to print LIS
def printLIS(arr: list):
    for x in arr:
        print(x, end=" ")
    print()

# Function to construct and print Longest Increasing
# Subsequence
def constructPrintLIS(arr: list, n: int):

    # L[i] - The longest increasing sub-sequence
    # ends with arr[i]
    l = [[] for i in range(n)]

    # L[0] is equal to arr[0]
    l[0].append(arr[0])

    # start from index 1
    for i in range(1, n):

        # do for every j less than i
        for j in range(i):

            # L[i] = {Max(L[j])} + arr[i]
            # where j < i and arr[j] < arr[i]
            if arr[i] > arr[j] and (len(l[i]) < len(l[j]) + 1):
                l[i] = l[j].copy()

        # L[i] ends with arr[i]
        l[i].append(arr[i])

    # L[i] now stores increasing sub-sequence of
    # arr[0..i] that ends with arr[i]
    maxx = l[0]

    # LIS will be max of all increasing sub-
    # sequences of arr
    for x in l:
        if len(x) > len(maxx):
            maxx = x

    # max will contain LIS
    printLIS(maxx)

# Driver Code
if __name__ == "__main__":

    arr = [3, 2, 6, 4, 5, 1]
    n = len(arr)

    # construct and print LIS of arr
    constructPrintLIS(arr, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// Dynamic Programming solution to construct Longest
// Increasing Subsequence
using System;
using System.Collections.Generic;
class GFG
{

    // Utility function to print LIS
    static void printLIS(List<int> arr)
    {
        foreach(int x in arr)
        {
            Console.Write(x + " ");
        }
        Console.WriteLine();
    }

    // Function to construct and print Longest Increasing
    // Subsequence
    static void constructPrintLIS(int[] arr, int n)
    {

        // L[i] - The longest increasing sub-sequence
        // ends with arr[i]
        List<List<int>> L = new List<List<int>>();
        for(int i = 0; i < n; i++)
        {
            L.Add(new List<int>());
        }

        // L[0] is equal to arr[0]
        L[0].Add(arr[0]);

        // start from index 1
        for (int i = 1; i < n; i++)
        {
            // do for every j less than i
            for (int j = 0; j < i; j++)
            {
                /* L[i] = {Max(L[j])} + arr[i]
                where j < i and arr[j] < arr[i] */
                if ((arr[i] > arr[j]) && (L[i].Count < L[j].Count + 1))
                    L[i] = L[j];
            }

            // L[i] ends with arr[i]
            L[i].Add(arr[i]);
        }

        // L[i] now stores increasing sub-sequence of
        // arr[0..i] that ends with arr[i]
        List<int> max = L[0];

        // LIS will be max of all increasing sub-
        // sequences of arr
        foreach(List<int> x in L)
        {
            if (x.Count > max.Count)
            {
                max = x;
            }
        }

        // max will contain LIS
        printLIS(max);
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 3, 2, 4, 5, 1 };
    int n = arr.Length;

    // construct and print LIS of arr
    constructPrintLIS(arr, n);
  }
}

// This code is contributed by divyesh072019
```

输出:

```
2 4 5
```

注意，上述动态规划(DP)解决方案的时间复杂度是 O(n^2 ),并且对于 LIS 问题存在 O(n Log n)非 DP 解决方案。关于 O(n Log n)解决方案，请参见下面的帖子。

[构造最长单调递增子序列(N ^ log N)](https://www.geeksforgeeks.org/construction-of-longest-monotonically-increasing-subsequence-n-log-n/)

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。