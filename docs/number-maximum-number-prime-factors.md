# 质因数最大的数

> 原文:[https://www . geesforgeks . org/number-maximum-number-prime-factors/](https://www.geeksforgeeks.org/number-maximum-number-prime-factors/)

给定一个整数 **N** 。任务是找到一个小于或等于 N 并且具有最大质因数的数。如果有两个或两个以上的数具有相同的质因数最大值，则找出其中的最小值。
**例:**

```
Input : N = 10
Output : 6
Number of prime factor of:
1 : 0
2 : 1
3 : 1
4 : 1
5 : 1
6 : 2
7 : 1
8 : 1
9 : 1
10 : 2
6 and 10 have maximum (2) prime factor
but 6 is smaller.

Input : N = 40
Output : 30
```

**方法 1(蛮力):**
对于 1 到 N 的每个整数，求每个整数的素因子个数，求素因子个数最大的最小数。
**方法 2(更好的方法):**
使用[筛选法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)对每个小于 n 的数的质因数进行计数，找出计数最大的最小数。
以下是本办法的实施:

## C++

```
// C++ program to find integer having maximum number
// of prime factor in first N natural numbers.
#include<bits/stdc++.h>

using namespace std;

// Return smallest number having maximum
// prime factors.
int maxPrimefactorNum(int N)
{
    int arr[N + 5];
    memset(arr, 0, sizeof(arr));

    // Sieve of eratosthenes method to count
    // number of prime factors.
    for (int i = 2; i*i <= N; i++)
    {
        if (!arr[i])
            for (int j = 2*i; j <= N; j+=i)
                arr[j]++;

        arr[i] = 1;
    }

    int maxval = 0, maxint = 1;

    // Finding number having maximum number
    // of prime factor.
    for (int i = 1; i <= N; i++)
    {
        if (arr[i] > maxval)
        {
            maxval = arr[i];
            maxint = i;
        }
    }

    return maxint;
}

// Driven Program
int main()
{
    int N = 40;
    cout << maxPrimefactorNum(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find integer having maximum number
// of prime factor in first N natural numbers.
import java.util.Arrays;
public class GFG {

// Return smallest number having maximum
// prime factors.
    static int maxPrimefactorNum(int N) {
        int arr[] = new int[N + 5];
        Arrays.fill(arr, 0);

        // Sieve of eratosthenes method to count
        // number of prime factors.
        for (int i = 2; i * i <= N; i++) {
            if (arr[i] == 0) {
                for (int j = 2 * i; j <= N; j += i) {
                    arr[j]++;
                }
            }

            arr[i] = 1;
        }

        int maxval = 0, maxint = 1;

        // Finding number having maximum number
        // of prime factor.
        for (int i = 1; i <= N; i++) {
            if (arr[i] > maxval) {
                maxval = arr[i];
                maxint = i;
            }
        }

        return maxint;
    }
// Driver program

    public static void main(String[] args) {
        int N = 40;
        System.out.println(maxPrimefactorNum(N));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find integer having
# maximum number of prime factor in first
# N natural numbers.
from math import sqrt

# Return smallest number having maximum
# prime factors.
def maxPrimefactorNum(N):
    arr = [0 for i in range(N + 5)]

    # Sieve of eratosthenes method to
    # count number of prime factors.
    for i in range(2, int(sqrt(N)) + 1, 1):
        if (arr[i] == 0):
            for j in range(2 * i, N + 1, i):
                arr[j] += 1

        arr[i] = 1

    maxval = 0
    maxint = 1

    # Finding number having maximum
    # number of prime factor.
    for i in range(1, N + 1, 1):
        if (arr[i] > maxval):
            maxval = arr[i]
            maxint = i

    return maxint

# Driver Code
if __name__ == '__main__':
    N = 40
    print(maxPrimefactorNum(N))

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# program to find integer having
// maximum number of prime factor in
// first N natural numbers.
using System;

class GFG
{

// Return smallest number having
// prime factors.
static int maxPrimefactorNum(int N)
{
    int []arr = new int[N + 5];

    // Sieve of eratosthenes method to
    // count number of prime factors.
    for (int i = 2; i * i <= N; i++)
    {
        if (arr[i] == 0)
        {
            for (int j = 2 * i; j <= N; j += i)
            {
                arr[j]++;
            }
        }

        arr[i] = 1;
    }

    int maxval = 0, maxint = 1;

    // Finding number having maximum
    // number of prime factor.
    for (int i = 1; i <= N; i++)
    {
        if (arr[i] > maxval)
        {
            maxval = arr[i];
            maxint = i;
        }
    }

    return maxint;
}

// Driver Code
public static void Main()
{
    int N = 40;
    Console.WriteLine(maxPrimefactorNum(N));
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find integer having
// maximum number of prime factor in
// first N natural numbers.

// Return smallest number having
// maximum prime factors.
function maxPrimefactorNum($N)
{
    $arr[$N + 5] = array();
    $arr = array_fill(0, $N + 1, NULL);

    // Sieve of eratosthenes method to count
    // number of prime factors.
    for ($i = 2; ($i * $i) <= $N; $i++)
    {
        if (!$arr[$i])
            for ($j = 2 * $i; $j <= $N; $j += $i)
                $arr[$j]++;

        $arr[$i] = 1;
    }

    $maxval = 0;
    $maxint = 1;

    // Finding number having maximum
    // number of prime factor.
    for ($i = 1; $i <= $N; $i++)
    {
        if ($arr[$i] > $maxval)
        {
            $maxval = $arr[$i];
            $maxint = $i;
        }
    }

    return $maxint;
}

// Driver Code
$N = 40;
echo maxPrimefactorNum($N), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript program to find integer having maximum number
// of prime factor in first N natural numbers.

// Return smallest number having maximum
// prime factors.
function maxPrimefactorNum(N) {
    var arr = Array.from({length: N + 5}, (_, i) => 0);

    // Sieve of eratosthenes method to count
    // number of prime factors.
    for (i = 2; i * i <= N; i++) {
        if (arr[i] == 0) {
            for (j = 2 * i; j <= N; j += i) {
                arr[j]++;
            }
        }

        arr[i] = 1;
    }

    var maxval = 0, maxvar = 1;

    // Finding number having maximum number
    // of prime factor.
    for (i = 1; i <= N; i++) {
        if (arr[i] > maxval) {
            maxval = arr[i];
            maxvar = i;
        }
    }

    return maxvar;
}
// Driver program
var N = 40;
document.write(maxPrimefactorNum(N));

// This code contributed by Princi Singh
</script>
```

**输出:**

```
30
```

**方法 3(有效方法):**
使用[筛选](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成 N 之前的所有素数。现在，将连续的素数(从第一个素数开始)一个接一个地相乘，直到乘积小于 n。
下面是这种方法的实现:

## C++

```
// C++ program to find integer having maximum number
// of prime factor in first N natural numbers
#include<bits/stdc++.h>

using namespace std;

// Return smallest number having maximum prime factors.
int maxPrimefactorNum(int N)
{
    bool arr[N + 5];
    memset(arr, true, sizeof(arr));

    // Sieve of eratosthenes
    for (int i = 3; i*i <= N; i += 2)
    {
        if (arr[i])
            for (int j = i*i; j <= N; j+=i)
                arr[j] = false;
    }

    // Storing prime numbers.
    vector<int> prime;
    prime.push_back(2);

    for(int i = 3; i <= N; i += 2)
        if(arr[i])
            prime.push_back(i);

    // Generating number having maximum prime factors.
    int i = 0, ans = 1;
    while (ans*prime[i] <= N && i < prime.size())
    {
        ans *= prime[i];
        i++;
    }

    return ans;
}

// Driven Program
int main()
{
    int N = 40;
    cout << maxPrimefactorNum(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find integer having maximum number
// of prime factor in first N natural numbers
import java.util.Vector;

public class GFG {

// Return smallest number having maximum prime factors.
    static int maxPrimefactorNum(int N) {
        //default value of boolean is false
        boolean arr[] = new boolean[N + 5];

        // Sieve of eratosthenes
        for (int i = 3; i * i <= N; i += 2) {
            if (!arr[i]) {
                for (int j = i * i; j <= N; j += i) {
                    arr[j] = true;
                }
            }
        }

        // Storing prime numbers.
        Vector<Integer> prime = new Vector<>();
        prime.add(prime.size(), 2);
        for (int i = 3; i <= N; i += 2) {
            if (!arr[i]) {
                prime.add(prime.size(), i);
            }
        }

        // Generating number having maximum prime factors.
        int i = 0, ans = 1;
        while (ans * prime.get(i) <= N && i < prime.size()) {
            ans *= prime.get(i);
            i++;
        }

        return ans;
    }
// Driver program

    public static void main(String[] args) {
        int N = 40;
        System.out.println(maxPrimefactorNum(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find integer having
# maximum number of prime factor in first
# N natural numbers

# Return smallest number having
# maximum prime factors.
def maxPrimefactorNum(N):

    arr = [True] * (N + 5);

    # Sieve of eratosthenes
    i = 3;
    while (i * i <= N):
        if (arr[i]):
            for j in range(i * i, N + 1, i):
                arr[j] = False;
        i += 2;

    # Storing prime numbers.
    prime = [];
    prime.append(2);

    for i in range(3, N + 1, 2):
        if(arr[i]):
            prime.append(i);

    # Generating number having maximum
    # prime factors.
    i = 0;
    ans = 1;
    while (ans * prime[i] <= N and
                    i < len(prime)):
        ans *= prime[i];
        i += 1;

    return ans;

# Driver Code
N = 40;
print(maxPrimefactorNum(N));

# This code is contributed by mits
```

## C#

```
// C# program to find integer having maximum number
// of prime factor in first N natural numbers
using System;
using System.Collections;

class GFG {

    // Return smallest number having maximum prime factors.
    static int maxPrimefactorNum(int N)
    {
        //default value of boolean is false
        bool []arr = new bool[N + 5];
        int i ;

        // Sieve of eratosthenes
        for (i = 3; i * i <= N; i += 2)
        {
            if (!arr[i])
            {
                for (int j = i * i; j <= N; j += i)
                {
                    arr[j] = true;
                }
            }
        }

        // Storing prime numbers.
        ArrayList prime = new ArrayList();
        prime.Add(2);
        for (i = 3; i <= N; i += 2)
        {
            if (!arr[i])
            {
                prime.Add(i);
            }
        }

        // Generating number having
        // maximum prime factors.
        int ans = 1;
        i = 0;
        while (ans * (int)prime[i] <= N && i < prime.Count)
        {
            ans *= (int)prime[i];
            i++;
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int N = 40;
        Console.Write(maxPrimefactorNum(N));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find integer having maximum number
// of prime factor in first N natural numbers

// Return smallest number having
// maximum prime factors.
function maxPrimefactorNum($N)
{
    $arr = array_fill(0, $N + 5, true);

    // Sieve of eratosthenes
    for ($i = 3; $i * $i <= $N; $i += 2)
    {
        if ($arr[$i])
            for ($j = $i * $i; $j <= $N; $j += $i)
                $arr[$j] = false;
    }

    // Storing prime numbers.
    $prime = array();
    array_push($prime, 2);

    for($i = 3; $i <= $N; $i += 2)
        if($arr[$i])
            array_push($prime, $i);

    // Generating number having maximum
    // prime factors.
    $i = 0;
    $ans = 1;
    while ($ans * $prime[$i] <= $N &&
                  $i < count($prime))
    {
        $ans *= $prime[$i];
        $i++;
    }

    return $ans;
}

// Driver Code
$N = 40;
print(maxPrimefactorNum($N));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // integer having maximum number
    // of prime factor in first
    // N natural numbers

    // Return smallest number having
    // maximum prime factors.
    function maxPrimefactorNum(N)
    {
        // default value of boolean is false
        let arr = new Array(N + 5);
        arr.fill(false);
        let i ;

        // Sieve of eratosthenes
        for (i = 3; i * i <= N; i += 2)
        {
            if (!arr[i])
            {
                for (let j = i * i; j <= N; j += i)
                {
                    arr[j] = true;
                }
            }
        }

        // Storing prime numbers.
        let prime = [];
        prime.push(2);
        for (i = 3; i <= N; i += 2)
        {
            if (!arr[i])
            {
                prime.push(i);
            }
        }

        // Generating number having
        // maximum prime factors.
        let ans = 1;
        i = 0;
        while (ans * prime[i] <= N && i < prime.length)
        {
            ans *= prime[i];
            i++;
        }

        return ans;
    }

    let N = 40;
      document.write(maxPrimefactorNum(N));

</script>
```

**输出:**

```
30
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。