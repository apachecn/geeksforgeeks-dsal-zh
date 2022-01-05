# 最大的字典式数组，最多有 K 次连续交换

> 原文:[https://www . geeksforgeeks . org/最大字典顺序数组最多 k 个连续交换/](https://www.geeksforgeeks.org/largest-lexicographic-array-with-at-most-k-consecutive-swaps/)

给定一个数组 arr[]，找到字典上最大的数组，该数组可以通过最多执行 k 次连续交换来获得。

**示例:**

```
Input : arr[] = {3, 5, 4, 1, 2}
        k = 3
Output : 5, 4, 3, 2, 1
Explanation : Array given : 3 5 4 1 2
After swap 1 : 5 3 4 1 2
After swap 2 : 5 4 3 1 2
After swap 3 : 5 4 3 2 1

Input : arr[] = {3, 5, 1, 2, 1}
        k = 3
Output : 5, 3, 2, 1, 1
```

**蛮力法:**生成数组的所有置换，然后选择满足最多 K 个置换条件的一个。这种方法的时间复杂度是 **O(n！)**。

**优化方法:**在这种贪婪方法中，首先找到数组中存在的最大元素，该元素大于(如果第一个位置元素不是最大的)第一个位置，并且可以通过最多 K 次交换放置在第一个位置。找到那个元素后，记下它的索引。然后，交换数组的元素并更新 K 值。对其他位置应用此过程，直到 k 非零或数组按字典顺序变得最大。

**以下是上述方法的实施:**

## C++

```
// C++ program to find lexicographically
// maximum value after k swaps.
#include <bits/stdc++.h>
using namespace std;

// Function which modifies the array
void KSwapMaximum(int arr[], int n, int k)
{
    for (int i = 0; i < n - 1 && k > 0; ++i) {

        // Here, indexPosition is set where we
        // want to put the current largest integer
        int indexPosition = i;
        for (int j = i + 1; j < n; ++j) {

            // If we exceed the Max swaps
            // then break the loop
            if (k <= j - i)
                break;

            // Find the maximum value from i+1 to
            // max k or n which will replace
            // arr[indexPosition]
            if (arr[j] > arr[indexPosition])
                indexPosition = j;
        }

        // Swap the elements from Maximum indexPosition
        // we found till now to the ith index
        for (int j = indexPosition; j > i; --j)
            swap(arr[j], arr[j - 1]);

        // Updates k after swapping indexPosition-i
        // elements
        k -= indexPosition - i;
    }
}

// Driver code
int main()
{
    int arr[] = { 3, 5, 4, 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    KSwapMaximum(arr, n, k);

    // Print the final Array
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// lexicographically
// maximum value after
// k swaps.
import java.io.*;

class GFG
{
    static void SwapInts(int array[],
                         int position1,
                         int position2)
    {
        // Swaps elements
        // in an array.

        // Copy the first
        // position's element
        int temp = array[position1];

        // Assign to the
        // second element
        array[position1] = array[position2];

        // Assign to the
        // first element
        array[position2] = temp;
    }

    // Function which
    // modifies the array
    static void KSwapMaximum(int []arr,
                             int n, int k)
    {
        for (int i = 0;
                 i < n - 1 && k > 0; ++i)
        {

            // Here, indexPosition
            // is set where we want to
            // put the current largest
            // integer
            int indexPosition = i;
            for (int j = i + 1; j < n; ++j)
            {

                // If we exceed the
                // Max swaps then
                // break the loop
                if (k <= j - i)
                    break;

                // Find the maximum value
                // from i+1 to max k or n
                // which will replace
                // arr[indexPosition]
                if (arr[j] > arr[indexPosition])
                    indexPosition = j;
            }

            // Swap the elements from
            // Maximum indexPosition
            // we found till now to
            // the ith index
            for (int j = indexPosition; j > i; --j)
                SwapInts(arr, j, j - 1);

            // Updates k after swapping
            // indexPosition-i elements
            k -= indexPosition - i;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int []arr = { 3, 5, 4, 1, 2 };
        int n = arr.length;
        int k = 3;

        KSwapMaximum(arr, n, k);

        // Print the final Array
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python program to find
# lexicographically
# maximum value after
# k swaps.

arr = [3, 5, 4, 1, 2]

# Function which
# modifies the array
def KSwapMaximum(n, k) :

    global arr
    for i in range(0, n - 1) :
        if (k > 0) :

            # Here, indexPosition
            # is set where we want to
            # put the current largest
            # integer
            indexPosition = i
            for j in range(i + 1, n) :        

                # If we exceed the Max swaps
                # then break the loop
                if (k <= j - i) :
                    break

                # Find the maximum value
                # from i+1 to max k or n
                # which will replace
                # arr[indexPosition]
                if (arr[j] > arr[indexPosition]) :
                    indexPosition = j

            # Swap the elements from
            # Maximum indexPosition
            # we found till now to
            # the ith index
            for j in range(indexPosition, i, -1) :
                t = arr[j]
                arr[j] = arr[j - 1]
                arr[j - 1] = t

            # Updates k after swapping
            # indexPosition-i elements
            k = k - indexPosition - i

# Driver code
n = len(arr)
k = 3

KSwapMaximum(n, k)

# Print the final Array
for i in range(0, n) :
    print ("{} " .
            format(arr[i]),
                 end = "")

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to find
// lexicographically
// maximum value after
// k swaps.
using System;

class GFG
{
    static void SwapInts(int[] array,
                         int position1,
                         int position2)
    {
        // Swaps elements in an array.

        // Copy the first position's element
        int temp = array[position1];

        // Assign to the second element
        array[position1] = array[position2];

        // Assign to the first element
        array[position2] = temp;
    }

    // Function which
    // modifies the array
    static void KSwapMaximum(int []arr,
                             int n, int k)
    {
        for (int i = 0;
                 i < n - 1 && k > 0; ++i)
        {

            // Here, indexPosition
            // is set where we want to
            // put the current largest
            // integer
            int indexPosition = i;
            for (int j = i + 1; j < n; ++j)
            {

                // If we exceed the
                // Max swaps then
                // break the loop
                if (k <= j - i)
                    break;

                // Find the maximum value
                // from i+1 to max k or n
                // which will replace
                // arr[indexPosition]
                if (arr[j] > arr[indexPosition])
                    indexPosition = j;
            }

            // Swap the elements from
            // Maximum indexPosition
            // we found till now to
            // the ith index
            for (int j = indexPosition; j > i; --j)
                SwapInts(arr, j, j - 1);

            // Updates k after swapping
            // indexPosition-i elements
            k -= indexPosition - i;
        }
    }

    // Driver code
    static void Main()
    {
        int []arr = new int[]{ 3, 5, 4, 1, 2 };
        int n = arr.Length;
        int k = 3;

        KSwapMaximum(arr, n, k);

        // Print the final Array
        for (int i = 0; i < n; ++i)
            Console.Write(arr[i] + " ");
    }
}
// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// lexicographically
// maximum value after
// k swaps.

function swap(&$x, &$y)
{
    $x ^= $y ^= $x ^= $y;
}

// Function which
// modifies the array
function KSwapMaximum(&$arr, $n, $k)
{
    for ($i = 0;
         $i < $n - 1 &&
         $k > 0; $i++)
    {

        // Here, indexPosition
        // is set where we want to
        // put the current largest
        // integer
        $indexPosition = $i;
        for ($j = $i + 1;
             $j < $n; $j++)
        {

            // If we exceed the Max swaps
            // then break the loop
            if ($k <= $j - $i)
                break;

            // Find the maximum value
            // from i+1 to max k or n
            // which will replace
            // arr[indexPosition]
            if ($arr[$j] > $arr[$indexPosition])
                $indexPosition = $j;
        }

        // Swap the elements from
        // Maximum indexPosition
        // we found till now to
        // the ith index
        for ($j = $indexPosition;
             $j > $i; $j--)
            swap($arr[$j], $arr[$j - 1]);

        // Updates k after swapping
        // indexPosition-i elements
        $k -= $indexPosition - $i;
    }
}

// Driver code
$arr = array( 3, 5, 4, 1, 2 );
$n = count($arr);
$k = 3;

KSwapMaximum($arr, $n, $k);

// Print the final Array
for ($i = 0; $i < $n; $i++)
    echo ($arr[$i]." ");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript program to find
// lexicographically
// maximum value after
// k swaps.

    function SwapLets(array, position1, position2)
    {
        // Swaps elements
        // in an array.

        // Copy the first
        // position's element
        let temp = array[position1];

        // Assign to the
        // second element
        array[position1] = array[position2];

        // Assign to the
        // first element
        array[position2] = temp;
    }

    // Function which
    // modifies the array
    function KSwapMaximum(arr, n, k)
    {
        for (let i = 0;
                 i < n - 1 && k > 0; ++i)
        {

            // Here, indexPosition
            // is set where we want to
            // put the current largest
            // integer
            let indexPosition = i;
            for (let j = i + 1; j < n; ++j)
            {

                // If we exceed the
                // Max swaps then
                // break the loop
                if (k <= j - i)
                    break;

                // Find the maximum value
                // from i+1 to max k or n
                // which will replace
                // arr[indexPosition]
                if (arr[j] > arr[indexPosition])
                    indexPosition = j;
            }

            // Swap the elements from
            // Maximum indexPosition
            // we found till now to
            // the ith index
            for (let j = indexPosition; j > i; --j)
                SwapLets(arr, j, j - 1);

            // Updates k after swapping
            // indexPosition-i elements
            k -= indexPosition - i;
        }
    }

// Driver code

        let arr = [ 3, 5, 4, 1, 2 ];
        let n = arr.length;
        let k = 3;

        KSwapMaximum(arr, n, k);

        // Print the final Array
        for (let i = 0; i < n; ++i)
            document.write(arr[i] + " ");

    // This code is contributed by coode_hunt.
</script>
```

**Output:** 

```
5 4 3 1 2
```

**时间复杂度:**O(N * N)
T3】辅助空间: O(1)