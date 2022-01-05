# 从 1 到 N 可被 M 整除的所有整数的最后一位之和

> 原文:[https://www . geesforgeks . org/从 1 到 n 的所有整数的最后一位之和可被 m 整除/](https://www.geeksforgeeks.org/sum-of-last-digit-of-all-integers-from-1-to-n-divisible-by-m/)

给定两个整数 **N** 和 **N** 。任务是计算从 **1** 到 **N** 的所有整数最后一位的和，该和可被 **M** 整除。

**示例:**

> **输入:** N = 12，M = 1
> T3】输出: 48
> 从 1 到 12 被 M = 1 整除的数为:
> { 1+2+3+4+5+6+7+8+9+0+1+2 } = 48
> 
> **输入:** N = 100，M = 3
> T3】输出: 153

**方法:**问题基于简单的观察。
设 k = floor(N/M)为 1 到 N 之间可被 M 整除的整数个数
因为需要在原始和中加上最后几个数字。因此，最后一个数字可以在 0 到 9 的范围内，并且周期可以通过观察阵列图案来形成。
所以对于每个循环，sum =前 10 个最后一位数字的和，在此之后，我们可以用 k 除以 10，并从开始添加剩余数字的最后一位数字。
所以， **Sum =** (循环次数*前 10 个可被 M 整除的整数最后一位之和)+(k % 10 个可被 M 整除的整数最后一位之和)。

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the approach
#include<iostream>
using namespace std;

#define long long long

// Function to return the
// required sum
long sumOfLastDig(long n, long m) {

    long sum = 0, k;

    // Number of element between
    // 1 to n divisible by m
    k = n/m;

    // Array to store the last digit
    // of elements in a cycle
    long arr[10];

    // Storing and adding last
    // digit of cycle
    for (int i = 0; i < 10; i++) {
        arr[i] = m*(i+1) % 10;
        sum += arr[i];
    }

    // Number of elements
    // present in last cycle
    long rem = k % 10;

    // Sum of k/10 cycle
    long ans = (k/10)*sum;

    // Adding value of digits
    // of last cycle to the answer
    for (int i = 0; i < rem; i++) {
        ans += arr[i];
    }

    return ans;
}

// Driver Code
int main() {

    // input n and m
    long n = 100, m = 3;

    cout<<sumOfLastDig(n,m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the required sum
static long sumOfLastDig(long n, long m)
{
    long sum = 0, k;

    // Number of element between
    // 1 to n divisible by m
    k = n / m;

    // Array to store the last digit
    // of elements in a cycle
    long []arr = new long[10];

    // Storing and adding last
    // digit of cycle
    for (int i = 0; i < 10; i++)
    {
        arr[i] = m * (i + 1) % 10;
        sum += arr[i];
    }

    // Number of elements
    // present in last cycle
    long rem = k % 10;

    // Sum of k/10 cycle
    long ans = (k / 10) * sum;

    // Adding value of digits
    // of last cycle to the answer
    for (int i = 0; i < rem; i++)
    {
        ans += arr[i];
    }
    return ans;
}

// Driver Code
public static void main (String[] args)
{

    // input n and m
    long n = 100, m = 3;

    System.out.println(sumOfLastDig(n, m));
}
}

// This code is contributed by jit_t
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# required sum
def sumOfLastDig(n, m) :

    sum = 0;

    # Number of element between
    # 1 to n divisible by m
    k = n // m;

    # Array to store the last digit
    # of elements in a cycle
    arr = [0] * 10;

    # Storing and adding last
    # digit of cycle
    for i in range(10) :
        arr[i] = m * (i + 1) % 10;
        sum += arr[i];

    # Number of elements
    # present in last cycle
    rem = k % 10;

    # Sum of k/10 cycle
    ans = (k // 10) * sum;

    # Adding value of digits
    # of last cycle to the answer
    for i in range(rem) :
        ans += arr[i];

    return ans;

# Driver Code
if __name__ == "__main__" :

    # input n and m
    n = 100; m = 3;

    print(sumOfLastDig(n, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required sum
static long sumOfLastDig(long n, long m)
{
    long sum = 0, k;

    // Number of element between
    // 1 to n divisible by m
    k = n / m;

    // Array to store the last digit
    // of elements in a cycle
    long []arr = new long[10];

    // Storing and adding last
    // digit of cycle
    for (int i = 0; i < 10; i++)
    {
        arr[i] = m * (i + 1) % 10;
        sum += arr[i];
    }

    // Number of elements
    // present in last cycle
    long rem = k % 10;

    // Sum of k/10 cycle
    long ans = (k / 10) * sum;

    // Adding value of digits
    // of last cycle to the answer
    for (int i = 0; i < rem; i++)
    {
        ans += arr[i];
    }
    return ans;
}

// Driver Code
static public void Main ()
{

    // input n and m
    long n = 100, m = 3;

    Console.Write(sumOfLastDig(n, m));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation
// of the approach

// Function to return the
// required sum
function sumOfLastDig(n, m)
{

    let sum = 0, k;

    // Number of element between
    // 1 to n divisible by m
    k = parseInt(n/m);

    // Array to store the last digit
    // of elements in a cycle
    let arr = new Array(10);

    // Storing and adding last
    // digit of cycle
    for (let i = 0; i < 10; i++) {
        arr[i] = m*(i+1) % 10;
        sum += arr[i];
    }

    // Number of elements
    // present in last cycle
    let rem = k % 10;

    // Sum of k/10 cycle
    let ans = parseInt(k/10)*sum;

    // Adding value of digits
    // of last cycle to the answer
    for (let i = 0; i < rem; i++)
    {
        ans += arr[i];
    }

    return ans;
}

// Driver Code

    // input n and m
    let n = 100, m = 3;

    document.write(sumOfLastDig(n,m));

</script>
```

**Output:** 

```
153
```