# 从除数中找出数

> 原文:[https://www . geesforgeks . org/find-number-from-its-dividers/](https://www.geeksforgeeks.org/find-number-from-its-divisors/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。整数表示一个数 **X** 除了 **1** 和 **X** 本身之外的所有除数。任务是找到编号 **X** 。如果没有这样的元素，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {2，10，5，4}
> **输出:** 20
> 
> **输入:** arr[] = {2，10，5 }
> T3】输出: 20
> 
> **输入:** arr[] = {2，15}
> **输出:** -1

**方法:**对给定的 **N** 除数进行排序，编号 **X** 将是排序数组中的**第一个编号*最后一个编号**。通过将除 **1** 和 **X** 之外的所有 **X** 的除数存储在另一个数组中，交叉检查 **X** 是否与给定语句矛盾，如果形成的数组与给定数组不相同，则打印 **-1** ，否则打印 **X** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns X
int findX(int a[], int n)
{
    // Sort the given array
    sort(a, a + n);

    // Get the possible X
    int x = a[0] * a[n - 1];

    // Container to store divisors
    vector<int> vec;

    // Find the divisors of x
    for (int i = 2; i * i <= x; i++)
    {
        // Check if divisor
        if (x % i == 0)
        {
            vec.push_back(i);
            if ((x / i) != i)
                vec.push_back(x / i);
        }
    }

    // sort the vec because a is sorted
    // and we have to compare all the elements
    sort(vec.begin(), vec.end());

    // if size of both vectors is not same
    // then we are sure that both vectors
    // can't be equal
    if (vec.size() != n)
        return -1;
    else
    {
        // Check if a and vec have
        // same elements in them
        int i = 0;
        for (auto it : vec)
        {
            if (a[i++] != it)
                return -1;
        }
    }

    return x;
}

// Driver code
int main()
{
    int a[] = { 2, 5, 4, 10 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << findX(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function that returns X
    static int findX(int a[], int n)
    {
        // Sort the given array
        Arrays.sort(a);

        // Get the possible X
        int x = a[0] * a[n - 1];

        // Container to store divisors
        Vector<Integer> vec = new Vector<Integer>();

        // Find the divisors of x
        for (int i = 2; i * i <= x; i++)
        {
            // Check if divisor
            if (x % i == 0)
            {
                vec.add(i);
                if ((x / i) != i)
                    vec.add(x / i);
            }
        }
        // sort the vec because a is sorted
        // and we have to compare all the elements
        Collections.sort(vec);

        // if size of both vectors is not same
        // then we are sure that both vectors
        // can't be equal
        if (vec.size() != n)
            return -1;
        else {
            // Check if a and vec have
            // same elements in them
            int i = 0;
            for (int it : vec) {
                if (a[i++] != it)
                    return -1;
            }
        }

        return x;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 5, 4, 10 };
        int n = a.length;

        // Function call
        System.out.print(findX(a, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function that returns X
import math

def findX(list, int):
    # Sort the given array
    list.sort()

    # Get the possible X
    x = list[0]*list[int-1]

    # Container to store divisors
    vec = []

    # Find the divisors of x
    i = 2
    while(i * i <= x):
        # Check if divisor
        if(x % i == 0):
            vec.append(i)
            if ((x//i) != i):
                vec.append(x//i)
        i += 1

    # sort the vec because a is sorted
        # and we have to compare all the elements
    vec.sort()
    # if size of both vectors is not same
    # then we are sure that both vectors
    # can't be equal
    if(len(vec) != int):
        return -1
    else:
        # Check if a and vec have
        # same elements in them
        j = 0
        for it in range(int):
            if(a[j] != vec[it]):
                return -1
            else:
                j += 1
    return x

# Driver code
a = [2, 5, 4, 10]
n = len(a)

# Function call
print(findX(a, n))
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function that returns X
    static int findX(int[] a, int n)
    {
        // Sort the given array
        Array.Sort(a);

        // Get the possible X
        int x = a[0] * a[n - 1];

        // Container to store divisors
        List<int> vec = new List<int>();

        // Find the divisors of a number
        for (int i = 2; i * i <= x; i++)
        {
            // Check if divisor
            if (x % i == 0) {
                vec.Add(i);
                if ((x / i) != i)
                    vec.Add(x / i);
            }
        }

        // sort the vec because a is sorted
        // and we have to compare all the elements
        vec.Sort();

        // if size of both vectors is not same
        // then we are sure that both vectors
        // can't be equal
        if (vec.Count != n)
        {
            return -1;
        }
        else
        {
            // Check if a and vec have
            // same elements in them
            int i = 0;
            foreach(int it in vec)
            {
                if (a[i++] != it)
                    return -1;
            }
        }

        return x;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 2, 5, 4, 10 };
        int n = a.Length;

        // Function call
        Console.Write(findX(a, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns X
function findX(a, n)
{
    // Sort the given array
    a.sort((x,y) => x - y);

    // Get the possible X
    let x = a[0] * a[n - 1];

    // Container to store divisors
    let vec = [];

    // Find the divisors of x
    for (let i = 2; i * i <= x; i++)
    {
        // Check if divisor
        if (x % i == 0)
        {
            vec.push(i);
            if (parseInt(x / i) != i)
                vec.push(parseInt(x / i));
        }
    }

    // sort the vec because a is sorted
    // and we have to compare all the elements
    vec.sort((x,y) => x - y);

    // if size of both vectors is not same
    // then we are sure that both vectors
    // can't be equal
    if (vec.length != n)
        return -1;
    else
    {
        // Check if a and vec have
        // same elements in them
        let i = 0;
        for (let j = 0; j < vec.length; j++)
        {
            if (a[i++] != vec[j])
                return -1;
        }
    }

    return x;
}

// Driver code
    let a = [ 2, 5, 4, 10 ];
    let n = a.length;

    // Function call
    document.write(findX(a, n));

</script>
```

**Output**

```
20
```