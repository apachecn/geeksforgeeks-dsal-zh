# 求满足给定方程的 n 个正整数

> 原文:[https://www . geesforgeks . org/find-n-满足给定方程的正整数/](https://www.geeksforgeeks.org/find-n-positive-integers-that-satisfy-the-given-equations/)

给定三个整数 **N** 、 **X** 和 **Y** 。任务是找到满足给定方程的 **N** 正整数。

1.  **a<sub><sup>【2】</sup>+a<sub>【2】</sub><sup>【2】</sup>+。+a<sub><sup>【2】</sup>≥x</sub></sub>**
2.  **a<sub>【1】</sub>+a<sub>【2】</sub>+。+ a <sub>n</sub> ≤ Y**

如果没有这样的整数序列，则打印 **-1** 。

**示例:**

> **输入:** N = 3，X = 254，Y = 18
> **输出:**1 1 16
> 1<sup>2</sup>+1<sup>2</sup>+16<sup>2</sup>= 1+1+256 = 258≥X
> 1+1+16 = 18≤Y
> 
> **输入:** N = 2，X = 3，Y = 2
> **输出:** -1
> 不存在这样的序列。

**逼近:**很容易看出，为了最大化平方和，应该使除第一个数以外的所有数都等于 1，最大化第一个数。记住这一点，我们只需要检查给定的 y 值是否足够大，以满足所有 n 个数字都是正数的限制。如果 y 不是太小，那么我们只需要保证**X≤1+1+……+(y –( n–1))<sup>2</sup>T5。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find n positive integers
// that satisfy the given conditions
void findIntegers(int n, int x, int y)
{

    // To store n positive integers
    vector<int> ans;

    // Place N - 1 one's
    for (int i = 0; i < n - 1; i++)
        ans.push_back(1);

    // If can not place (y - (n - 1))
    // as the Nth integer
    if (y - (n - 1) <= 0) {
        cout << "-1";
        return;
    }

    // Place Nth integer
    ans.push_back(y - (n - 1));

    // To store the sum of
    // squares of N integers
    int store = 0;
    for (int i = 0; i < n; i++)
        store += ans[i] * ans[i];

    // If it is less than x
    if (store < x) {
        cout << "-1";
        return;
    }

    // Print the required integers
    for (int i = 0; i < n; i++)
        cout << ans[i] << " ";
}

// Driver code
int main()
{
    int n = 3, x = 254, y = 18;
    findIntegers(n, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find n positive integers
// that satisfy the given conditions
static void findIntegers(int n, int x, int y)
{

    // To store n positive integers
    ArrayList<Integer> ans = new ArrayList<Integer>();

    // Place N - 1 one's
    for (int i = 0; i < n - 1; i++)
        ans.add(1);

    // If can not place (y - (n - 1))
    // as the Nth integer
    if (y - (n - 1) <= 0)
    {
        System.out.print("-1");
        return;
    }

    // Place Nth integer
    ans.add(y - (n - 1));

    // To store the sum of
    // squares of N integers
    int store = 0;
    for (int i = 0; i < n; i++)
        store += ans.get(i) * ans.get(i);

    // If it is less than x
    if (store < x)
    {
        System.out.print("-1");
        return;
    }

    // Print the required integers
    for (int i = 0; i < n; i++)
        System.out.print(ans.get(i)+" ");
}

// Driver code
public static void main (String[] args)
{
    int n = 3, x = 254, y = 18;
    findIntegers(n, x, y);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find n positive integers
# that satisfy the given conditions
def findIntegers(n, x, y):

    # To store n positive integers
    ans = []

    # Place N - 1 one's
    for i in range(n - 1):
        ans.append(1)

    # If can not place (y - (n - 1))
    # as the Nth integer
    if (y - (n - 1) <= 0):
        print("-1", end = "")
        return

    # Place Nth integer
    ans.append(y - (n - 1))

    # To store the sum of
    # squares of N integers
    store = 0

    for i in range(n):
        store += ans[i] * ans[i]

    # If it is less than x
    if (store < x):
        print("-1", end = "")
        return;

    # Print the required integers
    for i in range(n):
        print(ans[i], end = " ")

# Driver code
n, x, y = 3, 254, 18
findIntegers(n, x, y)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{

// Function to find n positive integers
// that satisfy the given conditions
static void findIntegers(int n, int x, int y)
{

    // To store n positive integers
    ArrayList ans = new ArrayList();

    // Place N - 1 one's
    for (int i = 0; i < n - 1; i++)
        ans.Add(1);

    // If can not place (y - (n - 1))
    // as the Nth integer
    if (y - (n - 1) <= 0)
    {
        Console.Write("-1");
        return;
    }

    // Place Nth integer
    ans.Add(y - (n - 1));

    // To store the sum of
    // squares of N integers
    int store = 0;
    for (int i = 0; i < n; i++)
        store += (int)ans[i] *(int)ans[i];

    // If it is less than x
    if (store < x)
    {
        Console.Write("-1");
        return;
    }

    // Print the required integers
    for (int i = 0; i < n; i++)
        Console.Write((int)ans[i]+" ");
}

// Driver code
static void Main()
{
    int n = 3, x = 254, y = 18;
    findIntegers(n, x, y);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to find n positive integers
// that satisfy the given conditions
function findIntegers($n, $x, $y)
{

    // To store n positive integers
    $ans = array();

    // Place N - 1 one's
    for ($i = 0; $i < $n - 1; $i++)
        array_push($ans,1) ;

    // If can not place (y - (n - 1))
    // as the Nth integer
    if ($y - ($n - 1) <= 0)
    {
        echo "-1";
        return;
    }

    // Place Nth integer
    array_push($ans,$y - ($n - 1));

    // To store the sum of
    // squares of N integers
    $store = 0;
    for ($i = 0; $i < $n; $i++)
        $store += $ans[$i] * $ans[$i];

    // If it is less than x
    if ($store < $x)
    {
        echo "-1";
        return;
    }

    // Print the required integers
    for ($i = 0; $i < $n; $i++)
        echo $ans[$i]," ";
}

    // Driver code
    $n = 3; $x = 254; $y = 18;
    findIntegers($n, $x, $y);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find n positive integers
// that satisfy the given conditions
function findIntegers(n, x, y)
{

    // To store n positive integers
    let ans = [];

    // Place N - 1 one's
    for (let i = 0; i < n - 1; i++)
        ans.push(1);

    // If can not place (y - (n - 1))
    // as the Nth integer
    if (y - (n - 1) <= 0)
    {
        document.write("-1");
        return;
    }

    // Place Nth integer
    ans.push(y - (n - 1));

    // To store the sum of
    // squares of N integers
    let store = 0;
    for (let i = 0; i < n; i++)
        store += ans[i] * ans[i];

    // If it is less than x
    if (store < x)
    {
        document.write("-1");
        return;
    }

    // Print the required integers
    for (let i = 0; i < n; i++)
        document.write(ans[(i)]+" ");
}     

// Driver Code

     let n = 3, x = 254, y = 18;
    findIntegers(n, x, y);

</script>
```

**Output:** 

```
1 1 16
```