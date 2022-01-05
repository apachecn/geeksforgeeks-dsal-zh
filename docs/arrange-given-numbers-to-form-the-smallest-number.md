# 排列给定的数字形成最小的数字

> 原文:[https://www . geeksforgeeks . org/排列给定数字形成最小数字/](https://www.geeksforgeeks.org/arrange-given-numbers-to-form-the-smallest-number/)

给定一个整数元素的数组 **arr[]** ，任务是以这样的方式排列它们，使得这些数字形成最小可能的数字。
例如，如果给定的数组是{5，6，2，9，21，1}，那么排列将是 1212569。

**示例:**

> **输入:** arr[] = {5，6，2，9，21，1 }
> T3】输出: 1212569
> 
> **输入:** arr[] = {1，2，1，12，33，211，50}
> **输出:** 111221123350

**方法:**如果所有给定的数字最多只有一个数字，那么简单的方法是按升序排列所有数字。但是，如果有些数字超过一位数，那么这种方法就行不通了。
因此，我们必须通过以下方式比较任意两个元素来对数组进行排序:
如果元素是 **A** 和 **B** ，则比较 **(A + B)** 和 **(B + A)** ，其中 **+** 表示**串联**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <iostream>
using namespace std;

// Utility function to print
// the contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i];
}

// A comparison function that return true
// if 'AB' is smaller than 'BA' when
// we concatenate two numbers 'A' and 'B'
// For example, it will return true if
// we pass 12 and 24 as arguments.
// This function will be used by sort() function
bool compare(int num1, int num2)
{
    // to_string function is predefined function
    // to convert a number in string

    // Convert first number to string format
    string A = to_string(num1);

    // Convert second number to string format
    string B = to_string(num2);

    // Check if 'AB' is smaller or 'BA'
    // and return bool value since
    // comparison operator '<=' returns
    // true or false
    return (A + B) <= (B + A);
}

// Function to print the arrangement
// with the smallest value
void printSmallest(int N, int arr[])
{
    // If we pass the name of the comparison
    // function it will sort the array
    // according to the compare function
    sort(arr, arr + N, compare);

    // Print the sorted array
    printArr(arr, N);
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 2, 9, 21, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    printSmallest(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Utility function to print
    // the contents of an array
    public static void printArr(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i]);
    }

    // A comparison function that return negative
    // if 'AB' is smaller than 'BA' when
    // we concatenate two numbers 'A' and 'B'
    // For example, it will return negative value if
    // we pass 12 and 24 as arguments.
    // This function will be used during sort
    public static int compare(int num1, int num2)
    {

        // toString function is predefined function
        // to convert a number in string

        // Convert first number to string format
        String A = Integer.toString(num1);

        // Convert second number to string format
        String B = Integer.toString(num2);

        // Check if 'AB' is smaller or 'BA'
        // and return integer value
        return (A+B).compareTo(B+A);
    }

    // Function to print the arrangement
    // with the smallest value
    public static void printSmallest(int N, int[] arr)
    {

        // Sort using compare function which
        // is defined above
        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                if (compare(arr[i], arr[j]) > 0)
                {
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }

        // Print the sorted array
        printArr(arr, N);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 5, 6, 2, 9, 21, 1 };
        int N = arr.length;
        printSmallest(N, arr);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# the contents of an array
def printArr(arr, n):

    for i in range(0, n):
        print(arr[i], end = "")

# A comparison function that return true
# if 'AB' is smaller than 'BA' when
# we concatenate two numbers 'A' and 'B'
# For example, it will return true if
# we pass 12 and 24 as arguments.
# This function will be used by sort() function
def compare(num1, num2):

    # Convert first number to string format
    A = str(num1)

    # Convert second number to string format
    B = str(num2)

    # Check if 'AB' is smaller or 'BA'
    # and return bool value since
    # comparison operator '<=' returns
    # true or false
    return int(A + B) <= int(B + A)

def sort(arr):

    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):

            if compare(arr[i], arr[j]) == False:
                arr[i], arr[j] = arr[j], arr[i]

# Function to print the arrangement
# with the smallest value
def printSmallest(N, arr):

    # If we pass the name of the comparison
    # function it will sort the array
    # according to the compare function
    sort(arr)

    # Print the sorted array
    printArr(arr, N)

# Driver code
if __name__ == "__main__":

    arr = [5, 6, 2, 9, 21, 1]
    N = len(arr)
    printSmallest(N, arr)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation for above approach
using System;

class GFG
{

    // Utility function to print
    // the contents of an array
    public static void printArr(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i]);
    }

    // A comparison function that return negative
    // if 'AB' is smaller than 'BA' when
    // we concatenate two numbers 'A' and 'B'
    // For example, it will return negative value if
    // we pass 12 and 24 as arguments.
    // This function will be used during sort
    public static int compare(int num1, int num2)
    {

        // toString function is predefined function
        // to convert a number in string

        // Convert first number to string format
        String A = num1.ToString();

        // Convert second number to string format
        String B = num2.ToString();

        // Check if 'AB' is smaller or 'BA'
        // and return integer value
        return (A+B).CompareTo(B+A);
    }

    // Function to print the arrangement
    // with the smallest value
    public static void printSmallest(int N, int[] arr)
    {

        // Sort using compare function which
        // is defined above
        for (int i = 0; i < N; i++)
        {
            for (int j = i + 1; j < N; j++)
            {
                if (compare(arr[i], arr[j]) > 0)
                {
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }

        // Print the sorted array
        printArr(arr, N);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 5, 6, 2, 9, 21, 1 };
        int N = arr.Length;
        printSmallest(N, arr);
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to print
// the contents of an array
function printArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i];
}

// A comparison function that return true
// if 'AB' is smaller than 'BA' when
// we concatenate two numbers 'A' and 'B'
// For example, it will return true if
// we pass 12 and 24 as arguments.
// This function will be used by sort() function
function compare($num1, $num2)
{
    // to_string function is predefined function
    // to convert a number in string

    // Convert first number to string format
    $A = (string)$num1 ;

    // Convert second number to string format
    $B = (string)$num2 ;

    // Check if 'AB' is smaller or 'BA'
    // and return bool value since
    // comparison operator '<=' returns
    // true or false
    if((int)($A . $B) <= (int)($B . $A))
    {
        return true;
    }
    else
        return false;
}

function sort_arr($arr)
{

    for ($i = 0; $i < count($arr) ; $i++)
    {
        for ($j = $i + 1;$j < count($arr) ; $j++)
        {
            if (compare($arr[$i], $arr[$j]) == false)
            {
                $temp = $arr[$i] ;
                $arr[$i] = $arr[$j] ;
                $arr[$j] = $temp ;
            }
        }
    }
        return $arr ;
    }

// Function to print the arrangement
// with the smallest value
function printSmallest($N, $arr)
{
    // If we pass the name of the comparison
    // function it will sort the array
    // according to the compare function
    $arr = sort_arr($arr);

    // Print the sorted array
    printArr($arr, $N);
}

    // Driver code
    $arr = array(5, 6, 2, 9, 21, 1 );
    $N = count($arr);
    printSmallest($N, $arr);

    // This code is contributed by Ryuga

?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Utility function to print
    // the contents of an array
    function printArr(arr,n)
    {
        for (let i = 0; i < n; i++)
            document.write(arr[i]);
    }

    // A comparison function that return true
    // if 'AB' is smaller than 'BA' when
    // we concatenate two numbers 'A' and 'B'
    // For example, it will return true if
    // we pass 12 and 24 as arguments.
    // This function will be used by sort() function
    function compare(num1,num2)
    {
        // to_string function is predefined function
        // to convert a number in string

        // Convert first number to string format
        let A = num1.toString();

        // Convert second number to string format
        let B = num2.toString();

        // Check if 'AB' is smaller or 'BA'
        // and return bool value since
        // comparison operator '<=' returns
        // true or false
        return (A + B).localeCompare(B + A);
    }

    // Function to print the arrangement
    // with the smallest value
    function printSmallest(N,arr)
    {
        // If we pass the name of the comparison
        // function it will sort the array
        // according to the compare function
        // Sort using compare function which
        // is defined above
        for (let i = 0; i < N; i++)
        {
            for (let j = i + 1; j < N; j++)
            {
                if (compare(arr[i], arr[j]) > 0)
                {
                    let temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }

        // Print the sorted array
        printArr(arr,N);
    }

    // Driver code

    let arr = [ 5, 6, 2, 9, 21, 1 ];
    let N = arr.length;
    printSmallest(N,arr);
</script>
```

**Output:** 

```
1212569
```