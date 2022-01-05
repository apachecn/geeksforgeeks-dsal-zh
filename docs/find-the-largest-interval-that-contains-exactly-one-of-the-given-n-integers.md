# 找出恰好包含给定的 N 个整数之一的最大区间。

> 原文:[https://www . geesforgeks . org/find-包含给定 n 个整数中恰好一个整数的最大区间/](https://www.geeksforgeeks.org/find-the-largest-interval-that-contains-exactly-one-of-the-given-n-integers/)

给定一个由 **N** 个不同整数组成的数组**arr【】**，任务是找出区间**【L，R】**中的最大元素，使得该区间恰好包含给定的 **N** 个整数和**1≤L≤R≤10<sup>5</sup>**T12】中的一个

> **输入:** arr[] = {5，10，200}
> **输出:** 99990
> 所有可能的区间为[1，9]，[6，199]和[11，100000]。
> 【11，100000】具有最大整数，即 99990。
> **输入:** arr[] = {15000，25000，40000，70000，80000}
> **输出:** 44999

**方法:**想法是固定我们希望区间包含的元素。现在我们感兴趣的是，在不与其他元素重叠的情况下，我们可以在多大程度上左右扩展我们的间隔。
所以，我们先整理一下我们的阵列。然后对于一个固定的元素，我们使用前一个和后一个元素来确定它的结束。我们也应该注意那些在我们固定第一个和最后一个时间间隔的角落情况。这样，对于每个元素 I，我们找到了区间的最大长度。
以下是上述办法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// size of the required interval
int maxSize(vector<int>& v, int n)
{
    // Insert the borders for array
    v.push_back(0);
    v.push_back(100001);
    n += 2;

    // Sort the elements in ascending order
    sort(v.begin(), v.end());

    // To store the maximum size
    int mx = 0;
    for (int i = 1; i < n - 1; i++) {

        // To store the range [L, R] such that
        // only v[i] lies within the range
        int L = v[i - 1] + 1;
        int R = v[i + 1] - 1;

        // Total integers in the range
        int cnt = R - L + 1;
        mx = max(mx, cnt);
    }

    return mx;
}

// Driver code
int main()
{
    vector<int> v = { 200, 10, 5 };
    int n = v.size();

    cout << maxSize(v, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import static java.lang.Integer.max;
import java.util.*;

class GFG
{

    // Function to return the maximum
    // size of the required interval
    static int maxSize(Vector<Integer> v, int n)
    {
        // Insert the borders for array
        v.add(0);
        v.add(100001);
        n += 2;

        // Sort the elements in ascending order
        Collections.sort(v);

        // To store the maximum size
        int mx = 0;
        for (int i = 1; i < n - 1; i++)
        {

            // To store the range [L, R] such that
            // only v[i] lies within the range
            int L = v.get(i - 1) + 1;
            int R = v.get(i + 1) - 1;

            // Total integers in the range
            int cnt = R - L + 1;
            mx = max(mx, cnt);
        }

        return mx;
    }

    // Driver code
    public static void main(String[] args)
    {
        Integer arr[] = {200, 10, 5};
        Vector v = new Vector(Arrays.asList(arr));
        int n = v.size();

        System.out.println(maxSize(v, n));
    }
}

// This code is contributed by Princi Singh
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the maximum
# size of the required interval
def maxSize(v, n):

    # Insert the borders for array
    v.append(0)
    v.append(100001)
    n += 2

    # Sort the elements in ascending order
    v = sorted(v)

    # To store the maximum size
    mx = 0
    for i in range(1, n - 1):

        # To store the range [L, R] such that
        # only v[i] lies within the range
        L = v[i - 1] + 1
        R = v[i + 1] - 1

        # Total integers in the range
        cnt = R - L + 1
        mx = max(mx, cnt)

    return mx

# Driver code
v = [ 200, 10, 5]
n = len(v)

print(maxSize(v, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the maximum
    // size of the required interval
    static int maxSize(List<int> v, int n)
    {
        // Insert the borders for array
        v.Add(0);
        v.Add(100001);
        n += 2;

        // Sort the elements in ascending order
        v.Sort();

        // To store the maximum size
        int mx = 0;
        for (int i = 1; i < n - 1; i++)
        {

            // To store the range [L, R] such that
            // only v[i] lies within the range
            int L = v[i - 1] + 1;
            int R = v[i + 1] - 1;

            // Total integers in the range
            int cnt = R - L + 1;
            mx = Math.Max(mx, cnt);
        }

        return mx;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {200, 10, 5};
        List<int> v = new List<int>(arr);
        int n = v.Count;

        Console.WriteLine(maxSize(v, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum
// size of the required interval
function maxSize(v, n)
{
    // Insert the borders for array
    v.push(0);
    v.push(100001);
    n += 2;

    // Sort the elements in ascending order
    v.sort((a, b) => a - b);

    // To store the maximum size
    let mx = 0;
    for (let i = 1; i < n - 1; i++) {

        // To store the range [L, R] such that
        // only v[i] lies within the range
        let L = v[i - 1] + 1;
        let R = v[i + 1] - 1;

        // Total integers in the range
        let cnt = R - L + 1;
        mx = Math.max(mx, cnt);
    }

    return mx;
}

// Driver code
    let v = [ 200, 10, 5 ];
    let n = v.length;

    document.write(maxSize(v, n));

</script>
```

**Output:** 

```
99990
```