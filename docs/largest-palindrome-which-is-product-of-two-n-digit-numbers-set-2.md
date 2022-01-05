# 两个 N 位数乘积的最大回文:集合 2

> 原文:[https://www . geesforgeks . org/maximum-回文-哪个是两个 n 位数的乘积-set-2/](https://www.geeksforgeeks.org/largest-palindrome-which-is-product-of-two-n-digit-numbers-set-2/)

给定一个值 **N** ，找出最大的回文数，它是两个 **N** 位数的乘积。
**例:**

> **输入:** N = 2
> **输出:** 9009
> **说明:**
> 9009 是两个 2 位数 91 和 99 (9009 = 91*99)
> **输入:** N = 3
> **输出:** 906609
> **输入:** N = 4 【T18

**观察:**对于上面的问题可以做如下观察:
**让 N = 2，**那么乘积将包含 4 位数。由于产品将是回文，它将是“ **abba** ”形式，其中 a、b 是它们各自位置值的数字。
因此，

> **为 N = 2:**T2【阿爸】= 1000 a+100b+10b+a
> = 1001 a+110 b
> = 11。(91a + 10b)
> **同样，对于 N = 3:**
> “abcba”= 100000 a+10000 b+1000c+100c+10 b+ 1a
> = 100001 a+10010 b+1100 c
> = 11。(9091a + 910b + 100c)
> **为 N = 5:**
> 【abcdeedcba】= 100000000 a+10000000 b+100000000 c+10000000d+1000000 e+10000d+10000 c+10 b+ a
> = 100000000000001 a+10000000010 b(90909091 a+909091 b+91000 c+10000d)

**方法:**从上面的观察，可以观察到一个模式，每个回文积总会有一个因子 11。

1.  对于任何 N 位数的 P 和 Q，如果 P 和 Q 的乘积是回文，那么 P 或 Q 都可以被 11 整除，但不能同时被 11 整除。
2.  因此，我们可以通过只检查其中一个数字的 11 的倍数来减少计算量，而不是检查 P 和 Q 的乘积是否是所有可能的 P 和 Q 对的回文。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG {

    // Function to check if a number is a
    // Palindrome or not
    static boolean isPalindrome(long x)
    {
        // Taking the string value
        // of the number
        String num = String.valueOf(x);
        boolean result = true;
        int i = 0;
        int j = num.length() - 1;

        // Loop to check if every i-th
        // character from beginning is
        // equal to every (N - i)th char
        while (i < j && result) {
            result = num.charAt(i++)
                     == num.charAt(j--);
        }

        return result;
    }

    // Function to find the largest palindrome
    // which is a product of two N digited numbers
    public static void find(final int nDigits)
    {

        // Find lowerBound, upperBound for
        // a given nDigits. for n=2; [10, 99]
        final long lowerBound
            = (long)Math.pow(10, nDigits - 1);

        final long upperBound
            = (lowerBound * 10) - 1;

        // Result variables
        long resultP = 0, resultQ = 0,
             resultR = 0;

        // Keep p decrementing by 11
        for (long p = upperBound;
             p > lowerBound;
             p -= 11) {

            // Find the nearest number
            // divisible by 11
            while (p % 11 != 0) {
                p--;
            }

            // Keep decrementing q by 1
            for (long q = upperBound;
                 q > lowerBound;
                 q--) {
                long t = p * q;

                // Update the result if
                // t > r and is a palindrome
                if (t > resultR
                    && isPalindrome(t)) {
                    resultP = p;
                    resultQ = q;
                    resultR = t;
                    break;
                }
            }
        }

        // Printing the final result
        System.out.println(resultR);
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 2;
        find(N);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of
# the above approach

# Function to check if a
# number is a Palindrome
# or not
def isPalindrome(x):

    # Taking the string value
    # of the number
    num = str(x)
    result = True
    i = 0
    j = len(num) - 1

    # Loop to check if every i-th
    # character from beginning is
    # equal to every(N - i)th char
    while (i < j and result):
        result = num[i] == num[j]
        i += 1
        j -= 1

    return result

# Function to find the largest
# palindrome which is a product
# of two N digited numbers
def find(nDigits):

    # Find lowerBound, upperBound
    # for a given nDigits. for n = 2
    # [10, 99]
    lowerBound = pow(10, nDigits - 1)

    upperBound = (lowerBound * 10) - 1

    # Result variables
    resultP = 0
    resultQ = 0
    resultR = 0

    # Keep p decrementing by 11
    for p in range(upperBound,
                   lowerBound, -11):

        # Find the nearest number
        # divisible by 11
        while (p % 11 != 0):
            p -= 1

        # Keep decrementing q by 1
        for q in range(upperBound,
                       lowerBound, -1):
            t = p * q

            # Update the result if
            # t > r and is a palindrome
            if (t > resultR and
                isPalindrome(t)):
                resultP = p
                resultQ = q
                resultR = t
                break

    # Printing the final result
    print(resultR)

# Driver code
if __name__ == "__main__":

    N = 2
    find(N)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Function to check if a number is a
    // Palindrome or not
    static bool isPalindrome(long x)
    {
        // Taking the string value
        // of the number
        String num = String.Join("",x);
        bool result = true;
        int i = 0;
        int j = num.Length - 1;

        // Loop to check if every i-th
        // character from beginning is
        // equal to every (N - i)th char
        while (i < j && result) {
            result = num[i++]
                     == num[j--];
        }

        return result;
    }

    // Function to find the largest palindrome
    // which is a product of two N digited numbers
    public static void find(int nDigits)
    {

        // Find lowerBound, upperBound for
        // a given nDigits. for n=2; [10, 99]
        long lowerBound
            = (long)Math.Pow(10, nDigits - 1);

        long upperBound
            = (lowerBound * 10) - 1;

        // Result variables
        long resultP = 0, resultQ = 0,
             resultR = 0;

        // Keep p decrementing by 11
        for (long p = upperBound;
             p > lowerBound;
             p -= 11) {

            // Find the nearest number
            // divisible by 11
            while (p % 11 != 0) {
                p--;
            }

            // Keep decrementing q by 1
            for (long q = upperBound;
                 q > lowerBound;
                 q--) {
                long t = p * q;

                // Update the result if
                // t > r and is a palindrome
                if (t > resultR
                    && isPalindrome(t)) {
                    resultP = p;
                    resultQ = q;
                    resultR = t;
                    break;
                }
            }
        }

        // Printing the readonly result
        Console.WriteLine(resultR);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int N = 2;
        find(N);
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to check if a number is a
    // Palindrome or not
    function isPalindrome(x)
    {
        // Taking the string value
        // of the number
        let num = x.toString();
        let result = true;
        let i = 0;
        let j = num.length - 1;

        // Loop to check if every i-th
        // character from beginning is
        // equal to every (N - i)th char
        while (i < j && result) {
            result = num[i++]
                     == num[j--];
        }

        return result;
    }

    // Function to find the largest palindrome
    // which is a product of two N digited numbers
    function find(nDigits)
    {

        // Find lowerBound, upperBound for
        // a given nDigits. for n=2; [10, 99]
        let lowerBound
            = Math.floor(Math.pow(10, nDigits - 1));

        let upperBound
            = (lowerBound * 10) - 1;

        // Result variables
        let resultP = 0, resultQ = 0,
             resultR = 0;

        // Keep p decrementing by 11
        for (let p = upperBound;
             p > lowerBound;
             p -= 11) {

            // Find the nearest number
            // divisible by 11
            while (p % 11 != 0) {
                p--;
            }

            // Keep decrementing q by 1
            for (let q = upperBound;
                 q > lowerBound;
                 q--) {
                let t = p * q;

                // Update the result if
                // t > r and is a palindrome
                if (t > resultR
                    && isPalindrome(t)) {
                    resultP = p;
                    resultQ = q;
                    resultR = t;
                    break;
                }
            }
        }

        // Printing the readonly result
        document.write(resultR);
    }

// Driver Code

    let N = 2;
    find(N);

</script>
```

**Output:** 

```
9009
```

时间复杂度:O(上限–下限) <sup>2</sup>

辅助空间:0(1)

**相关文章:** [最大回文，是两个 n 位数](https://www.geeksforgeeks.org/largest-palindrome-product-two-n-digit-numbers/)的乘积