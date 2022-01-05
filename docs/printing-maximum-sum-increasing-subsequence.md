# 打印最大和增加子序列

> 原文:[https://www . geesforgeks . org/printing-maximum-sum-递增-subsequence/](https://www.geeksforgeeks.org/printing-maximum-sum-increasing-subsequence/)

最大和递增子序列问题是求给定序列的最大和子序列，使得子序列的所有元素按递增顺序排序。

**示例:**

```
Input:  [1, 101, 2, 3, 100, 4, 5]
Output: [1, 2, 3, 100]

Input:  [3, 4, 5, 10]
Output: [3, 4, 5, 10]

Input:  [10, 5, 4, 3]
Output: [10]

Input:  [3, 2, 6, 4, 5, 1]
Output: [3, 4, 5]
```

在[之前的](https://www.geeksforgeeks.org/dynamic-programming-set-14-maximum-sum-increasing-subsequence/)帖子中，我们已经讨论了最大和增子序列问题。然而，这篇文章只涵盖了与求增子序列的最大和有关的代码，而没有涉及子序列的构造。在这篇文章中，我们将讨论如何构造最大和增子序列本身。

让 arr[0..n-1]是输入数组。我们定义向量 L，使得 L[i]本身是存储 arr[0]的最大和增子序列的向量..那以逮捕结束。因此，对于索引 I，L[i]可以递归地写成

```
L[0] = {arr[0]}
L[i] = {MaxSum(L[j])} + arr[i] where j < i and arr[j] < arr[i]
     = arr[i], if there is no j such that arr[j] < arr[i]
```

例如，对于数组[3，2，6，4，5，1]，

```
L[0]: 3
L[1]: 2
L[2]: 3 6
L[3]: 3 4
L[4]: 3 4 5
L[5]: 1
```

以下是上述想法的实现–

## C++

```
/* Dynamic Programming solution to construct
   Maximum Sum Increasing Subsequence */
#include <iostream>
#include <vector>
using namespace std;

// Utility function to calculate sum of all
// vector elements
int findSum(vector<int> arr)
{
    int sum = 0;
    for (int i : arr)
        sum += i;
    return sum;
}

// Function to construct Maximum Sum Increasing
// Subsequence
void printMaxSumIS(int arr[], int n)
{
    // L[i] - The Maximum Sum Increasing
    // Subsequence that ends with arr[i]
    vector<vector<int> > L(n);

    // L[0] is equal to arr[0]
    L[0].push_back(arr[0]);

    // start from index 1
    for (int i = 1; i < n; i++) {
        // for every j less than i
        for (int j = 0; j < i; j++) {
            /* L[i] = {MaxSum(L[j])} + arr[i]
            where j < i and arr[j] < arr[i] */
            if ((arr[i] > arr[j])
                && (findSum(L[i]) < findSum(L[j])))
                L[i] = L[j];
        }

        // L[i] ends with arr[i]
        L[i].push_back(arr[i]);

        // L[i] now stores Maximum Sum Increasing
        // Subsequence of arr[0..i] that ends with
        // arr[i]
    }

    vector<int> res = L[0];

    // find max
    for (vector<int> x : L)
        if (findSum(x) > findSum(res))
            res = x;

    // max will contain result
    for (int i : res)
        cout << i << " ";
    cout << endl;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 6, 4, 5, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // construct and print Max Sum IS of arr
    printMaxSumIS(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic Programming solution to construct
Maximum Sum Increasing Subsequence */
import java.util.*;

class GFG {

    // Utility function to calculate sum of all
    // vector elements
    static int findSum(Vector<Integer> arr)
    {
        int sum = 0;
        for (int i : arr)
            sum += i;
        return sum;
    }

    // Function to construct Maximum Sum Increasing
    // Subsequence
    static void printMaxSumIs(int[] arr, int n)
    {

        // L[i] - The Maximum Sum Increasing
        // Subsequence that ends with arr[i]
        @SuppressWarnings("unchecked")
        Vector<Integer>[] L = new Vector[n];

        for (int i = 0; i < n; i++)
            L[i] = new Vector<>();

        // L[0] is equal to arr[0]
        L[0].add(arr[0]);

        // start from index 1
        for (int i = 1; i < n; i++) {

            // for every j less than i
            for (int j = 0; j < i; j++) {

                /*
                * L[i] = {MaxSum(L[j])} + arr[i]
                  where j < i and arr[j] < arr[i]
                */
                if ((arr[i] > arr[j])
                    && (findSum(L[i]) < findSum(L[j]))) {
                    for (int k : L[j])
                        if (!L[i].contains(k))
                            L[i].add(k);
                }
            }

            // L[i] ends with arr[i]
            L[i].add(arr[i]);

            // L[i] now stores Maximum Sum Increasing
            // Subsequence of arr[0..i] that ends with
            // arr[i]
        }

        Vector<Integer> res = new Vector<>(L[0]);
        // res = L[0];

        // find max
        for (Vector<Integer> x : L)
            if (findSum(x) > findSum(res))
                res = x;

        // max will contain result
        for (int i : res)
            System.out.print(i + " ");
        System.out.println();
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 3, 2, 6, 4, 5, 1 };
        int n = arr.length;

        // construct and print Max Sum IS of arr
        printMaxSumIs(arr, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Dynamic Programming solution to construct
# Maximum Sum Increasing Subsequence */

# Utility function to calculate sum of all
# vector elements

def findSum(arr):

    summ = 0
    for i in arr:
        summ += i
    return summ

# Function to construct Maximum Sum Increasing
# Subsequence

def printMaxSumIS(arr, n):

    # L[i] - The Maximum Sum Increasing
    # Subsequence that ends with arr[i]
    L = [[] for i in range(n)]

    # L[0] is equal to arr[0]
    L[0].append(arr[0])

    # start from index 1
    for i in range(1, n):

        # for every j less than i
        for j in range(i):

            # L[i] = {MaxSum(L[j])} + arr[i]
            # where j < i and arr[j] < arr[i]
            if ((arr[i] > arr[j]) and
                    (findSum(L[i]) < findSum(L[j]))):
                for e in L[j]:
                    if e not in L[i]:
                        L[i].append(e)

        # L[i] ends with arr[i]
        L[i].append(arr[i])

        # L[i] now stores Maximum Sum Increasing
        # Subsequence of arr[0..i] that ends with
        # arr[i]

    res = L[0]

    # find max
    for x in L:
        if (findSum(x) > findSum(res)):
            res = x

    # max will contain result
    for i in res:
        print(i, end=" ")

# Driver Code
arr = [3, 2, 6, 4, 5, 1]
n = len(arr)

# construct and prMax Sum IS of arr
printMaxSumIS(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
/* Dynamic Programming solution to construct
Maximum Sum Increasing Subsequence */
using System;
using System.Collections.Generic;

class GFG {

    // Utility function to calculate sum of all
    // vector elements
    static int findSum(List<int> arr)
    {
        int sum = 0;
        foreach(int i in arr) sum += i;
        return sum;
    }

    // Function to construct Maximum Sum Increasing
    // Subsequence
    static void printMaxSumIs(int[] arr, int n)
    {

        // L[i] - The Maximum Sum Increasing
        // Subsequence that ends with arr[i]
        List<int>[] L = new List<int>[ n ];

        for (int i = 0; i < n; i++)
            L[i] = new List<int>();

        // L[0] is equal to arr[0]
        L[0].Add(arr[0]);

        // start from index 1
        for (int i = 1; i < n; i++) {

            // for every j less than i
            for (int j = 0; j < i; j++) {

                /*
                * L[i] = {MaxSum(L[j])} + arr[i]
                where j < i and arr[j] < arr[i]
                */
                if ((arr[i] > arr[j])
                    && (findSum(L[i]) < findSum(L[j]))) {
                    foreach(int k in
                                L[j]) if (!L[i].Contains(k))
                        L[i]
                            .Add(k);
                }
            }

            // L[i] ends with arr[i]
            L[i].Add(arr[i]);

            // L[i] now stores Maximum Sum Increasing
            // Subsequence of arr[0..i] that ends with
            // arr[i]
        }

        List<int> res = new List<int>(L[0]);
        // res = L[0];

        // find max
        foreach(List<int> x in L) if (findSum(x)
                                      > findSum(res)) res
            = x;

        // max will contain result
        foreach(int i in res) Console.Write(i + " ");
        Console.WriteLine();
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 2, 6, 4, 5, 1 };
        int n = arr.Length;

        // construct and print Max Sum IS of arr
        printMaxSumIs(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

/* Dynamic Programming solution to construct
Maximum Sum Increasing Subsequence */

    // Utility function to calculate sum of all
    // vector elements
    function findSum(arr)
    {
        let sum = 0;
        for (let i=0;i<arr.length;i++)
            sum += arr[i];
        return sum;
    }

    // Function to construct Maximum Sum Increasing
    // Subsequence
    function printMaxSumIs(arr,n)
    {
        // L[i] - The Maximum Sum Increasing
        // Subsequence that ends with arr[i]

        let L = new Array(n);

        for (let i = 0; i < n; i++)
            L[i] = [];

        // L[0] is equal to arr[0]
        L[0].push(arr[0]);

        // start from index 1
        for (let i = 1; i < n; i++) {

            // for every j less than i
            for (let j = 0; j < i; j++) {

                /*
                * L[i] = {MaxSum(L[j])} + arr[i]
                  where j < i and arr[j] < arr[i]
                */
                if ((arr[i] > arr[j])
                    && (findSum(L[i]) < findSum(L[j])))
                    {
                    for (let k=0;k<L[j].length;k++)
                        if (!L[i].includes(L[j][k]))
                            L[i].push(L[j][k]);
                }
            }

            // L[i] ends with arr[i]
            L[i].push(arr[i]);

            // L[i] now stores Maximum Sum Increasing
            // Subsequence of arr[0..i] that ends with
            // arr[i]
        }

        let res = L[0];
        // res = L[0];

        // find max
        for (let x=0;x<L.length;x++)
            if (findSum(L[x]) > findSum(res))
                res = L[x];

        // max will contain result
        for (let i=0;i<res.length;i++)
            document.write(res[i] + " ");
        document.write("<br>");
    }

     // Driver Code
    let arr=[3, 2, 6, 4, 5, 1];
    let n = arr.length;

    // construct and print Max Sum IS of arr
    printMaxSumIs(arr, n);

// This code is contributed by unknown2108

</script>
```

**Output**

```
3 4 5
```

我们可以通过移除 findSum()函数来优化上面的 DP 解决方案。相反，我们可以维护另一个向量/数组来存储以 arr[i]结束的最大和递增子序列的和。实现可以在这里看到。

以上动态规划解的**时间复杂度**为 O(n <sup>2</sup> )。
**程序使用的辅助空间**为 O(n <sup>2</sup> )。

**方法 2: (** 使用使用 O(N)空间的动态规划

上述方法涵盖了如何在 O(N <sup>2</sup> )时间和 O(N <sup>2</sup> 空间中构造最大和增子序列。在这种方法中，我们将优化空间复杂度，并在 O(N)<sup>2</sup>时间和 O(N)空间中构造最大和增子序列。

*   让 arr[0..n-1]是输入数组。
*   我们定义一个向量对 L，使得 L[i]首先存储 arr[0]的最大和增加子序列..以逮捕和拘留结束。第二个存储用于生成总和的前一个元素的索引。
*   由于第一个元素没有任何前一个元素，因此它的索引应该是 L[0]中的-1。

例如，

```
array = [3, 2, 6, 4, 5, 1]

L[0]: {3, -1}
L[1]: {2,  1}
L[2]: {9,  0}
L[3]: {7, 0}
L[4]: {12, 3}
L[5]: {1, 5}
```

如上所述，最大和递增子序列的值是 12。为了构建实际的子序列，我们将使用存储在 L[i]中的索引。其次，构建子序列的步骤如下所示:

*   在向量结果中，存储找到最大和递增子序列的元素的值(即 currIndex = 4)。所以在结果向量中，我们将添加 arr[currIndex]。
*   将 currIndex 更新为 L[currIndex]。其次，重复步骤 1，直到 currIndex 不为-1 或不发生变化(即 currIndex = = previousIndex)。
*   以相反的顺序显示结果向量的元素。

下面是上述想法的实现:

## C++14

```
/* Dynamic Programming solution to construct
Maximum Sum Increasing Subsequence */
#include <bits/stdc++.h>
using namespace std;

// Function to construct and print the Maximum Sum
// Increasing Subsequence
void constructMaxSumIS(vector<int> arr, int n)
{
    // L[i] stores the value of Maximum Sum Increasing
    // Subsequence that ends with arr[i] and the index of
    // previous element used to construct the Subsequence
    vector<pair<int, int> > L(n);

    int index = 0;
    for (int i : arr) {
        L[index] = { i, index };
        index++;
    }

    // Set L[0].second equal to -1
    L[0].second = -1;

    // start from index 1
    for (int i = 1; i < n; i++) {
        // for every j less than i
        for (int j = 0; j < i; j++) {
            if (arr[i] > arr[j]
                and L[i].first < arr[i] + L[j].first) {
                L[i].first = arr[i] + L[j].first;
                L[i].second = j;
            }
        }
    }

    int maxi = INT_MIN, currIndex, track = 0;

    for (auto p : L) {
        if (p.first > maxi) {
            maxi = p.first;
            currIndex = track;
        }
        track++;
    }

    // Stores the final Subsequence
    vector<int> result;

    // Index of previous element
    // used to construct the Subsequence
    int prevoiusIndex;

    while (currIndex >= 0) {
        result.push_back(arr[currIndex]);
        prevoiusIndex = L[currIndex].second;

        if (currIndex == prevoiusIndex)
            break;

        currIndex = prevoiusIndex;
    }

    for (int i = result.size() - 1; i >= 0; i--)
        cout << result[i] << " ";
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 101, 2, 3, 100, 4, 5 };
    int n = arr.size();

    // Function call
    constructMaxSumIS(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Dynamic Programming solution to construct
// Maximum Sum Increasing Subsequence
import java.util.*;
import java.awt.Point;

class GFG{

// Function to construct and print the Maximum Sum
// Increasing Subsequence
static void constructMaxSumIS(List<Integer> arr, int n)
{

    // L.get(i) stores the value of Maximum Sum Increasing
    // Subsequence that ends with arr.get(i) and the index of
    // previous element used to construct the Subsequence
    List<Point> L = new ArrayList<Point>();

    int index = 0;
    for(int i : arr)
    {
        L.add(new Point(i, index));
        index++;
    }

    // Set L[0].second equal to -1
    L.set(0, new Point(L.get(0).x, -1));

    // Start from index 1
    for(int i = 1; i < n; i++)
    {

        // For every j less than i
        for(int j = 0; j < i; j++)
        {
            if (arr.get(i) > arr.get(j) &&
                L.get(i).x < arr.get(i) +
                L.get(j).x)
            {
                L.set(i, new Point(arr.get(i) +
                                     L.get(j).x, j));
            }
        }
    }

    int maxi = -100000000, currIndex = 0, track = 0;

    for(Point p : L)
    {
        if (p.x > maxi)
        {
            maxi = p.x;
            currIndex = track;
        }
        track++;
    }

    // Stores the final Subsequence
    List<Integer> result = new ArrayList<Integer>();

    // Index of previous element
    // used to construct the Subsequence
    int prevoiusIndex;

    while (currIndex >= 0)
    {
        result.add(arr.get(currIndex));
        prevoiusIndex = L.get(currIndex).y;

        if (currIndex == prevoiusIndex)
            break;

        currIndex = prevoiusIndex;
    }

    for(int i = result.size() - 1; i >= 0; i--)
        System.out.print(result.get(i) + " ");
}

// Driver Code
public static void main(String []s)
{
    List<Integer> arr = new ArrayList<Integer>();
    arr.add(1);
    arr.add(101);
    arr.add(2);
    arr.add(3);
    arr.add(100);
    arr.add(4);
    arr.add(5);

    int n = arr.size();

    // Function call
    constructMaxSumIS(arr, n);
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Dynamic Programming solution to construct
# Maximum Sum Increasing Subsequence
import sys

# Function to construct and print the Maximum Sum
# Increasing Subsequence
def constructMaxSumIS(arr, n) :

    # L[i] stores the value of Maximum Sum Increasing
    # Subsequence that ends with arr[i] and the index of
    # previous element used to construct the Subsequence
    L = []

    index = 0
    for i in arr :
        L.append([i, index])
        index += 1

    # Set L[0].second equal to -1
    L[0][1] = -1

    # start from index 1
    for i in range(1, n) :

        # for every j less than i
        for j in range(i) :
            if (arr[i] > arr[j] and L[i][0] < arr[i] + L[j][0]) :
                L[i][0] = arr[i] + L[j][0]
                L[i][1] = j

    maxi, currIndex, track = -sys.maxsize, 0, 0

    for p in L :
        if (p[0] > maxi) :
            maxi = p[0]
            currIndex = track

        track += 1

    # Stores the final Subsequence
    result = []

    while (currIndex >= 0) :
        result.append(arr[currIndex])
        prevoiusIndex = L[currIndex][1]

        if (currIndex == prevoiusIndex) :
            break

        currIndex = prevoiusIndex

    for i in range(len(result) - 1, -1, -1) :
        print(result[i] , end = " ")

arr = [ 1, 101, 2, 3, 100, 4, 5 ]
n = len(arr)

# Function call
constructMaxSumIS(arr, n)

# This code is contributed by divyeshrabadiya07
```

## C#

```
/* Dynamic Programming solution to construct
Maximum Sum Increasing Subsequence */
using System;
using System.Collections.Generic;
class GFG
{

    // Function to construct and print the Maximum Sum
    // Increasing Subsequence
    static void constructMaxSumIS(List<int> arr, int n)
    {

        // L[i] stores the value of Maximum Sum Increasing
        // Subsequence that ends with arr[i] and the index of
        // previous element used to construct the Subsequence
        List<Tuple<int, int>> L = new List<Tuple<int, int>>();

        int index = 0;
        foreach(int i in arr) {
            L.Add(new Tuple<int, int>(i, index));
            index++;
        }

        // Set L[0].second equal to -1
        L[0] = new Tuple<int, int>(L[0].Item1, -1);

        // start from index 1
        for (int i = 1; i < n; i++)
        {

            // for every j less than i
            for (int j = 0; j < i; j++)
            {
                if (arr[i] > arr[j] &&
                    L[i].Item1 < arr[i] +
                    L[j].Item1)
                {
                    L[i] = new Tuple<int,
                  int>(arr[i] + L[j].Item1, j);
                }
            }
        }

        int maxi = Int32.MinValue,
      currIndex = 0, track = 0;

        foreach(Tuple<int, int> p in L)
        {
            if (p.Item1 > maxi)
            {
                maxi = p.Item1;
                currIndex = track;
            }
            track++;
        }

        // Stores the final Subsequence
        List<int> result = new List<int>();

        // Index of previous element
        // used to construct the Subsequence
        int prevoiusIndex;

        while (currIndex >= 0)
        {
            result.Add(arr[currIndex]);
            prevoiusIndex = L[currIndex].Item2;

            if (currIndex == prevoiusIndex)
                break;

            currIndex = prevoiusIndex;
        }

        for (int i = result.Count - 1; i >= 0; i--)
            Console.Write(result[i] + " ");
    } 

  static void Main()
  {
    List<int> arr = new List<int>(new
                                  int[] { 1, 101, 2, 3, 100, 4, 5 });
    int n = arr.Count;

    // Function call
    constructMaxSumIS(arr, n);
  }
}

// This code is contributed by divyesh072019
```

**Output**

```
1 2 3 100
```

**时间复杂度:**O(N<sup>2</sup>)
T5】空间复杂度: O(N)

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。