# 3 位奥西里斯数字

> 原文:[https://www.geeksforgeeks.org/3-digit-osiris-number/](https://www.geeksforgeeks.org/3-digit-osiris-number/)

给定一个 3 位数 **N** ，任务是找出 **N** 是否是奥西里斯数字。Osiris 数是等于它们自己的数字的子样本排列的和的数。例如 **132** 等于 **12 + 21 + 13 + 31 + 23 + 32** ，是奥西里斯数字。

**示例:**

> **输入:**N = 132
> T3】输出:是
> 12 + 21 + 13 + 31 + 23 + 32 = 132
> 
> **输入:**N = 154
> T3】输出:否

**进场:**

> 如果 **n = 132** 、
> 132 = 12+21+13+31+23+32
> 132 = 2 * 11+2 * 22+2 * 33
> 132 = 22+44+66
> 132 =(2+4+6)* 11
> 132 = 2 *(1+2+3)* 11，则 132 的每个数字在的 1 和 10 位置出现两次
> 同样的规则适用于每 3 位数的奥西里斯数字，并且可以往复检查一个数字是否是奥西里斯数字。
> 对于一个 3 位数 **N** 被认为是奥西里斯数， **N** 必须等于 **2 *(位数之和)* 11**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// n is an Osiris number
bool isOsiris(int n)
{
    // 3rd digit
    int a = n % 10;

    // 2nd digit
    int b = (n / 10) % 10;

    // 1st digit
    int c = n / 100;

    int digit_sum = a + b + c;

    // Check the required condition
    if (n == (2 * (digit_sum)*11)) {
        return true;
    }

    return false;
}

// Driver code
int main()
{
    int n = 132;
    if (isOsiris(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if
// n is an Osiris number
static boolean isOsiris(int n)
{
    // 3rd digit
    int a = n % 10;

    // 2nd digit
    int b = (n / 10) % 10;

    // 1st digit
    int c = n / 100;

    int digit_sum = a + b + c;

    // Check the required condition
    if (n == (2 * (digit_sum)*11))
    {
        return true;
    }

    return false;
}

// Driver code
public static void main(String args[])
{
    int n = 132;
    if (isOsiris(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Akanksha Rai
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if
# n is an Osiris number
def isOsiris(n):

    # 3rd digit
    a = n % 10

    # 2nd digit
    b = (n//10)% 10

    # 1st digit
    c = n//100

    digit_sum = a + b + c

    # Check the required condition
    if(n == (2 * (digit_sum) * 11)):
        return True

    return False

# Driver code
if __name__ == '__main__':
    n = 132
    if isOsiris(n):
        print("Yes")
    else :
        print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
// Function that returns true if
// n is an Osiris number
static bool isOsiris(int n)
{
    // 3rd digit
    int a = n % 10;

    // 2nd digit
    int b = (n / 10) % 10;

    // 1st digit
    int c = n / 100;

    int digit_sum = a + b + c;

    // Check the required condition
    if (n == (2 * (digit_sum)*11))
    {
        return true;
    }

    return false;
}

// Driver code
static void Main()
{
    int n = 132;
    if (isOsiris(n))
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

// Function that returns true if
// n is an Osiris number
function isOsiris($n)
{
    // 3rd digit
    $a = $n % 10;

    // 2nd digit
    $b = floor($n / 10) % 10;

    // 1st digit
    $c = floor($n / 100);

    $digit_sum = $a + $b + $c;

    // Check the required condition
    if ($n == (2 * ($digit_sum) * 11))
    {
        return true;
    }

    return false;
}

// Driver code
$n = 132;
if (isOsiris($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if
// n is an Osiris number
function isOsiris(n)
{

    // 3rd digit
    let a = n % 10;

    // 2nd digit
    let b = parseInt((n / 10) % 10);

    // 1st digit
    let c = parseInt(n / 100);

    let digit_sum = a + b + c;

    // Check the required condition
    if (n == (2 * (digit_sum) * 11))
    {
        return true;
    }
    return false;
}

// Driver code
let n = 132;

if (isOsiris(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
Yes
```

**时间复杂度**:O(1)
T3】空间复杂度 : O(1)