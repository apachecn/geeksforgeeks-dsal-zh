# 奇偶序列中的第 k 个数字

> 原文:[https://www . geesforgeks . org/k-th-number-奇数-偶数-序列/](https://www.geeksforgeeks.org/k-th-number-odd-even-sequence/)

给定两个数字 n 和 k，在由 n 组成的**奇-偶**序列中找到第 k 个数字。**奇-偶**序列首先包含从 1 到 n 的所有奇数，然后包含集合 1 到 n 中的所有偶数。

```
Examples :
Input :  n = 5, k = 3
Output : 5
In this example, the Odd-Even  is
{1, 3, 5, 2, 4}. 
The third number in sequence is 5.
```

**天真方法:**

第一种方法是简单地制作一个**奇偶**序列，然后在其中找到第 k 个元素。

## C++

```
// CPP program to find k-th
// element in the Odd-Even
// sequence.
#include <bits/stdc++.h>
using namespace std;

int findK(int n, int k)
{
    vector<long> a;

    // insert all the odd
    // numbers from 1 to n.
    for (int i = 1; i < n; i++)
        if (i % 2 == 1)
            a.push_back(i);

    // insert all the even
    // numbers from 1 to n.
    for (int i = 1; i < n; i++)
        if (i % 2 == 0)
            a.push_back(i);

    return (a[k - 1]);
}

// Driver code
int main()
{
    long n = 10, k = 3;
    cout << findK(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k-th
// element in the Odd-Even
// sequence.
import java.util.*;

class GFG{
static int findK(int n, int k)
{
    ArrayList<Integer> a = new ArrayList<Integer>(n);

    // insert all the odd
    // numbers from 1 to n.
    for (int i = 1; i < n; i++)
        if (i % 2 == 1)
            a.add(i);

    // insert all the even
    // numbers from 1 to n.
    for (int i = 1; i < n; i++)
        if (i % 2 == 0)
            a.add(i);

    return (a.get(k - 1));
}

// Driver code
public static void main(String[] args)
{
    int n = 10, k = 3;
    System.out.println(findK(n, k));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 code to find
# k-th element in the
# Odd-Even sequence.

def findK (n, k ):
    a = list()

    # insert all the odd
    # numbers from 1 to n.
    i = 1
    while i < n:
        a.append(i)
        i = i + 2

    # insert all the even
    # numbers from 1 to n.
    i = 2
    while i < n:
        a.append(i)
        i = i + 2

    return (a[k - 1])

# Driver code
n = 10
k = 3
print(findK(n, k))

# This code is contributed
# by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find k-th
// element in the Odd-Even
// sequence.
using System;
using System.Collections;

class GFG{
static int findK(int n, int k)
{
    ArrayList a = new ArrayList(n);

    // insert all the odd
    // numbers from 1 to n.
    for (int i = 1; i < n; i++)
        if (i % 2 == 1)
            a.Add(i);

    // insert all the even
    // numbers from 1 to n.
    for (int i = 1; i < n; i++)
        if (i % 2 == 0)
            a.Add(i);

    return (int)(a[k - 1]);
}

// Driver code
static void Main()
{
    int n = 10, k = 3;
    Console.WriteLine(findK(n, k));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find k-th
// element in the Odd-Even
// sequence.

function findK($n, $k)
{
    $a;
    $index = 0;

    // insert all the odd
    // numbers from 1 to n.
    for ($i = 1; $i < $n; $i++)
        if ($i % 2 == 1)
            $a[$index++] = $i;

    // insert all the even
    // numbers from 1 to n.
    for ($i = 1; $i < $n; $i++)
        if ($i % 2 == 0)
            $a[$index++] = $i;

    return ($a[$k - 1]);
}

// Driver code
$n = 10;
$k = 3;
echo findK($n, $k);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find k-th
    // element in the Odd-Even
    // sequence.

    function findK(n, k)
    {
        let a = [];

        // insert all the odd
        // numbers from 1 to n.
        for (let i = 1; i < n; i++)
            if (i % 2 == 1)
                a.push(i);

        // insert all the even
        // numbers from 1 to n.
        for (let i = 1; i < n; i++)
            if (i % 2 == 0)
                a.push(i);

        return (a[k - 1]);
    }

    let n = 10, k = 3;
    document.write(findK(n, k));

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
 5
```

上述方法的时间复杂度为 O(n)，对于 O(1)方法，请阅读这里讨论的方法。