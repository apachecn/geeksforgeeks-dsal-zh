# 用左侧最小的元素替换每个元素

> 原文:[https://www . geeksforgeeks . org/用左侧最小的元素替换每个元素/](https://www.geeksforgeeks.org/replace-every-element-with-the-smallest-element-on-its-left-side/)

给定一个整数数组，任务是用其左侧的最小元素替换每个元素。
**注意:**将第一个元素替换为-1，因为它的左边没有元素。
**示例:**

```
Input: arr[] = {4, 5, 2, 1, 7, 6}
Output: -1 4 4 2 1 1
Since, 4 has no element in its left, so replace it by -1.
For 5, 4 is the smallest element in its left.
For 2, 4 is the smallest element in its left.
For 1, 2 is the smallest element in its left.
For 7, 1 is the smallest element in its left.
For 6, 1 is the smallest element in its left.

Input: arr[] = {3, 2, 5, 7, 1}
Output: -1 3 2 2 2
```

**进场:**

1.  维护一个存储最小元素的变量 min_ele。
2.  最初，min_ele 将等于第 0 个索引处的元素。
3.  首先用-1 替换 arr[0]，然后遍历数组
4.  然后用最小值替换该元素，如果该元素小于最小值，则更新最小值。
5.  打印修改后的数组。

以下是上述方法的实现:

## C++

```
// C++ program to Replace every
// element with the smaller element
// on its left side
#include <bits/stdc++.h>
using namespace std;

// Function to replace the elements
void ReplaceElements(int arr[], int n)
{
    // MIN value initialised
    // to element at 0th index
    int min_ele = arr[0];
    arr[0] = -1;

    for (int i = 1; i < n; ++i) {

        // If min_ele is smaller than arr[i]
        // then just replace arr[i] with min_ele
        if (min_ele < arr[i])
            arr[i] = min_ele;

        // Else if update the min_ele also
        else if (min_ele >= arr[i]) {
            int temp = arr[i];
            arr[i] = min_ele;
            min_ele = temp;
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 2, 1, 7, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Replace the elements
    // with the smaller element
    // on its left side
    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Replace every
// element with the smaller element
// on its left side

class GFG {

// Function to replace the elements
    static void ReplaceElements(int arr[], int n) {
        // MIN value initialised
        // to element at 0th index
        int min_ele = arr[0];
        arr[0] = -1;

        for (int i = 1; i < n; ++i) {

            // If min_ele is smaller than arr[i]
            // then just replace arr[i] with min_ele
            if (min_ele < arr[i]) {
                arr[i] = min_ele;
            } // Else if update the min_ele also
            else if (min_ele >= arr[i]) {
                int temp = arr[i];
                arr[i] = min_ele;
                min_ele = temp;
            }
        }
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {4, 5, 2, 1, 7, 6};
        int n = arr.length;

        // Replace the elements
        // with the smaller element
        // on its left side
        ReplaceElements(arr, n);

        // Print the modified array
        for (int i = 0; i < n; ++i) {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 program to Replace every
# element with the smaller element
# on its left side

# Function to replace the elements
def ReplaceElements(arr, n):

    # MIN value initialised
    # to element at 0th index
    min_ele = arr[0]
    arr[0] = -1

    for i in range(1, n):

        # If min_ele is smaller than arr[i]
        # then just replace arr[i] with min_ele
        if (min_ele < arr[i]):
            arr[i] = min_ele

        # Else if update the min_ele also
        elif (min_ele >= arr[i]) :
            temp = arr[i]
            arr[i] = min_ele
            min_ele = temp

# Driver code
if __name__ == "__main__":

    arr = [ 4, 5, 2, 1, 7, 6 ]
    n = len (arr)

    # Replace the elements
    # with the smaller element
    # on its left side
    ReplaceElements(arr, n)

    # Print the modified array
    for i in range( n):
        print (arr[i], end = " ")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to Replace every
// element with the smaller element
// on its left side
using System;
public class GFG {

// Function to replace the elements
    static void ReplaceElements(int []arr, int n) {
        // MIN value initialised
        // to element at 0th index
        int min_ele = arr[0];
        arr[0] = -1;

        for (int i = 1; i < n; ++i) {

            // If min_ele is smaller than arr[i]
            // then just replace arr[i] with min_ele
            if (min_ele < arr[i]) {
                arr[i] = min_ele;
            } // Else if update the min_ele also
            else if (min_ele >= arr[i]) {
                int temp = arr[i];
                arr[i] = min_ele;
                min_ele = temp;
            }
        }
    }

// Driver code
    public static void Main() {
        int []arr = {4, 5, 2, 1, 7, 6};
        int n = arr.Length;

        // Replace the elements
        // with the smaller element
        // on its left side
        ReplaceElements(arr, n);

        // Print the modified array
        for (int i = 0; i < n; ++i) {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code is contributed by Rajput-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Replace every
// element with the smaller element
// on its left side

// Function to replace the elements
function ReplaceElements($arr, $n)
{
    // MIN value initialised
    // to element at 0th index
    $min_ele = $arr[0];
    $arr[0] = -1;

    for ($i = 1; $i < $n; ++$i)
    {

        // If min_ele is smaller than arr[i]
        // then just replace arr[i] with min_ele
        if ($min_ele < $arr[$i])
            $arr[$i] = $min_ele;

        // Else if update the min_ele also
        else if ($min_ele >= $arr[$i])
        {
            $temp = $arr[$i];
            $arr[$i] = $min_ele;
            $min_ele = $temp;
        }
    }
    return $arr;
}

// Driver code
$arr = array(4, 5, 2, 1, 7, 6);
$n = sizeof($arr);

// Replace the elements
// with the smaller element
// on its left side
$arr1 = ReplaceElements($arr, $n);

// Print the modified array
for ($i = 0; $i < $n; ++$i)
    echo $arr1[$i] . " ";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
      // JavaScript program to Replace every
      // element with the smaller element
      // on its left side

      // Function to replace the elements
      function ReplaceElements(arr, n)
      {

        // MIN value initialised
        // to element at 0th index
        var min_ele = arr[0];
        arr[0] = -1;

        for (var i = 1; i < n; ++i)
        {

          // If min_ele is smaller than arr[i]
          // then just replace arr[i] with min_ele
          if (min_ele < arr[i]) arr[i] = min_ele;
          // Else if update the min_ele also
          else if (min_ele >= arr[i])
          {
            var temp = arr[i];
            arr[i] = min_ele;
            min_ele = temp;
          }
        }
      }

      // Driver code
      var arr = [4, 5, 2, 1, 7, 6];
      var n = arr.length;

      // Replace the elements
      // with the smaller element
      // on its left side
      ReplaceElements(arr, n);

      // Print the modified array
      for (var i = 0; i < n; ++i) document.write(arr[i] + " ");

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
-1 4 4 2 1 1
```

**时间复杂度:** O(N)