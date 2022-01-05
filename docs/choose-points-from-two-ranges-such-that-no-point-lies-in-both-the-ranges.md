# 从两个范围中选择点，使得两个范围中都没有点

> 原文:[https://www . geesforgeks . org/从两个范围中选择点，这样两个范围中都没有点/](https://www.geeksforgeeks.org/choose-points-from-two-ranges-such-that-no-point-lies-in-both-the-ranges/)

给定两段**【L1、R1】**和**【L2、R2】**，任务是从两个范围(一个来自范围一，另一个来自范围二)中选择两个元素 **x** 和 **y** ，使得没有元素属于这两个范围，即 **x** 属于第一范围， **y** 属于第二范围。如果不存在这样的元素，则打印 **-1** 。

**示例:**

> **输入:** L1 = 1，R1 = 6，L2 = 3，R2 = 1 1
> **输出:** 1 11
> 1 只在范围【1，6】内，11 只在【3，11】内
> 
> **输入:** L1 = 5，R1 = 10，L2 = 1，R2 = 7
> T3】输出: 1 10

**进场:**

*   如果 **L1！= L2** 和 **R1！= R2** 则积分为**min(L2 L1)**和**max(R2 R1)**。
*   否则只能从一个范围中选择一个点，因为其中一个范围完全在另一个范围内，所以我们为该点打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required points
void findPoints(int l1, int r1, int l2, int r2)
{

    int x = (l1 != l2) ? min(l1, l2) : -1;
    int y = (r1 != r2) ? max(r1, r2) : -1;
    cout << x << " " << y;
}

// Driver code
int main()
{
    int l1 = 5, r1 = 10, l2 = 1, r2 = 7;
    findPoints(l1, r1, l2, r2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the required points
static void findPoints(int l1, int r1,
                       int l2, int r2)
{

    int x = (l1 != l2) ? Math.min(l1, l2) : -1;
    int y = (r1 != r2) ? Math.max(r1, r2) : -1;
    System.out.println(x + " " + y);
}

// Driver code
public static void main(String[] args)
{
    int l1 = 5, r1 = 10, l2 = 1, r2 = 7;
    findPoints(l1, r1, l2, r2);
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required points
def findPoints(l1, r1, l2, r2):

    x = min(l1, l2) if(l1 != l2) else -1
    y = max(r1, r2) if(r1 != r2) else -1
    print(x, y)

# Driver code
if __name__ == "__main__":

    l1 = 5
    r1 = 10
    l2 = 1
    r2 = 7
    findPoints(l1, r1, l2, r2)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to find the required points
    static void findPoints(int l1, int r1,
                            int l2, int r2)
    {
        int x = (l1 != l2) ? Math.Min(l1, l2) : -1;
        int y = (r1 != r2) ? Math.Max(r1, r2) : -1;
        Console.WriteLine(x + " " + y);
    }

    // Driver code
    public static void Main()
    {
        int l1 = 5, r1 = 10, l2 = 1, r2 = 7;
        findPoints(l1, r1, l2, r2);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find the required points
function findPoints($l1, $r1, $l2, $r2)
{

    $x = ($l1 != $l2) ? min($l1, $l2) : -1;
    $y = ($r1 != $r2) ? max($r1, $r2) : -1;
    echo $x , " " , $y;
}

// Driver code
$l1 = 5;
$r1 = 10;
$l2 = 1;
$r2 = 7;
findPoints($l1, $r1, $l2, $r2);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach   

// Function to find the required points
function findPoints(l1 , r1 , l2 , r2)
{
    var x = (l1 != l2) ? Math.min(l1, l2) : -1;
    var y = (r1 != r2) ? Math.max(r1, r2) : -1;
    document.write(x + " " + y);
}

// Driver code
var l1 = 5, r1 = 10, l2 = 1, r2 = 7;

findPoints(l1, r1, l2, r2);

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
1 10
```