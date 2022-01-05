# Java 中排序数组中的第一个严格意义上更大的元素

> 原文:[https://www . geeksforgeeks . org/first-严格意义上的 java 排序数组中的大元素/](https://www.geeksforgeeks.org/first-strictly-greater-element-in-a-sorted-array-in-java/)

给定一个排序数组和一个目标值，找到严格大于给定元素的第一个元素。

**示例:**

```
Input : arr[] = {1, 2, 3, 5, 8, 12} 
        Target = 5
Output : 4 (Index of 8)

Input : {1, 2, 3, 5, 8, 12} 
        Target = 8
Output : 5 (Index of 12)

Input : {1, 2, 3, 5, 8, 12} 
        Target = 15
Output : -1
```

一个**简单的解决方案**是线性遍历给定的数组，找到严格意义上更大的第一个元素。如果不存在这样的元素，则返回-1。

一个**高效的解决方案**是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。在一般的二分搜索法中，我们寻找出现在数组中的值。然而，有时我们需要找到大于目标的第一个元素。

为了验证该算法是否正确，请考虑正在进行的每个比较。如果我们找到一个不大于目标元素的元素，那么它和它下面的所有东西都不可能匹配，所以没有必要搜索那个区域。因此，我们可以搜索右半部分。如果我们找到一个比所讨论的元素更大的元素，那么它之后的任何东西也必须更大，所以它们不可能是第一个更大的元素，所以我们不需要搜索它们。因此，中间元素是最后可能的位置。

请注意，在每一次迭代中，我们都会考虑至少一半的剩余元素。如果顶部分支执行，那么[低，(低+高)/ 2]范围内的元素全部被丢弃，导致我们失去 floor((低+高)/ 2)–low+1 > =(低+高)/2–low =(高-低)/2 个元素。

如果底部分支执行，则[(低+高)/ 2 + 1，高]范围内的元素都将被丢弃。这使我们失去了高–地板(低+高)/ 2 + 1 >=高–(低+高)/ 2 =(高–低)/ 2 个元素。

因此，我们最终会在这个过程的 O(lg n)次迭代中找到比目标大的第一个元素。

## C++

```
// C++ program to find first element that
// is strictly greater than given target.
#include <iostream>
using namespace std;

int next(int arr[], int target, int end)
{
    int start = 0;

    int ans = -1;
    while (start <= end)
    {
        int mid = (start + end) / 2;

        // Move to right side if target is
        // greater.
        if (arr[mid] <= target)
            start = mid + 1;

        // Move left side.
        else
        {
            ans = mid;
            end = mid - 1;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 5, 8, 12};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << next(arr, 8, n);
    return 0;
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first element that
// is strictly greater than given target.

class GfG {
    private static int next(int[] arr, int target)
    {
        int start = 0, end = arr.length - 1;

        int ans = -1;
        while (start <= end) {
            int mid = (start + end) / 2;

            // Move to right side if target is
            // greater.
            if (arr[mid] <= target) {
                start = mid + 1;
            }

            // Move left side.
            else {
                ans = mid;
                end = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 2, 3, 5, 8, 12 };
        System.out.println(next(arr, 8));
    }
}
```

## 蟒蛇 3

```
# Python program to find first element that
# is strictly greater than given target.

def next(arr, target):
    start = 0;
    end = len(arr) - 1;

    ans = -1;
    while (start <= end):
        mid = (start + end) // 2;

        # Move to right side if target is
        # greater.
        if (arr[mid] <= target):
            start = mid + 1;

        # Move left side.
        else:
            ans = mid;
            end = mid - 1;

    return ans;

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 5, 8, 12];
    print(next(arr, 8));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find first element that
// is strictly greater than given target.
using System;

class GfG
{
    private static int next(int[] arr, int target)
    {
        int start = 0, end = arr.Length - 1;

        int ans = -1;
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // Move to right side if target is
            // greater.
            if (arr[mid] <= target)
            {
                start = mid + 1;
            }

            // Move left side.
            else
            {
                ans = mid;
                end = mid - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 5, 8, 12 };
        Console.WriteLine(next(arr, 8));
    }
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find first element that
// is strictly greater than given target.
function next0($arr, $target)
{
    $start = 0; $end = sizeof($arr) - 1;

    $ans = -1;
    while ($start <= $end)
    {
        $mid = (int)(($start + $end) / 2);

        // Move to right side if target is
        // greater.
        if ($arr[$mid] <= $target)
        {
            $start = $mid + 1;
        }

        // Move left side.
        else
        {
            $ans = $mid;
            $end = $mid - 1;
        }
    }
    return $ans;
}

// Driver code
{
    $arr = array( 1, 2, 3, 5, 8, 12 );
    echo(next0($arr, 8));
}

// This code  is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript program to find first element that
// is strictly greater than given target.
function next(arr, target)
{
    let start = 0, end = arr.length - 1;
    let ans = -1;

    while (start <= end)
    {
        let mid = parseInt((start + end) / 2, 10);

        // Move to right side if target is
        // greater.
        if (arr[mid] <= target)
        {
            start = mid + 1;
        }

        // Move left side.
        else
        {
            ans = mid;
            end = mid - 1;
        }
    }
    return ans;
}

// Driver code
let arr = [ 1, 2, 3, 5, 8, 12 ];
document.write(next(arr, 8));

// This code is contributed by decode2207

</script>
```

**Output:** 

```
5
```