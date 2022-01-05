# 阶乘的最后一个非零数字

> 原文:[https://www . geesforgeks . org/last-非零数字-阶乘/](https://www.geeksforgeeks.org/last-non-zero-digit-factorial/)

给定一个数字 n，求 n 中最后一个非零数字！。
示例:

```
Input  : n = 5
Output : 2
5! = 5 * 4 * 3 * 2 * 1 = 120
Last non-zero digit in 120 is 2.

Input  : n = 33
Output : 4
```

一个**简单的解决方法**就是先找 n！，然后找到 n 的最后一个非零数字。由于算术溢出，这个解决方案甚至不适用于稍大的数字。
更好的解决方案是基于下面的递归公式

```
Let D(n) be the last non-zero digit in n!
If tens digit (or second last digit) of n is odd
    D(n) = 4 * D(floor(n/5)) * D(Unit digit of n) 
If tens digit (or second last digit) of n is even
    D(n) = 6 * D(floor(n/5)) * D(Unit digit of n)
```

**对**的说明**公式:**
对于小于 10 的数字，我们可以通过上面的简单解法，即先计算 n，很容易找到最后一个非零数字！，然后找到最后一个数字。
D(1) = 1，D(2) = 2，D(3) = 6，D(4) = 4，D(5) = 2，
D(6) = 2，D(7) = 4，D(8) = 2，D(9) = 8。

```
D(1) to D(9) are assumed to be precomputed.

Example 1: n = 27 [Second last digit is even]:
D(27) = 6 * D(floor(27/5)) * D(7)
      = 6 * D(5) * D(7)
      = 6 * 2 * 4 
      = 48
Last non-zero digit is  8

Example 2: n = 33 [Second last digit is odd]:
D(33) = 4 * D(floor(33/5)) * D(3)
      = 4 * D(6) * 6
      = 4 * 2 * 6
      = 48
Last non-zero digit is  8
```

****以上公式是如何工作的？**
下面的解释提供了公式背后的直觉。读者可参考[http://math . stackexchange . com/questions/130352/阶乘最后一个非零数字](http://math.stackexchange.com/questions/130352/last-non-zero-digit-of-a-factorial)获取完整证明。** 

```
14! = 14 * 13 * 12 * 11 * 10 * 9 * 8 * 7 * 
                     6 * 5 * 4 * 3 * 2 * 1

Since we are asked about last non-zero digit, 
we remove all 5's and equal number of 2's from
factors of 14!.  We get following:

14! = 14 * 13 * 12 * 11 * 2 * 9 * 8 * 7 *
                           6 * 3 * 2 * 1

Now we can get last non-zero digit by multiplying
last digits of above factors!
```

**在 n！2 的数量总是大于 5 的数量。要移除尾随的 0，我们移除 5 和相等数量的 2。
让**a**= floor(n/5)**b**= n % 5。去掉相等数量的 5 和 2 后，我们可以把问题从 n 减少！至 2 <sup>a</sup> * a！* b！
D(n)= 2<sup>a</sup>* D(a)* D(b)
**实现:**** 

## **C++**

```
// C++ program to find last non-zero digit in n!
#include<bits/stdc++.h>
using namespace std;

// Initialize values of last non-zero digit of
// numbers from 0 to 9
int dig[] = {1, 1, 2, 6, 4, 2, 2, 4, 2, 8};

int lastNon0Digit(int n)
{
     if (n < 10)
        return dig[n];

    // Check whether tens (or second last) digit
    // is odd or even
    // If n = 375, So n/10 = 37 and (n/10)%10 = 7
    // Applying formula for even and odd cases.
    if (((n/10)%10)%2 == 0)
        return (6*lastNon0Digit(n/5)*dig[n%10]) % 10;
    else
        return (4*lastNon0Digit(n/5)*dig[n%10]) % 10;
}

// Driver code
int main()
{
    int n = 14;
    cout << lastNon0Digit(n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find last
// non-zero digit in n!

class GFG
{
    // Initialize values of last non-zero digit of
    // numbers from 0 to 9
    static int dig[] = {1, 1, 2, 6, 4, 2, 2, 4, 2, 8};

    static int lastNon0Digit(int n)
    {
        if (n < 10)
            return dig[n];

        // Check whether tens (or second last)
        // digit is odd or even
        // If n = 375, So n/10 = 37 and
        // (n/10)%10 = 7 Applying formula for
        // even and odd cases.
        if (((n / 10) % 10) % 2 == 0)
            return (6 * lastNon0Digit(n / 5)
                    * dig[n % 10]) % 10;
        else
            return (4 * lastNon0Digit(n / 5)
                    * dig[n % 10]) % 10;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 14;
        System.out.print(lastNon0Digit(n));
    }
}
// This code is contributed by Anant Agarwal.
```

## **蟒蛇 3**

```
# Python program to find
# last non-zero digit in n!

# Initialize values of
# last non-zero digit of
# numbers from 0 to 9
dig= [1, 1, 2, 6, 4, 2, 2, 4, 2, 8]

def lastNon0Digit(n):
    if (n < 10):
        return dig[n]

     # Check whether tens (or second last) digit
     # is odd or even
     # If n = 375, So n/10 = 37 and (n/10)%10 = 7
     # Applying formula for even and odd cases.
    if (((n//10)%10)%2 == 0):
        return (6*lastNon0Digit(n//5)*dig[n%10]) % 10
    else:
        return (4*lastNon0Digit(n//5)*dig[n%10]) % 10
    return 0

# driver code
n = 14

print(lastNon0Digit(n))

# This code is contributed
# by Anant Agarwal.
```

## **C#**

```
// C# program to find last
// non-zero digit in n!
using System;

class GFG {

    // Initialize values of last non-zero
    // digit of numbers from 0 to 9
    static int []dig = {1, 1, 2, 6, 4, 2, 2, 4, 2, 8};

    static int lastNon0Digit(int n)
    {
        if (n < 10)
            return dig[n];

        // Check whether tens (or second
        // last) digit is odd or even
        // If n = 375, So n/10 = 37 and
        // (n/10)%10 = 7 Applying formula
        // for even and odd cases.
        if (((n / 10) % 10) % 2 == 0)
            return (6 * lastNon0Digit(n / 5) *
                    dig[n % 10]) % 10;
        else
            return (4 * lastNon0Digit(n / 5) *
                    dig[n % 10]) % 10;
    }

    // Driver code
    public static void Main ()
    {
        int n = 14;
        Console.Write(lastNon0Digit(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to find last
// non-zero digit in n!

// Initialize values of
// last non-zero digit of
// numbers from 0 to 9
$dig = array(1, 1, 2, 6, 4,
             2, 2, 4, 2, 8);

function lastNon0Digit($n)
{

    global $dig;
    if ($n < 10)
        return $dig[$n];

    // Check whether tens(or second 
    // last) digit is odd or even
    // If n = 375, So n/10 = 37 and
    // (n/10)%10 = 7
    // Applying formula for even
    // and odd cases.
    if ((($n / 10) % 10) % 2 == 0)
        return (6 * lastNon0Digit($n / 5) *
                       $dig[$n % 10]) % 10;
    else
        return (4 * lastNon0Digit($n / 5) *
                        $dig[$n % 10]) % 10;
}

// Driver code
$n = 14;
echo(lastNon0Digit($n));

// This code is contributed by Ajit.
?>
```

## **java 描述语言**

```
<script>

    // Javascript program to find
    // last non-zero digit in n!

    // Initialize values of last non-zero
    // digit of numbers from 0 to 9
    let dig = [1, 1, 2, 6, 4, 2, 2, 4, 2, 8];

    function lastNon0Digit(n)
    {
        if (n < 10)
            return dig[n];

        // Check whether tens (or second
        // last) digit is odd or even
        // If n = 375, So n/10 = 37 and
        // (n/10)%10 = 7 Applying formula
        // for even and odd cases.
        if ((parseInt(n / 10, 10) % 10) % 2 == 0)
         return (6 * lastNon0Digit(parseInt(n / 5, 10))
            * dig[n % 10]) % 10;
        else
         return (4 * lastNon0Digit(parseInt(n / 5, 10))
            * dig[n % 10]) % 10;
    }

    let n = 14;
      document.write(lastNon0Digit(n));

</script>
```

****Output**

```
2
```** 

*****基于递归的简单解决方案，具有最坏情况时间复杂度 O(nLog(n))。**T3】***

> *****进场:-*****
> 
> 1.  **假设你必须找到最后一个正数。如果有 2 和 5，那么一个数字就是 10 的倍数。他们产生一个最后一位为 0 的数字。**
> 2.  **现在我们可以做的是把每个数组元素分成最短的可被 5 整除的形式，并增加这样的出现次数。**
> 3.  **现在将每个数组元素分成可被 2 整除的最短形式，并减少这样的出现次数。这样，我们在乘法中就不考虑 2 和 5 的乘法(乘法结果中出现的 2 的个数最多总是大于 5 的个数)。**
> 4.  **现在将每个数字相乘(去掉成对的 2 和 5 后)，然后用余数乘以 10 来存储最后一个数字。**
> 5.  **现在通过(currentNumber–1)作为参数递归调用较小的数字。**

****以下是上述方法的实现:****

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

// Helper Function to return the rightmost non-zero digit
void callMeFactorialLastDigit(int n, int result[], int sumOf5)
{
  int number = n; // assaigning to new variable.
  if (number == 1)
    return; // base case

  // To store the count of times 5 can
  // divide the number.
  while (number % 5 == 0) {
    number /= 5;

    // increase count of 5
    sumOf5++;
  }

  // Divide the number by
  // 2 as much as possible
  while (sumOf5 != 0 && (number & 1) == 0) {
    number >>= 1; // dividing the number by 2
    sumOf5--;
  }

  /*multiplied result and current number(after
    removing pairs) and do modular division to get the
    last digit of the resultant number.*/
  result[0] = (result[0] * (number % 10)) % 10;

  // calling again for (currentNumber - 1)
  callMeFactorialLastDigit(n - 1, result, sumOf5);
}

int lastNon0Digit(int n)
{
  int result[] = { 1 }; // single element array.
  callMeFactorialLastDigit(n, result, 0);
  return result[0];
}

int main()
{
  cout << lastNon0Digit(7) << endl;
  cout << lastNon0Digit(12) << endl;
  return 0;
}

// This code is contributed by rameshtravel07.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    // Helper Function to return the rightmost non-zero
    // digit
    public static void
    callMeFactorialLastDigit(int n, int[] result,
                             int sumOf5)
    {
        int number = n; // assaigning to new variable.
        if (number == 1)
            return; // base case

        // To store the count of times 5 can
        // divide the number.
        while (number % 5 == 0) {
            number /= 5;
            // increase count of 5
            sumOf5++;
        }

        // Divide the number by
        // 2 as much as possible
        while (sumOf5 != 0 && (number & 1) == 0) {
            number >>= 1; // dividing the number by 2
            sumOf5--;
        }

        /*multiplied result and current number(after
        removing pairs) and do modular division to get the
        last digit of the resultant number.*/
        result[0] = (result[0] * (number % 10)) % 10;
        // calling again for (currentNumber - 1)
        callMeFactorialLastDigit(n - 1, result, sumOf5);
    }

    public static int lastNon0Digit(int n)
    {
        int[] result = { 1 }; // single element array.
        callMeFactorialLastDigit(n, result, 0);
        return result[0];
    }

    public static void main(String[] args)
    {
        System.out.println(lastNon0Digit(7)); // 3040
        System.out.println(lastNon0Digit(12)); // 479001600
    }
}
//This code is contributed by KaaL-EL.
```

## **蟒蛇 3**

```
# Helper Function to return the rightmost non-zero digit
def callMeFactorialLastDigit(n, result, sumOf5):
    number = n # assaigning to new variable.
    if number == 1:
        return # base case

    # To store the count of times 5 can
    # divide the number.
    while (number % 5 == 0):
        number = int(number / 5)
        # increase count of 5
        sumOf5 += 1

    # Divide the number by
    # 2 as much as possible
    while (sumOf5 != 0 and (number & 1) == 0):
        number >>= 1 # dividing the number by 2
        sumOf5 -= 1

    """multiplied result and current number(after
    removing pairs) and do modular division to get the
    last digit of the resultant number."""
    result[0] = (result[0] * (number % 10)) % 10
    # calling again for (currentNumber - 1)
    callMeFactorialLastDigit(n - 1, result, sumOf5)

def lastNon0Digit(n):
    result = [ 1 ] # single element array.
    callMeFactorialLastDigit(n, result, 0)
    return result[0]

print(lastNon0Digit(7)) # 3040
print(lastNon0Digit(12)) # 479001600

# This code is contributed by suresh07.
```

## **C#**

```
using System;
class GFG {

    // Helper Function to return the rightmost non-zero
    // digit
    static void
    callMeFactorialLastDigit(int n, int[] result,
                             int sumOf5)
    {
        int number = n; // assaigning to new variable.
        if (number == 1)
            return; // base case

        // To store the count of times 5 can
        // divide the number.
        while (number % 5 == 0) {
            number /= 5;
            // increase count of 5
            sumOf5++;
        }

        // Divide the number by
        // 2 as much as possible
        while (sumOf5 != 0 && (number & 1) == 0) {
            number >>= 1; // dividing the number by 2
            sumOf5--;
        }

        /*multiplied result and current number(after
        removing pairs) and do modular division to get the
        last digit of the resultant number.*/
        result[0] = (result[0] * (number % 10)) % 10;

        // calling again for (currentNumber - 1)
        callMeFactorialLastDigit(n - 1, result, sumOf5);
    }

    static int lastNon0Digit(int n)
    {
        int[] result = { 1 }; // single element array.
        callMeFactorialLastDigit(n, result, 0);
        return result[0];
    }

  static void Main() {
    Console.WriteLine(lastNon0Digit(7)); // 3040
    Console.WriteLine(lastNon0Digit(12)); // 479001600
  }
}

// This code is contributed by mukesh07.
```

## **java 描述语言**

```
<script>
    // Helper Function to return the rightmost non-zero
    // digit
    function callMeFactorialLastDigit(n, result, sumOf5)
    {
        let number = n; // assaigning to new variable.
        if (number == 1)
            return; // base case

        // To store the count of times 5 can
        // divide the number.
        while (number % 5 == 0) {
            number /= 5;
            // increase count of 5
            sumOf5++;
        }

        // Divide the number by
        // 2 as much as possible
        while (sumOf5 != 0 && (number & 1) == 0) {
            number >>= 1; // dividing the number by 2
            sumOf5--;
        }

        /*multiplied result and current number(after
        removing pairs) and do modular division to get the
        last digit of the resultant number.*/
        result[0] = (result[0] * (number % 10)) % 10;
        // calling again for (currentNumber - 1)
        callMeFactorialLastDigit(n - 1, result, sumOf5);
    }

    function lastNon0Digit(n)
    {
        let result = [ 1 ]; // single element array.
        callMeFactorialLastDigit(n, result, 0);
        return result[0];
    }

    document.write(lastNon0Digit(7) + "</br>"); // 3040
      document.write(lastNon0Digit(12)); // 479001600

    // This code is contributed by divyeshrabadiya07
</script>
```

****Output**

```
4
6
```** 

> **我们使用了单元素数组(int[] result = {1})而不是整数，因为 Java 是严格按值传递的！。它不允许基元数据类型通过引用传递。这就是为什么我使用了单元素数组，这样递归函数就可以改变变量值(这里是结果)。如果我们取(int result = 1)，那么这个变量不受影响。**

**本文由**尼泰什·库马尔& KaaL-EL** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**