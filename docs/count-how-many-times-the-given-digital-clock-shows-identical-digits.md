# 统计给定数字钟显示相同数字的次数

> 原文:[https://www . geeksforgeeks . org/count-给定数字时钟显示相同数字的次数/](https://www.geeksforgeeks.org/count-how-many-times-the-given-digital-clock-shows-identical-digits/)

给定一个普通的数字时钟，有 **h** 小时数和 **m** 分钟数，任务是找出时钟显示相同时间的次数。如果小时和分钟中的每个数字都相同，则称特定时间相同，即时间类型为 **D:D** 、 **D:DD** 、 **DD:D** 或 **DD:DD** 。
**注意**时间写在数字时钟上，没有任何前导零，时钟显示从 **0** 到**h–1**小时和 **0** 到**m–1**分钟之间的时间。相同时间的例子很少:

*   1:1
*   twenty two past ten p.m.
*   twenty seven to four
*   11:1

**例:**

> **输入:**小时= 24，分钟= 60
> **输出:** 19
> 时钟有 24 小时 60 分钟。
> 所以相同的时间是:
> 个位数的小时和个位数的分钟- > 0:0，1:1，2:2，…。，9:9
> 一位数小时和两位数分钟- > 1:11，2:22，3:33，4:44 和 5:55
> 两位数小时和一位数分钟- > 11:1 和 22:2
> 两位数小时和两位数分钟- > 11:11，22:22
> 总计= 10 + 5 + 2 + 2 = 19
> **输入:**小时

**方法:**正如我们在解释的例子中看到的，我们必须首先计算一位数(小时)的相同时间，然后是两位数的小时。在每一个计数过程中，我们需要考虑一位数的分钟数以及两位数的分钟数。
会有两个循环。第一个循环处理一位数的小时数。第二个是两位数的小时数。在每个循环中，应该有两个条件。首先，如果迭代器变量小于总分钟数，则递增计数器。其次，如果(迭代器变量+迭代器变量* 10)小于总分钟数，则递增计数器。最后，我们将得到时钟显示的完全相同的时间。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// identical times the clock shows
int countIdentical(int hours, int minutes)
{

    // To store the count of identical times
    // Initialized to 1 because of 0:0
    int i, count = 1;

    // For single digit hour
    for (i = 1; i <= 9 && i < hours; i++) {

        // Single digit minute
        if (i < minutes)
            count++;

        // Double digit minutes
        if ((i * 10 + i) < minutes)
            count++;
    }

    // For double digit hours
    for (i = 11; i <= 99 && i < hours; i = i + 11) {

        // Single digit minute
        if ((i % 10) < minutes)
            count++;

        // Double digit minutes
        if (i < minutes)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    int hours = 24;
    int minutes = 60;

      // Function Call
    cout << countIdentical(hours, minutes);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // Function to return the count of
    // identical times the clock shows
    static int countIdentical(int hours, int minutes)
    {

        // To store the count of identical times
        // Initialized to 1 because of 0:0
        int i, count = 1;

        // For single digit hour
        for (i = 1; i <= 9 && i < hours; i++) {

            // Single digit minute
            if (i < minutes) {
                count++;
            }

            // Double digit minutes
            if ((i * 10 + i) < minutes) {
                count++;
            }
        }

        // For double digit hours
        for (i = 11; i <= 99 && i < hours; i = i + 11) {

            // Double digit minutes
            if (i < minutes) {
                count++;
            }

            // Single digit minute
            if ((i % 10) < minutes) {
                count++;
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int hours = 24;
        int minutes = 60;

        // Function Call
        System.out.println(countIdentical(hours, minutes));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count of
# identical times the clock shows

def countIdentical(hours, minutes):

    # To store the count of identical times
    # Initialized to 1 because of 0:0
    count = 1
    i = 1

    # For single digit hour
    while(i <= 9 and i < hours):

        # Single digit minute
        if (i < minutes):
            count += 1

        # Double digit minutes
        if ((i * 10 + i) < minutes):
            count += 1

        i += 1

    # For double digit hours
    i = 11
    while(i <= 99 and i < hours):

         # Double digit minutes
        if (i < minutes):
            count += 1

        # Single digit minute
        if ((i % 10) < minutes):
            count += 1

        i += 11

    # Return the required count
    return count

# Driver code
if __name__ == '__main__':
    hours = 24
    minutes = 60

    # Function Call
    print(countIdentical(hours, minutes))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Function to return the count of
    // identical times the clock shows
    static int countIdentical(int hours, int minutes)
    {

        // To store the count of identical times
        // Initialized to 1 because of 0:0
        int i, count = 1;

        // For single digit hour
        for (i = 1; i <= 9 && i < hours; i++) {

            // Single digit minute
            if (i < minutes) {
                count++;
            }

            // Double digit minutes
            if ((i * 10 + i) < minutes) {
                count++;
            }
        }

        // For double digit hours
        for (i = 11; i <= 99 && i < hours; i = i + 11) {

            // Double digit minutes
            if (i < minutes) {
                count++;
            }

            // Single digit minute
            if ((i % 10) < minutes) {
                count++;
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int hours = 24;
        int minutes = 60;

        // Function Call
        Console.WriteLine(countIdentical(hours, minutes));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// identical times the clock shows
function countIdentical($hours, $minutes)
{

    // To store the count of identical times
    // Initialized to 1 because of 0:0
    $i;
    $count = 1;

    // For single digit hour
    for ($i = 1; $i <= 9 && $i < $hours; $i++)
    {

        // Single digit minute
        if ($i < $minutes)
            $count++;

        // Double digit minutes
        if (($i * 10 + $i) < $minutes)
            $count++;
    }

    // For double digit hours
    for ($i = 11; $i <= 99 &&
                  $i < $hours; $i = $i + 11)
    {

        // Double digit minutes
        if ($i < $minutes)
            $count++;

        // Single digit minute
        if (($i % 10) < $minutes)
            $count++;
    }

    // Return the required count
    return $count;
}

// Driver Code
$hours = 24;
$minutes = 60;

// Function call
echo countIdentical($hours, $minutes);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// javascript implementation of the above approach   
// Function to return the count of
// identical times the clock shows
    function countIdentical(hours , minutes) {

        // To store the count of identical times
        // Initialized to 1 because of 0:0
        var i, count = 1;

        // For single digit hour
        for (i = 1; i <= 9 && i < hours; i++) {

            // Single digit minute
            if (i < minutes) {
                count++;
            }

            // Double digit minutes
            if ((i * 10 + i) < minutes) {
                count++;
            }
        }

        // For var digit hours
        for (i = 11; i <= 99 && i < hours; i = i + 11) {

            // Double digit minutes
            if (i < minutes) {
                count++;
            }

            // Single digit minute
            if ((i % 10) < minutes) {
                count++;
            }
        }

        // Return the required count
        return count;
    }

    // Driver code

        var hours = 24;
        var minutes = 60;

        // Function Call
        document.write(countIdentical(hours, minutes));

// This code contributed by Rajput-Ji

</script>
```

**Output**

```
19
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)