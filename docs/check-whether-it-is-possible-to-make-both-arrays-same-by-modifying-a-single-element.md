# 检查是否可以通过修改单个元素使两个数组相等

> 原文:[https://www . geesforgeks . org/check-是否有可能通过修改单个元素来使两个数组相同/](https://www.geeksforgeeks.org/check-whether-it-is-possible-to-make-both-arrays-same-by-modifying-a-single-element/)

给定两个整数序列“A”和“B”，以及一个整数“k”。任务是检查我们是否可以通过以下方式修改序列 A 中的任何一个元素来使两个序列相等:
我们可以将范围[-k，k]中的任何数字添加到 A 的任何元素中。该操作只能执行一次。如果可能，打印*是*，否则打印*否*。
**例:**

> **输入:** K = 2，A[] = {1，2，3}，B[] = {3，2，1}
> **输出:**是
> 0 可以添加到任何元素，两个序列将相等。
> **输入:** K = 4，A[] = {1，5}，B[] = {1，1}
> **输出:**是
> -4 可以加到 5 那么序列 A 就变成了{1，1}，等于序列 B.

**方法:**请注意，要使两个序列只移动一次就相等，两个序列中必须只有一个不匹配元素，并且它们之间的绝对差值必须小于或等于“k”。

*   对两个数组进行排序，并查找不匹配的元素。
*   如果有多个不匹配的元素，则打印“否”
*   否则，找出元素之间的绝对差异。
*   如果**差< = k** 则打印“是”，否则打印“否”。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if both
// sequences can be made equal
static bool check(int n, int k,
                    int *a, int *b)
{
    // Sorting both the arrays
    sort(a,a+n);
    sort(b,b+n);

    // Flag to tell if there are
    // more than one mismatch
    bool fl = false;

    // To stores the index
    // of mismatched element
    int ind = -1;
    for (int i = 0; i < n; i++)
    {
        if (a[i] != b[i])
        {

            // If there is more than one
            // mismatch then return False
            if (fl == true)
            {
                return false;
            }
            fl = true;
            ind = i;
        }
    }

    // If there is no mismatch or the
    // difference between the
    // mismatching elements is <= k
    // then return true
    if (ind == -1 | abs(a[ind] - b[ind]) <= k)
    {
        return true;
    }
    return false;

}

// Driver code
int main()
{
    int n = 2, k = 4;
    int a[] = {1, 5};
    int b[] = {1, 1};
    if (check(n, k, a, b))
    {
        printf("Yes");
    }
    else
    {
        printf("No");
    }
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;
class GFG
{

    // Function to check if both
    // sequences can be made equal
    static boolean check(int n, int k,
                        int[] a, int[] b)
    {

        // Sorting both the arrays
        Arrays.sort(a);
        Arrays.sort(b);

        // Flag to tell if there are
        // more than one mismatch
        boolean fl = false;

        // To stores the index
        // of mismatched element
        int ind = -1;
        for (int i = 0; i < n; i++)
        {
            if (a[i] != b[i])
            {

                // If there is more than one
                // mismatch then return False
                if (fl == true)
                {
                    return false;
                }
                fl = true;
                ind = i;
            }
        }

        // If there is no mismatch or the
        // difference between the
        // mismatching elements is <= k
        // then return true
        if (ind == -1 | Math.abs(a[ind] - b[ind]) <= k)
        {
            return true;
        }
        return false;

    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 2, k = 4;
        int[] a = {1, 5};
        int b[] = {1, 1};
        if (check(n, k, a, b))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to check if both
# sequences can be made equal
def check(n, k, a, b):

    # Sorting both the arrays
    a.sort()
    b.sort()

    # Flag to tell if there are
    # more than one mismatch
    fl = False

    # To stores the index
    # of mismatched element
    ind = -1
    for i in range(n):
        if(a[i] != b[i]):

            # If there is more than one
            # mismatch then return False
            if(fl == True):
                return False
            fl = True
            ind = i

    # If there is no mismatch or the
    # difference between the
    # mismatching elements is <= k
    # then return true
    if(ind == -1 or abs(a[ind]-b[ind]) <= k):
        return True
    return False

n, k = 2, 4
a =[1, 5]
b =[1, 1]
if(check(n, k, a, b)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to check if both
    // sequences can be made equal
    static bool check(int n, int k,
                        int[] a, int[] b)
    {

        // Sorting both the arrays
        Array.Sort(a);
        Array.Sort(b);

        // Flag to tell if there are
        // more than one mismatch
        bool fl = false;

        // To stores the index
        // of mismatched element
        int ind = -1;
        for (int i = 0; i < n; i++)
        {
            if (a[i] != b[i])
            {

                // If there is more than one
                // mismatch then return False
                if (fl == true)
                {
                    return false;
                }
                fl = true;
                ind = i;
            }
        }

        // If there is no mismatch or the
        // difference between the
        // mismatching elements is <= k
        // then return true
        if (ind == -1 | Math.Abs(a[ind] - b[ind]) <= k)
        {
            return true;
        }
        return false;
    }

    // Driver code
    public static void Main()
    {
        int n = 2, k = 4;
        int[] a = {1, 5};
        int[] b = {1, 1};
        if (check(n, k, a, b))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to check if both
// sequences can be made equal
function check($n, $k, &$a, &$b)
{

    // Sorting both the arrays
    sort($a);
    sort($b);

    // Flag to tell if there are
    // more than one mismatch
    $fl = False;

    // To stores the index
    // of mismatched element
    $ind = -1;
    for ($i = 0; $i < $n; $i++)
    {
        if($a[$i] != $b[$i])
        {

            // If there is more than one
            // mismatch then return False
            if($fl == True)
                return False;
            $fl = True;
            $ind = $i;
        }
    }

    // If there is no mismatch or the
    // difference between the
    // mismatching elements is <= k
    // then return true
    if($ind == -1 || abs($a[$ind] -
                         $b[$ind]) <= $k)
        return True;
    return False;

}

// Driver Code
$n = 2;
$k = 4;
$a = array(1, 5);
$b = array(1, 1);
if(check($n, $k, $a, $b))
    echo "Yes";
else
    echo "No";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript Implementation of above approach.

    // Function to check if both
    // sequences can be made equal
    function check(n, k, a, b)
    {

        // Sorting both the arrays
        a.sort();
        b.sort();

        // Flag to tell if there are
        // more than one mismatch
        let fl = false;

        // To stores the index
        // of mismatched element
        let ind = -1;
        for (let i = 0; i < n; i++)
        {
            if (a[i] != b[i])
            {

                // If there is more than one
                // mismatch then return False
                if (fl == true)
                {
                    return false;
                }
                fl = true;
                ind = i;
            }
        }

        // If there is no mismatch or the
        // difference between the
        // mismatching elements is <= k
        // then return true
        if (ind == -1 | Math.abs(a[ind] - b[ind]) <= k)
        {
            return true;
        }
        return false;

    }

    // Driver code

     let n = 2, k = 4;
        let a = [1, 5];
        let b = [1, 1];
        if (check(n, k, a, b))
        {
            document.write("Yes");
        }
        else
        {
            document.write("No");
        }

</script>
```

**Output:** 

```
Yes
```