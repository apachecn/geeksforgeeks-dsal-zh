# 从给定列表中找出函数值最接近 A 的数字

> 原文:[https://www . geesforgeks . org/find-number-from-给定-list-for-the-value-of-function-最接近 a/](https://www.geeksforgeeks.org/find-number-from-given-list-for-which-value-of-the-function-is-closest-to-a/)

给定一个函数**F(n)= P–(0.006 * n)**，其中 P 是给定的。给定一列整数和一个数字，![A ](img/d1a0ee89cb1a1e0b2aaae4707c872b24.png "Rendered by QuickLaTeX.com")。任务是从给定列表中找到函数值最接近![A ](img/d1a0ee89cb1a1e0b2aaae4707c872b24.png "Rendered by QuickLaTeX.com")的数字。
**例** :

```
Input : P = 12, A = 5
        List = {1000, 2000} 
Output : 1
Explanation :
Given, P=12, A=5
For 1000, F(1000) is 12 - 1000×0.006 = 6
For 2000, F(2000) is 12 - 2000×0.006 = 0
As the nearest value to 5 is 6, 
so the answer is 1000.

Input : P = 21, A = -11
        List = {81234, 94124, 52141}
Output : 3
```

**方法:**迭代给定列表中的每个值，并为每个值找到 F(n)。现在，比较 F(n)和 A 的每个值与![n ](img/872c13b29b9001d12460c34eb30ae8d0.png "Rendered by QuickLaTeX.com")的值的绝对差，对于后者，绝对差最小就是答案。
以下是上述办法的实施:

## C++

```
// C++ program to find number from
// given list for which value of the
// function is closest to A
#include <bits/stdc++.h>
using namespace std;

// Function to find number from
// given list for which value of the
// function is closest to A
int leastValue(int P, int A, int N, int a[])
{

    // Stores the final index
    int ans = -1;

    // Declaring a variable to store
    // the minimum absolute difference
    float tmp = (float)INFINITY;

    for (int i = 0; i < N; i++)
    {

        // Finding F(n)
        float t = P - a[i] * 0.006;

        // Updating the index of the answer if
        // new absolute difference is less than tmp
        if (abs(t-A) < tmp)
        {
            tmp = abs(t - A);
            ans = i;
        }
    }
    return a[ans];
}

// Driver code
int main()
{
    int N = 2, P = 12, A = 2005;
    int a[] = {1000, 2000};

    cout << leastValue(P, A, N, a) << endl;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number from
// given list for which value of the
// function is closest to A
import java.util.*;

class GFG
{

// Function to find number from
// given list for which value of the
// function is closest to A
static int leastValue(int P, int A,
                      int N, int a[])
{

    // Stores the final index
    int ans = -1;

    // Declaring a variable to store
    // the minimum absolute difference
    float tmp = Float.MAX_VALUE;

    for (int i = 0; i < N; i++)
    {

        // Finding F(n)
        float t = (float) (P - a[i] * 0.006);

        // Updating the index of the answer if
        // new absolute difference is less than tmp
        if (Math.abs(t-A) < tmp)
        {
            tmp = Math.abs(t - A);
            ans = i;
        }
    }
    return a[ans];
}

// Driver code
public static void main(String[] args)
{
    int N = 2, P = 12, A = 2005;
    int a[] = {1000, 2000};

    System.out.println(leastValue(P, A, N, a));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find number from
# given list for which value of the
# function is closest to A

# Function to find number from
# given list for which value of the
# function is closest to A
def leastValue(P, A, N, a):
    # Stores the final index
    ans = -1

    # Declaring a variable to store
    # the minimum absolute difference
    tmp = float('inf')
    for i in range(N):
        # Finding F(n)
        t = P - a[i] * 0.006

        # Updating the index of the answer if
        # new absolute difference is less than tmp
        if abs(t - A) < tmp:
            tmp = abs(t - A)
            ans = i

    return a[ans]

# Driver Code
N, P, A = 2, 12, 5
a = [1000, 2000]

print(leastValue(P, A, N, a))
```

## C#

```
// C# program to find number from
// given list for which value of the
// function is closest to A
using System;

class GFG
{

// Function to find number from
// given list for which value of the
// function is closest to A
static int leastValue(int P, int A,
                      int N, int []a)
{

    // Stores the final index
    int ans = -1;

    // Declaring a variable to store
    // the minimum absolute difference
    float tmp = float.MaxValue;

    for (int i = 0; i < N; i++)
    {

        // Finding F(n)
        float t = (float) (P - a[i] * 0.006);

        // Updating the index of the answer if
        // new absolute difference is less than tmp
        if (Math.Abs(t-A) < tmp)
        {
            tmp = Math.Abs(t - A);
            ans = i;
        }
    }
    return a[ans];
}

// Driver code
public static void Main(String[] args)
{
    int N = 2, P = 12, A = 2005;
    int []a = {1000, 2000};

    Console.WriteLine(leastValue(P, A, N, a));
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number from
// given list for which value of the
// function is closest to A

// Function to find number from
// given list for which value of the
// function is closest to A
function leastValue($P, $A, $N, $a)
{
    // Stores the final index
    $ans = -1;

    // Declaring a variable to store
    // the minimum absolute difference
    $tmp = PHP_INT_MAX;
    for($i = 0; $i < $N; $i++)
    {
        // Finding F(n)
        $t = $P - $a[$i] * 0.006;

        // Updating the index of the
        // answer if new absolute
        // difference is less than tmp
        if (abs($t - $A) < $tmp)
        {
            $tmp = abs($t - $A);
            $ans = $i;
        }
    }    
    return $a[$ans];
}

// Driver Code
$N = 2;
$P = 12;
$A = 5;
$a = array(1000, 2000);

print(leastValue($P, $A, $N, $a));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find number from
// given list for which value of the
// function is closest to A

// Function to find number from
// given list for which value of the
// function is closest to A
function leastValue(P, A, N, a)
{

    // Stores the final index
    let ans = -1;

    // Declaring a variable to store
    // the minimum absolute difference
    let tmp = Number.MAX_VALUE;

    for (let i = 0; i < N; i++)
    {

        // Finding F(n)
        let t =  (P - a[i] * 0.006);

        // Updating the index of the answer if
        // new absolute difference is less than tmp
        if (Math.abs(t-A) < tmp)
        {
            tmp = Math.abs(t - A);
            ans = i;
        }
    }
    return a[ans];
}

    // Driver code

    let N = 2, P = 12, A = 2005;
    let a = [1000, 2000];

    document.write(leastValue(P, A, N, a))

</script>
```

**Output:** 

```
1000
```