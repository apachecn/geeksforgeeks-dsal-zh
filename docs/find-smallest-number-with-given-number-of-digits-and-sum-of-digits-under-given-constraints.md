# 在给定的约束条件下，求给定位数和位数之和的最小数

> 原文:[https://www . geesforgeks . org/find-给定约束下的最小位数和位数总和/](https://www.geeksforgeeks.org/find-smallest-number-with-given-number-of-digits-and-sum-of-digits-under-given-constraints/)

给定两个整数 **S** 和 **D** ，任务是找到具有 **D** 位数的数字及其位数之和为 **S** 的数字，使得数字中最大和最小位数之间的差值尽可能小。如果可能有多个这样的数字，请打印最小的数字。
**举例:**

> **输入:** S = 25，D = 4
> T3】输出: 6667
> 最大数字 7 和最小数字 6 之差为 1。
> **输入:** S = 27，D = 3
> **输出:** 999

**进场:**

*   在[这篇](https://www.geeksforgeeks.org/find-smallest-number-with-given-number-of-digits-and-digit-sum/)文章中已经讨论了给定位数和和的最小数。
*   在本文中，我们的想法是最小化所需数字中最大和最小数字之间的差异。因此，总和 s 应该均匀分布在 d 位数之间。
*   如果总和均匀分布，则差值最多为 1。当总和 s 可被 d 整除时，差值为零。在这种情况下，每个数字都有等于 s/d 的相同值
*   当总和 s 不能被 d 整除时，两者的差别就是 1。在这种情况下，在每个数字都被赋予 s/d 值后，s%d 总和值仍然被分配。
*   由于需要最小的数字，这个剩余的值平均分布在数字的最后% s 个数字中，即数字的最后% s 个数字加 1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number having
// sum of digits as s and d number of
// digits such that the difference between
// the maximum and the minimum digit
// the minimum possible
string findNumber(int s, int d)
{
    // To store the final number
    string num = "";

    // To store the value that is evenly
    // distributed among all the digits
    int val = s / d;

    // To store the remaining sum that still
    // remains to be distributed among d digits
    int rem = s % d;

    int i;

    // rem stores the value that still remains
    // to be distributed
    // To keep the difference of digits minimum
    // last rem digits are incremented by 1
    for (i = 1; i <= d - rem; i++) {
        num = num + to_string(val);
    }

    // In the last rem digits one is added to
    // the value obtained by equal distribution
    if (rem) {
        val++;
        for (i = d - rem + 1; i <= d; i++) {
            num = num + to_string(val);
        }
    }

    return num;
}

// Driver function
int main()
{
    int s = 25, d = 4;

    cout << findNumber(s, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the number having
// sum of digits as s and d number of
// digits such that the difference between
// the maximum and the minimum digit
// the minimum possible
static String findNumber(int s, int d)
{
    // To store the final number
    String num = "";

    // To store the value that is evenly
    // distributed among all the digits
    int val = s / d;

    // To store the remaining sum that still
    // remains to be distributed among d digits
    int rem = s % d;

    int i;

    // rem stores the value that still remains
    // to be distributed
    // To keep the difference of digits minimum
    // last rem digits are incremented by 1
    for (i = 1; i <= d - rem; i++)
    {
        num = num + String.valueOf(val);
    }

    // In the last rem digits one is added to
    // the value obtained by equal distribution
    if (rem > 0)
    {
        val++;
        for (i = d - rem + 1; i <= d; i++)
        {
            num = num + String.valueOf(val);
        }
    }
    return num;
}

// Driver function
public static void main(String[] args)
{
    int s = 25, d = 4;

    System.out.print(findNumber(s, d));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the number having
# sum of digits as s and d number of
# digits such that the difference between
# the maximum and the minimum digit
# the minimum possible
def findNumber(s, d) :

    # To store the final number
    num = ""

    # To store the value that is evenly
    # distributed among all the digits
    val = s // d

    # To store the remaining sum that still
    # remains to be distributed among d digits
    rem = s % d

    # rem stores the value that still remains
    # to be distributed
    # To keep the difference of digits minimum
    # last rem digits are incremented by 1
    for i in range(1, d - rem + 1) :
        num = num + str(val)

    # In the last rem digits one is added to
    # the value obtained by equal distribution
    if (rem) :
        val += 1
        for i in range(d - rem + 1, d + 1) :
            num = num + str(val)

    return num

# Driver function
if __name__ == "__main__" :

    s = 25
    d = 4

    print(findNumber(s, d))

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find the number having
    // sum of digits as s and d number of
    // digits such that the difference between
    // the maximum and the minimum digit
    // the minimum possible
    static String findNumber(int s, int d)
    {
        // To store the readonly number
        String num = "";

        // To store the value that is evenly
        // distributed among all the digits
        int val = s / d;

        // To store the remaining sum that still
        // remains to be distributed among d digits
        int rem = s % d;

        int i;

        // rem stores the value that still remains
        // to be distributed
        // To keep the difference of digits minimum
        // last rem digits are incremented by 1
        for (i = 1; i <= d - rem; i++)
        {
            num = num + String.Join("", val);
        }

        // In the last rem digits one is added to
        // the value obtained by equal distribution
        if (rem > 0)
        {
            val++;
            for (i = d - rem + 1; i <= d; i++)
            {
                num = num + String.Join("", val);
            }
        }
        return num;
    }

    // Driver function
    public static void Main(String[] args)
    {
        int s = 25, d = 4;

        Console.Write(findNumber(s, d));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find the number having
// sum of digits as s and d number of
// digits such that the difference between
// the maximum and the minimum digit
// the minimum possible
function findNumber(s, d)
{

    // To store the final number
    var num = [] ;

    // To store the value that is evenly
    // distributed among all the digits
    var val = parseInt(s / d);

    // To store the remaining sum that still
    // remains to be distributed among d digits
    var rem = s % d;

    // rem stores the value that still remains
    // to be distributed
    // To keep the difference of digits minimum
    // last rem digits are incremented by 1
    for (var i = 1; i <= d - rem; i++)
    {

       // num = num.concat(toString(val));
       num.push(val.toString());
    }

    // In the last rem digits one is added to
    // the value obtained by equal distribution
    if (rem != 0)
    {
        val++;
        for (var i = d - rem + 1; i <= d; i++)
        {
            // num = num + toString(val);
             num.push(val.toString());
        }
    }

    return num;
}

var s = 25, d = 4;
var n=findNumber(s, d);
for(var i = 0; i < n.length; i++)
{
    document.write(n[i]);
}

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
6667
```

**时间复杂度:**O(d)
T3】辅助空间: O(1)