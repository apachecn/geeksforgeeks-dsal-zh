# 前 n 个自然数的 LCM

> 原文:[https://www.geeksforgeeks.org/lcm-first-n-natural-numbers/](https://www.geeksforgeeks.org/lcm-first-n-natural-numbers/)

给定数字 n，使得 1 <= N <= 10^6，任务是找到前 n 个自然数的 LCM。

**示例:**

```
Input : n = 5
Output : 60

Input : n = 6
Output : 60

Input : n = 7
Output : 420 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/smallest-divisible-number/1)

我们在下面的文章中讨论了一个简单的解决方案。
[【可被前 n 个数字除尽的最小数字】](https://www.geeksforgeeks.org/smallest-number-divisible-first-n-numbers/)
上述解决方案适用于单个输入。但是如果我们有多个输入，使用厄拉多塞的[筛来存储所有质因数是一个好主意。我们知道，如果 LCM(a，b) = X，那么 a 或 b 的任何质因数也将是‘X’的质因数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

1.  用 1 初始化 lcm 变量
2.  使用埃拉托色尼筛生成所有小于 10^6 素数并存储在数组素数中。
3.  求小于给定数且等于素数幂的最大数。
4.  然后将这个数字乘以 lcm 变量。
5.  重复步骤 3 和 4，直到素数小于给定的数。

插图:

```
For example, if n = 10 
8 will be the first number which is equal to 2^3
then 9 which is equal to 3^2
then 5 which is equal to 5^1
then 7 which is equal to 7^1
Finally, we multiply those numbers 8*9*5*7 = 2520
```

以下是上述想法的实现。

## C++

```
// C++ program to find LCM of First N Natural Numbers.
#include <bits/stdc++.h>
#define MAX 100000
using namespace std;

// array to store all prime less than and equal to 10^6
vector<int> primes;

// utility function for sieve of sieve of Eratosthenes
void sieve()
{
    bool isComposite[MAX] = { false };
    for (int i = 2; i * i <= MAX; i++)
    {
        if (isComposite[i] == false)
            for (int j = 2; j * i <= MAX; j++)
                isComposite[i * j] = true;
    }

    // Store all prime numbers in vector primes[]
    for (int i = 2; i <= MAX; i++)
        if (isComposite[i] == false)
            primes.push_back(i);
}

// Function to find LCM of first n Natural Numbers
long long LCM(int n)
{
    long long lcm = 1;
    for (int i = 0;
         i < primes.size() && primes[i] <= n;
         i++)
    {
        // Find the highest power of prime, primes[i]
        // that is less than or equal to n
        int pp = primes[i];
        while (pp * primes[i] <= n)
            pp = pp * primes[i];

        // multiply lcm with highest power of prime[i]
        lcm *= pp;
        lcm %= 1000000007;
    }
    return lcm;
}

// Driver code
int main()
{
    // build sieve
    sieve();
    int N = 7;

    // Function call
    cout << LCM(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCM of First N Natural Numbers.
import java.util.*;

class GFG
{
    static int MAX = 100000;

    // array to store all prime less than and equal to 10^6
    static ArrayList<Integer> primes
        = new ArrayList<Integer>();
    // utility function for sieve of sieve of Eratosthenes
    static void sieve()
    {
        boolean[] isComposite = new boolean[MAX + 1];
        for (int i = 2; i * i <= MAX; i++)
        {
            if (isComposite[i] == false)
                for (int j = 2; j * i <= MAX; j++)
                    isComposite[i * j] = true;
        }

        // Store all prime numbers in vector primes[]
        for (int i = 2; i <= MAX; i++)
            if (isComposite[i] == false)
                primes.add(i);
    }

    // Function to find LCM of first n Natural Numbers
    static long LCM(int n)
    {
        long lcm = 1;
        for (int i = 0;
             i < primes.size() && primes.get(i) <= n;
             i++)
        {
            // Find the highest power of prime, primes[i]
            // that is less than or equal to n
            int pp = primes.get(i);
            while (pp * primes.get(i) <= n)
                pp = pp * primes.get(i);

            // multiply lcm with highest power of prime[i]
            lcm *= pp;
            lcm %= 1000000007;
        }
        return lcm;
    }

    // Driver code
    public static void main(String[] args)
    {
        sieve();
        int N = 7;

        // Function call
        System.out.println(LCM(N));
    }
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find LCM of
# First N Natural Numbers.
MAX = 100000

# array to store all prime less
# than and equal to 10^6
primes = []

# utility function for
# sieve of Eratosthenes

def sieve():

    isComposite = [False]*(MAX+1)
    i = 2
    while (i * i <= MAX):
        if (isComposite[i] == False):
            j = 2
            while (j * i <= MAX):
                isComposite[i * j] = True
                j += 1
        i += 1

    # Store all prime numbers in
    # vector primes[]
    for i in range(2, MAX+1):
        if (isComposite[i] == False):
            primes.append(i)

# Function to find LCM of
# first n Natural Numbers

def LCM(n):

    lcm = 1
    i = 0
    while (i < len(primes) and primes[i] <= n):
        # Find the highest power of prime,
        # primes[i] that is less than or
        # equal to n
        pp = primes[i]
        while (pp * primes[i] <= n):
            pp = pp * primes[i]

        # multiply lcm with highest
        # power of prime[i]
        lcm *= pp
        lcm %= 1000000007
        i += 1
    return lcm

# Driver code
sieve()
N = 7

# Function call
print(LCM(N))

# This code is contributed by mits
```

## C#

```
// C# program to find LCM of First N
// Natural Numbers.
using System.Collections;
using System;

class GFG {
    static int MAX = 100000;

    // array to store all prime less than
    // and equal to 10^6
    static ArrayList primes = new ArrayList();

    // utility function for sieve of
    // sieve of Eratosthenes
    static void sieve()
    {
        bool[] isComposite = new bool[MAX + 1];
        for (int i = 2; i * i <= MAX; i++)
        {
            if (isComposite[i] == false)
                for (int j = 2; j * i <= MAX; j++)
                    isComposite[i * j] = true;
        }

        // Store all prime numbers in vector primes[]
        for (int i = 2; i <= MAX; i++)
            if (isComposite[i] == false)
                primes.Add(i);
    }

    // Function to find LCM of first
    // n Natural Numbers
    static long LCM(int n)
    {
        long lcm = 1;
        for (int i = 0;
             i < primes.Count && (int)primes[i] <= n;
             i++)
        {
            // Find the highest power of prime, primes[i]
            // that is less than or equal to n
            int pp = (int)primes[i];
            while (pp * (int)primes[i] <= n)
                pp = pp * (int)primes[i];

            // multiply lcm with highest power of prime[i]
            lcm *= pp;
            lcm %= 1000000007;
        }
        return lcm;
    }

    // Driver code
    public static void Main()
    {
        sieve();
        int N = 7;

        // Function call
        Console.WriteLine(LCM(N));
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
    // Javascript program to find LCM of First N
    // Natural Numbers.

    let MAX = 100000;

    // array to store all prime less than
    // and equal to 10^6
    let primes = [];

    // utility function for sieve of
    // sieve of Eratosthenes
    function sieve()
    {
        let isComposite = new Array(MAX + 1);
        isComposite.fill(false);
        for (let i = 2; i * i <= MAX; i++)
        {
            if (isComposite[i] == false)
                for (let j = 2; j * i <= MAX; j++)
                    isComposite[i * j] = true;
        }

        // Store all prime numbers in vector primes[]
        for (let i = 2; i <= MAX; i++)
            if (isComposite[i] == false)
                primes.push(i);
    }

    // Function to find LCM of first
    // n Natural Numbers
    function LCM(n)
    {
        let lcm = 1;
        for (let i = 0;
             i < primes.length && primes[i] <= n;
             i++)
        {
            // Find the highest power of prime, primes[i]
            // that is less than or equal to n
            let pp = primes[i];
            while (pp * primes[i] <= n)
                pp = pp * primes[i];

            // multiply lcm with highest power of prime[i]
            lcm *= pp;
            lcm %= 1000000007;
        }
        return lcm;
    }

    sieve();
    let N = 7;

    // Function call
    document.write(LCM(N));

// This code is contributed by decode2207.
</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find LCM of
// First N Natural Numbers.
$MAX = 100000;

// array to store all prime less
// than and equal to 10^6
$primes = array();

// utility function for
// sieve of Eratosthenes
function sieve()
{
    global $MAX, $primes;
    $isComposite = array_fill(0, $MAX, false);
    for ($i = 2; $i * $i <= $MAX; $i++)
    {
        if ($isComposite[$i] == false)
            for ($j = 2; $j * $i <= $MAX; $j++)
                $isComposite[$i * $j] = true;
    }

    // Store all prime numbers in
    // vector primes[]
    for ($i = 2; $i <= $MAX; $i++)
        if ($isComposite[$i] == false)
            array_push($primes, $i);
}

// Function to find LCM of
// first n Natural Numbers
function LCM($n)
{
    global $MAX, $primes;
    $lcm = 1;
    for ($i = 0; $i < count($primes) &&
                 $primes[$i] <= $n; $i++)
    {
        // Find the highest power of prime,
        // primes[i] that is less than or
        // equal to n
        $pp = $primes[$i];
        while ($pp * $primes[$i] <= $n)
            $pp = $pp * $primes[$i];

        // multiply lcm with highest
        // power of prime[i]
        $lcm *= $pp;
        $lcm %= 1000000007;
    }
    return $lcm;
}

// Driver code
sieve();
$N = 7;

// Function call
echo LCM($N);

// This code is contributed by mits
?>
```

**Output**

```
420
```

**另一种方法:**

这个想法是，如果数字小于 3，那么返回数字。如果该数大于 2，则求 n 的 LCM，n-1

*   假设 x=LCM(n，n-1)
*   同样 x=LCM(x，n-2)
*   同样 x=LCM(x，n-3) …
*   。
*   。
*   同样 x=LCM(x，1) …

现在结果是 x。

为了找到 LCM(a，b)，我们使用了一个函数 hcf(a，b)，它将返回(a，b)的 hcf

我们知道 **LCM(a，b)= (a*b)/HCF(a，b)**

插图:

```
For example, if n = 7 
function call lcm(7,6)
now lets say a=7 , b=6

Now , b!= 1 Hence 
a=lcm(7,6) = 42 and b=6-1=5

function call lcm(42,5)
a=lcm(42,5) = 210 and b=5-1=4

function call lcm(210,4)
a=lcm(210,4) = 420 and b=4-1=3

function call lcm(420,3)
a=lcm(420,3) = 420 and b=3-1=2

function call lcm(420,2)
a=lcm(420,2) = 420 and b=2-1=1

Now b=1
Hence return a=420
```

下面是上述方法的实现

## C++

```
// C++ program to find LCM of First N Natural Numbers.
#include <bits/stdc++.h>
using namespace std;

// to calculate hcf
int hcf(int a, int b)
{
    if (b == 0)
        return a;
    return hcf(b, a % b);
}

int findlcm(int a,int b)
{
    if (b == 1)

        // lcm(a,b)=(a*b)/hcf(a,b)
        return a;

    // assign a=lcm of n,n-1
    a = (a * b) / hcf(a, b);

    // b=b-1
    b -= 1;
    return findlcm(a, b);
}

// Driver code
int main()
{
    int n = 7;
    if (n < 3)
        cout << n; // base case
    else

        // Function call
        // pass n,n-1 in function to find LCM of first n natural
        // number
        cout << findlcm(n, n - 1);

    return 0;
}

// contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCM of First N Natural Numbers
public class Main
{
  // to calculate hcf
  static int hcf(int a, int b)
  {
    if (b == 0)
      return a;
    return hcf(b, a % b);
  }

  static int findlcm(int a,int b)
  {
    if (b == 1)

      // lcm(a,b)=(a*b)/hcf(a,b)
      return a;

    // assign a=lcm of n,n-1
    a = (a * b) / hcf(a, b);

    // b=b-1
    b -= 1;
    return findlcm(a, b);
  }

  // Driver code.
  public static void main(String[] args)
  {
    int n = 7;
    if (n < 3)
      System.out.print(n); // base case
    else

      // Function call
      // pass n,n-1 in function to find LCM of first n natural
      // number
      System.out.print(findlcm(n, n - 1));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program to find LCM
# of First N Natural Numbers.

# To calculate hcf
def hcf(a, b):

    if (b == 0):
        return a

    return hcf(b, a % b)

def findlcm(a, b):

    if (b == 1):

        # lcm(a,b)=(a*b)//hcf(a,b)
        return a

    # Assign a=lcm of n,n-1
    a = (a * b) // hcf(a, b)

    # b=b-1
    b -= 1

    return findlcm(a, b)

# Driver code
n = 7

if (n < 3):
    print(n)
else:

    # Function call
    # pass n,n-1 in function
    # to find LCM of first n
    # natural number
    print(findlcm(n, n - 1))

# This code is contributed by Shubham_Singh
```

## C#

```
// C# program to find LCM of First N Natural Numbers.
using System;
class GFG {

  // to calculate hcf
  static int hcf(int a, int b)
  {
    if (b == 0)
      return a;
    return hcf(b, a % b);
  }

  static int findlcm(int a,int b)
  {
    if (b == 1)

      // lcm(a,b)=(a*b)/hcf(a,b)
      return a;

    // assign a=lcm of n,n-1
    a = (a * b) / hcf(a, b);

    // b=b-1
    b -= 1;
    return findlcm(a, b);
  }

  // Driver code
  static void Main() {
    int n = 7;
    if (n < 3)
      Console.Write(n); // base case
    else

      // Function call
      // pass n,n-1 in function to find LCM of first n natural
      // number
      Console.Write(findlcm(n, n - 1));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

    // Javascript program to find LCM of First N Natural Numbers.

    // to calculate hcf
    function hcf(a, b)
    {
        if (b == 0)
            return a;
        return hcf(b, a % b);
    }

    function findlcm(a,b)
    {
        if (b == 1)

            // lcm(a,b)=(a*b)/hcf(a,b)
            return a;

        // assign a=lcm of n,n-1
        a = (a * b) / hcf(a, b);

        // b=b-1
        b -= 1;
        return findlcm(a, b);
    }

    let n = 7;
    if (n < 3)
        document.write(n); // base case
    else

        // Function call
        // pass n,n-1 in function to find LCM of first n natural
        // number
        document.write(findlcm(n, n - 1));

</script>
```

**Output**

```
420
```

**时间复杂度:** O(nlog n)

本文由**库尔迪普·辛格(kulli_d_coder)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。