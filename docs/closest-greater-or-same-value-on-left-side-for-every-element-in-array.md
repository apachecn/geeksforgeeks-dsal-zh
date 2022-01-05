# 数组中每个元素左侧最接近的较大或相同的值

> 原文:[https://www . geeksforgeeks . org/数组中每个元素的左侧最接近-更大或相同值/](https://www.geeksforgeeks.org/closest-greater-or-same-value-on-left-side-for-every-element-in-array/)

给定一个整数数组，在每个元素的左边找到最接近的(不考虑距离，而是值)大于或等于相同的值。如果元素在左侧没有大于或等于的值，则打印-1。

**示例:**

> 输入:arr[] = {10，5，11，6，20，12}
> 输出:-1，10，-1，10，-1，20
> 第一个元素左边什么都没有，所以第一个的答案是-1。
> 其次，元素 5 左边有 10，所以答案是 10。
> 第三个元素 11 没有更大或相同的东西，所以答案是-1。
> 第四个元素 6 的值为 10，所以答案是 10
> 同样，我们得到第五个和第六个元素的值。

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每一个拾取的元素，我们都向它的左边遍历，并找到最近的(按值)较大的元素。这个解的时间复杂度是 O(n*n)

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function for ceiling in left side for every element in an
// array
void printPrevGreater(int arr[], int n)
{
    cout << "-1"
         << " "; // for first element
    for (int i = 1; i < n; i++) {
        int diff = INT_MAX;
        for (int j = 0; j < i;
             j++) // traverse left side to i-th element
        {
            if (arr[j] >= arr[i])
                diff = min(diff, arr[j] - arr[i]);
        }
        if (diff == INT_MAX)
            cout << "-1"
                 << " "; // if not found at left side
        else
            cout << arr[i] + diff << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 10, 5, 11, 10, 20, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printPrevGreater(arr, n);
    return 0;
}

// This code is contributed by
// @itsrahulhere_
```

**输出:**

```
-1 10 -1 10 -1 20
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(1)

一个**有效的解决方案**是使用自平衡 BST(在 C++中实现为 set，在 Java 中实现为 TreeSet)。在自平衡 BST 中，我们可以在 O(Log n)时间内完成插入和最近的更大操作。
我们使用 C++ 中的[下界()来寻找最近的更大元素。这个函数在一个集合的 Log n 时间内工作。](https://www.geeksforgeeks.org/lower_bound-in-cpp/)

## C++

```
// C++ implementation of efficient algorithm to find
// greater or same element on left side
#include <iostream>
#include <set>
using namespace std;

// Prints greater elements on left side of every element
void printPrevGreater(int arr[], int n)
{
    set<int> s;
    for (int i = 0; i < n; i++) {

        // First search in set
        auto it = s.lower_bound(arr[i]);
        if (it == s.end()) // If no greater found
            cout << "-1"
                 << " ";
        else
            cout << *it << " ";

        // Then insert
        s.insert(arr[i]);
    }
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = { 10, 5, 11, 10, 20, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printPrevGreater(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of efficient algorithm
// to find greater or same element on left side
import java.util.TreeSet;

class GFG {

    // Prints greater elements on left side
    // of every element
    static void printPrevGreater(int[] arr, int n)
    {
        TreeSet<Integer> ts = new TreeSet<>();
        for (int i = 0; i < n; i++) {
            Integer c = ts.ceiling(arr[i]);
            if (c == null) // If no greater found
                System.out.print(-1 + " ");
            else
                System.out.print(c + " ");

            // Then insert
            ts.add(arr[i]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 10, 5, 11, 10, 20, 12 };
        int n = arr.length;
        printPrevGreater(arr, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of efficient algorithm
# to find greater or same element on left side

# Prints greater elements
# on left side of every element
def printPrevGreater(arr, n):

    s = set()
    for i in range(0, n):

        # First search in set
        it = [x for x in s if x >= arr[i]]
        if len(it) == 0: # If no greater found
            print("-1", end = " ")
        else:                
            print(min(it), end = " ")        

        # Then insert
        s.add(arr[i])

# Driver Code
if __name__ == "__main__":

    arr = [10, 5, 11, 10, 20, 12]
    n = len(arr)
    printPrevGreater(arr, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of efficient algorithm
// to find greater or same element on left side
using System;
using System.Collections.Generic;

class GFG {

    // To get the minimum value
    static int minimum(SortedSet<int> ss)
    {
        int min = int.MaxValue;

        foreach(int i in ss) if (i < min)
            min = i;

        return min;
    }

    // Prints greater elements on left side
    // of every element
    static void printPrevGreater(int[] arr, int n)
    {
        SortedSet<int> s = new SortedSet<int>();

        for (int i = 0; i < n; i++) {
            SortedSet<int> ss = new SortedSet<int>();

            // First search in set
            foreach(int x in s) if (x >= arr[i])
                ss.Add(x);

            if (ss.Count == 0) // If no greater found
                Console.Write(-1 + " ");
            else
                Console.Write(minimum(ss) + " ");

            // Then insert
            s.Add(arr[i]);
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 10, 5, 11, 10, 20, 12 };
        int n = arr.Length;
        printPrevGreater(arr, n);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of efficient algorithm to find
// greater or same element on left side

// To get the minimum value
function minimum(ss)
{
    var min = 1000000000;
    ss.forEach(i => {
        if (i < min)
            min = i;
    });
    return min;
}
// Prints greater elements on left side of every element
function printPrevGreater(arr, n)
{
    var s = new Set();
    for (var i = 0; i < n; i++) {

        var ss = new Set();

         // First search in set
         s.forEach(x => {
                if(x >= arr[i])
                    ss.add(x);
         });

            if (ss.size == 0) // If no greater found
                document.write(-1 + " ");
            else
                document.write(minimum(ss) + " ");

        // Then insert
        s.add(arr[i]);
    }
}

/* Driver program to test insertion sort */
var arr = [10, 5, 11, 10, 20, 12];
var n = arr.length;
printPrevGreater(arr, n);

</script>
```

**Output:** 

```
-1 10 -1 10 -1 20
```

**时间复杂度:** O(n Log n)

**辅助空间:** O(n)