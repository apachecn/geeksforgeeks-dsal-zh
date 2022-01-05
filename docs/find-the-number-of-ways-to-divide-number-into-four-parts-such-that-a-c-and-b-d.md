# 找到数的方式将数分成四份，这样 a = c，b = d

> 原文:[https://www . geeksforgeeks . org/find-the-number-of-way-to-number-division-to-a-c-and-b-d/](https://www.geeksforgeeks.org/find-the-number-of-ways-to-divide-number-into-four-parts-such-that-a-c-and-b-d/)

给定一个数字 **N** 。求数的方法把一个数分成四份(a，b，c，d)，这样 a = c，b = d，a 不等于 b.
**例:**

> **输入:** N = 6
> **输出:** 1
> **解释:**四个部分为{1，2，1，2}
> **输入:** N = 20
> **输出:** 4
> **解释:**可能的方式有{1，1，9，9}、{2，2，8，8}、{3，3，7，7}和{4，4，8 }

**逼近:**
如果给定的 **N** 为奇数，则答案为 0，因为四个部分之和不会是偶数。
如果 n 能被 4 整除，那么答案就是 n/4 -1(这里 a 等于 b 是可能的，所以减去那个可能性)，否则就是 n/4。
以下是上述方法的实现:

## C++

```
// C++ implementation for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of ways to divide
// N into four parts such that a = c and b = d
int possibleways(int n)
{
    if (n % 2 == 1)
        return 0;
    else if (n % 4 == 0)
        return n / 4 - 1;
    else
        return n / 4;
}

// Driver code
int main()
{
    int n = 20;
    cout << possibleways(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
class GFG
{

// Function to find the number of ways to divide
// N into four parts such that a = c and b = d
static int possibleways(int n)
{
    if (n % 2 == 1)
        return 0;
    else if (n % 4 == 0)
        return n / 4 - 1;
    else
        return n / 4;
}

// Driver code
public static void main(String[] args)
{
    int n = 20;
    System.out.println(possibleways(n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation for above approach

# Function to find the number of ways
# to divide N into four parts
# such that a = c and b = d
def possibleways(n):

    if (n % 2 == 1):
        return 0;
    elif (n % 4 == 0):
        return n // 4 - 1;
    else:
        return n // 4;

# Driver code
n = 20;
print(possibleways(n));

# This code is contributed by mits
```

## C#

```
// C# implementation for above approach
class GFG
{

// Function to find the number of ways to divide
// N into four parts such that a = c and b = d
static int possibleways(int n)
{
    if (n % 2 == 1)
        return 0;
    else if (n % 4 == 0)
        return n / 4 - 1;
    else
        return n / 4;
}

// Driver code
static void Main()
{
    int n = 20;
    System.Console.WriteLine(possibleways(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation for above approach

// Function to find the number of ways to divide
// N into four parts such that a = c and b = d
function possibleways($n)
{
    if ($n % 2 == 1)
        return 0;
    else if ($n % 4 == 0)
        return $n / 4 - 1;
    else
        return $n / 4;
}

// Driver code
$n = 20;
echo possibleways($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// java script  implementation for above approach

// Function to find the number of ways to divide
// N into four parts such that a = c and b = d
function possibleways(n)
{
    if (n % 2 == 1)
        return 0;
    else if (n % 4 == 0)
        return n / 4 - 1;
    else
        return n / 4;
}

// Driver code
let n = 20;
document.write( possibleways(n));

// This code is contributed by Gottumukkala Bobby
</script>
```

**时间复杂度:** O(1)

**辅助空间:** O(1)