# 检查一个号码是否为三分号码

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-tri rfect-number/](https://www.geeksforgeeks.org/check-if-a-number-is-triperfect-number/)

给定一个数字![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。任务是检查给定的数字是否是三分位数。
**三分位数**:一个数等于其除数之和的三倍，也就是其正除数之和的三倍，就是三分位数。
**例:**

```
Input: N = 15
Output: false
Divisors of 15 are 1, 3, 5 and 15\. Sum of 
divisors is 24 which is not equal to 3*15 i.e. 45.

Input: N = 120
Output: true
Sum of divisors is 360 i.e. 3*120.
Hence 120 is a triperfect number.
```

一个**简单的解决方法**就是把从 1 到 N 的每一个数都过一遍，检查它是不是除数。保持所有因子的和。如果和等于 3*N，则返回真，否则返回假。
一个**有效的解决方案**是通过数直到 n 的平方根。如果一个数“I”除以 n，然后将“I”和 n/i 相加。
下面是高效方法的实现:

## C++

```
// CPP code to check if a given
// number is Triperfect or not
#include<bits/stdc++.h>
using namespace std;

// Returns true if n is Triperfect
bool isTriPerfect(int n )
{
    // To store sum of divisors.
    // Adding 1 and n since they are divisors of n.
    int sum = 1 + n;

    // Find all divisors and add them
    int i = 2;
    while (i * i <= n)
    {
    if (n % i == 0)
        {
            if (n / i == i)
                sum = sum + i;
            else
                sum = sum + i + n / i;
        }
        i += 1;
    }

    // If sum of divisors is equal to
    // 3 * n, then n is a Triperfect number
    if (sum == 3 * n and n != 1)
       return true;
    else
       false;
}

// Driver program
int main()
{
 int n = 120;

 if (isTriPerfect(n))
    cout<<n<<" is a Triperfect number";   
}

//This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a given
// number is Triperfect or not

public class GFG{

    // Returns true if n is Triperfect
    static boolean isTriPerfect(int n )
    {
        // To store sum of divisors.
        // Adding 1 and n since they are divisors of n.
        int sum = 1 + n;

        // Find all divisors and add them
        int i = 2;
        while (i * i <= n)
        {
        if (n % i == 0)
            {
                if (n / i == i)
                    sum = sum + i;
                else
                    sum = sum + i + n / i;
            }
            i += 1;
        }

        // If sum of divisors is equal to
        // 3 * n, then n is a Triperfect number
        if (sum == 3 * n & n != 1)
            return true;
        else
            return  false;
    }

    // Driver program
    public static void main(String []args)
    {
    int n = 120;

    if (isTriPerfect(n))
        System.out.println(n + " is a Triperfect number");    
    }

    //This code is contributed by
    // Ryuga
}
```

## 蟒蛇 3

```
# Python3 code to check if a given
# number is Triperfect or not

# Returns true if n is Triperfect
def isTriPerfect( n ):

    # To store sum of divisors.
    # Adding 1 and n since they are divisors of n.
    sum = 1 + n

    # Find all divisors and add them
    i = 2
    while i * i <= n:
        if n % i == 0:
            if n / i == i:
                sum = sum + i
            else:
                sum = sum + i + n / i
        i += 1

    # If sum of divisors is equal to
    # 3 * n, then n is a Triperfect number
    return (True if sum == 3 * n and n != 1 else False)

# Driver program
n = 120

if isTriPerfect (n):
    print(n, "is a Triperfect number")

```

## C#

```
// C# code to check if a given
// number is Triperfect or not
using System;
public class GFG{

    // Returns true if n is Triperfect
    static bool isTriPerfect(int n )
    {
        // To store sum of divisors.
        // Adding 1 and n since they are divisors of n.
        int sum = 1 + n;

        // Find all divisors and add them
        int i = 2;
        while (i * i <= n)
        {
        if (n % i == 0)
            {
                if (n / i == i)
                    sum = sum + i;
                else
                    sum = sum + i + n / i;
            }
            i += 1;
        }

        // If sum of divisors is equal to
        // 3 * n, then n is a Triperfect number
        if (sum == 3 * n & n != 1)
            return true;
        else
            return false;
    }

    // Driver program
    public static void Main()
    {
    int n = 120;

    if (isTriPerfect(n))
        Console.WriteLine(n + " is a Triperfect number");    
    }

    //This code is contributed by
    // Mukul Singh
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP code to check if a given
// number is Triperfect or not

// Returns true if n is Triperfect
function isTriPerfect($n )
{
    // To store sum of divisors.
    // Adding 1 and n since they
    // are divisors of n.
    $sum = 1 + $n;

    // Find all divisors and add them
    $i = 2;
    while ($i * $i <= $n)
    {
        if ($n % $i == 0)
        {
            if ($n / $i == $i)
                $sum = $sum + $i;
            else
                $sum = $sum + $i + $n / $i;
        }
        $i += 1;
    }

    // If sum of divisors is equal to
    // 3 * n, then n is a Triperfect number
    if ($sum == 3 * $n and $n != 1)
        return true;
    else
        false;
}

// Driver Code
$n = 120;

if (isTriPerfect($n))
    echo $n . " is a Triperfect number";
else
    echo $n . " is not a Triperfect number";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript code to check if a given
    // number is Triperfect or not

    // Returns true if n is Triperfect
    function isTriPerfect(n)
    {
        // To store sum of divisors.
        // Adding 1 and n since they are divisors of n.
        let sum = 1 + n;

        // Find all divisors and add them
        let i = 2;
        while (i * i <= n)
        {
            if (n % i == 0)
            {
                if (parseInt(n / i, 10) == i)
                    sum = sum + i;
                else
                    sum = sum + i + parseInt(n / i, 10);
            }
            i += 1;
        }

        // If sum of divisors is equal to
        // 3 * n, then n is a Triperfect number
        if (sum == 3 * n & n != 1)
            return true;
        else
            return  false;
    }

    let n = 120;

    if (isTriPerfect(n))
        document.write(n + " is a Triperfect number");   

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
120 is a Triperfect number
```

**一些关于三航电号码**的有趣事实:

*   到目前为止，只知道 6 个三分位数。这些是 120，672，523776，459818240，1476304896 和 51001180160。
*   还没有证明不存在更多的三分位数，但据信这是唯一的六个。

同样，我们可以检查四完全数(因子之和= 4*n)、五完全数(因子之和= 5*n)等等。目前已知有 36 个四完全数和 65 个五完全数。