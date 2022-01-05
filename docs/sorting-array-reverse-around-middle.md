# 中间反绕排序数组

> 原文:[https://www . geesforgeks . org/sorting-array-reverse-环绕-middle/](https://www.geeksforgeeks.org/sorting-array-reverse-around-middle/)

考虑给定的数组 arr[]，我们需要找出是否可以用给定的操作对数组进行排序。操作为
1。我们必须从给定的阵列中选择一个子阵列，使得子阵列的中间元素(或者元素(在偶数
个元素的情况下))也是给定阵列的中间元素(或者元素(在偶数个元素的情况下))。
2。然后我们必须反转选定的子阵列，并将这个反转的子阵列放入阵列中。
以上操作我们想做多少次就做多少次。任务是找出我们是否能用给定的操作对数组进行排序。
**例:**

```
Input : arr[] = {1, 6, 3, 4, 5, 2, 7}
Output : Yes
We can choose sub-array[3, 4, 5] on 
reversing this we get [1, 6, 5, 4, 3, 2, 7]
again on selecting [6, 5, 4, 3, 2] and 
reversing this one we get [1, 2, 3, 4, 5, 6, 7] 
which is sorted at last thus it is possible
to sort on multiple reverse operation.

Input : arr[] = {1, 6, 3, 4, 5, 7, 2}
Output : No
```

**一种解决方案**是我们可以围绕中心旋转每个元素，这在数组中给出了两种可能性，即索引‘I’处的值或索引“length–1–I”处的值。
如果数组有 n 个元素，那么 2^n 组合是可能的，因此运行时间是 O(2^n).
**另一种解决方案**可以是制作数组副本并对复制的数组进行排序。然后将排序后的数组中的每个元素与原始数组的等价元素及其围绕中心旋转时的镜像进行比较。对数组进行排序需要 O(n*logn)，需要 2n 次比较，因此运行时间为 O(n*logn)。

## C++

```
// CPP program to find possibility to sort
// by multiple subarray reverse operarion
#include <bits/stdc++.h>
using namespace std;

bool ifPossible(int arr[], int n)
{
    int cp[n];

    // making the copy of the original array
    copy(arr, arr + n, cp);

    // sorting the copied array
    sort(cp, cp + n);

    for (int i = 0; i < n; i++) {

        // checking mirror image of elements of sorted
        // copy array and equivalent element of original
        // array
        if (!(arr[i] == cp[i]) && !(arr[n - 1 - i] == cp[i]))
            return false;
    }

    return true;
}

// driver code
int main()
{
    int arr[] = { 1, 7, 6, 4, 5, 3, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (ifPossible(arr, n))
       cout << "Yes";
    else
       cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find possibility to sort
// by multiple subarray reverse operation
import java.util.*;
class GFG {

    static boolean ifPossible(int arr[], int n)
    {

        // making the copy of the original array
        int copy[] = Arrays.copyOf(arr, arr.length);

        // sorting the copied array
        Arrays.sort(copy);

        for (int i = 0; i < n; i++) {

            // checking mirror image of elements of
            // sorted copy array and equivalent element
            // of original array
            if (!(arr[i] == copy[i]) && !(arr[n - 1 - i] == copy[i]))
                return false;
        }

        return true;
    }

    // driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 7, 6, 4, 5, 3, 2, 8 };
        int n = arr.length;
        if (ifPossible(arr, n))
           System.out.println("Yes");
        else
           System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# possibility to sort by
# multiple subarray reverse
# operarion

def ifPossible(arr, n):

    cp = [0] * n

    # making the copy of
    # the original array
    cp = arr

    # sorting the copied array
    cp.sort()

    for i in range(0 , n) :

        # checking mirror image of
        # elements of sorted copy
        # array and equivalent element
        # of original array
        if (not(arr[i] == cp[i]) and not
               (arr[n - 1 - i] == cp[i])):
            return False

    return True

# Driver code
arr = [1, 7, 6, 4, 5, 3, 2, 8]
n = len(arr)
if (ifPossible(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Smitha
```

## C#

```
// C# Program to answer queries on sum
// of sum of odd number digits of all
// the factors of a number
using System;

class GFG {

    static bool ifPossible(int []arr, int n)
    {
        int []cp = new int[n];

        // making the copy of the original
        // array
        Array.Copy(arr, cp, n);

        // sorting the copied array
        Array.Sort(cp);

        for (int i = 0; i < n; i++) {

            // checking mirror image of
            // elements of sorted copy
            // array and equivalent element
            // of original array
            if (!(arr[i] == cp[i]) &&
                 !(arr[n - 1 - i] == cp[i]))
                return false;
        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        int []arr = new int[]{ 1, 7, 6, 4,
                               5, 3, 2, 8 };
        int n = arr.Length;

        if (ifPossible(arr, n))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine( "No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find possibility to sort
// by multiple subarray reverse operarion
function ifPossible(&$arr, $n)
{
    $cp = array();

    // making the copy of the
    // original array
    $cp = $arr;

    // sorting the copied array
    sort($cp);

    for ($i = 0; $i < $n; $i++)
    {

        // checking mirror image of elements
        // of sorted copy array and equivalent
        // element of original array
        if (!($arr[$i] == $cp[$i]) &&
            !($arr[$n - 1 - $i] == $cp[$i]))
            return false;
    }

    return true;
}

// Driver code
$arr = array(1, 7, 6, 4, 5, 3, 2, 8);
$n = sizeof($arr);
if (ifPossible($arr, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find possibility to sort
// by multiple subarray reverse operation

    function ifPossible(arr, n)
    {

        // making the copy of the original array
        let copy = arr;

        // sorting the copied array
        copy.sort();

        for (let i = 0; i < n; i++) {

            // checking mirror image of elements of
            // sorted copy array and equivalent element
            // of original array
            if (!(arr[i] == copy[i]) && !(arr[n - 1 - i] == copy[i]))
                return false;
        }

        return true;
    }

// driver code

     let arr = [ 1, 7, 6, 4, 5, 3, 2, 8 ];
        let n = arr.length;
        if (ifPossible(arr, n))
           document.write("Yes");
        else
           document.write("No");;

</script>
```

**Output:** 

```
Yes
```