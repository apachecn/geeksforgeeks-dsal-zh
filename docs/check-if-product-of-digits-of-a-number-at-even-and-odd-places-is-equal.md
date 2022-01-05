# 检查偶数和奇数位数字的乘积是否相等

> 原文:[https://www . geeksforgeeks . org/检查偶数和奇数位数字的乘积是否相等/](https://www.geeksforgeeks.org/check-if-product-of-digits-of-a-number-at-even-and-odd-places-is-equal/)

给定一个整数 **N** ，任务是检查一个数的偶数和奇数位的数字乘积是否相等。如果相等，打印**是**否则打印**否**。

**示例:**

> **输入:** N = 2841
> **输出:**是
> 奇数位位数乘积= 2 * 4 = 8
> 偶数位位数乘积= 8 * 1 = 8
> 
> **输入:** N = 4324
> **输出:** No
> 奇数位数字乘积= 4 * 2 = 8
> 偶数位数字乘积= 3 * 4 = 12

**进场:**

*   在偶数位置找到数字的乘积并存储在**prod ever**中。
*   在奇数位置找到数字的乘积并存储在 **prodOdd** 中。
*   如果 **prodEven = prodOdd** 则打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the product
// of even positioned digits is equal to
// the product of odd positioned digits in n
bool productEqual(int n)
{

    // If n is a single digit number
    if (n < 10)
        return false;
    int prodOdd = 1, prodEven = 1;

    while (n > 0) {

        // Take two consecutive digits
        // at a time
        // last digit
        int digit = n % 10;
        prodEven *= digit;
        n /= 10;

        // Second last digit
        digit = n % 10;
        prodOdd *= digit;
        n /= 10;
    }

    // If the products are equal
    if (prodEven == prodOdd)
        return true;

    // If products are not equal
    return false;
}

// Driver code
int main()
{
    int n = 4324;

    if (productEqual(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

    // Function that returns true
    // if the product of even positioned
    // digits is equal to the product of
    // odd positioned digits in n
    static boolean productEqual(int n)
    {

        // If n is a single digit number
        if (n < 10)
            return false;
        int prodOdd = 1, prodEven = 1;

        while (n > 0) {

            // Take two consecutive digits
            // at a time
            // First digit
            int digit = n % 10;
            prodOdd *= digit;
            n /= 10;

            // If n becomes 0 then
            // there's no more digit
            if (n == 0)
                break;

            // Second digit
            digit = n % 10;
            prodEven *= digit;
            n /= 10;
        }

        // If the products are equal
        if (prodEven == prodOdd)
            return true;

        // If products are not equal
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4324;

        if (productEqual(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if the product
# of even positioned digits is equal to
# the product of odd positioned digits in n

def productEqual(n):
    if n < 10:
        return False
    prodOdd = 1
    prodEven = 1

    # Take two consecutive digits
    # at a time
    # First digit
    while n > 0:
        digit = n % 10
        prodOdd *= digit
        n = n//10

        # If n becomes 0 then
        # there's no more digit
        if n == 0:
            break
        digit = n % 10
        prodEven *= digit
        n = n//10

    # If the products are equal
    if prodOdd == prodEven:
        return True

    # If the products are not equal
    return False

# Driver code
n = 4324
if productEqual(n):
    print("Yes")
else:
    print("No")

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function that returns true
    // if the product of even positioned
    // digits is equal to the product of
    // odd positioned digits in n
    static bool productEqual(int n)
    {

        // If n is a single digit number
        if (n < 10)
            return false;
        int prodOdd = 1, prodEven = 1;

        while (n > 0) {

            // Take two consecutive digits
            // at a time
            // First digit
            int digit = n % 10;
            prodOdd *= digit;
            n /= 10;

            // If n becomes 0 then
            // there's no more digit
            if (n == 0)
                break;

            // Second digit
            digit = n % 10;
            prodEven *= digit;
            n /= 10;
        }

        // If the products are equal
        if (prodEven == prodOdd)
            return true;

        // If products are not equal
        return false;
    }

    // Driver code
    static void Main()
    {
        int n = 4324;

        if (productEqual(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if the product
// of even positioned digits is equal to
// the product of odd positioned digits in n
function productEqual($n)
{

    // If n is a single digit number
    if ($n < 10)
        return false;
    $prodOdd = 1;
    $prodEven = 1;

    while ($n > 0)
    {

        // Take two consecutive digits
        // at a time

        // First digit
        $digit = $n % 10;
        $prodOdd *= $digit;
        $n /= 10;

        // If n becomes 0 then
        // there's no more digit
        if ($n == 0)
            break;

        // Second digit
        $digit = $n % 10;
        $prodEven *= $digit;
        $n /= 10;
    }

    // If the products are equal
    if ($prodEven == $prodOdd)
        return true;

    // If products are not equal
    return false;
}

// Driver code
$n = 4324;
if (productEqual(!$n))
    echo "Yes";
else
    echo "No";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if the product
// of even positioned digits is equal to
// the product of odd positioned digits in n
function productEqual(n)
{

    // If n is a single digit number
    if (n < 10)
        return false;
    let prodOdd = 1, prodEven = 1;

    while (n > 0) {

        // Take two consecutive digits
        // at a time
        // First digit
        let digit = n % 10;
        prodOdd *= digit;
        n = Math.floor(n / 10);

        // If n becomes 0 then
        // there's no more digit
        if (n == 0)
            break;

        // Second digit
        digit = n % 10;
        prodEven *= digit;
        n = Math.floor(n / 10);
    }

    // If the products are equal
    if (prodEven == prodOdd)
        return true;

    // If products are not equal
    return false;
}

// Driver code

    let n = 4324;

    if (productEqual(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
No
```

#### 方法 2:将整数转换为字符串:

1.  将整数转换为字符串。遍历字符串，将所有偶数索引的乘积存储在一个变量中，将所有奇数索引的乘积存储在另一个变量中。
2.  如果两者相等，则打印是，否则打印否

下面是实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

void getResult(int n)
{

    // To store the respective product
    int proOdd = 1;
    int proEven = 1;

    // Converting integer to string
    string num = to_string(n);

    // Traversing the string
    for(int i = 0; i < num.size(); i++)
        if (i % 2 == 0)
            proOdd = proOdd * (num[i] - '0');
        else
            proEven = proEven * (num[i] - '0');

    if (proOdd == proEven)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    int n = 4324;

    getResult(n);

    return 0;
}

// This code is contributed by sudhanshugupta2019a
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

class GFG{

static void getResult(int n)
{

    // To store the respective product
    int proOdd = 1;
    int proEven = 1;

    // Converting integer to String
    String num = String.valueOf(n);

    // Traversing the String
    for(int i = 0; i < num.length(); i++)
        if (i % 2 == 0)
            proOdd = proOdd * (num.charAt(i) - '0');
        else
            proEven = proEven * (num.charAt(i) - '0');

    if (proOdd == proEven)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int n = 4324;

    getResult(n);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

def getResult(n):

    # To store the respective product
    proOdd = 1
    proEven = 1

    # Converting integer to string
    num = str(n)

    # Traversing the string
    for i in range(len(num)):
        if(i % 2 == 0):
            proOdd = proOdd*int(num[i])
        else:
            proEven = proEven*int(num[i])

    if(proOdd == proEven):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == "__main__":
    n = 4324
    getResult(n)

# This code is contributed by vikkycirus
```

## C#

```
// C# implementation of the approach
using System;
public class GFG{

static void getResult(int n)
{

    // To store the respective product
    int proOdd = 1;
    int proEven = 1;

    // Converting integer to String
    String num = String.Join("",n);

    // Traversing the String
    for(int i = 0; i < num.Length; i++)
        if (i % 2 == 0)
            proOdd = proOdd * (num[i] - '0');
        else
            proEven = proEven * (num[i] - '0');

    if (proOdd == proEven)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(String[] args)
{
    int n = 4324;
    getResult(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    function getResult(n)
    {

        // To store the respective product
        let proOdd = 1;
        let proEven = 1;

        // Converting integer to String
        let num = n.toString();

        // Traversing the String
        for(let i = 0; i < num.length; i++)
            if (i % 2 == 0)
                proOdd = proOdd * (num[i].charCodeAt() - '0'.charCodeAt());
            else
                proEven = proEven * (num[i].charCodeAt() - '0'.charCodeAt());

        if (proOdd == proEven)
            document.write("Yes");
        else
            document.write("No");
    }

    let n = 4324;

    getResult(n);

</script>
```

**输出:**

```
No
```