# 将 K^N 表示为正好 n 个数字的和

> 原文:[https://www . geesforgeks . org/representative-k-to-power-n-as-sum-of-n-numbers/](https://www.geeksforgeeks.org/represent-k-to-the-power-n-as-the-sum-of-exactly-n-numbers/)

给定两个数字 **N** 和 **K** ，任务是将**K<sup>N</sup>T7】表示为恰好 **N** 个数字的和。如果没有这样的数字，打印 **NA** 。
**示例:**** 

> **输入:** N = 5，K = 2
> **输出:** 2 2 4 8 16
> **解释:**T8】2+2+4+8+16 = 32 = 2<sup>5</sup>
> **输入:** N = 4，K = 3
> **输出:** 3 6 18 54
> **解释:**
> 3+6+6

**方法:**为了得到其和是 K 的幂的数，我们可以选择满足以下条件的数:

这将总是给出 k 的幂的和。
**例如:**这可以表示为:

```
Let N = 3 and K = 4.

We need to represent 43 (=64)
as the sum of exactly 3 numbers

According to the mentioned approach,
The 3 numbers which can be chosen are 
  (41) = 4
  (42 - 41) = 16 - 4 = 12
  (43 - 42) = 64 - 16 = 48

Adding the numbers = 4 + 12 + 48 = 64
which is clearly 43

Therefore the required 3 numbers
are 4, 12 and 48.
```

以下是上述方法的实现:

## C++

```
// C++ program to represent K^N
// as the sum of exactly N numbers

#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to print N numbers whose
// sum is a power of K
void print(ll n, ll k)
{
    // Printing K ^ 1
    cout << k << " ";

    // Loop to print the difference of
    // powers from K ^ 2
    for (int i = 2; i <= n; i++) {
        ll x = pow(k, i) - pow(k, i - 1);
        cout << x << " ";
    }
}

// Driver code
int main()
{
    ll N = 3, K = 4;
    print(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to represent K^N
// as the sum of exactly N numbers
import java.util.*;

class GFG{

// Function to print N numbers whose
// sum is a power of K
static void print(int n, int k)
{
    // Printing K ^ 1
    System.out.print(k+ " ");

    // Loop to print the difference of
    // powers from K ^ 2
    for (int i = 2; i <= n; i++) {
        int x = (int) (Math.pow(k, i) - Math.pow(k, i - 1));
        System.out.print(x+ " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 3, K = 4;
    print(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to represent K^N
# as the sum of exactly N numbers
from math import pow

# Function to print N numbers whose
# sum is a power of K
def printf(n, k):

    # Printing K ^ 1
    print(int(k),end = " ")

    # Loop to print the difference of
    # powers from K ^ 2
    for i in range(2, n + 1, 1):
        x = pow(k, i) - pow(k, i - 1)
        print(int(x),end= " ")

# Driver code
if __name__ == '__main__':
    N = 3
    K = 4
    printf(N, K)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to represent K^N
// as the sum of exactly N numbers
using System;

class GFG{

// Function to print N numbers whose
// sum is a power of K
static void print(int n, int k)
{
    // Printing K ^ 1
    Console.Write(k+ " ");

    // Loop to print the difference of
    // powers from K ^ 2
    for (int i = 2; i <= n; i++) {
        int x = (int) (Math.Pow(k, i) - Math.Pow(k, i - 1));
        Console.Write(x+ " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 3, K = 4;
    print(N, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to represent K^N
// as the sum of exactly N numbers

// Function to print N numbers whose
// sum is a power of K
function print(n, k)
{
    // Printing K ^ 1
    document.write( k + " ");

    // Loop to print the difference of
    // powers from K ^ 2
    for (var i = 2; i <= n; i++) {
        var x = Math.pow(k, i) - Math.pow(k, i - 1);
        document.write( x + " ");
    }
}

// Driver code
var N = 3, K = 4;
print(N, K);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
4 12 48
```

时间复杂度:0(n)

辅助空间:0(1)