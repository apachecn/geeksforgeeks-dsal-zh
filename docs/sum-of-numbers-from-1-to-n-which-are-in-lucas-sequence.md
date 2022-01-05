# 卢卡斯序列中 1 到 N 的数的和

> 原文:[https://www . geesforgeks . org/numbers-sum-from-1-n-in-Lucas-sequence/](https://www.geeksforgeeks.org/sum-of-numbers-from-1-to-n-which-are-in-lucas-sequence/)

给定一个数字 **N** 。任务是找到从 1 到 N 的数字的和，这些数字存在于[卢卡斯序列](https://www.geeksforgeeks.org/lucas-numbers/)中。

卢卡斯数的整数序列如下:

```
2, 1, 3, 4, 7, 11, 18, 29, 47, 76, 123 ......
```

**例:**

```
Input :  N = 10
Output : 17

Input : N = 5
Output : 10
```

**进场:**

*   循环遍历所有小于给定值 n 的卢卡斯数
*   用 0 初始化一个和变量。
*   继续把这些卢卡斯数字相加，得到所需的总和。

下面是上述方法的实现:

## c++

```
// C++ program to find sum of numbers from
// 1 to N which are in Lucas Sequence
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// required sum
int LucasSum(int N)
{
    // Generate lucas number and keep on
    // adding them
    int sum = 0;
    int a = 2, b = 1, c;

    sum += a;

    while (b <= N) {

        sum += b;
        int c = a + b;
        a = b;
        b = c;
    }

    return sum;
}

// Driver code
int main()
{
    int N = 20;
    cout << LucasSum(N);
    return 0;
}
```

## Java

```
// java program to find sum of numbers from
// 1 to N which are in Lucas Sequence
class GFG
{

// Function to return the
// required sum
static int LucasSum(int N)
{
    // Generate lucas number and keep on
    // adding them
    int sum = 0;
    int a = 2, b = 1, c;

    sum += a;

    while (b <= N) {

        sum += b;
        c = a + b;
        a = b;
        b = c;
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int N = 20;
    System.out.println(LucasSum(N));

}
// This code is contributed by princiraj1992
}
```

## python 3

T2T19】c#T3T23】PHPT4

## Javascript

T5T31】

**输出:**

```
46
```