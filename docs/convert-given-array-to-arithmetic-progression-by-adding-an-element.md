# 通过添加元素

将给定数组转换为算术级数

> 原文:[https://www . geeksforgeeks . org/通过添加元素将给定数组转换为算术级数/](https://www.geeksforgeeks.org/convert-given-array-to-arithmetic-progression-by-adding-an-element/)

给定一个数组 **arr[]** ，任务是找到一个可以添加到数组中的元素，以便将其转换为算术级数。如果无法将给定数组转换为 AP，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，7}
> **输出:** 11
> 3，7 和 11 是有限的 AP 序列。
> 
> **输入:** a[] = {4，6，8，15}
> **输出:** -1

**进场:**

*   对数组进行排序，开始逐元素遍历数组元素，并注意两个连续元素之间的差异。
*   如果所有元素的差异相同，则打印**最后一个元素+共同差异**。
*   如果最多一对**(arr[I–1]，arr[i])** 和**的差异= 2 *所有其他元素的共同差异**，则打印**arr[I]–共同差异**。
*   否则打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include<bits/stdc++.h>
using namespace std;

// Function to return the number to be
// added
int getNumToAdd(int arr[], int n)
{
    sort(arr,arr+n);
    int d = arr[1] - arr[0];
    int numToAdd = -1;
    bool numAdded = false;

    for (int i = 2; i < n; i++) {
        int diff = arr[i] - arr[i - 1];

        // If difference of the current
        // consecutive elements is
        // different from the common
        // difference
        if (diff != d) {

            // If number has already been
            // chosen then it's not possible
            // to add another number
            if (numAdded)
                return -1;

            // If the current different is
            // twice the common difference
            // then a number can be added midway
            // from current and previous element
            if (diff == 2 * d) {
                numToAdd = arr[i] - d;

                // Number has been chosen
                numAdded = true;
            }

            // It's not possible to maintain
            // the common difference
            else
                return -1;
        }
    }

    // Return last element + common difference
    // if no element is chosen and the array
    // is already in AP
    if (numToAdd == -1)
        return (arr[n - 1] + d);

    // Else return the chosen number
    return numToAdd;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 5, 7, 11, 13, 15 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << getNumToAdd(arr, n);
}

// This code is contributed
// by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class GFG {

    // Function to return the number to be
    // added
    static int getNumToAdd(int arr[], int n)
    {
        Arrays.sort(arr);
        int d = arr[1] - arr[0];
        int numToAdd = -1;
        boolean numAdded = false;

        for (int i = 2; i < n; i++) {
            int diff = arr[i] - arr[i - 1];

            // If difference of the current
            // consecutive elements is
            // different from the common
            // difference
            if (diff != d) {

                // If number has already been
                // chosen then it's not possible
                // to add another number
                if (numAdded)
                    return -1;

                // If the current different is
                // twice the common difference
                // then a number can be added midway
                // from current and previous element
                if (diff == 2 * d) {
                    numToAdd = arr[i] - d;

                    // Number has been chosen
                    numAdded = true;
                }

                // It's not possible to maintain
                // the common difference
                else
                    return -1;
            }
        }

        // Return last element + common difference
        // if no element is chosen and the array
        // is already in AP
        if (numToAdd == -1)
            return (arr[n - 1] + d);

        // Else return the chosen number
        return numToAdd;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 3, 5, 7, 11, 13, 15 };
        int n = arr.length;
        System.out.println(getNumToAdd(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the number
# to be added
def getNumToAdd(arr, n):
    arr.sort(reverse = False)
    d = arr[1] - arr[0]
    numToAdd = -1
    numAdded = False

    for i in range(2, n, 1):
        diff = arr[i] - arr[i - 1]

        # If difference of the current consecutive
        # elements is different from the common
        # difference
        if (diff != d):

            # If number has already been chosen
            # then it's not possible to add
            # another number
            if (numAdded):
                return -1

            # If the current different is twice
            # the common difference then a
            # number can be added midway from
            # current and previous element
            if (diff == 2 * d):
                numToAdd = arr[i] - d

                # Number has been chosen
                numAdded = True

            # It's not possible to maintain
            # the common difference
            else:
                return -1

    # Return last element + common difference
    # if no element is chosen and the array
    # is already in AP
    if (numToAdd == -1):
        return (arr[n - 1] + d)

    # Else return the chosen number
    return numToAdd

# Driver code
if __name__ == '__main__':
    arr = [1, 3, 5, 7, 11, 13, 15]
    n = len(arr)
    print(getNumToAdd(arr, n))

# This code is contributed
# mohit kumar 29
```

## C#

```
// C# implementation of the approach

using System;
public class GFG {

    // Function to return the number to be
    // added
    static int getNumToAdd(int []arr, int n)
    {
        Array.Sort(arr);
        int d = arr[1] - arr[0];
        int numToAdd = -1;
        bool numAdded = false;

        for (int i = 2; i < n; i++) {
            int diff = arr[i] - arr[i - 1];

            // If difference of the current
            // consecutive elements is
            // different from the common
            // difference
            if (diff != d) {

                // If number has already been
                // chosen then it's not possible
                // to add another number
                if (numAdded)
                    return -1;

                // If the current different is
                // twice the common difference
                // then a number can be added midway
                // from current and previous element
                if (diff == 2 * d) {
                    numToAdd = arr[i] - d;

                    // Number has been chosen
                    numAdded = true;
                }

                // It's not possible to maintain
                // the common difference
                else
                    return -1;
            }
        }

        // Return last element + common difference
        // if no element is chosen and the array
        // is already in AP
        if (numToAdd == -1)
            return (arr[n - 1] + d);

        // Else return the chosen number
        return numToAdd;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 3, 5, 7, 11, 13, 15 };
        int n = arr.Length;
        Console.WriteLine(getNumToAdd(arr, n));
    }
}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number
// to be added
function getNumToAdd($arr, $n)
{
    sort($arr);
    $d = $arr[1] - $arr[0];
    $numToAdd = -1;
    $numAdded = false;

    for ($i = 2; $i < $n; $i++)
    {
        $diff = $arr[$i] - $arr[$i - 1];

        // If difference of the current
        // consecutive elements is
        // different from the common
        // difference
        if ($diff != $d)
        {

            // If number has already been
            // chosen then it's not possible
            // to add another number
            if ($numAdded)
                return -1;

            // If the current different is
            // twice the common difference
            // then a number can be added midway
            // from current and previous element
            if ($diff == 2 * $d)
            {
                $numToAdd = $arr[$i] - $d;

                // Number has been chosen
                $numAdded = true;
            }

            // It's not possible to maintain
            // the common difference
            else
                return -1;
        }
    }

    // Return last element + common difference
    // if no element is chosen and the array
    // is already in AP
    if ($numToAdd == -1)
        return ($arr[$n - 1] + $d);

    // Else return the chosen number
    return $numToAdd;
}

// Driver code
$arr = array( 1, 3, 5, 7, 11, 13, 15 );
$n = sizeof($arr);
echo getNumToAdd($arr, $n);

// This code is contributed by Sachin..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number to be
// added
function getNumToAdd(arr, n)
{
    arr.sort(function(a, b){return a - b});
    var d = arr[1] - arr[0];
    var numToAdd = -1;
    var numAdded = false;

    for(var i = 2; i < n; i++)
    {
        var diff = arr[i] - arr[i - 1];

        // If difference of the current
        // consecutive elements is
        // different from the common
        // difference
        if (diff != d)
        {

            // If number has already been
            // chosen then it's not possible
            // to add another number
            if (numAdded)
                return -1;

            // If the current different is
            // twice the common difference
            // then a number can be added midway
            // from current and previous element
            if (diff == 2 * d)
            {
                numToAdd = arr[i] - d;

                // Number has been chosen
                numAdded = true;
            }

            // It's not possible to maintain
            // the common difference
            else
                return -1;
        }
    }

    // Return last element + common difference
    // if no element is chosen and the array
    // is already in AP
    if (numToAdd == -1)
        return (arr[n - 1] + d);

    // Else return the chosen number
    return numToAdd;
}

// Driver code
var arr = [ 1, 3, 5, 7, 11, 13, 15 ];
var n = arr.length;
document.write(getNumToAdd(arr, n));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(n Log n)