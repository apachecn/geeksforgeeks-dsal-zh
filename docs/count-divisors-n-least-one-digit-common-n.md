# 计算 n 的除数，其中至少有一个数字与 n 相同

> 原文:[https://www . geesforgeks . org/count-dividers-n-至少一位数-common-n/](https://www.geeksforgeeks.org/count-divisors-n-least-one-digit-common-n/)

给定一个数字 n，求小数表示中至少有一位数字与数字 n 相匹配的除数

**示例:**

```
Input : n = 10
Output: 2
Explanation: numbers are 1 and 10, 1 and 10 
both have a nimbus of 1 digit common with n = 10.

Input : n = 15 
Output: 3 
Explanation: the numbers are 1, 5, 15, all of them
have a minimum of 1 digit common. 
```

一种**简单的方法**是从 1 迭代到 n，检查所有除数，并使用散列法来确定是否有任何数字与 n 匹配。
时间复杂度:O(n)
辅助空间:O(1)
一种**高效的方法**是从 1 迭代到 sqrt(n)并检查所有的除数 I 和 n/i，如果两者都不同，我们检查 I 和 n/i 是否有匹配，如果有，我们简单地在答案上加 1。我们使用哈希来存储一个数字是否存在。
以下是上述方法的实现

## C++

```
// C++ program to count divisors of n that have at least
// one digit common with n
#include <bits/stdc++.h>
using namespace std;

// function to return true if any digit of m is
// present in hash[].
bool isDigitPresent(int m, bool hash[])
{
    // check till last digit
    while (m) {

        // if number is also present in original number
        // then return true
        if (hash[m % 10])
            return true;
        m = m / 10;
    }

    // if no number matches then return 1
    return false;
}

// Count the no of divisors that have at least 1 digits
// same
int countDivisibles(int n)
{
    // Store digits present in n in a hash[]
    bool hash[10] = { 0 };
    int m = n;
    while (m) {

        // marks that the number is present
        hash[m % 10] = true;

        // last digit removed
        m = m / 10;
    }

    // loop to traverse from 1 to sqrt(n) to
    // count divisors
    int ans = 0;
    for (int i = 1; i <= sqrt(n); i++) {

        // if i is the factor
        if (n % i == 0) {

            // call the function to check if any
            // digits match or not
            if (isDigitPresent(i, hash))
                ans++;

            if (n / i != i) {

                // if n/i != i then a different number,
                // then check it also
                if (isDigitPresent(n/i, hash))
                ans++;
            }
        }
    }

    // return the answer
    return ans;
}

// driver program to test the above function
int main()
{
    int n = 15;
    cout << countDivisibles(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count divisors of n that
// have at least one digit common with n
class GFG {

    // function to return true if any digit
    // of m is present in hash[].
    static boolean isDigitPresent(int m,
                            boolean hash[])
    {

        // check till last digit
        while (m > 0) {

            // if number is also present
            // in original number then
            // return true
            if (hash[m % 10])
                return true;
            m = m / 10;
        }

        // if no number matches then
        // return 1
        return false;
    }

    // Count the no of divisors that
    // have at least 1 digits same
    static int countDivisibles(int n)
    {

        // Store digits present in n
        // in a hash[]
        boolean hash[] = new boolean[10];
        int m = n;
        while (m > 0) {

            // marks that the number
            // is present
            hash[m % 10] = true;

            // last digit removed
            m = m / 10;
        }

        // loop to traverse from 1 to
        // sqrt(n) to count divisors
        int ans = 0;
        for (int i = 1; i <= Math.sqrt(n);
                                    i++)
        {

            // if i is the factor
            if (n % i == 0) {

                // call the function to
                // check if any digits
                // match or not
                if (isDigitPresent(i, hash))
                    ans++;

                if (n / i != i) {

                    // if n/i != i then a
                    // different number,
                    // then check it also
                    if (isDigitPresent(n/i, hash))
                        ans++;
                }
            }
        }

        // return the answer
        return ans;
    }

    //driver code
    public static void main (String[] args)
    {
        int n = 15;

        System.out.print(countDivisibles(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to count divisors
# of n that have at least
# one digit common with n
import math

# Function to return true if any 
# digit of m is present in hash[].
def isDigitPresent(m, Hash):

    # check till last digit
    while (m):

        # if number is also present in original 
        # number then return true
        if (Hash[m % 10]):
            return True
        m = m // 10

    # if no number matches then return 1
    return False

# Count the no of divisors that
# have at least 1 digits same
def countDivisibles(n):

    # Store digits present in n in a hash[]
    Hash = [False for i in range(10)]
    m = n
    while (m):

        # marks that the number is present
        Hash[m % 10] = True

        # last digit removed
        m = m // 10

    # loop to traverse from 1 to sqrt(n) to
    # count divisors
    ans = 0
    for i in range(1, int(math.sqrt(n)) + 1):

        # if i is the factor
        if (n % i == 0):

            # call the function to check if any
            # digits match or not
            if (isDigitPresent(i, Hash)):
                ans += 1

            if (n // i != i):

                # if n/i != i then a different number,
                # then check it also
                if (isDigitPresent(n // i, Hash)):
                    ans += 1

    # return the answer
    return ans

# Driver Code
n = 15
print(countDivisibles(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// Program to count divisors of
// n that have at least one digit
// common with n
using System;

class GFG {

    // function to return true if
    // any digit of m is present
    // in hash[].
    static bool isDigitPresent(int m, bool[] hash)
    {
        // check till last digit
        while (m > 0) {

            // if number is also present in the
            // original number then return true
            if (hash[m % 10])
                return true;
            m = m / 10;
        }

        // if no number matches then return 1
        return false;
    }

    // Count the no of divisors that have
    // at least 1 digits same
    static int countDivisibles(int n)
    {
        // Store digits present in n in a hash[]
        bool[] hash = new bool[10];
        int m = n;
        while (m > 0) {

            // marks that the number is present
            hash[m % 10] = true;

            // last digit removed
            m = m / 10;
        }

        // loop to traverse from 1 to sqrt(n) to
        // count divisors
        int ans = 0;
        for (int i = 1; i <= Math.Sqrt(n); i++) {

            // if i is the factor
            if (n % i == 0) {

                // call the function to check if any
                // digits match or not
                if (isDigitPresent(i, hash))
                    ans++;

                if (n / i != i) {

                    // if n/i != i then a different number,
                    // then check it also
                    if (isDigitPresent(n / i, hash))
                        ans++;
                }
            }
        }

        // return the answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int n = 15;
        Console.Write(countDivisibles(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count divisors
// of n that have at least
// one digit common with n

// function to return true
// if any digit of m is
// present in hash[].
function isDigitPresent($m, $hash)
{
    // check till last digit
    while ($m)
    {

        // if number is also
        // present in original
        // number then return true
        if ($hash[$m % 10])
            return true;
        $m = (int)($m / 10);
    }

    // if no number matches
    // then return 1
    return false;
}

// Count the no of divisors
// that have at least 1 digits
// same
function countDivisibles($n)
{
    // Store digits present
    // in n in a hash[]
    $hash = array_fill(0, 10, false);
    $m = $n;
    while ($m)
    {

        // marks that the
        // number is present
        $hash[$m % 10] = true;

        // last digit removed
        $m = (int)($m / 10);
    }

    // loop to traverse from
    // 1 to sqrt(n) to count divisors
    $ans = 0;
    for ($i = 1; $i <= sqrt($n); $i++)
    {

        // if i is the factor
        if ($n % $i == 0)
        {

            // call the function
            // to check if any
            // digits match or not
            if (isDigitPresent($i, $hash))
                $ans++;

            if ((int)($n / $i) != $i)
            {

                // if n/i != i then a
                // different number,
                // then check it also
                if (isDigitPresent((int)($n / $i), $hash))
                $ans++;
            }
        }
    }

    // return the answer
    return $ans;
}

// Driver code
$n = 15;
echo countDivisibles($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// JavaScript program to count divisors of n that
// have at least one digit common with n

    // function to return true if any digit
    // of m is present in hash[].
    function isDigitPresent(m, hash)
    {

        // check till last digit
        while (m > 0) {

            // if number is also present
            // in original number then
            // return true
            if (hash[m % 10])
                return true;
            m = Math.floor(m / 10);
        }

        // if no number matches then
        // return 1
        return false;
    }

    // Count the no of divisors that
    // have at least 1 digits same
    function countDivisibles(n)
    {

        // Store digits present in n
        // in a hash[]
        let hash = Array.from({length: 10}, (_, i) => 0);
        let m = n;
        while (m > 0) {

            // marks that the number
            // is present
            hash[m % 10] = true;

            // last digit removed
            m = Math.floor(m / 10);
        }

        // loop to traverse from 1 to
        // sqrt(n) to count divisors
        let ans = 0;
        for (let i = 1; i <= Math.sqrt(n);
                                    i++)
        {

            // if i is the factor
            if (n % i == 0) {

                // call the function to
                // check if any digits
                // match or not
                if (isDigitPresent(i, hash))
                    ans++;

                if (n / i != i) {

                    // if n/i != i then a
                    // different number,
                    // then check it also
                    if (isDigitPresent(n/i, hash))
                        ans++;
                }
            }
        }

        // return the answer
        return ans;
    }

// Driver Code

    let n = 15;

    document.write(countDivisibles(n));

</script>
```

**输出:**

```
3
```

**时间复杂度:**O(sqrt n)
T3】辅助空间: O(1)
本文由[**Raja vikramatitya**](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。