# 对数组元素进行处理时永不变为负数的最小数

> 原文:[https://www . geesforgeks . org/最小数-永不变成负数-已处理-数组-元素/](https://www.geeksforgeeks.org/smallest-number-never-becomes-negative-processed-array-elements/)

给定一个大小为 n 的数组，你的目标是找到一个数，这样当在下面给定的条件下，从第 0 个索引到第(n-1)个索引，对每个数组元素处理这个数时，它永远不会变成负数。

1.  如果该数大于数组元素，则该数将增加该数与数组元素之差。
2.  如果该数小于数组元素，则该数将减去该数与数组元素之差。

**示例:**

```
Input : arr[] = {3 4 3 2 4}
Output : 4
Explanation : 
If we process 4 from left to right
in given array, we get following :
When processed with 3, it becomes 5.
When processed with 5, it becomes 6
When processed with 3, it becomes 9
When processed with 2, it becomes 16
When processed with 4, it becomes 28
We always get a positive number. For 
all values lower than 4, it would
become negative for some value of the 
array.

Input: arr[] = {4 4}
Output : 3
Explanation : 
When processed with 4, it becomes 2
When processed with next 4, it becomes 1
```

**简单的方法:**简单的方法是找到数组中最大的元素，并测试从 1 开始到最大元素的每个数字，它是否以 0 值穿过整个数组。

## C++

```
// C++ program to find the smallest number
// that never becomes positive when processed
// with given array elements.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

ll suitable_num(ll a[], int n)
{
    // Finding max element in the array
    ll max = *max_element(a, a + n);

    for (int x = 1; x < max; x++) {

        // Creating copy of i since it's 
        // getting modified at later steps.
        int num = x;

        // Checking that num doesn't becomes
        // negative.
        int j;
        for (j = 0; j < n; j++)
        { 
            if (num > a[j])
                num += (num - a[j]);
            else if (a[j] > num)
                num -= (a[j] - num);
            if (num < 0)
                break;
        }

        if (j == n)
            return x;       
    }

    return max;
}

// Driver code
int main()
{
    ll a[] = { 3, 4, 3, 2, 4 };
    int n = sizeof(a)/(sizeof(a[0]));
    cout << suitable_num(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find the smallest number
// that never becomes positive when processed
// with given array elements.
import java.util.Arrays;
public class Largest_Number_NotNegate
{
    static long suitable_num(long a[], int n)
    {
        // Finding max element in the array
        long max = Arrays.stream(a).max().getAsLong();

        for (int x = 1; x < max; x++) {

            // Creating copy of i since it's
            // getting modified at later steps.
            int num = x;

            // Checking that num doesn't becomes
            // negative.
            int j;
            for (j = 0; j < n; j++) {
                if (num > a[j])
                    num += (num - a[j]);
                else if (a[j] > num)
                    num -= (a[j] - num);
                if (num < 0)
                    break;
            }

            if (j == n)
                return x;
        }

        return max;
    }

    // Driver program to test above method
    public static void main(String[] args) {

        long a[] = { 3, 4, 3, 2, 4 };
        int n = a.length;
        System.out.println(suitable_num(a, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to find the smallest number
# that never becomes positive when processed
# with given array elements.
def suitable_num(a):
    mx = max(a)

    for x in range(1, mx):

        # Creating copy of i since it's 
        # getting modified at later steps.
        num = x

        # Checking that num doesn't becomes
        # negative.
        j = 0;
        while j < len(a):
            if num > a[j]:
                num += num - a[j]
            elif a[j] > num:
                num -= (a[j] - num)
            if num < 0:
                break
            j += 1
        if j == len(a):
            return x
    return mx

# Driver code
a =[ 3, 4, 3, 2, 4 ]
print suitable_num(a)

# This code is contributed by Sachin Bisht
```

## C#

```
// A C# program to find the smallest number
// that never becomes positive when processed
// with given array elements.
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class GFG
{
    static long suitable_num(long []a, int n)
    {
        // Finding max element in the array
        long max = a.Max();

        for (int x = 1; x < max; x++)
        {

            // Creating copy of i since it's
            // getting modified at later steps.
            long num = x;

            // Checking that num doesn't becomes
            // negative.
            int j;
            for (j = 0; j < n; j++)
            {
                if (num > a[j])
                    num += (num - a[j]);
                else if (a[j] > num)
                    num -= (a[j] - num);
                if (num < 0)
                    break;
            }

            if (j == n)
                return x;
        }
        return max;
    }

    // Driver Code
    public static void Main(String []args)
    {
        long []a = { 3, 4, 3, 2, 4 };
        int n = a.Length;
        Console.Write(suitable_num(a, n));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// A Javascript program to find the smallest number
// that never becomes positive when processed
// with given array elements.

    function suitable_num(a,n)
    {
        // Finding max element in the array
        let max = Math.max(...a)

        for (let x = 1; x < max; x++) {

            // Creating copy of i since it's
            // getting modified at later steps.
            let num = x;

            // Checking that num doesn't becomes
            // negative.
            let j;
            for (j = 0; j < n; j++) {
                if (num > a[j])
                    num += (num - a[j]);
                else if (a[j] > num)
                    num -= (a[j] - num);
                if (num < 0)
                    break;
            }

            if (j == n)
                return x;
        }

        return max;
    }

    // Driver program to test above method
    let a=[3, 4, 3, 2, 4];
    let n = a.length;
    document.write(suitable_num(a, n));

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
4
```

时间复杂度:O (n^2)
辅助空间:O (1)

**有效方法:**解决这个问题的有效方法是利用这样一个事实，当你到达最后一个数组元素时，我们开始的值至少可以是 0，这意味着假设最后一个数组元素是[n-1]，那么[n-2]处的值必须大于或等于[n-1]/2。

## C++

```
// Efficient C++ program to find the smallest
// number that never becomes positive when
// processed with given array elements.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

ll suitable_num(ll a[], int n)
{
    ll num = 0;

    // Calculating the suitable number at each step.
    for (int i = n - 1; i >= 0; i--)
        num = round((a[i] + num) / 2.0);

    return num;
}

// Driver code
int main()
{
    ll a[] = { 3, 4, 3, 2, 4 };
    int n = sizeof(a)/(sizeof(a[0]));
    cout << suitable_num(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find the smallest
// number that never becomes positive when
// processed with given array elements.
public class Largest_Number_NotNegate {
    static long suitable_num(long a[], int n) {
        long num = 0;

        // Calculating the suitable number at each step.
        for (int i = n - 1; i >= 0; i--)
            num = Math.round((a[i] + num) / 2.0);

        return num;
    }

    // Driver Program to test above function
    public static void main(String[] args) {

        long a[] = { 3, 4, 3, 2, 4 };
        int n = a.length;
        System.out.println(suitable_num(a, n));

    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Efficient Python program to find the smallest
# number that never becomes positive when
# processed with given array elements.
def suitable_num(a):
    num = 0

    # Calculating the suitable number at each step.
    i = len(a) - 1
    while i >= 0:
        num = round((a[i] + num) / 2.0)

        i -= 1
    return int(num)

# Driver code
a = [ 3, 4, 3, 2, 4 ]
print suitable_num(a)

# This code is contributed by Sachin Bisht
```

## C#

```
// Efficient C# program to find the smallest
// number that never becomes positive when
// processed with given array elements.
using System;

class GFG
{
static long suitable_num(long[] a, int n)
{
    long num = 0;

    // Calculating the suitable number
    // at each step.
    for (int i = n - 1; i >= 0; i--)
        num = (long)Math.Round((a[i] + num) / 2.0,
                                MidpointRounding.AwayFromZero);

    return num;
}

// Driver Code
public static void Main()
{
    long[] a = { 3, 4, 3, 2, 4 };
    int n = a.Length;
    Console.Write(suitable_num(a, n));
}
}

// This code is contributed by ita_c
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find the smallest
// number that never becomes positive when
// processed with given array elements.

function suitable_num(&$a, $n)
{
    $num = 0;

    // Calculating the suitable number
    // at each step.
    for ($i = $n - 1; $i >= 0; $i--)
        $num = round(($a[$i] + $num) / 2.0);

    return $num;
}

// Driver code
$a = array( 3, 4, 3, 2, 4 );
$n = sizeof($a);
echo suitable_num($a, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to find the smallest
// number that never becomes positive when
// processed with given array elements.
function suitable_num(a,n)
{
    let num = 0;

    // Calculating the suitable
    // number at each step.
    for(let i = n - 1; i >= 0; i--)
        num = Math.round((a[i] + num) / 2.0);

    return num;
}

// Driver code
let a = [ 3, 4, 3, 2, 4 ];
let n = a.length;

document.write(suitable_num(a, n));

// This code is contributed by rag2127

</script>
```

**输出:**

```
4
```

**时间复杂度:**O(n)
T3】辅助空间: O (1)

本文由 [**阿迪蒂亚·古普塔**](https://www.linkedin.com/in/aditya-gupta-437504a7?trk=hp-identity-name) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
参考:https://www.hackerrank.com/challenges/chief-hopper
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。