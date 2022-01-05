# 在双音素序列中插入元素的查询

> 原文:[https://www . geeksforgeeks . org/bitonic 序列中插入元素时的查询/](https://www.geeksforgeeks.org/queries-on-insertion-of-an-element-in-a-bitonic-sequence/)

给定一个[双音素序列](https://www.geeksforgeeks.org/find-bitonic-point-given-bitonic-sequence/)**和**【Q】**的查询数量。每个查询包含一个整数 **x <sub>i</sub>** ，1 < = i < = Q，任务是在为每个查询插入整数后打印出二进制序列的长度。此外，在所有查询后打印双音素序列。
**举例:**** 

> ****输入:** S = { 1，2，5，2 }，Q = 4，x = { 5，1，3，2 }
> **输出:**
> 4
> 5
> 6
> 6
> 双音素序列:1 2 3 5 2
> 1**解释:**** 
> 
> *   **对于第一个查询，我们需要插入 x <sub>1</sub> = 5，但是由于 5 是最大元素，并且 S 中最大元素只能出现一次，因此我们不会在 S 中插入 5。因此，size = 4。**
> *   **对于第二个查询，我们需要插入 x <sub>2</sub> = 1，所以我们将其插入递减部分，因为递增部分已经有 1 了。因此，大小= 5。**
> *   **对于第三个查询，我们在递增边插入 x <sub>3</sub> = 3，因此大小变为 6。**
> *   **对于第四个查询，我们不能插入 x <sub>2</sub> = 2，因为 2 同时在递增和递减侧。**
> 
> ****输入:** S = { 1，2，5，2 }，Q = 4，x = { 5，6，4，4 }
> T3】输出:T5】4
> 5
> 6
> 7
> 双音素序列:1 2 4 5 6 4 2**

****做法:**思路是做两套，一套增序，一套减序。** 

1.  **现在，对于每个查询，首先检查 x <sub>i</sub> 是否大于双音素序列中的最大元素。**
2.  **如果是，更新最大序列，并将该元素包括在递增序列的集合中。**
3.  **如果否，则检查该元素是否存在于递增序列集中，如果不包含在递增序列集中，则将其包含在递减序列集中。**

****以下是本办法的实施:**** 

## **C++**

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the bitonic sequence
void solveQuery(int a[], int n, int x[], int q)
{
    int maxx = INT_MIN;

    // Finding the maximum element
    for (int i = 0; i < n; i++)
        maxx = max(maxx, a[i]);

    set<int> s1, s2;

    s1.insert(a[0]);
    s2.insert(a[n - 1]);

    // set to include increasing sequence element
    for (int i = 1; i < n; i++)
        if (a[i] > a[i - 1])
            s1.insert(a[i]);

    // set to include decreasing sequence element
    for (int i = n - 2; i >= 0; i--)
        if (a[i] > a[i + 1])
            s2.insert(a[i]);

    // removing maximum element from
    // decreasing sequence set
    s2.erase(s2.find(maxx));

    // for each query
    for (int i = 0; i < q; i++) {

        // checking if x is greater than
        // maximum element or not.
        if (maxx <= x[i]) {
            maxx = x[i];
            s1.insert(x[i]);
        }

        else {

            // checking if x lie in increasing sequence
            if (s1.find(x[i]) == s1.end())
                s1.insert(x[i]);

            // else insert into decreasing sequence set
            else
                s2.insert(x[i]);
        }

        // finding the length
        int ans = s1.size() + s2.size();
        cout << ans << "\n";
    }

    // printing the sequence
    set<int>::iterator it;
    for (it = s1.begin(); it != s1.end(); it++)
        cout << (*it) << " ";

    set<int>::reverse_iterator rit;

    for (rit = s2.rbegin(); rit != s2.rend(); rit++)
        cout << (*rit) << " ";
}

// Driver code
int main()
{
    int a[] = { 1, 2, 5, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    int x[] = { 5, 1, 3, 2 };
    int q = sizeof(x) / sizeof(x[0]);

    solveQuery(a, n, x, q);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of above approach
import java.util.*;

class GFG
{

// Function to find the bitonic sequence
static void solveQuery(int a[], int n, int x[], int q)
{
    int maxx = Integer.MIN_VALUE;

    // Finding the maximum element
    for (int i = 0; i < n; i++)
        maxx = Math.max(maxx, a[i]);

    Set<Integer> s1 = new HashSet<>(), s2 = new HashSet<>();

    s1.add(a[0]);
    s2.add(a[n - 1]);

    // set to include increasing sequence element
    for (int i = 1; i < n; i++)
        if (a[i] > a[i - 1])
            s1.add(a[i]);

    // set to include decreasing sequence element
    for (int i = n - 2; i >= 0; i--)
        if (a[i] > a[i + 1])
            s2.add(a[i]);

    // removing maximum element from
    // decreasing sequence set
    s2.remove(maxx);

    // for each query
    for (int i = 0; i < q; i++)
    {

        // checking if x is greater than
        // maximum element or not.
        if (maxx <= x[i])
        {
            maxx = x[i];
            s1.add(x[i]);
        }

        else
        {

            // checking if x lie in increasing sequence
            if (!s1.contains(x[i]))
                s1.add(x[i]);

            // else insert into decreasing sequence set
            else
                s2.add(x[i]);
        }

        // finding the length
        int ans = s1.size() + s2.size();
        System.out.print(ans + "\n");
    }

    // printing the sequence
    for (Integer it : s1)
        System.out.print((it) + " ");

    for (Integer it : s2)
        System.out.print((it) + " ");
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 5, 2 };
    int n = a.length;
    int x[] = { 5, 1, 3, 2 };
    int q = x.length;

    solveQuery(a, n, x, q);
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 implementation of above approach
import sys

# Function to find the bitonic sequence
def solveQuery(a, n, x, q):
    maxx = -sys.maxsize

    # Finding the maximum element
    for i in range(n):
        maxx = max(maxx, a[i])

    s1, s2 = set(), set()

    s1.add(a[0])
    s2.add(a[n - 1])

    # set to include increasing sequence element
    for i in range(1, n):
        if a[i] > a[i - 1]:
            s1.add(a[i])

    # set to include decreasing sequence element
    for i in range(n - 2, -1, -1):
        if a[i] > a[i + 1]:
            s2.add(a[i])

    # removing maximum element from
    # decreasing sequence set
    s2.remove(maxx)

    # for each query
    for i in range(q):

        # checking if x is greater than
        # maximum element or not.
        if maxx <= x[i]:
            maxx = x[i]
            s1.add(x[i])
        else:

            # checking if x lie in increasing sequence
            if x[i] not in s1:
                s1.add(x[i])

            # else insert into decreasing sequence set
            else:
                s2.add(x[i])

        # finding the length
        ans = len(s1) + len(s2)
        print(ans)

    # printing the sequence
    for i in s1:
        print(i, end = " ")

    for i in reversed(list(s2)):
        print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    a = [1, 2, 5, 2]
    n = len(a)
    x = [5, 1, 3, 2]
    q = len(x)

    solveQuery(a, n, x, q)

# This code is contributed by
# sanjeev2552
```

## **C#**

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the bitonic sequence
static void solveQuery(int []a, int n, int []x, int q)
{
    int maxx = int.MinValue;

    // Finding the maximum element
    for (int i = 0; i < n; i++)
        maxx = Math.Max(maxx, a[i]);

    HashSet<int> s1 = new HashSet<int>(), s2 = new HashSet<int>();

    s1.Add(a[0]);
    s2.Add(a[n - 1]);

    // set to include increasing sequence element
    for (int i = 1; i < n; i++)
        if (a[i] > a[i - 1])
            s1.Add(a[i]);

    // set to include decreasing sequence element
    for (int i = n - 2; i >= 0; i--)
        if (a[i] > a[i + 1])
            s2.Add(a[i]);

    // removing maximum element from
    // decreasing sequence set
    s2.Remove(maxx);

    // for each query
    for (int i = 0; i < q; i++)
    {

        // checking if x is greater than
        // maximum element or not.
        if (maxx <= x[i])
        {
            maxx = x[i];
            s1.Add(x[i]);
        }

        else
        {

            // checking if x lie in increasing sequence
            if (!s1.Contains(x[i]))
                s1.Add(x[i]);

            // else insert into decreasing sequence set
            else
                s2.Add(x[i]);
        }

        // finding the length
        int ans = s1.Count + s2.Count;
        Console.Write(ans + "\n");
    }

    // printing the sequence
    foreach (int it in s1)
        Console.Write((it) + " ");

    foreach (int it in s2)
        Console.Write((it) + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 2, 5, 2 };
    int n = a.Length;
    int []x = { 5, 1, 3, 2 };
    int q = x.Length;

    solveQuery(a, n, x, q);
}
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>
    // Javascript implementation of above approach

    // Function to find the bitonic sequence
    function solveQuery(a, n, x, q)
    {
        let maxx = Number.MIN_VALUE;

        // Finding the maximum element
        for (let i = 0; i < n; i++)
            maxx = Math.max(maxx, a[i]);

        let s1 = new Set();
        let s2 = new Set();

        s1.add(a[0]);
        s2.add(a[n - 1]);

        // set to include increasing sequence element
        for (let i = 1; i < n; i++)
            if (a[i] > a[i - 1])
                s1.add(a[i]);

        // set to include decreasing sequence element
        for (let i = n - 2; i >= 0; i--)
            if (a[i] > a[i + 1])
                s2.add(a[i]);

        // removing maximum element from
        // decreasing sequence set
        s2.delete(maxx);

        // for each query
        for (let i = 0; i < q; i++)
        {

            // checking if x is greater than
            // maximum element or not.
            if (maxx <= x[i])
            {
                maxx = x[i];
                s1.add(x[i]);
            }

            else
            {

                // checking if x lie in increasing sequence
                if (!s1.has(x[i]))
                    s1.add(x[i]);

                // else insert into decreasing sequence set
                else
                    s2.add(x[i]);
            }

            // finding the length
            let ans = s1.size + s2.size;
            document.write(ans + "</br>");
        }

        let S1 = Array.from(s1);
        S1.sort(function(a, b){return a - b});

        // printing the sequence
        S1.forEach (function(it) {
          document.write(it + " ");
        })
        s2.forEach (function(it) {
          document.write(it + " ");
        })
    }

    let a = [ 1, 2, 5, 2 ];
    let n = a.length;
    let x = [ 5, 1, 3, 2 ];
    let q = x.length;

    solveQuery(a, n, x, q);

// This code is contributed by decode2207.
</script>
```

****Output:** 

```
4
5
6
6
1 2 3 5 2 1
```**