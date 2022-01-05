# 第 n 天结束时未解决的问题

> 原文:[https://www . geesforgeks . org/问题-第 n 天结束时未解决/](https://www.geeksforgeeks.org/problems-not-solved-at-the-end-of-nth-day/)

给定 3 个整数 K，P 和 n，其中，K 是每天给这个人的问题数，P 是他一天能解决的最大问题数。找出第 N 天之后没有解决的问题总数。
**例** :

```
Input :  K = 2, P = 1, N = 3
Output : 3
On each day 1 problem is left so 3*1 = 3 
problems left after Nth day.

Input : K = 4, P = 1, N = 10
Output : 30
```

如果 P 大于或等于 K，那么所有问题将在当天解决，或者(K-P)问题将在每天解决，因此如果 K <=P else the answer will be (K-P)*N.
答案将为 0。以下是上述方法的实现:

## C++

```
// C++ program to find problems not
// solved at the end of Nth day

#include <bits/stdc++.h>
using namespace std;

// Function to find problems not
// solved at the end of Nth day
int problemsLeft(int K, int P, int N)
{
    if (K <= P)
        return 0;
    else
        return (K - P) * N;
}

// Driver Code
int main()
{
    int K, P, N;

    K = 4;
    P = 1;
    N = 10;

    cout << problemsLeft(K, P, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find problems not
// solved at the end of Nth day

class Gfg {

    // Function to find problems not
    // solved at the end of Nth day
    public static int problemsLeft(int K, int P, int N)
    {
        if (K <= P)
            return 0;
        else
            return ((K - P) * N);
    }

    // Driver Code
    public static void main(String args[])
    {
        int K, P, N;
        K = 4;
        P = 1;
        N = 10;

        System.out.println(problemsLeft(K, P, N));
    }
}
```

## 蟒蛇 3

```
# Python program to find problems not
# solved at the end of Nth day

def problemsLeft(K, P, N):
    if(K<= P):
        return 0
    else:
        return ((K-P)*N)

# Driver Code
K, P, N = 4, 1, 10

print(problemsLeft(K, P, N))
```

## C#

```
// C# program to find problems not
// solved at the end of Nth day
using System;

class GFG
{

// Function to find problems not
// solved at the end of Nth day
public static int problemsLeft(int K,
                               int P, int N)
{
    if (K <= P)
        return 0;
    else
        return ((K - P) * N);
}

// Driver Code
public static void Main()
{
    int K, P, N;
    K = 4;
    P = 1;
    N = 10;

    Console.WriteLine(problemsLeft(K, P, N));
}
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find problems not
// solved at the end of Nth day

// Function to find problems not
// solved at the end of Nth day
function problemsLeft($K, $P, $N)
{
    if ($K <= $P)
        return 0;
    else
        return ($K - $P) * $N;
}

// Driver Code
$K = 4;
$P = 1;
$N = 10;

echo problemsLeft($K, $P, $N);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>
// JavaScript program to find problems not
// solved at the end of Nth day

// Function to find problems not
// solved at the end of Nth day
function problemsLeft( K, P, N){
    if (K <= P)
        return 0;
    else
        return (K - P) * N;
}

// Driver Code
let K, P, N;

    K = 4;
    P = 1;
    N = 10;

document.write(problemsLeft(K, P, N));

// This code is contributed by rohitsingh07052.
</script>
```

**Output:** 

```
30
```