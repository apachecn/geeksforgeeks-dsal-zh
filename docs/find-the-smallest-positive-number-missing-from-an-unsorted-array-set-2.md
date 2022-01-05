# 查找未排序数组中缺失的最小正数|集合 2

> 原文:[https://www . geeksforgeeks . org/find-最小正数-未排序数组集缺失-2/](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array-set-2/)

给定一个包含正负元素的未排序数组。使用恒定的额外空间，在 O(n)时间内找到数组中缺失的最小正数。允许修改原始数组。
**例:**

```
Input:  {2, 3, 7, 6, 8, -1, -10, 15}
Output: 1

Input:  { 2, 3, -7, 6, 8, 1, -10, 15 }
Output: 4

Input: {1, 1, 0, -1, -2}
Output: 2 
```

[Recommended: Please solve it on *“PRACTICE”* first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/smallest-positive-missing-number/0)

我们已经在[之前的](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)帖子中讨论了 O(n)时间和 O(1)额外空间的解决方案。在这篇文章中，讨论了另一种替代解决方案。
我们使给定数组元素对应的索引处的值等于一个数组元素。例如:考虑数组= {2，3，7，6，8，-1，-10，15}。为了标记这个数组中元素 2 的存在，我们使 arr[2-1] = 2。在数组下标[2-1]中，2 是要标记的元素，减去 1 是因为我们正在索引值范围[0，N-1]上映射元素值范围[1，N]。但是如果我们使 arr[1] = 2，我们将丢失存储在 arr[1]中的数据。为了避免这种情况，我们首先存储 arr[1]处的值，然后更新它。接下来，我们将标记 arr[1]中先前存在的元素的存在，即 3。显然，这导致了某种类型的随机遍历数组。现在我们必须指定一个条件来标记这个遍历的结束。有三个条件标志着这个遍历的结束:
1。如果要标记的元素是负数:不需要标记这个元素的存在，因为我们感兴趣的是找到第一个丢失的正整数。因此，如果找到了一个负元素，只要结束遍历，因为不再标记元素的存在。
2。如果要标记的元素大于 N:不需要标记这个元素的存在，因为如果这个元素存在，那么它肯定代替了大小为 N 的数组中[1，N]范围内的元素，从而确保我们的答案在[1，N]范围内。所以简单地结束遍历，因为不再标记元素的存在。
3。如果当前元素的存在已经被标记:假设被标记为存在的元素是 val。如果 arr[val-1] = val，那么我们已经标记了这个元素的存在。所以简单地结束遍历，因为不再标记元素的存在。
还要注意，在当前遍历中，范围[1，N]内的数组的所有元素都可能没有被标记为存在。为了确保该范围内的所有元素都被标记为存在，我们检查位于该范围内的数组的每个元素。如果该元素没有被标记，那么我们从该数组元素开始新的遍历。
在我们标记了位于范围[1，N]中的所有数组元素之后，我们检查哪个索引值 ind 不等于 ind+1。如果 arr[ind]不等于 ind+1，那么 ind+1 就是最小的正缺失数。回想一下，我们正在将索引值范围[0，N-1]映射到元素值范围[1，N]，因此 1 被添加到 ind。如果没有找到这样的 ind，那么数组中存在[1，N]范围内的所有元素。所以第一个缺失的正数是 N+1。
**这个解决方案在 O(n)时间内是如何工作的？**
观察在最坏的情况下[1，N]范围内的每个元素最多遍历两次。首先，从范围中的其他元素开始执行遍历。其次，当检查是否需要从此元素开始新的遍历来标记未标记元素的存在时。在最坏的情况下，数组中存在[1，N]范围内的每个元素，因此所有 N 个元素都被遍历两次。所以总计算量是 2*n，因此时间复杂度是 O(n)。
以下是上述方法的实施:

## C++

```
/* CPP program to find the smallest
  positive missing number */
#include <bits/stdc++.h>
using namespace std;

// Function to find smallest positive
// missing number.
int findMissingNo(int arr[], int n)
{
    // to store current array element
    int val;

    // to store next array element in
    // current traversal
    int nextval;

    for (int i = 0; i < n; i++) {

        // if value is negative or greater
        // than array size, then it cannot
        // be marked in array. So move to
        // next element.
        if (arr[i] <= 0 || arr[i] > n)
            continue;

        val = arr[i];

        // traverse the array until we
        // reach at an element which
        // is already marked or which
        // could not be marked.
        while (arr[val - 1] != val) {
            nextval = arr[val - 1];
            arr[val - 1] = val;
            val = nextval;
            if (val <= 0 || val > n)
                break;
        }
    }

    // find first array index which is
    // not marked which is also the
    // smallest positive missing
    // number.
    for (int i = 0; i < n; i++) {
        if (arr[i] != i + 1) {
            return i + 1;
        }
    }

    // if all indices are marked, then
    // smallest missing positive
    // number is array_size + 1.
    return n + 1;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 7, 6, 8, -1, -10, 15 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);
    int missing = findMissingNo(arr, arr_size);
    cout << "The smallest positive missing number is "
         << missing;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find the smallest
positive missing number */
import java.io.*;

class GFG {

    // Function to find smallest positive
    // missing number.
    static int findMissingNo(int []arr, int n)
    {
        // to store current array element
        int val;

        // to store next array element in
        // current traversal
        int nextval;

        for (int i = 0; i < n; i++) {

            // if value is negative or greater
            // than array size, then it cannot
            // be marked in array. So move to
            // next element.
            if (arr[i] <= 0 || arr[i] > n)
                continue;

            val = arr[i];

            // traverse the array until we
            // reach at an element which
            // is already marked or which
            // could not be marked.
            while (arr[val - 1] != val) {
                nextval = arr[val - 1];
                arr[val - 1] = val;
                val = nextval;
                if (val <= 0 || val > n)
                    break;
            }
        }

        // find first array index which is
        // not marked which is also the
        // smallest positive missing
        // number.
        for (int i = 0; i < n; i++) {
            if (arr[i] != i + 1) {
                return i + 1;
            }
        }

        // if all indices are marked, then
        // smallest missing positive
        // number is array_size + 1.
        return n + 1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 3, 7, 6, 8, -1, -10, 15 };
        int arr_size = arr.length;

        int missing = findMissingNo(arr, arr_size);

        System.out.println( "The smallest positive"
                + " missing number is " + missing);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find the smallest
# positive missing number

# Function to find smallest positive
# missing number.
def findMissingNo(arr, n):

    # to store current array element

    # to store next array element in
    # current traversal
    for i in range(n) :

        # if value is negative or greater
        # than array size, then it cannot
        # be marked in array. So move to
        # next element.
        if (arr[i] <= 0 or arr[i] > n):
            continue

        val = arr[i]

        # traverse the array until we
        # reach at an element which
        # is already marked or which
        # could not be marked.
        while (arr[val - 1] != val):
            nextval = arr[val - 1]
            arr[val - 1] = val
            val = nextval
            if (val <= 0 or val > n):
                break

    # find first array index which is
    # not marked which is also the
    # smallest positive missing
    # number.
    for i in range(n):
        if (arr[i] != i + 1) :
            return i + 1

    # if all indices are marked, then
    # smallest missing positive
    # number is array_size + 1.
    return n + 1

# Driver code
if __name__ == "__main__":
    arr = [ 2, 3, 7, 6, 8, -1, -10, 15 ]
    arr_size = len(arr)
    missing = findMissingNo(arr, arr_size)
    print( "The smallest positive",
           "missing number is ", missing)

# This code is contributed
# by ChitraNayal
```

## C#

```
/* C# program to find the smallest
positive missing number */
using System;

class GFG
{
    // Function to find smallest
    // positive missing number.
    static int findMissingNo(int []arr,
                             int n)
    {
        // to store current
        // array element
        int val;

        // to store next array element
        // in current traversal
        int nextval;

        for (int i = 0; i < n; i++)
        {

            // if value is negative or greater
            // than array size, then it cannot
            // be marked in array. So move to
            // next element.
            if (arr[i] <= 0 || arr[i] > n)
                continue;

            val = arr[i];

            // traverse the array until we
            // reach at an element which
            // is already marked or which
            // could not be marked.
            while (arr[val - 1] != val)
            {
                nextval = arr[val - 1];
                arr[val - 1] = val;
                val = nextval;
                if (val <= 0 || val > n)
                    break;
            }
        }

        // find first array index which
        // is not marked which is also
        // the smallest positive missing
        // number.
        for (int i = 0; i < n; i++)
        {
            if (arr[i] != i + 1)
            {
                return i + 1;
            }
        }

        // if all indices are marked,
        // then smallest missing
        // positive number is
        // array_size + 1.
        return n + 1;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = {2, 3, 7, 6,
                     8, -1, -10, 15};
        int arr_size = arr.Length;

        int missing = findMissingNo(arr, arr_size);

        Console.Write("The smallest positive" +
                        " missing number is " +
                                      missing);
    }
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the smallest positive
// missing number

// Function to find smallest
// positive missing number.
function findMissingNo($arr, $n)
{
    // to store current
    // array element
    $val;

    // to store next array element
    // in current traversal
    $nextval;

    for ($i = 0; $i < $n; $i++)
    {

        // if value is negative or
        // greater than array size,
        // then it cannot be marked
        // in array. So move to
        // next element.
        if ($arr[$i] <= 0 ||
            $arr[$i] > $n)
            continue;

        $val = $arr[$i];

        // traverse the array until
        // we reach at an element
        // which is already marked
        // or which could not be marked.
        while ($arr[$val - 1] != $val)
        {
            $nextval = $arr[$val - 1];
            $arr[$val - 1] = $val;
            $val = $nextval;
            if ($val <= 0 ||
                $val > $n)
                break;
        }
    }

    // find first array index
    // which is not marked
    // which is also the smallest
    // positive missing number.
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] != $i + 1)
        {
            return $i + 1;
        }
    }

    // if all indices are marked,
    // then smallest missing
    // positive number is
    // array_size + 1.
    return $n + 1;
}

// Driver code
$arr = array(2, 3, 7, 6, 8,
            -1, -10, 15);
$arr_size = sizeof($arr) /
            sizeof($arr[0]);
$missing = findMissingNo($arr,
                         $arr_size);
echo "The smallest positive " .
         "missing number is " ,
                      $missing;

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>

/* Javascript program to find the smallest
  positive missing number */

// Function to find smallest positive
// missing number.
function findMissingNo(arr, n)
{
    // to store current array element
    var val;

    // to store next array element in
    // current traversal
    var nextval;

    for (var i = 0; i < n; i++) {

        // if value is negative or greater
        // than array size, then it cannot
        // be marked in array. So move to
        // next element.
        if (arr[i] <= 0 || arr[i] > n)
            continue;

        val = arr[i];

        // traverse the array until we
        // reach at an element which
        // is already marked or which
        // could not be marked.
        while (arr[val - 1] != val) {
            nextval = arr[val - 1];
            arr[val - 1] = val;
            val = nextval;
            if (val <= 0 || val > n)
                break;
        }
    }

    // find first array index which is
    // not marked which is also the
    // smallest positive missing
    // number.
    for (var i = 0; i < n; i++) {
        if (arr[i] != i + 1) {
            return i + 1;
        }
    }

    // if all indices are marked, then
    // smallest missing positive
    // number is array_size + 1.
    return n + 1;
}

// Driver code
var arr = [ 2, 3, 7, 6, 8, -1, -10, 15 ];
var arr_size = arr.length;
var missing = findMissingNo(arr, arr_size);
document.write(  "The smallest positive missing number is "
     + missing);

</script>
```

**Output:** 

```
The smallest positive missing number is 1
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)