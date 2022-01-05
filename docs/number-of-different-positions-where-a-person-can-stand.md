# 一个人可以站立的不同位置的数量

> 原文:[https://www . geesforgeks . org/不同位置的数量-一个人可以站立的位置/](https://www.geeksforgeeks.org/number-of-different-positions-where-a-person-can-stand/)

一个人站在 n 个人的队伍中，但他不知道自己到底占据了哪个位置。他可以说，站在他面前的不下于‘f’人，站在他身后的不下于‘b’人。任务是找到他能占据的不同位置的数量。

**示例:**

```
Input: n = 3, f = 1, b = 1 
Output: 2
3 is the number of people in the line and there can be no less than 1 people standing 
in front of him and no more than 1 people standing behind him.So the positions could be 2 and 3
(if we number the positions starting with 1).

Input: n = 5, f = 2, b = 3
Output: 3
In this example the positions are 3, 4, 5\. 
```

**进场:**我们对每一项进行迭代，检查是否适合条件 a < =i-1 和 n-i < =b(对于 I 从 1 到 n)。第一个条件可以转换成 **a+1 < =i** ，条件 **n-i < =b** 在 **n-b <中=i** ，那么一般条件可以写成 **max(a+1，n-b) < =i** ，然后我们的答案就可以用公式 **n-max(a+1，n-b)+1** 来计算了。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the position
int findPosition(int n, int f, int b)
{

    return n - max(f + 1, n - b) + 1;
}

// Driver code
int main()
{

    int n = 5, f = 2, b = 3;
    cout << findPosition(n, f, b);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find the position
static int findPosition(int n, int f, int b)
{

    return n - Math.max(f + 1, n - b) + 1;
}

// Driver code
public static void main(String args[])
{

    int n = 5, f = 2, b = 3;
    System.out.print(findPosition(n, f, b));

}
}
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to find the position
def findPosition(n, f, b):

    return n - max(f + 1, n - b) + 1;

# Driver code
n, f, b = 5, 2, 3
print(findPosition(n, f, b))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{

// Function to find the position
static int findPosition(int n,
                        int f, int b)
{

    return n - Math.Max(f + 1, n - b) + 1;
}

// Driver code
public static void Main()
{
    int n = 5, f = 2, b = 3;
    Console.WriteLine(findPosition(n, f, b));
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the position
function findPosition($n, $f, $b)
{
    return $n - max($f + 1,
                    $n - $b) + 1;
}

// Driver code
$n = 5; $f = 2; $b = 3;
echo findPosition($n, $f, $b);

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>
// Java Script implementation of above approach

// Function to find the position
function findPosition(n,f,b)
{

    return n - Math.max(f + 1, n - b) + 1;
}

// Driver code

    let n = 5, f = 2, b = 3;
    document.write(findPosition(n, f, b));
//contributed by 171fa07058
</script>
```

**Output:** 

```
3
```