# 检查 N 的阶乘是否能被前 N 个自然数的和整除

> 原文:[https://www . geesforgeks . org/check-n 的阶乘是否可被第一个 n 个自然数的和整除/](https://www.geeksforgeeks.org/check-whether-factorial-of-n-is-divisible-by-sum-of-first-n-natural-numbers/)

给定一个数字“N”。检查“N”的阶乘是否能被前“N”个自然数的和整除？如果可分性是可能的，那么打印是否则打印否
**示例:**

```
Input: N = 3
Output: YES
As (1*2*3)%(1+2+3) = 0, 
Hence divisibility is possible.

Input: N = 4
Output: NO
Here (1*2*3*4)%(1+2+3+4) != 0, 
Hence  divisibility doesn't occur.
```

**进场:**

1.  前 n 个自然数之和:s = (n)*(n+1)/2。这可以表示为(n+1)！/2*(n-1)！
2.  现在 n！/s = 2*(n-1)！/(n+1)。
3.  根据上述公式，观测值可推导为:
    *   如果“n+1”是素数，那么“n！”不能被前 n 个自然数的和整除。
    *   如果“n+1”不是素数，那么“n！”可被前 n 个自然数的和整除。

**例如:**

*   设 n = 4。
*   因此不！/s' = 2*(3！)/5.= 1*2*3*2/5 .
*   这里是 n！要被“s”整除，我们需要分子中至少有“5”的倍数，即在给定的例子中，分子表示为 3 的乘积！和 2，为了使整个乘积能被‘5’
    整除，至少应该有一个 5 的倍数，即 5*1 或 5*2 或 5*3，依此类推。因为在阶乘项中出现的最高数是“n-1”，所以如果“n+1”是素数，则乘积即分子永远不能用“n+1”表示。因此分裂是不可能的。
*   在任何其他情况下，无论“n+1”是偶数还是奇数，但不是“质数”，可除性总是可能的。

**注:**对于 n=1 的情况，需要特别注意。As 1！总是能被 1 整除。
以下是上述办法的实施情况:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// a number is prime or not.
bool is_prime(int num)
{

    // Count variable to store
    // the number of factors of 'num'
    int count = 0;

    // Counting the number of factors
    for (int i = 1; i * i <= (num); i++) {

        if ((num) % i == 0) {

            if (i * i != (num))
                count += 2;

            else
                count++;
        }
    }

    // If number is prime return true
    if (count == 2)
        return true;

    else
        return false;
}

// Function to check for divisibility
string is_divisible(int n)
{

    // if 'n' equals 1 then divisibility is possible
    if (n == 1) {
        return "YES";
    }

    // Else check whether 'n+1' is prime or not
    else {

        // If 'n+1' is prime then 'n!' is
        // not divisible by 'n*(n+1)/2'
        if (is_prime(n + 1))
            return "NO";

        // else divisibility occurs
        else
            return "YES";
    }
}

// Driver Code
int main()
{

    int n;

    // Test for n=3
    n = 3;

    cout << is_divisible(n) << endl;

    // Test for n=4
    n = 4;

    cout << is_divisible(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GfG
{

// Function to check whether
// a number is prime or not.
static boolean is_prime(int num)
{

    // Count variable to store
    // the number of factors of 'num'
    int count = 0;

    // Counting the number of factors
    for (int i = 1; i * i <= (num); i++)
    {

        if ((num) % i == 0)
        {

            if (i * i != (num))
                count += 2;

            else
                count++;
        }
    }

    // If number is prime return true
    if (count == 2)
        return true;

    else
        return false;
}

// Function to check for divisibility
static String is_divisible(int n)
{

    // if 'n' equals 1 then divisibility is possible
    if (n == 1)
    {
        return "YES";
    }

    // Else check whether 'n+1' is prime or not
    else
    {

        // If 'n+1' is prime then 'n!' is
        // not divisible by 'n*(n+1)/2'
        if (is_prime(n + 1))
            return "NO";

        // else divisibility occurs
        else
            return "YES";
    }
}

// Driver Code
public static void main(String[] args)
{

    int n;

    // Test for n=3
    n = 3;

    System.out.println(is_divisible(n));

    // Test for n=4
    n = 4;

    System.out.println(is_divisible(n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Function to check whether
# a number is prime or not.
def is_prime(num):

    # Count variable to store
    # the number of factors of 'num'
    count = 0

    # Counting the number of factors
    for i in range(1, num + 1):

        if i * i > num:
            break

        if ((num) % i == 0):

            if (i * i != (num)):
                count += 2
            else:
                count += 1

    # If number is prime return true
    if (count == 2):
        return True
    else:
        return False

# Function to check for divisibility
def is_divisible(n):

    # if 'n' equals 1 then
    # divisibility is possible
    if (n == 1):
        return "YES"

    # Else check whether 'n+1' is prime or not
    else:

        # If 'n+1' is prime then 'n!' is
        # not divisible by 'n*(n+1)/2'
        if (is_prime(n + 1)):
            return "NO"

        # else divisibility occurs
        else:
            return "YES"

# Driver Code

# Test for n=3
n = 3

print(is_divisible(n))

# Test for n=4
n = 4

print(is_divisible(n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implement the approach
class GfG
{

// Function to check whether
// a number is prime or not.
static bool is_prime(int num)
{

    // Count variable to store
    // the number of factors of 'num'
    int count = 0;

    // Counting the number of factors
    for (int i = 1; i * i <= (num); i++)
    {

        if ((num) % i == 0)
        {

            if (i * i != (num))
                count += 2;

            else
                count++;
        }
    }

    // If number is prime return true
    if (count == 2)
        return true;

    else
        return false;
}

// Function to check for divisibility
static string is_divisible(int n)
{

    // if 'n' equals 1 then divisibility is possible
    if (n == 1)
    {
        return "YES";
    }

    // Else check whether 'n+1' is prime or not
    else
    {

        // If 'n+1' is prime then 'n!' is
        // not divisible by 'n*(n+1)/2'
        if (is_prime(n + 1))
            return "NO";

        // else divisibility occurs
        else
            return "YES";
    }
}

// Driver Code
static void Main()
{

    int n;

    // Test for n=3
    n = 3;

    System.Console.WriteLine(is_divisible(n));

    // Test for n=4
    n = 4;

    System.Console.WriteLine(is_divisible(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to check whether
// a number is prime or not.
function is_prime($num)
{

    // Count variable to store
    // the number of factors of 'num'
    $count1 = 0;

    // Counting the number of factors
    for ($i = 1; $i * $i <= ($num); $i++)
    {
        if (($num) % $i == 0)
        {

            if ($i * $i != ($num))
                $count1 += 2;

            else
                $count1++;
        }
    }

    // If number is prime return true
    if ($count1 == 2)
        return true;

    else
        return false;
}

// Function to check for divisibility
function is_divisible($n)
{

    // if 'n' equals 1 then divisibility is possible
    if ($n == 1)
    {
        return "YES";
    }

    // Else check whether 'n+1' is prime or not
    else
    {

        // If 'n+1' is prime then 'n!' is
        // not divisible by 'n*(n+1)/2'
        if (is_prime($n + 1))
            return "NO";

        // else divisibility occurs
        else
            return "YES";
    }
}

// Driver Code

// Test for n=3
$n = 3;

echo is_divisible($n) . "\n";

// Test for n=4
$n = 4;

echo is_divisible($n) . "\n";

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Function to check whether
// a number is prime or not.
function is_prime(num)
{

    // Count variable to store
    // the number of factors of 'num'
    var count = 0;

    // Counting the number of factors
    for (i = 1; i * i <= (num); i++)
    {

        if ((num) % i == 0)
        {

            if (i * i != (num))
                count += 2;

            else
                count++;
        }
    }

    // If number is prime return true
    if (count == 2)
        return true;

    else
        return false;
}

// Function to check for divisibility
function is_divisible(n)
{

    // if 'n' equals 1 then divisibility is possible
    if (n == 1)
    {
        return "YES";
    }

    // Else check whether 'n+1' is prime or not
    else
    {

        // If 'n+1' is prime then 'n!' is
        // not divisible by 'n*(n+1)/2'
        if (is_prime(n + 1))
            return "NO";

        // else divisibility occurs
        else
            return "YES";
    }
}

// Driver Code
var n;

// Test for n=3
n = 3;
document.write(is_divisible(n)+"<br>");

// Test for n=4
n = 4;
document.write(is_divisible(n));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
YES
NO
```