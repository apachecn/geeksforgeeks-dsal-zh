# 检查一个阵列是否为波阵

> 原文:[https://www . geesforgeks . org/check-if-a-array-wave-array/](https://www.geeksforgeeks.org/check-if-an-array-is-wave-array/)

给定一个 N 个正整数的数组。任务是检查数组是否[按波形排序。](https://www.geeksforgeeks.org/sort-array-wave-form-2/)
**例** :

```
Input: arr[] = {1, 2, 3, 4, 5}
Output: NO

Input: arr[] = {1, 5, 3, 7, 2, 8, 6}
Output: YES
```

**进场:**

*   首先检查索引 1 处的元素，即 A[1]，并观察模式。
*   如果 arr[1]大于它的左元素和右元素，那么这个模式将被其他元素跟随。
*   否则如果 arr[1]小于它的左右元素，那么这个模式将被其他元素跟随。
*   检查上述步骤中发现的相同模式。如果在任何时候，这个规则违反了，返回假，否则返回真。

以下是上述方法的实现:

## C++

```
// CPP code to check if the array is wave array
#include <iostream>
using namespace std;

// Function to check if array is wave array
// arr : input array
// n : size of array
bool isWaveArray(int arr[], int n)
{

    bool result = true;

    /* Check the wave form
    * If arr[1] is greater than left and right
    * Same pattern will be followed by whole
    * elements, else reverse pattern
    * will be followed by array elements
    */
    if (arr[1] > arr[0] && arr[1] > arr[2]) {
        for (int i = 1; i < n - 1; i += 2) {

            if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
                result = true;
            }
            else {
                result = false;
                break;
            }
        }

        // Check for last element
        if (result == true && n % 2 == 0) {
            if (arr[n - 1] <= arr[n - 2]) {
                result = false;
            }
        }
    }
    else if (arr[1] < arr[0] && arr[1] < arr[2]) {
        for (int i = 1; i < n - 1; i += 2) {

            if (arr[i] < arr[i - 1] && arr[i] < arr[i + 1]) {
                result = true;
            }
            else {
                result = false;
                break;
            }
        }

        // Check for last element
        if (result == true && n % 2 == 0) {
            if (arr[n - 1] >= arr[n - 2]) {
                result = false;
            }
        }
    }

    return result;
}

// Driver Code
int main()
{

    // Array
    int arr[] = { 1, 3, 2, 4 };

    int n = sizeof(arr) / sizeof(int);

    if (isWaveArray(arr, n)) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if the array is wave array 

public class GFG {

    // Function to check if array is wave array
    // arr : input array
    // n : size of array
    static boolean isWaveArray(int arr[], int n)
    {

        boolean result = true;

        /* Check the wave form
        * If arr[1] is greater than left and right
        * Same pattern will be followed by whole 
        * elements, else reverse pattern
        * will be followed by array elements
        */
        if (arr[1] > arr[0] && arr[1] > arr[2]) {
            for (int i = 1; i < n - 1; i += 2) {

                if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
                    result = true;
                }
                else {
                    result = false;
                    break;
                }
            }

            // Check for last element
            if (result == true && n % 2 == 0) {
                if (arr[n - 1] <= arr[n - 2]) {
                    result = false;
                }
            }
        }
        else if (arr[1] < arr[0] && arr[1] < arr[2]) {
            for (int i = 1; i < n - 1; i += 2) {

                if (arr[i] < arr[i - 1] && arr[i] < arr[i + 1]) {
                    result = true;
                }
                else {
                    result = false;
                    break;
                }
            }

            // Check for last element
            if (result == true && n % 2 == 0) {
                if (arr[n - 1] >= arr[n - 2]) {
                    result = false;
                }
            }
        }

        return result;
    }

    // Driver code
    public static void main(String args[])
    {
          int arr[] = { 1, 3, 2, 4 };

            int n = arr.length;

            if (isWaveArray(arr, n)) {
                System.out.println("YES");
            }
            else {
                System.out.println("NO");
            }      
    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 code to check if
# the array is wave array

# Function to check if
# array is wave array
# arr : input array
# n : size of array
def isWaveArray(arr , n):

    result = True

    # Check the wave form
    # If arr[1] is greater than
    # left and right. Same pattern
    # will be followed by whole
    # elements, else reverse pattern
    # will be followed by array elements

    if (arr[1] > arr[0] and arr[1] > arr[2]):
        for i in range(1, n - 1, 2):

            if (arr[i] > arr[i - 1] and
                arr[i] > arr[i + 1]):
                result = True

            else :
                result = False
                break

        # Check for last element
        if (result == True and n % 2 == 0):
            if (arr[n - 1] <= arr[n - 2]) :
                result = False

    elif (arr[1] < arr[0] and
          arr[1] < arr[2]) :
        for i in range(1, n - 1, 2) :

            if (arr[i] < arr[i - 1] and
                arr[i] < arr[i + 1]):
                result = True

            else :
                result = False
                break

        # Check for last element
        if (result == True and n % 2 == 0) :
            if (arr[n - 1] >= arr[n - 2]) :
                result = False

    return result

# Driver Code
if __name__ == "__main__":

    # Array
    arr = [ 1, 3, 2, 4 ]

    n = len(arr)

    if (isWaveArray(arr, n)):
        print("YES")
    else:
        print("NO")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to check if the
// array is wave array
using System;

class GFG
{

// Function to check if array
// is wave array
// arr : input array
// n : size of array
static bool isWaveArray(int []arr, int n)
{

    bool result = true;

    /* Check the wave form
    * If arr[1] is greater than left
    * and right. Same pattern will be
    * followed by whole elements, else
    * reverse pattern will be followed
      by array elements */
    if (arr[1] > arr[0] && arr[1] > arr[2])
    {
        for (int i = 1; i < n - 1; i += 2)
        {

            if (arr[i] > arr[i - 1] &&
                arr[i] > arr[i + 1])
            {
                result = true;
            }
            else
            {
                result = false;
                break;
            }
        }

        // Check for last element
        if (result == true && n % 2 == 0)
        {
            if (arr[n - 1] <= arr[n - 2])
            {
                result = false;
            }
        }
    }
    else if (arr[1] < arr[0] &&
             arr[1] < arr[2])
    {
        for (int i = 1; i < n - 1; i += 2)
        {

            if (arr[i] < arr[i - 1] &&
                arr[i] < arr[i + 1])
            {
                result = true;
            }
            else
            {
                result = false;
                break;
            }
        }

        // Check for last element
        if (result == true && n % 2 == 0)
        {
            if (arr[n - 1] >= arr[n - 2])
            {
                result = false;
            }
        }
    }

    return result;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 3, 2, 4 };

    int n = arr.Length;

    if (isWaveArray(arr, n))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if the array is wave array

// Function to check if array is wave array
// arr : input array
// n : size of array
function isWaveArray( $arr, $n)
{

    $result = true;

    /* Check the wave form
    * If arr[1] is greater than left and right
    * Same pattern will be followed by whole
    * elements, else reverse pattern
    * will be followed by array elements
    */
    if ($arr[1] > $arr[0] &&
        $arr[1] > $arr[2])
    {
        for ( $i = 1; $i < ($n - 1); $i += 2)
        {

            if ($arr[$i] > $arr[$i - 1] &&
                $arr[$i] > $arr[$i + 1])
            {
                $result = true;
            }
            else
            {
                $result = false;
                break;
            }
        }

        // Check for last element
        if ($result == true && $n % 2 == 0)
        {
            if ($arr[$n - 1] <= $arr[$n - 2])
            {
                $result = false;
            }
        }
    }
    else if ($arr[1] < $arr[0] &&
             $arr[1] < $arr[2])
    {
        for ($i = 1; $i < $n - 1; $i += 2)
        {

            if ($arr[$i] < $arr[$i - 1] &&
                $arr[$i] < $arr[$i + 1])
            {
                $result = true;
            }
            else
            {
                $result = false;
                break;
            }
        }

        // Check for last element
        if ($result == true && $n % 2 == 0)
        {
            if ($arr[$n - 1] >= $arr[$n - 2])
            {
                $result = false;
            }
        }
    }

    return $result;
}

// Driver Code

// Array
$arr = array (1, 3, 2, 4 );
$n = sizeof($arr);
if (isWaveArray($arr, $n))
{
    echo "YES";
}
else
{
    echo "NO";
}

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript code to check if the array is wave array

    // Function to check if array is wave array
    // arr : input array
    // n : size of array
    function isWaveArray(arr, n)
    {

        let result = true;

        /* Check the wave form
        * If arr[1] is greater than left and right
        * Same pattern will be followed by whole
        * elements, else reverse pattern
        * will be followed by array elements
        */
        if (arr[1] > arr[0] && arr[1] > arr[2]) {
            for (let i = 1; i < n - 1; i += 2) {

                if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1]) {
                    result = true;
                }
                else {
                    result = false;
                    break;
                }
            }

            // Check for last element
            if (result == true && n % 2 == 0) {
                if (arr[n - 1] <= arr[n - 2]) {
                    result = false;
                }
            }
        }
        else if (arr[1] < arr[0] && arr[1] < arr[2]) {
            for (let i = 1; i < n - 1; i += 2) {

                if (arr[i] < arr[i - 1] && arr[i] < arr[i + 1]) {
                    result = true;
                }
                else {
                    result = false;
                    break;
                }
            }

            // Check for last element
            if (result == true && n % 2 == 0) {
                if (arr[n - 1] >= arr[n - 2]) {
                    result = false;
                }
            }
        }

        return result;
    }

    // Array
    let arr = [ 1, 3, 2, 4 ];

    let n = arr.length;

    if (isWaveArray(arr, n)) {
        document.write("YES");
    }
    else {
        document.write("NO");
    }

        // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
YES
```