# 在比赛中寻找起跑线的程序

> 原文:[https://www . geesforgeks . org/program-to-find-head-start-in-race/](https://www.geeksforgeeks.org/program-to-find-the-head-start-in-a-race/)

鉴于 A 在百米赛跑中领先 B 和 C。任务是在同一场比赛中找到 B 能给 C 的领先优势。

**示例:**

```
Input: B = 10 meters, C = 28 meters
Output: 20 meters
B can give C a start of 20 meters.

Input: B = 20 meters, C = 50 meters
Output: 62 meters
B can give C a start of 62 meters.
```

**进场:**

> 赛跑总米数= 100 米。
> A 领先 by 10 米。当甲完成了 100 米，乙完成了 90 米。
> 同样，A 领先 C 28 米。当 A 完成时是 100 米，C 完成时是 72 米。
> 现在，B 完成了 90 米，C 完成了 72 米。
> 所以 B 完成的时候是 100 米 C 完成的时候是 80 米。
> –>((C * 100)/B)
> –>((72 * 100)/90)即 **80 米**/T8】所以 B 可以给 C 20 米的起步

**以下是上述方法的实现:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the B start to C
int Race(int B, int C)
{
    int result = 0;

    // When B completed it's 100 meter
    // then Completed meters by C is
    result = ((C * 100) / B);

    return 100 - result;
}

// Driver Code.
int main()
{
    int B = 10, C = 28;

    // When A completed it's 100 meter
    // Then completed meters of B and C is
    B = 100 - B;
    C = 100 - C;

    cout << Race(B, C) << " meters";

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
public class GFG
{

// Function to find the B start to C
static int Race(int B, int C)
{
    int result = 0;

    // When B completed it's 100 meter
    // then Completed meters by C is
    result = ((C * 100) / B);

    return 100 - result;
}

// Driver Code
public static void main(String[] args)
{
    int B = 10;
    int C = 28;

    // When A completed it's 100 meter
    // Then completed meters of B and C is
    B = 100 - B;
    C = 100 - C;

    System.out.println(Race(B, C) + " meters");
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach

# Function to find the
# B start to C
def Race(B, C):

    result = 0;

    # When B completed it's 100 meter
    # then Completed meters by C is
    result = ((C * 100) // B)

    return 100 - result

# Driver Code
if __name__ == "__main__":
    B = 10
    C = 28

    # When A completed it's 100 meter
    # Then completed meters of B and C is
    B = 100 - B;
    C = 100 - C;

    print(str(Race(B, C)) + " meters")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{

// Function to find the B start to C
static int Race(int B, int C)
{
    int result = 0;

    // When B completed it's 100 meter
    // then Completed meters by C is
    result = ((C * 100) / B);

    return 100 - result;
}

// Driver Code
public static void Main()
{
    int B = 10;
    int C = 28;

    // When A completed it's 100 meter
    // Then completed meters of B and C is
    B = 100 - B;
    C = 100 - C;

    Console.Write(Race(B, C) + " meters");
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the B start to C
function Race($B, $C)
{
    $result = 0;

    // When B completed it's 100 meter
    // then Completed meters by C is
    $result = (($C * 100) / $B);

    return 100 - $result;
}

// Driver Code
$B = 10;
$C = 28;

// When A completed it's 100 meter
// Then completed meters of B and C is
$B = 100 - $B;
$C = 100 - $C;

echo Race($B, $C) . " meters";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to find the B start to C
function Race(B, C)
{
    var result = 0;

    // When B completed it's 100 meter
    // then Completed meters by C is
    result = ((C * 100) / B);

    return 100 - result;
}

// Driver Code
var B = 10, C = 28;

// When A completed it's 100 meter
// Then completed meters of B and C is
B = 100 - B;
C = 100 - C;

document.write(Race(B, C) + " meters");

// This code is contributed by itsok

</script>
```

**Output:** 

```
20 meters
```