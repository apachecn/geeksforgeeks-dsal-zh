# 找到最大可能的 k 倍数集

> 原文:[https://www . geesforgeks . org/find-最大可能 k-multiple-set/](https://www.geeksforgeeks.org/find-the-largest-possible-k-multiple-set/)

给定一个包含不同正整数和整数 k 的数组。任务是从给定元素的数组中找到最大可能的 k 倍集。
如果集合中没有两个元素，即 x，y 存在，使得 y = x*k，则集合被称为 **k-multiple** 集合
可以有多个答案。你可以打印任何一个。
**例:**

> **输入:** a[] = {2，3，4，5，6，10}，k = 2
> **输出:** {2，3，5}
> {2，3，5}、{2，3，10}、{2，5，6}、{2，6，10}、{3，4，5}、{3，4，10}、
> {4，5，6}、{4，6，10}可能是 2-多组。
> **输入:** a[] = {1，2，3，4，5，6，7，8，9，10}，k = 2
> **输出:** {1，3，4，5，7，9}

**方法:**一种有效的方法是对给定的元素数组进行排序，遍历整个数组，如果集合中不包含等于 x/k 的元素，则推送集合中的元素 x，其中 x 可被 k 整除。
下面是上述方法的实现:

## C++

```
// C++ program to find the largest
// possible k-multiple set
#include <bits/stdc++.h>
using namespace std;

// Function to find the largest
// possible k-multiple set
void K_multiple(int a[], int n, int k)
{
    // Sort the given array
    sort(a, a + n);

    // To store k-multiple set
    set<int> s;

    // Traverse through the whole array
    for (int i = 0; i < n; i++) {
        // Check if x/k is already present or not
        if ((a[i] % k == 0 && s.find(a[i] / k) == s.end())
             || a[i] % k != 0)
            s.insert(a[i]);
    }

    // Print the k-multiple set
    for (auto i = s.begin(); i != s.end(); i++){
        cout << *i << " ";}
}

// Driver code
int main()
{
    int a[] = { 2, 3, 4, 5, 6, 10 } ;
    int k = 2;

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    K_multiple(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest
// possible k-multiple set
import java.util.*;

class GFG
{

// Function to find the largest
// possible k-multiple set
static void K_multiple(int a[], int n, int k)
{
    // Sort the given array
    Arrays.sort(a);

    // To store k-multiple set
    HashSet<Integer> s = new HashSet<>();

    // Traverse through the whole array
    for (int i = 0; i < n; i++)
    {
        // Check if x/k is already present or not
        if ((a[i] % k == 0 && !s.contains(a[i] / k))
            || a[i] % k != 0)
            s.add(a[i]);
    }

    // Print the k-multiple set
    for (Integer i:s)
        System.out.print(i+" ");
}

// Driver code
public static void main(String args[])
{
    int a[] = { 2, 3, 4, 5, 6, 10 } ;
    int k = 2;

    int n = a.length;

    // Function call
    K_multiple(a, n, k);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the largest
# possible k-multiple set

# Function to find the largest
# possible k-multiple set
def K_multiple(a, n, k) :

    # Sort the given array
    a.sort();

    # To store k-multiple set
    s = set();

    # Traverse through the whole array
    for i in range(n) :

        # Check if x/k is already present or not
        if ((a[i] % k == 0 and
             a[i] // k not in s ) or a[i] % k != 0) :
            s.add(a[i]);

    # Print the k-multiple set
    for i in s :
        print(i, end = " ")

# Driver code
if __name__ == "__main__" :

    a = [ 2, 3, 4, 5, 6, 10 ];
    k = 2;

    n = len(a);

    # Function call
    K_multiple(a, n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the largest
// possible k-multiple set
using System;
using System.Collections.Generic;
public class GFG
{

// Function to find the largest
// possible k-multiple set
static void K_multiple(int []a, int n, int k)
{
    // Sort the given array
    Array.Sort(a);

    // To store k-multiple set
    HashSet<int> s = new HashSet<int>();

    // Traverse through the whole array
    for (int i = 0; i < n; i++)
    {
        // Check if x/k is already present or not
        if ((a[i] % k == 0 && !s.Contains(a[i] / k))
            || a[i] % k != 0)
            s.Add(a[i]);
    }

    // Print the k-multiple set
    foreach (int i in s)
        Console.Write(i+" ");
}

// Driver code
public static void Main(String []args)
{
    int []a = { 2, 3, 4, 5, 6, 10 } ;
    int k = 2;

    int n = a.Length;

    // Function call
    K_multiple(a, n, k);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the largest
// possible k-multiple set

// Function to find the largest
// possible k-multiple set
function K_multiple(a, n, k) {
    // Sort the given array
    a.sort((a, b) => a - b);

    // To store k-multiple set
    let s = new Set();

    // Traverse through the whole array
    for (let i = 0; i < n; i++) {
        // Check if x/k is already present or not
        if ((a[i] % k == 0 && !s.has(a[i] / k))
            || a[i] % k != 0)
            s.add(a[i]);
    }

    // Print the k-multiple set
    for (let i of s) {
        document.write(i + " ");
    }
}

// Driver code

let a = [2, 3, 4, 5, 6, 10];
let k = 2;

let n = a.length;

// Function call
K_multiple(a, n, k);

// This code is contributed by gfgking

</script>
```

**Output**

```
2 3 5 
```

**时间复杂度:** O (N*log(N))