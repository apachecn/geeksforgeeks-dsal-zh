# 检查一个数的偶数位的位数乘积是否能被 K 整除

> 原文:[https://www . geeksforgeeks . org/check-number 的偶数位数乘积是否可被 k 整除/](https://www.geeksforgeeks.org/check-whether-product-of-digits-at-even-places-of-a-number-is-divisible-by-k/)

给定一个数 N，任务是检查一个数偶数处的数字乘积是否能被 k 整除，如果能整除，则输出“是”，否则输出“否”。
**例:**

```
Input: N = 5478, K = 5
Output: YES
Since, 5 * 7 = 35, which is divisible by 5

Input: N = 19270, K = 2
Output: NO 
```

**进场:**

1.  在从右到左的偶数位置寻找数字的乘积。
2.  然后通过取其与“K”的模来检查可除性
3.  如果模给出 0，输出是，否则输出否

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// below function checks whether
// product of digits at even places
// is divisible by K
bool productDivisible(int n, int k)
{
    int product = 1, position = 1;
    while (n > 0) {

        // if position is even
        if (position % 2 == 0)
            product *= n % 10;
        n = n / 10;
        position++;
    }

    if (product % k == 0)
        return true;
    return false;
}

// Driver code
int main()
{
    int n = 321922;
    int k = 3;

    if (productDivisible(n, k))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA implementation of the above approach
class GFG {
// below function checks whether
// product of digits at even places
// is divisible by K

    static boolean productDivisible(int n, int k) {
        int product = 1, position = 1;
        while (n > 0) {

            // if position is even
            if (position % 2 == 0) {
                product *= n % 10;
            }
            n = n / 10;
            position++;
        }

        if (product % k == 0) {
            return true;
        }
        return false;
    }

// Driver code
    public static void main(String[] args) {
        int n = 321922;
        int k = 3;

        if (productDivisible(n, k)) {
            System.out.println("YES");
        } else {
            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# below function checks whether
# product of digits at even places
# is divisible by K
def productDivisible(n, k):
    product = 1
    position = 1
    while n > 0:

        # if position is even
        if position % 2 == 0:
            product *= n % 10
        n = n / 10
        position += 1
    if product % k == 0:
        return True
    return False

# Driver code
n = 321922
k = 3
if productDivisible(n, k) == True:
    print("YES")
else:
    print("NO")

# This code is contributed
# by Shrikant13
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// below function checks whether
// product of digits at even places
// is divisible by K
static bool productDivisible(int n, int k)
{
    int product = 1, position = 1;
    while (n > 0)
    {

        // if position is even
        if (position % 2 == 0)
            product *= n % 10;
        n = n / 10;
        position++;
    }

    if (product % k == 0)
        return true;
    return false;
}

// Driver code
public static void Main()
{
    int n = 321922;
    int k = 3;

    if (productDivisible(n, k))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Below function checks whether
// product of digits at even places
// is divisible by K
function productDivisible($n, $k)
{
    $product = 1;
    $position = 1;
    while ($n > 0)
    {

        // if position is even
        if ($position % 2 == 0)
            $product *= $n % 10;
        $n = (int)($n / 10);
        $position++;
    }

    if ($product % $k == 0)
        return true;
    return false;
}

// Driver code
$n = 321922;
$k = 3;

if (productDivisible($n, $k))
    echo "YES";
else
    echo "NO";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// below function checks whether
// product of digits at even places
// is divisible by K
function productDivisible(n, k)
{
    var product = 1, position = 1;
    while (n > 0) {

        // if position is even
        if (position % 2 == 0)
            product *= n % 10;
        n =parseInt(n / 10);
        position++;
    }

    if (product % k == 0)
        return true;
    return false;
}

// Driver code
var n = 321922;
var k = 3;
if (productDivisible(n, k))
    document.write( "YES");
else
    document.write( "NO");

</script>
```

**Output:** 

```
YES
```

#### 方法 2:使用 string()方法:

1.  将整数转换为字符串，然后遍历字符串，并通过将其存储在乘积中来乘以所有偶数索引。
2.  如果乘积能被 k 整除，则返回真，否则返回假。

下面是实现:

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function checks whether
# product of digits at even places
# is divisible by K
def productDivisible(n, k):
    product = 1

    # Converting integer to string
    num = str(n)

    # Traversing the string
    for i in range(len(num)):
        if(i % 2 == 0):
            product = product*int(num[i])

    if product % k == 0:
        return True
    return False

# Driver code
n = 321922
k = 3
if productDivisible(n, k) == True:
    print("YES")
else:
    print("NO")

# This code is contributed by vikkycirus
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function checks whether
// product of digits at even places
// is divisible by K
function productDivisible(n, k){
    var product = 1 ;

    // Converting integer to string
    var num = n.toString()

    // Traversing the string
    for(let i = 0 ; i < num.length ; i++){
        if(i % 2 == 0){
            product = product * Number(num[i])
        }
    }
    if (product % k == 0){
        return true
    }
    else{
    return false;
    }
}

// Driver code
var n = 321922
var k = 3
if(productDivisible(n, k)){
    document.write("YES")
}
else{
    document.write("NO")
}

</script>
```

**输出:**

```
YES
```