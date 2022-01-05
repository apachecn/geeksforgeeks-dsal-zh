# 密钥 K 出现在数组中的概率

> 原文:[https://www . geesforgeks . org/a-key-k-present-in-array/](https://www.geeksforgeeks.org/probability-of-a-key-k-present-in-array/)

给定一个数组 A[]，数组的大小是 N，另一个是 key K，任务是找出 Key K 出现在数组中的概率。
**例:**

```
Input : N = 6
        A[] = { 4, 7, 2, 0, 8, 7, 5 }
        K = 3
Output :0
Since value of k = 3  is not present in array,
hence the probability of 0.

Input :N = 10
       A[] = { 2, 3, 5, 1, 9, 8, 0, 7, 6, 5 }
       K = 5
Output :0.2
```

的概率可以用下面的公式求出:

```
Probability = total number of K present /
                          size of array.
```

首先计算 K 的数量，然后概率将是 K 的数量除以 N，即 count/N
下面是上述方法的实现:

## C++

```
// C++ code to find the probability of
// search key K present in array
#include <bits/stdc++.h>
using namespace std;

// Function to find the probability
float kPresentProbability(int a[], int n, int k)
{
    float count = 0;

    for (int i = 0; i < n; i++)
        if (a[i] == k)
            count++;

    // find probability
    return count / n;
}

// Driver Code
int main()
{

    int A[] = { 4, 7, 2, 0, 8, 7, 5 };
    int K = 3;
    int N = sizeof(A) / sizeof(A[0]);
    cout << kPresentProbability(A, N, K);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 code to find the
# probability of search key
# K present in 1D-array (list).

# Function to find the probability
def kPresentProbability(a, n, k) :

    count = a.count(k)

    # find probability upto
    # 2 decimal places
    return round(count / n , 2)

# Driver Code
if __name__ == "__main__" :

    A = [ 4, 7, 2, 0, 8, 7, 5 ]
    K = 2
    N = len(A)

    print(kPresentProbability( A, N, K))

# This code is contributed
# by AnkitRai1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the probability
// of search key K present in array
class GFG
{

// Function to find the probability
static float kPresentProbability(int a[],
                                 int n,
                                 int k)
{
    float count = 0;

    for (int i = 0; i < n; i++)
        if (a[i] == k)
            count++;

    // find probability
    return count/ n;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 4, 7, 2, 0, 8, 7, 5 };
    int K = 2;
    int N = A.length;
    double n = kPresentProbability(A, N, K);
    double p = (double)Math.round(n * 100) / 100;
    System.out.println(p);
}
}

// This code is contributed
// by ChitraNayal
```

## C#

```
// C# code to find the probability
// of search key K present in array
using System;

class GFG
{

// Function to find the probability
static float kPresentProbability(int[] a,
                                 int n,
                                 int k)
{
    float count = 0;

    for (int i = 0; i < n; i++)
        if (a[i] == k)
            count++;

    // find probability
    return count/ n;
}

// Driver Code
public static void Main()
{
    int[] A = { 4, 7, 2, 0, 8, 7, 5 };
    int K = 2;
    int N = A.Length;
    double n = kPresentProbability(A, N, K);
    double p = (double)Math.Round(n * 100) / 100;
    Console.Write(p);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the probability
// of search key K present in array

// Function to find the probability
function kPresentProbability(&$a, $n, $k)
{
    $count = 0;

    for ($i = 0; $i < $n; $i++)
        if ($a[$i] == $k)
            $count++;

    // find probability
    return $count / $n;
}

// Driver Code
$A = array( 4, 7, 2, 0, 8, 7, 5 );
$K = 2;
$N = sizeof($A);
echo round(kPresentProbability($A, $N, $K), 2);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// JavaScript code to find the probability of
// search key K present in array

// Function to find the probability
function kPresentProbability(a,n,k)
{
    let count = 0;

    for (let i = 0; i < n; i++)
        if (a[i] == k)
            count+=1;
    // find probability
    return count / n;
}

// Driver Code

    let A = [ 4, 7, 2, 0, 8, 7, 5 ];
    let K = 3;
    let N = A.length;
    document.write(kPresentProbability(A, N,K));

// This code contributed by Rajput-Ji

</script>
```

**Output**

```
0
```

**时间复杂度:O(N)**