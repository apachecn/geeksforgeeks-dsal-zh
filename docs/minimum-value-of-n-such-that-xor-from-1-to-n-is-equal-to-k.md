# N 的最小值，使得从 1 到 N 的异或等于 K

> 原文:[https://www . geesforgeks . org/n 的最小值，这样从 1 到 n 的异或等于 k/](https://www.geeksforgeeks.org/minimum-value-of-n-such-that-xor-from-1-to-n-is-equal-to-k/)

给定一个值 K，它是从 1 到 N 的所有值的异或，任务是找到 N 的最小值，使得从 1 到 N 的异或等于 K。
**示例** :

```
Input: K = 7
Output: 6
1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6 = 7

Input: K = 10
Output: Not Possible
```

**方法:**这个问题类似于[从 1 到 n](https://www.geeksforgeeks.org/calculate-xor-1-n/) 计算异或。以下是需要检查的条件:

1.  如果 k = 0，那么 N = 3。
2.  如果 k = 1，那么 N = 1。
3.  如果 k % 4 = 0，那么 N = k。
4.  如果 k % 4 = 3，那么 N = k-1。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of N
int findN(int k)
{

    // variable to store the result
    int ans;

    // handling case for '0'
    if (k == 0)
        ans = 3;

    // handling case for '1'
    if (k == 1)
        ans = 1;

    // when number is completely divided by
    // 4 then minimum 'x' will be 'k'
    else if (k % 4 == 0)
        ans = k;

    // when number divided by 4 gives 3 as
    // remainder then minimum 'x' will be 'k-1'
    else if (k % 4 == 3)
        ans = k - 1;

    // else it is not possible to get
    // k for any value of x
    else
        ans = -1;

    return ans;
}

// Driver code
int main()
{
    // let the given number be 7
    int k = 7;

    int res = findN(k);
    if (res == -1)
        cout << "Not possible";
    else
        cout << res;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.io.*;

class GFG
{

// Function to find the
// value of N
static int findN(int k)
{

    // variable to store
    // the result
    int ans;

    // handling case for '0'
    if (k == 0)
        ans = 3;

    // handling case for '1'
    if (k == 1)
        ans = 1;

    // when number is completely
    // divided by 4 then minimum
    // 'x' will be 'k'
    else if (k % 4 == 0)
        ans = k;

    // when number divided by 4
    // gives 3 as remainder then
    // minimum 'x' will be 'k-1'
    else if (k % 4 == 3)
        ans = k - 1;

    // else it is not possible to
    // get k for any value of x
    else
        ans = -1;

    return ans;
}

// Driver code
public static void main (String[] args)
{
    // let the given number be 7
    int k = 7;

    int res = findN(k);
    if (res == -1)
        System.out.println("Not possible");
    else
        System.out.println(res);
}
}

// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to find the value of N
def findN(k) :

    # handling case for '0'
    if (k == 0) :
        ans = 3

    # handling case for '1'
    if (k == 1) :
        ans = 1

    # when number is completely
    # divided by 4 then minimum
    # 'x' will be 'k'
    elif (k % 4 == 0) :
        ans = k

    # when number divided by 4
    # gives 3 as remainder then
    # minimum 'x' will be 'k-1'
    elif (k % 4 == 3) :
        ans = k - 1

    # else it is not possible to 
    # get k for any value of x
    else:
        ans = -1

    return ans

# Driver code

# let the given number be 7
k = 7

res = findN(k)
if (res == -1):
    print("Not possible")
else:
    print(res)

# This code is contributed
# by Smitha
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{

// Function to find the
// value of N
static int findN(int k)
{

    // variable to store
    // the result
    int ans;

    // handling case for '0'
    if (k == 0)
        ans = 3;

    // handling case for '1'
    if (k == 1)
        ans = 1;

    // when number is completely
    // divided by 4 then minimum
    // 'x' will be 'k'
    else if (k % 4 == 0)
        ans = k;

    // when number divided by 4
    // gives 3 as remainder then
    // minimum 'x' will be 'k-1'
    else if (k % 4 == 3)
        ans = k - 1;

    // else it is not possible to
    // get k for any value of x
    else
        ans = -1;

    return ans;
}

// Driver code
public static void Main ()
{
    // let the given number be 7
    int k = 7;

    int res = findN(k);
    if (res == -1)
        Console.WriteLine("Not possible");
    else
        Console.WriteLine(res);
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the value of N
function findN($k)
{

    // variable to store the result
    $ans;

    // handling case for '0'
    if ($k == 0)
        $ans = 3;

    // handling case for '1'
    if ($k == 1)
        $ans = 1;

    // when number is completely divided
    // by 4 then minimum 'x' will be 'k'
    else if ($k % 4 == 0)
        $ans = $k;

    // when number divided by 4 gives 3 as
    // remainder then minimum 'x' will be 'k-1'
    else if ($k % 4 == 3)
        $ans = $k - 1;

    // else it is not possible to
    // get k for any value of x
    else
        $ans = -1;

    return $ans;
}

// Driver code

// let the given number be 7
$k = 7;

$res = findN($k);
if ($res == -1)
    echo "Not possible";
else
    echo $res;

// This code is contributed by Mahadev
?>
```

## java 描述语言

```
<script>
// javascript implementation of
// above approach

// Function to find the
// value of N
function findN(k)
{

    // variable to store
    // the result
    var ans;

    // handling case for '0'
    if (k == 0)
        ans = 3;

    // handling case for '1'
    if (k == 1)
        ans = 1;

    // when number is completely
    // divided by 4 then minimum
    // 'x' will be 'k'
    else if (k % 4 == 0)
        ans = k;

    // when number divided by 4
    // gives 3 as remainder then
    // minimum 'x' will be 'k-1'
    else if (k % 4 == 3)
        ans = k - 1;

    // else it is not possible to
    // get k for any value of x
    else
        ans = -1;

    return ans;
}

// Driver code
// let the given number be 7
var k = 7;

var res = findN(k);
if (res == -1)
    document.write("Not possible");
else
    document.write(res);

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
6
```

**这是如何工作的？**
当我们对数字进行异或运算时，我们在 4 的倍数之前得到 0 作为异或值。这在每 4 的倍数之前不断重复。

```
Number Binary-Repr  XOR-from-1-to-n
1         1           [0001]
2        10           [0011]
3        11           [0000]  <----- We get a 0
4       100           [0100]  <----- Equals to n
5       101           [0001]
6       110           [0111]
7       111           [0000]  <----- We get 0
8      1000           [1000]  <----- Equals to n
9      1001           [0001]
10     1010           [1011]
11     1011           [0000] <------ We get 0
12     1100           [1100] <------ Equals to n
```