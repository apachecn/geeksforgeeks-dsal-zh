# 求给定圆的两个部分的最小角度差的程序

> 原文:[https://www . geesforgeks . org/program-find-最小差-角度-两部分-给定-圆/](https://www.geeksforgeeks.org/program-find-smallest-difference-angles-two-parts-given-circle/)

给定一个圆分成 n 个部分，作为一个大小为 n 的数组。数组的第 I 个元素表示一个部分的角度。我们的任务是用这些零件制造两个连续的零件，使这两个零件的角度差最小。
**例:**

```
Input : arr[] = {90, 90, 90, 90}
Output : 0
In this example, we can take 1 and 2 
pieces and 3 and 4 pieces. Then the 
answer is |(90 + 90) - (90 + 90)| = 0.

Input : arr[] = {170, 30, 150, 10}
Output : 0
In this example, we can take 1 and 4, 
and 2 and 3 pieces. So the answer is 
|(170 + 10) - (30 + 150)| = 0.

Input : arr[] = {100, 100, 160}
Output : 40
```

我们可以注意到，如果一个部分是连续的，那么所有剩余的部分也形成一个连续的部分。如果第一部分的角度等于 x，那么第一和第二部分的角度之差为| x –( 360–x)| = | 2 * x–360 | = 2 * | x–180 |。所以对于每一个可能的连续部分，我们可以统计它的角度，更新答案。

## C++

```
// CPP program to find minimum
// difference of angles of two
// parts of given circle.
#include <bits/stdc++.h>
using namespace std;

// Returns the minimum difference
// of angles.
int findMinimumAngle(int arr[], int n)
{
    int l = 0, sum = 0, ans = 360;
    for (int i = 0; i < n; i++) {
        // sum of array
        sum += arr[i];

        while (sum >= 180) {

            // calculating the difference of
            // angles and take minimum of
            // previous and newly calculated
            ans = min(ans, 2 * abs(180 - sum));
            sum -= arr[l];
            l++;
        }

        ans = min(ans, 2 * abs(180 - sum));
    }
    return ans;
}

// driver code
int main()
{
    int arr[] = { 100, 100, 160 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMinimumAngle(arr, n) << endl;
    return 0;
}

// This code is contributed by "Abhishek Sharma 44"
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find minimum
// difference of angles of two
// parts of given circle.
import java.util.*;

class Count{
    public static int findMinimumAngle(int arr[], int n)
    {
        int l = 0, sum = 0, ans = 360;
        for (int i = 0; i < n; i++)
        {
            // sum of array
            sum += arr[i];

            while (sum >= 180)
            {

                // calculating the difference of
                // angles and take minimum of
                // previous and newly calculated
                ans = Math.min(ans,
                            2 * Math.abs(180 - sum));
                sum -= arr[l];
                l++;
            }

            ans = Math.min(ans,
                            2 * Math.abs(180 - sum));
        }

        return ans;

    }

    public static void main(String[] args)
    {
        int arr[] = { 100, 100, 160 };
        int n = 3;
        System.out.print(findMinimumAngle(arr, n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# java program to find minimum
# difference of angles of two
# parts of given circle.
import math

# function returns the minimum
# difference of angles.
def findMinimumAngle (arr, n):
    l = 0
    _sum = 0
    ans = 360
    for i in range(n):

        #sum of array
        _sum += arr[i]

        while _sum >= 180:

            # calculating the difference of
            # angles and take minimum of
            # previous and newly calculated
            ans = min(ans, 2 * abs(180 - _sum))
            _sum -= arr[l]
            l+=1
        ans = min(ans, 2 * abs(180 - _sum))
    return ans

# driver code
arr = [100, 100, 160]
n = len(arr)
print(findMinimumAngle (arr, n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find minimum
// difference of angles of two
// parts of given circle.
using System;

class GFG
{
    public static int findMinimumAngle(int []arr, int n)
    {
        int l = 0, sum = 0, ans = 360;
        for (int i = 0; i < n; i++)
        {
            // sum of array
            sum += arr[i];

            while (sum >= 180)
            {

                // calculating the difference of
                // angles and take minimum of
                // previous and newly calculated
                ans = Math.Min(ans,
                      2 * Math.Abs(180 - sum));
                sum -= arr[l];
                l++;
            }

            ans = Math.Min(ans,
                        2 * Math.Abs(180 - sum));
        }

        return ans;

    }

    // Driver code
    public static void Main()
    {
        int []arr = { 100, 100, 160 };
        int n = 3;
        Console.WriteLine(findMinimumAngle(arr, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// difference of angles of two
// parts of given circle.

// Returns the minimum difference
// of angles.
function findMinimumAngle($arr, $n)
{
    $l = 0; $sum = 0; $ans = 360;
    for ($i = 0; $i < $n; $i++)
    {
        // sum of array
        $sum += $arr[$i];

        while ($sum >= 180)
        {

            // calculating the difference of
            // angles and take minimum of
            // previous and newly calculated
            $ans = min($ans, 2 *
                             abs(180 - $sum));
            $sum -= $arr[$l];
            $l++;
        }

        $ans = min($ans, 2 * abs(180 - $sum));
    }
    return $ans;
}

// Driver Code
$arr = array( 100, 100, 160 );
$n = sizeof($arr);
echo findMinimumAngle($arr, $n), "\n" ;

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// javascript program to find minimum
// difference of angles of two
// parts of given circle.

let MAXN = 109;

    function findMinimumAngle(arr, n)
    {
        let l = 0, sum = 0, ans = 360;
        for (let i = 0; i < n; i++)
        {
            // sum of array
            sum += arr[i];

            while (sum >= 180)
            {

                // calculating the difference of
                // angles and take minimum of
                // previous and newly calculated
                ans = Math.min(ans,
                            2 * Math.abs(180 - sum));
                sum -= arr[l];
                l++;
            }

            ans = Math.min(ans,
                            2 * Math.abs(180 - sum));
        }

        return ans;

    }

// Driver code

        let arr = [ 100, 100, 160 ];
        let n = 3;
        document.write(findMinimumAngle(arr, n));

</script>
```

**输出:**

```
40
```