# 素性测验|第一套(入门和学校方法)

> 原文:[https://www . geesforgeks . org/primality-test-set-1-introduction-and-school-method/](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)

给定一个正整数，检查这个数是否是质数。质数是一个大于 1 的自然数，除了 1 和它本身之外，没有任何正整数。前几个素数的例子是{2，3，5，
**例子:**

```
Input:  n = 11
Output: true

Input:  n = 15
Output: false

Input:  n = 1
Output: false
```

**学校方法**
一个简单的解决方法是迭代从 2 到 n-1 的所有数字，对于每个数字，检查它是否除 n。如果我们找到任何除的数字，我们返回 false。
下面是这个方法的实现。

## C++

```
// A school method based C++ program to check if a
// number is prime
#include <bits/stdc++.h>
using namespace std;

bool isPrime(int n)
{
    // Corner case
    if (n <= 1)  return false;

    // Check from 2 to n-1
    for (int i=2; i<n; i++)
        if (n%i == 0)
            return false;

    return true;
}

// Driver Program to test above function
int main()
{
    isPrime(11)?  cout << " true\n": cout << " false\n";
    isPrime(15)?  cout << " true\n": cout << " false\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A school method based JAVA program
// to check if a number is prime
class GFG {

    static boolean isPrime(int n)
    {
        // Corner case
        if (n <= 1) return false;

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Driver Program
    public static void main(String args[])
    {
        if(isPrime(11))
            System.out.println(" true");
        else
            System.out.println(" false");
        if(isPrime(15))
            System.out.println(" true");
        else
            System.out.println(" false");

    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# A school method based Python3
# program to check if a number
# is prime

def isPrime(n):

    # Corner case
    if n <= 1:
        return False

    # Check from 2 to n-1
    for i in range(2, n):
        if n % i == 0:
            return False;

    return True

# Driver Program to test above function
print("true") if isPrime(11) else print("false")
print("true") if isPrime(14) else print("false")

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// A optimized school method based C#
// program to check if a number is prime
using System;

namespace prime
{
    public class GFG
    {    
        public static bool isprime(int n)
        {
            // Corner cases
            if (n <= 1) return false;

            for (int i = 2; i < n; i++)
                if (n % i == 0)
                return false;

            return true;
        }

        // Driver program
        public static void Main()
        {
            if (isprime(11)) Console.WriteLine("true");
            else Console.WriteLine("false");

            if (isprime(15)) Console.WriteLine("true");
            else Console.WriteLine("false");
        }
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A school method based PHP
// program to check if a number
// is prime

function isPrime($n)
{
    // Corner case
    if ($n <= 1) return false;

    // Check from 2 to n-1
    for ($i = 2; $i < $n; $i++)
        if ($n % $i == 0)
            return false;

    return true;
}

// Driver Code
$tet = isPrime(11) ? " true\n" :
                     " false\n";
echo $tet;
$tet = isPrime(15) ? " true\n" :
                     " false\n";
echo $tet;

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// A school method based Javascript program to check if a
// number is prime
function isPrime(n)
{
    // Corner case
    if (n <= 1) return false;

    // Check from 2 to n-1
    for (let i = 2; i < n; i++)
        if (n % i == 0)
            return false;
    return true;
}

// Driver Program to test above function
    isPrime(11)? document.write(" true" + "<br>"): document.write(" false" + "<br>");
    isPrime(15)? document.write(" true" + "<br>"): document.write(" false" + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
true
false
```

这个解的时间复杂度为 O(n)
**优化学校方法**
我们可以做以下优化:

1.  我们可以检查到√n，而不是检查到 n，因为 n 的较大因子必须是已经检查过的较小因子的倍数。
2.  通过观察除了 2 和 3 之外，所有素数都是 6k ^ 1 形式，可以进一步改进算法。这是因为对于某些整数 k 和对于 i = -1、0、1、2、3 或 4，所有整数都可以表示为(6k+I)；2 除(6k + 0)，(6k + 2)，(6k+4)；和 3 除(6k + 3)。所以更有效的方法是测试 n 是否能被 2 或 3 整除，然后检查 6k ^ 1 形式的所有数字。(来源:[维基百科](https://en.wikipedia.org/wiki/Primality_test))