# 从右侧可以看到的元素数量

> 原文:[https://www . geesforgeks . org/从右侧可以看到的元素数量/](https://www.geeksforgeeks.org/number-of-elements-that-can-be-seen-from-right-side/)

给定一个整数数组，将元素视为建筑物的高度，找出从右侧可以看到的建筑物数量。
**例:**

```
Input : height[] = {2, 6, 2, 4, 0, 1}
Output : 3
we can see only 3 building i.e with height 1, 4 and 6.

Input : height[] = {4, 8, 2, 0, 0, 5}
Output : 2
```

这个问题看似是从右边找到**最长的递增子序列**，其实不是。如果我们遇到迄今为止发现的任何高度更高的建筑，我们必须增加计数。
以下是上述办法的实施情况。

## C++

```
// CPP program to find number of elements
// that can be seen from right side.
#include <bits/stdc++.h>
using namespace std;

int numberOfElements(int height[], int n)
{
    int max_so_far = 0;
    int coun = 0;

    for (int i = n - 1; i >= 0; i--) {
        if (height[i] > max_so_far) {
            max_so_far = height[i];
            coun++;
        }
    }
    return coun;
}

// Driver code
int main()
{
    int n = 6;
    int height[] = { 4, 8, 2, 0, 0, 5 };
    cout << numberOfElements(height, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of elements
// that can be seen from right side.
import java.util.*;
class Solution
{

static int numberOfElements(int height[], int n)
{
    int max_so_far = 0;
    int coun = 0;

    for (int i = n - 1; i >= 0; i--) {
        if (height[i] > max_so_far) {
            max_so_far = height[i];
            coun++;
        }
    }
    return coun;
}

// Driver code
public static void main(String args[])
{
    int n = 6;
    int height[] = { 4, 8, 2, 0, 0, 5 };
    System.out.println( numberOfElements(height, n));

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find
# number of elements
# that can be seen from right side

def numberOfElements(height, n):

    max_so_far = 0
    coun = 0

    for i in range(n-1,-1,-1):
        if height[i] > max_so_far:
            max_so_far = height[i]
            coun = coun + 1
    return coun

#Driver code
if __name__=='__main__':
    n = 6
    height = [4, 8, 2, 0, 0, 5]
    print(numberOfElements(height, n))

# This code is contributed by
# Shashank_Sharma    
```

## C#

```
// C# program to find number of elements
// that can be seen from right side.
using System;

class GFG
{
public static int numberOfElements(int []height,
                                   int n)
{
    int max_so_far = 0;
    int coun = 0;

    for (int i = n - 1; i >= 0; i--)
    {
        if (height[i] > max_so_far)
        {
            max_so_far = height[i];
            coun++;
        }
    }
    return coun;
}

// Driver code
public static void Main()
{
    int n = 6;
    int []height = { 4, 8, 2, 0, 0, 5 };
    Console.WriteLine(numberOfElements(height, n));
}
}

// This code is contributed by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of elements
// that can be seen from right side.

function numberOfElements($height, $n)
{
    $max_so_far = 0;
    $coun = 0;

    for ($i = $n - 1; $i >= 0; $i--)
    {
        if ($height[$i] > $max_so_far)
        {
            $max_so_far = $height[$i];
            $coun++;
        }
    }
    return $coun;
}

// Driver code
$n = 6;
$height = array(4, 8, 2, 0, 0, 5 );
echo numberOfElements($height, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// javascript program to find number of elements
// that can be seen from right side.

    function numberOfElements(height , n)
    {
        var max_so_far = 0;
        var coun = 0;

        for (let i = n - 1; i >= 0; i--)
        {
            if (height[i] > max_so_far)
            {
                max_so_far = height[i];
                coun++;
            }
        }
        return coun;
    }

    // Driver code
    var n = 6;
    var height = [ 4, 8, 2, 0, 0, 5 ];
    document.write(numberOfElements(height, n));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
2
```