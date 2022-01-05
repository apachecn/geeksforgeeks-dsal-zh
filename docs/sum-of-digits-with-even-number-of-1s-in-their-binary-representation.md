# 二进制表示中偶数为 1 的数字的总和

> 原文:[https://www . geeksforgeeks . org/二进制表示中带有偶数个 1 的数字总和/](https://www.geeksforgeeks.org/sum-of-digits-with-even-number-of-1s-in-their-binary-representation/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找到包含偶数个 **1 的**的所有数组元素的数字总和。
**举例:**

> **输入:** arr[] = {4，9，15}
> **输出:** 15
> 4 = 10，包含 1 的奇数
> 9 = 1001，包含 1 的偶数
> 15 = 1111，包含 1 的偶数
> 总和= 9 和**15**= 9+1+5 = 15【T15

**方法:**
计算每个数组元素的二进制表示中的 1 的数量，如果是偶数，则计算其位数的总和。
以下是上述办法的实施:

## C++

```
// CPP program to find Sum of digits with even
// number of 1’s in their binary representation
#include <bits/stdc++.h>
using namespace std;

// Function to count and check the
// number of 1's is even or odd
int countOne(int n)
{
    int count = 0;
    while (n) {
        n = n & (n - 1);
        count++;
    }

    if (count % 2 == 0)
        return 1;
    else
        return 0;
}

// Function to calculate the sum
// of the digits of a number
int sumDigits(int n)
{
    int sum = 0;
    while (n != 0) {
        sum += n % 10;
        n /= 10;
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 4, 9, 15 };

    int n = sizeof(arr) / sizeof(arr[0]);
    int total_sum = 0;

    // Iterate through the array
    for (int i = 0; i < n; i++) {
        if (countOne(arr[i]))
            total_sum += sumDigits(arr[i]);
    }

    cout << total_sum << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum of digits with even
// number of 1's in their binary representation
import java.util.*;

class GFG
{

// Function to count and check the
// number of 1's is even or odd
static int countOne(int n)
{
    int count = 0;
    while (n > 0)
    {
        n = n & (n - 1);
        count++;
    }

    if (count % 2 == 0)
        return 1;
    else
        return 0;
}

// Function to calculate the sum
// of the digits of a number
static int sumDigits(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum += n % 10;
        n /= 10;
    }

    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 9, 15 };

    int n = arr.length;
    int total_sum = 0;

    // Iterate through the array
    for (int i = 0; i < n; i++)
    {
        if (countOne(arr[i]) == 1)
            total_sum += sumDigits(arr[i]);
    }
    System.out.println(total_sum);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find Sum of digits with even
# number of 1’s in their binary representation

# Function to count and check the
# number of 1's is even or odd
def countOne(n):
    count = 0
    while (n):
        n = n & (n - 1)
        count += 1

    if (count % 2 == 0):
        return 1
    else:
        return 0

# Function to calculate the summ
# of the digits of a number
def summDigits(n):
    summ = 0
    while (n != 0):
        summ += n % 10
        n //= 10

    return summ

# Driver Code
arr = [4, 9, 15]

n = len(arr)
total_summ = 0

# Iterate through the array
for i in range(n):
    if (countOne(arr[i])):
        total_summ += summDigits(arr[i])

print(total_summ )

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find Sum of digits with even
// number of 1's in their binary representation
using System;

class GFG
{

// Function to count and check the
// number of 1's is even or odd
static int countOne(int n)
{
    int count = 0;
    while (n > 0)
    {
        n = n & (n - 1);
        count++;
    }

    if (count % 2 == 0)
        return 1;
    else
        return 0;
}

// Function to calculate the sum
// of the digits of a number
static int sumDigits(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}

// Driver Code
public static void Main()
{
    int[] arr = { 4, 9, 15 };

    int n = arr.Length;
    int total_sum = 0;

    // Iterate through the array
    for (int i = 0; i < n; i++)
    {
        if (countOne(arr[i]) == 1)
            total_sum += sumDigits(arr[i]);
    }
    Console.WriteLine(total_sum);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find Sum of digits with even 
    // number of 1’s in their binary representation

    // Function to count and check the 
    // number of 1's is even or odd
    function countOne(n)
    {
        let count = 0;
        while (n) {
            n = n & (n - 1);
            count++;
        }

        if (count % 2 == 0)
            return 1;
        else
            return 0;
    }

    // Function to calculate the sum 
    // of the digits of a number
    function sumDigits(n)
    {
        let sum = 0;
        while (n != 0) {
            sum += n % 10;
            n = parseInt(n / 10, 10);
        }

        return sum;
    }

    let arr = [ 4, 9, 15 ];

    let n = arr.length;
    let total_sum = 0;

    // Iterate through the array
    for (let i = 0; i < n; i++) {
        if (countOne(arr[i]))
            total_sum += sumDigits(arr[i]);
    }

    document.write(total_sum);

</script>
```

**Output:** 

```
15
```