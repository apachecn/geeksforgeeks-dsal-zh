# 程序寻找 X 在 Y 基数的最后一位

> 原文:[https://www . geeksforgeeks . org/program-to-find-base-y 中 x 的最后一位数字/](https://www.geeksforgeeks.org/program-to-find-the-last-digit-of-x-in-base-y/)

给定一个正整数 X 和 Y，任务是在给定的基数 Y 中找到 X 的最后一个数字。

**示例:**

```
Input: X = 10, Y = 7
Output: 3
10 is 13 in base 9 with last digit 3

Input: X = 55, Y = 3
Output: 1
55 is 3 in base 601 with last digit 1
```

**进场:**

*   当我们试图[将 X 转换为基数 Y](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)
*   我们反复用 X 除以基数 Y，并存储余数。
*   所以最终结果是由剩余部分组成的，按照除法步骤的顺序排列。
*   假设除法第一步的余数是 p，第二步是 q，第三步是 r
*   那么以 Y 为基数的结果数将是 rqp
*   最后一位是 p
*   因此，我们只需要找到 X 除以 Y 时的第一个余数，就可以得到 X 在基数 Y 中的最后一位数字。

```
last digit = X % Y
```

以下是上述方法的实现:

## C++

```
// C++ Program to find
// the last digit of X in base Y

#include <bits/stdc++.h>
using namespace std;

// Function to find the last
// digit of X in base Y
void last_digit(int X, int Y)
{
    cout << X % Y;
}

// Driver code
int main()
{
    int X = 55, Y = 3;
    last_digit(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// the last digit of X in base Y
class GFG
{

// Function to find the last
// digit of X in base Y
static void last_digit(int X, int Y)
{
    System.out.print(X % Y);
}

// Driver code
public static void main(String []args)
{
    int X = 55, Y = 3;
    last_digit(X, Y);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to find
# the last digit of X in base Y

# Function to find the last
# digit of X in base Y
def last_digit(X, Y) :

    print(X % Y);

# Driver code
if __name__ == "__main__" :

    X = 55; Y = 3;
    last_digit(X, Y);

# This code is contributed
# by AnkitRai01
```

## C#

```
// C# Program to find the last digit
// of X in base Y
using System;

class GFG
{

// Function to find the last
// digit of X in base Y
static void last_digit(int X, int Y)
{
    Console.Write(X % Y);
}

// Driver code
public static void Main(String []args)
{
    int X = 55, Y = 3;
    last_digit(X, Y);
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the last digit
// of X in base Y

// Function to find the last
// digit of X in base Y
function last_digit($X,$Y){

  echo( $X % $Y );

}

// Driver code

$X = 55;
$Y = 3;

last_digit($X,$Y);

?>
```

## java 描述语言

```
<script>

// Javascript Program to find
// the last digit of X in base Y

// Function to find the last
// digit of X in base Y
function last_digit(X, Y)
{
    document.write(X % Y);
}

// Driver code
var X = 55, Y = 3;
last_digit(X, Y);

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(1)