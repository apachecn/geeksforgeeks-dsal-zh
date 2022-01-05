# 检查数组是否回文的程序

> 原文:[https://www . geeksforgeeks . org/program-to-check-如果一个数组是回文或非回文/](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-palindrome-or-not/)

给定一个数组，任务是确定一个数组是否是回文。
**例:**

```
Input: arr[] = {3, 6, 0, 6, 3}
Output: Palindrome

Input: arr[] = {1, 2, 3, 4, 5}
Output: Not Palindrome
```

**进场:**

*   初始化标志以取消设置 **int 标志= 0** 。
*   循环数组直到大小为 n/2
*   循环检查**是否停止！= arr[n-i-1]** 然后设置**标志= 1** 和**断开**
*   循环结束后，如果设置了标志，打印**“不是回文”**否则打印**“回文”**

以下是上述方法的实施:

## C++

```
// C++ Program to check whether the
// Array is palindrome or not

#include <iostream>
using namespace std;

void palindrome(int arr[], int n)
{
    // Initialise flag to zero.
    int flag = 0;

    // Loop till array size n/2.
    for (int i = 0; i <= n / 2 && n != 0; i++) {

        // Check if first and last element are different
        // Then set flag to 1.
        if (arr[i] != arr[n - i - 1]) {
            flag = 1;
            break;
        }
    }

    // If flag is set then print Not Palindrome
    // else print Palindrome.
    if (flag == 1)
        cout << "Not Palindrome";
    else
        cout << "Palindrome";
}

// Driver code.
int main()
{
    int arr[] = { 1, 2, 3, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    palindrome(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check whether the
// Array is palindromic or not

class GfG {

    static void palindrome(int arr[], int n)
    {
        // Initialise flag to zero.
        int flag = 0;

        // Loop till array size n/2.
        for (int i = 0; i <= n / 2 && n != 0; i++) {

            // Check if first and last element are different
            // Then set flag to 1.
            if (arr[i] != arr[n - i - 1]) {
                flag = 1;
                break;
            }
        }

        // If flag is set then print Not Palindrome
        // else print Palindrome.
        if (flag == 1)
            System.out.println("Not Palindrome");
        else
            System.out.println("Palindrome");
    }

    // Driver code.
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 2, 1 };
        int n = arr.length;

        palindrome(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to check whether the
# Array is palindromic or not
def palindrome(arr, n):

    # Initialise flag to zero.
    flag = 0;

    # Loop till array size n/2.
    i = 0;
    while (i <= n // 2 and n != 0):

        # Check if first and last element
        # are different. Then set flag to 1.
        if (arr[i] != arr[n - i - 1]):
            flag = 1;
            break;
        i += 1;

    # If flag is set then print Not Palindrome
    # else print Palindrome.
    if (flag == 1):
        print("Not Palindrome");
    else:
        print("Palindrome");

# Driver code.
arr = [ 1, 2, 3, 2, 1 ];
n = len(arr);

palindrome(arr, n);

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# Program to check whether the
// Array is palindromic or not
class GfG
{

    static void palindrome(int []arr, int n)
    {
        // Initialise flag to zero.
        int flag = 0;

        // Loop till array size n/2.
        for (int i = 0; i <= n / 2 && n != 0; i++)
        {

            // Check if first and last element are different
            // Then set flag to 1.
            if (arr[i] != arr[n - i - 1])
            {
                flag = 1;
                break;
            }
        }

        // If flag is set then print Not Palindrome
        // else print Palindrome.
        if (flag == 1)
            System.Console.WriteLine("Not Palindrome");
        else
            System.Console.WriteLine("Palindrome");
    }

    // Driver code.
    static void Main()
    {
        int []arr = { 1, 2, 3, 2, 1 };
        int n = arr.Length;

        palindrome(arr, n);
    }
}

// This code is contributed by chadan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check whether the
// Array is palindrome or not

function palindrome($arr, $n)
{
    // Initialise flag to zero.
    $flag = 0;

    // Loop till array size n/2.
    for ($i = 0; $i <= $n / 2 &&
                 $n != 0; $i++)
    {

        // Check if first and last element are
        // different then set flag to 1.
        if ($arr[$i] != $arr[$n - $i - 1])
        {
            $flag = 1;
            break;
        }
    }

    // If flag is set then print Not Palindrome
    // else print Palindrome.
    if ($flag == 1)
        echo "Not Palindrome";
    else
        echo "Palindrome";
}

// Driver code.
$arr = array( 1, 2, 3, 2, 1 );
$n = count($arr);

palindrome($arr, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript Program to check whether the
// Array is palindrome or not

function palindrome(arr, n)
{
    // Initialise flag to zero.
    let flag = 0;

    // Loop till array size n/2.
    for (let i = 0; i <= n / 2 && n != 0; i++) {

        // Check if first and last element are different
        // Then set flag to 1.
        if (arr[i] != arr[n - i - 1]) {
            flag = 1;
            break;
        }
    }

    // If flag is set then print Not Palindrome
    // else print Palindrome.
    if (flag == 1)
        document.write("Not Palindrome");
    else
        document.write("Palindrome");
}

// Driver code.

    let arr = [ 1, 2, 3, 2, 1 ];
    let n = arr.length;

    palindrome(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Palindrome
```

**相关文章:** [使用递归检查数组是否是回文的程序](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-palindrome-or-not-using-recursion/)