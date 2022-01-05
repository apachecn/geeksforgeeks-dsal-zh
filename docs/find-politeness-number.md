# 找到一个数字的礼貌

> 原文:[https://www.geeksforgeeks.org/find-politeness-number/](https://www.geeksforgeeks.org/find-politeness-number/)

给定一个整数 n .找到数字 **n** 的礼貌。一个数的礼貌性被定义为它可以被表达为连续整数之和的方式的数量。

示例:

```
Input: n = 15
Output: 3
Explanation:
There are only three ways to express
15 as sum of consecutive integers i.e.,
15 = 1 + 2 + 3 + 4 + 5
15 = 4 + 5 + 6
15 = 7 + 8
Hence answer is 3

Input: n = 9;
Output:  2
There are two ways of representation:
9 = 2 + 3 + 4
9 = 4 + 5
```

We strongly recommend that you click here and practice it, before moving on to the solution.

**天真的方法:**

一个循环一个循环地运行，找到每一个连续整数的和，直到 n。这种方法的时间复杂度将是 O(n <sup>2</sup> ，这对于大的 n 值是不够的

**高效** **进场:**

使用因式分解。我们对 n 进行因子分解，计算奇数因子的数量。奇数因子的总数(除 1 外)等于该数的礼貌度。这个事实的证明请参考[这个](https://en.wikipedia.org/wiki/Polite_number#Construction_of_polite_representations_from_odd_divisors)。一般来说，如果一个数可以表示为 a<sup>p</sup>* b<sup>q</sup>* c<sup>r</sup>…其中 a、b、c、…是 n 的质因数，如果 a = 2(偶数)，则丢弃它，并计算可以写成**[(q+1)*(r+1)*…]–1**(这里减去 1，因为不允许表示中有单个项)。
以上公式是如何工作的？事实是，如果一个数表示为 a<sup>p</sup>* b<sup>q</sup>* c<sup>r</sup>…其中 a、b、c、…是 n 的素因子，那么一个数的除数就是(p+1)*(q+1)*(r+1) ……
为了简化，设一个因子，这个数表示为 a <sup>p</sup> 。除数是 1，a，a <sup>2</sup> ，…。a <sup>p</sup> 。除数是 p+1。现在我们来看一个稍微复杂一点的案例 a <sup>p</sup> b <sup>p</sup> 。除数为:
1，a，a <sup>2</sup> ，…。a<sup>p</sup>T33】b、ba、ba <sup>2</sup> ，…。ba<sup>p</sup>T38】b<sup>2</sup>，b <sup>2</sup> a，b <sup>2</sup> a <sup>2</sup> ，…。b<sup>2</sup>a<sup>p</sup>
…………。
………………。
b <sup>q</sup> ，b <sup>q</sup> a，b <sup>q</sup> a <sup>2</sup> ，…。b<sup>q</sup>a<sup>p</sup>T66】以上条款的计数为(p+1)*(q+1)。同样，我们可以证明更多的质因数。
**图解:**对于 n = 90，素因子分解如下:-
=>90 = 2 * 3<sup>2</sup>* 5<sup>1</sup>。奇质因数 3、5 的幂分别是 2 和 1。将上述公式应用为:(2 + 1) * (1 + 1) -1 = 5。因此 5 将是答案。我们可以核对一下。所有奇数因子都是 3、5、9、15 和 45。
以下是上述步骤的程序:

## C++

```
// C+ program to find politeness of number
#include <iostream>
using namespace std;

// A function to count all odd prime factors
// of a given number n
int countOddPrimeFactors(int n)
{
    int result = 1;

    // Eliminate all even prime
    // factor of number of n
    while (n % 2 == 0)
        n /= 2;

    // n must be odd at this point,
    // so iterate for only
    // odd numbers till sqrt(n)
    for (int i = 3; i * i <= n; i += 2) {
        int divCount = 0;

        // if i divides n, then start counting of
        // Odd divisors
        while (n % i == 0) {
            n /= i;
            ++divCount;
        }

        result *= divCount + 1;
    }

    // If n odd prime still remains then count it
    if (n > 2)
        result *= 2;

    return result;
}

int politness(int n)
{
    return countOddPrimeFactors(n) - 1;
}

// Driver program to test above function
int main()
{
    int n = 90;
    cout << "Politness of " << n << " = "
         << politness(n) << "\n";

    n = 15;
    cout << "Politness of " << n << " = "
         << politness(n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find politeness of a number

public class Politeness {
    // A function to count all odd prime factors
    // of a given number n
    static int countOddPrimeFactors(int n)
    {
        int result = 1;

        // Eliminate all even prime
        // factor of number of n
        while (n % 2 == 0)
            n /= 2;

        // n must be odd at this point, so iterate
        // for only odd numbers till sqrt(n)
        for (int i = 3; i * i <= n; i += 2) {
            int divCount = 0;

            // if i divides n, then start counting of
            // Odd divisors
            while (n % i == 0) {
                n /= i;
                ++divCount;
            }

            result *= divCount + 1;
        }
        // If n odd prime still remains then count it
        if (n > 2)
            result *= 2;

        return result;
    }

    static int politness(int n)
    {
        return countOddPrimeFactors(n) - 1;
    }

    public static void main(String[] args)
    {
        int n = 90;
        System.out.println("Politness of " + n + " = "
                           + politness(n));

        n = 15;
        System.out.println("Politness of " + n + " = "
                           + politness(n));
    }
}

// This code is contributed by Saket Kumar
```

## 计算机编程语言

```
# Python program to find politeness of number

# A function to count all odd prime factors
# of a given number n
def countOddPrimeFactors(n) :
    result = 1;

    # Eliminate all even prime factor of
    # number of n
    while (n % 2 == 0) :
        n /= 2

    # n must be odd at this point, so iterate
    # for only odd numbers till sqrt(n)
    i = 3
    while i * i <= n :
        divCount = 0

        # if i divides n, then start counting
        # of Odd divisors
        while (n % i == 0) :
            n /= i
            divCount = divCount + 1

        result = result * divCount + 1
        i = i + 2

    # If n odd prime still remains then count it
    if (n > 2) :
        result = result * 2

    return result

def politness( n) :
    return countOddPrimeFactors(n) - 1;

# Driver program to test above function
n = 90
print "Politness of ", n, " = ", politness(n)
n = 15
print "Politness of ", n, " = ", politness(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find politeness of a number.
using System;

public class GFG {

    // A function to count all odd prime
    // factors of a given number n
    static int countOddPrimeFactors(int n)
    {

        int result = 1;

        // Eliminate all even prime factor
        // of number of n
        while (n % 2 == 0)
            n /= 2;

        // n must be odd at this point, so
        // iterate for only odd numbers
        // till sqrt(n)
        for (int i = 3; i * i <= n; i += 2)
        {
            int divCount = 0;

            // if i divides n, then start
            // counting of Odd divisors
            while (n % i == 0) {
                n /= i;
                ++divCount;
            }

            result *= divCount + 1;
        }

        // If n odd prime still remains
        // then count it
        if (n > 2)
            result *= 2;

        return result;
    }

    static int politness(int n)
    {
        return countOddPrimeFactors(n) - 1;
    }

    // Driver code
    public static void Main()
    {
        int n = 90;
        Console.WriteLine("Politness of "
               + n + " = " + politness(n));

        n = 15;
        Console.WriteLine("Politness of "
               + n + " = " + politness(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// politeness of number

// A function to count all
// odd prime factors of a
// given number n
function countOddPrimeFactors($n)
{
    $result = 1;

    // Eliminate all even prime
    // factor of number of n
    while($n % 2 == 0)
        $n /= 2;

    // n must be odd at this
    // point, so iterate for only
    // odd numbers till sqrt(n)
    for ($i = 3; $i * $i <= $n; $i += 2)
    {
        $divCount = 0;

        // if i divides n, then
        // start counting of
        // Odd divisors
        while($n % $i == 0)
        {
            $n /= $i;
            ++$divCount;
        }

        $result *= $divCount + 1;
    }

    // If n odd prime still
    // remains then count it
    if ($n > 2)
        $result *= 2;

    return $result;
}

function politness($n)
{
    return countOddPrimeFactors($n) - 1;
}

    // Driver Code
    $n = 90;
    echo "Politness of " , $n , " = "
               , politness($n), "\n";

    $n = 15;
    echo "Politness of " , $n , " = "
               , politness($n) ,"\n";

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

    // A function to count all odd prime
    // factors of a given number n
    function countOddPrimeFactors(n)
    {

        let result = 1;

        // Eliminate all even prime factor
        // of number of n
        while (n % 2 == 0)
            n /= 2;

        // n must be odd at this point, so
        // iterate for only odd numbers
        // till sqrt(n)
        for (let i = 3; i * i <= n; i += 2)
        {
            let divCount = 0;

            // if i divides n, then start
            // counting of Odd divisors
            while (n % i == 0) {
                n /= i;
                ++divCount;
            }

            result *= divCount + 1;
        }

        // If n odd prime still remains
        // then count it
        if (n > 2)
            result *= 2;

        return result;
    }

    function politness(n)
    {
        return countOddPrimeFactors(n) - 1;
    }

// Driver Code
     let n = 90;
        document.write("Politness of "
               + n + " = " + politness(n) + "<br />");

        n = 15;
        document.write("Politness of "
               + n + " = " + politness(n));

// This code is contributed by splevel62.
</script>
```

```
Output:
Politness of 90 = 5
Politness of 15 = 3
```

**时间复杂度:** O(sqrt(n))
**辅助空间:** O(1)
**参考:** [维基百科](https://en.wikipedia.org/wiki/Polite_number)

**另一种**高效**方法:**

计算给定长度域[2，sqrt(2*n)]是否可以生成 AP。计算直到 sqrt(2*n)的长度的原因是-

最大长度将为 AP 1，2，3…

```
Length for this AP is -

n= ( len * (len+1) ) / 2

len2 + len - (2*n) =0

so len≈sqrt(2*n) 
```

因此，我们可以检查从 1 到 sqrt(2*n)每个镜头，看看是否可以用这个镜头生成 AP。获得 AP 第一项的公式是–

```
n= ( len/2) * ( (2*A1) + len-1 )
```

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <iostream>
#include <math.h>
using namespace std;

// Function to find politeness
int politness(int n)
{
    int count = 0;

    // sqrt(2*n) as max length
    // will be when the sum starts
    // from 1
    // which follows the equation n^2 - n - (2*sum) = 0
    for (int i = 2; i <= sqrt(2 * n); i++) {
        int a;
        if ((2 * n) % i != 0)
            continue;
        a = 2 * n;
        a /= i;
        a -= (i - 1);
        if (a % 2 != 0)
            continue;
        a /= 2;
        if (a > 0) {
            count++;
        }
    }
    return count;
}

// Driver program to test above function
int main()
{
    int n = 90;
    cout << "Politness of " << n << " = " << politness(n)
         << "\n";

    n = 15;
    cout << "Politness of " << n << " = " << politness(n)
         << "\n";
    return 0;
}

// This code is contributed by Prajjwal Chittori
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.Math;
public class Main {

  // Function to find politeness
  static int politness(int n)
  {
    int count = 0;

    // sqrt(2*n) as max length
    // will be when the sum
    // starts from 1
    // which follows the
    // equation n^2 - n - (2*sum) = 0
    for (int i = 2; i <= Math.sqrt(2 * n); i++) {
      int a;
      if ((2 * n) % i != 0)
        continue;
      a = 2 * n;
      a /= i;
      a -= (i - 1);
      if (a % 2 != 0)
        continue;
      a /= 2;
      if (a > 0) {
        count++;
      }
    }
    return count;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int n = 90;
    System.out.println("Politness of " + n + " = "
                       + politness(n));

    n = 15;
    System.out.println("Politness of " + n + " = "
                       + politness(n));
  }
}

// This code is contributed by Prajjwal Chittori
```

## 计算机编程语言

```
# python program for the above approach
import math

# Function to find politeness
def politness(n):
    count = 0

    # sqrt(2*n) as max length will be
    # when the sum starts from 1
    # which follows the equation
    # n^2 - n - (2*sum) = 0
    for i in range(2, int(math.sqrt(2 * n)) + 1):
        if ((2 * n) % i != 0):
            continue
        a = 2 * n
        a = a / i
        a = a - (i - 1)
        if (a % 2 != 0):
            continue
        a /= 2
        if (a > 0):
            count = count + 1
    return count

# Driver program to test above function
n = 90
print "Politness of ", n, " = ", politness(n)
n = 15
print "Politness of ", n, " = ", politness(n)

# This code is contributed by Prajjwal Chittori
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

  // Function to find politeness
  static int politness(int n)
  {
    int count = 0;

    // sqrt(2*n) as max length
    // will be when the sum
    // starts from 1
    // which follows the
    // equation n^2 - n - (2*sum) = 0
    for (int i = 2; i <= Math.Sqrt(2 * n); i++) {
      int a;
      if ((2 * n) % i != 0)
        continue;
      a = 2 * n;
      a /= i;
      a -= (i - 1);
      if (a % 2 != 0)
        continue;
      a /= 2;
      if (a > 0) {
        count++;
      }
    }
    return count;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int n = 90;
    Console.WriteLine("Politness of " + n + " = "
                       + politness(n));

    n = 15;
    Console.WriteLine("Politness of " + n + " = "
                       + politness(n));
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

  // Function to find politeness
 function politness(n)
  {
    let count = 0;

    // sqrt(2*n) as max length
    // will be when the sum
    // starts from 1
    // which follows the
    // equation n^2 - n - (2*sum) = 0
    for (let i = 2; i <= Math.sqrt(2 * n); i++) {
      let a;
      if ((2 * n) % i != 0)
        continue;
      a = 2 * n;
      a = Math.floor(a / i);
      a -= (i - 1);
      if (a % 2 != 0)
        continue;
      a = Math.floor(a / 2);
      if (a > 0) {
        count++;
      }
    }
    return count;
  }

// Driver Code

     let n = 90;
    document.write("Politness of " + n + " = "
                       + politness(n) + "<br/>");

    n = 15;
    document.write("Politness of " + n + " = "
                       + politness(n));

</script>
```

**Output**

```
Politness of 90 = 5
Politness of 15 = 3
```

**时间复杂度** : O(sqrt(2*n)) ≈ O(sqrt(n)) **辅助空间:** O(1)

本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。