# 查找字符串中字符 ASCII 值乘积的程序

> 原文:[https://www . geesforgeks . org/program-to-find-product-of-ascii-values-of-in-a-string-characters/](https://www.geeksforgeeks.org/program-to-find-the-product-of-ascii-values-of-characters-in-a-string/)

给定一个字符串。任务是找到字符串中字符的 ASCII 值的乘积。
**例** :

```
Input : str = "IS"
Output : 6059
73 * 83 = 6059

Input : str = "GfG"
Output : 514182
```

这个想法是从迭代字符串的字符开始，并将它们的 ASCII 值乘以一个变量，即 prod。因此，在字符串完全迭代后，返回*戳*。
**注**:如果字符串很大，程序可能会因为 int 的大小有限而导致分段错误。
以下是上述方法的实施:

## C++

```
// C++ program to find product
// of ASCII value of characters
// in string

#include <bits/stdc++.h>
using namespace std;

// Function to find product
// of ASCII value of characters
// in string
long long productAscii(string str)
{
    long long prod = 1;

    // Traverse string to find the product
    for (int i = 0; i < str.length(); i++) {
        prod *= (int)str[i];
    }

    // Return the product
    return prod;
}

// Driver code
int main()
{
    string str = "GfG";

    cout << productAscii(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product
// of ASCII value of characters
// in string
class GFG
{

// Function to find product
// of ASCII value of characters
// in string
static long productAscii(String str)
{
    long prod = 1;

    // Traverse string to find the product
    for (int i = 0; i < str.length(); i++)
    {
        prod *= str.charAt(i);
    }

    // Return the product
    return prod;
}

// Driver Code
public static void main(String[] args)
{
    String str = "GfG";

    System.out.println(productAscii(str));
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python3 program to find product
# of ASCII value of characters
# in string

# Function to find product
# of ASCII value of characters
# in string
def productAscii(str):

    prod = 1

    # Traverse string to find the product
    for i in range(0, len(str)):
        prod = prod * ord(str[i])

    # Return the product
    return prod

# Driver code
if __name__=='__main__':
    str = "GfG"

    print(productAscii(str))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find product
// of ASCII value of characters
// in string
using System;

class GFG
{

// Function to find product
// of ASCII value of characters
// in string
static long productAscii(String str)
{
    long prod = 1;

    // Traverse string to find the product
    for (int i = 0; i < str.Length; i++)
    {
        prod *= str[i];
    }

    // Return the product
    return prod;
}

// Driver Code
static public void Main ()
{
    String str = "GfG";

    Console.Write(productAscii(str));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product
// of ASCII value of characters
// in string

// Function to find product
// of ASCII value of characters
// in string
function productAscii($str)
{
    $prod = 1;

    // Traverse string to find the product
    for ($i = 0; $i < strlen($str); $i++)
    {
        $prod *= ord($str[$i]);
    }

    // Return the product
    return $prod;
}

// Driver code
$str = "GfG";

echo productAscii($str);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// javascript program to find product
// of ASCII value of characters
// in string

// Function to find product
// of ASCII value of characters
// in string
function productAscii(str)
{
    var prod = 1;

    // Traverse string to find the product
    for (i = 0; i < str.length; i++)
    {
        prod *= str.charAt(i).charCodeAt(0);
    }

    // Return the product
    return prod;
}

// Driver Code

str = "GfG";

document.write(productAscii(str));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
514182
```

**时间复杂度:** O(N)，其中 N 为字符串长度。