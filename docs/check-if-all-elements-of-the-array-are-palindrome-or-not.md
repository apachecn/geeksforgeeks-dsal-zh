# 检查数组所有元素是否回文

> 原文:[https://www . geesforgeks . org/check-如果数组中的所有元素都是回文或非回文/](https://www.geeksforgeeks.org/check-if-all-elements-of-the-array-are-palindrome-or-not/)

给定一个由 **N** 元素组成的数组 **arr[]** 。任务是检查数组是否是**回文数组**，即数组的所有元素是否都是回文。
**举例:**

> **输入:** arr[] = {121，131，20}
> 输出:数组不是回文数组
> 对于给定的数组，元素 20 不是回文。因此，数组不是一个数组。
> **输入:** arr[] = {111，121，222，333，444}
> **输出:**数组是回文数组
> 对于给定的数组，数组的所有元素都是回文。因此，数组是一个数组。

**进场:**

*   遍历给定数组的所有元素，检查每个元素是否是回文。
*   如果是，打印数组是一个数组。
*   否则，打印数组不是一个数组。

以下是上述方法的实现:

## C++

```
// CPP implementation to check
// if an array is PalinArray or not
#include<bits/stdc++.h>
using namespace std;

    // Function to check if palindrome or not
    bool isPalindrome(int N)
    {
        string str = "" + N;
        int len = str.length();
        for (int i = 0; i < len / 2; i++) {
            if (str[i] != str[len - 1 - i])
                return false;
        }
        return true;
    }

    // Function to check
    // if an array is PalinArray or not
    bool isPalinArray(int arr[] , int n)
    {
        // Traversing each element of the array
        // and check if it is palindrome or not
        for (int i = 0; i < n; i++) {
            bool ans = isPalindrome(arr[i]);
            if (ans == false)
                return false;
        }
        return true;
    }

    // Driver code
    int main()
    {
        int arr[] = { 121, 131, 20 };

        // length of array
        int n = sizeof(arr)/sizeof(arr[0]);

        bool res = isPalinArray(arr, n);
        if (res == true)
            cout<<"Array is a PalinArray";
        else
            cout<<"Array is not a PalinArray";
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if an array is PalinArray or not
class GFG {

    // Function to check if palindrome or not
    static boolean isPalindrome(int N)
    {
        String str = "" + N;
        int len = str.length();
        for (int i = 0; i < len / 2; i++) {
            if (str.charAt(i) != str.charAt(len - 1 - i))
                return false;
        }
        return true;
    }

    // Function to check
    // if an array is PalinArray or not
    static boolean isPalinArray(int[] arr, int n)
    {
        // Traversing each element of the array
        // and check if it is palindrome or not
        for (int i = 0; i < n; i++) {
            boolean ans = isPalindrome(arr[i]);
            if (ans == false)
                return false;
        }
        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        int[] arr = { 121, 131, 20 };

        // length of array
        int n = arr.length;

        boolean res = isPalinArray(arr, n);
        if (res == true)
            System.out.println("Array is a PalinArray");
        else
            System.out.println("Array is not a PalinArray");
    }
}
```

## 蟒蛇 3

```
# Python3 implementation to check
# if an array is PalinArray or not

# Function to check if palindrome or not
def isPalindrome(N):
    str1 = "" + str(N)
    len1 = len(str1)
    for i in range(int(len1 / 2)):
        if (str1[i] != str1[len1 - 1 - i]):
            return False
    return True

# Function to check
# if an array is PalinArray or not
def isPalinArray(arr, n):

    # Traversing each element of the array
    # and check if it is palindrome or not
    for i in range(n):
        ans = isPalindrome(arr[i])
        if (ans == False):
            return False
    return True

# Driver code
if __name__ == '__main__':

    arr = [ 121, 131, 20 ]

    # length of array
    n = len(arr)
    res = isPalinArray(arr, n)
    if (res == True):
        print("Array is a PalinArray")
    else:
        print("Array is not a PalinArray")

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation to check
// if an array is PalinArray or not
using System;

class GFG
{

// Function to check if palindrome or not
static bool isPalindrome(int N)
{
    string str = "" + N;
    int len = str.Length;
    for (int i = 0; i < len / 2; i++)
    {
        if (str[i] != str[len - 1 - i ])
            return false;
    }
    return true;
}

// Function to check if an array is
// PalinArray or not
static bool isPalinArray(int[] arr, int n)
{
    // Traversing each element of the array
    // and check if it is palindrome or not
    for (int i = 0; i < n; i++)
    {
        bool ans = isPalindrome(arr[i]);
        if (ans == false)
            return false;
    }
    return true;
}

// Driver code
public static void Main()
{
    int[] arr = { 121, 131, 20 };

    // length of array
    int n = arr.Length;

    bool res = isPalinArray(arr, n);
    if (res == true)
        Console.WriteLine("Array is a PalinArray");
    else
        Console.WriteLine("Array is not a PalinArray");
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// if an array is PalinArray or not

// Function to check if palindrome or not
function isPalindrome($N)
{
    $str = "" . $N;
    $len = strlen($str);
    for ($i = 0; $i < $len / 2; $i++)
    {
        if ($str[$i] != $str[$len - 1 - $i])
            return false;
    }
    return true;
}

// Function to check if an array is
// PalinArray or not
function isPalinArray($arr , $n)
{
    // Traversing each element of the array
    // and check if it is palindrome or not
    for ($i = 0; $i < $n; $i++)
    {
        $ans = isPalindrome($arr[$i]);
        if ($ans == false)
            return false;
    }
    return true;
}

// Driver code
$arr = array(121, 131, 20);

// length of array
$n = sizeof($arr);

$res = isPalinArray($arr, $n);
if ($res == true)
    echo "Array is a PalinArray";
else
    echo "Array is not a PalinArray";

// This code is contributed by
// Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to check
    // if an array is PalinArray or not

    // Function to check if palindrome or not
    function isPalindrome(N)
    {
        let str = "" + N;
        let len = str.length;
        for (let i = 0; i < parseInt(len / 2, 10); i++)
        {
            if (str[i] != str[len - 1 - i ])
                return false;
        }
        return true;
    }

    // Function to check if an array is
    // PalinArray or not
    function isPalinArray(arr, n)
    {
        // Traversing each element of the array
        // and check if it is palindrome or not
        for (let i = 0; i < n; i++)
        {
            let ans = isPalindrome(arr[i]);
            if (ans == false)
                return false;
        }
        return true;
    }

    let arr = [ 121, 131, 20 ];

    // length of array
    let n = arr.length;

    let res = isPalinArray(arr, n);
    if (res == true)
        document.write("Array is a PalinArray");
    else
        document.write("Array is not a PalinArray");

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
Array is not a PalinArray
```