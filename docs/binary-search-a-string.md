# 二分搜索法一弦

> 原文:[https://www.geeksforgeeks.org/binary-search-a-string/](https://www.geeksforgeeks.org/binary-search-a-string/)

给定一个字符串的排序数组和一个字符串 x，如果数组中有 x，则找到它的索引。

**示例:**

```
Input :  arr[] = {"contribute", "geeks", "ide", "practice"}, x = "ide"
Output :  2
The String x is present at index 2.

Input :  arr[] = {"contribute", "geeks", "ide", "practice"}, x = "zz"
Output :  -1
The String "zz" is not present. 
```

先决条件:[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，[Java 中的字符串比较](https://www.geeksforgeeks.org/compare-two-Strings-in-java/)
想法是将 x 与给定数组中的中间字符串进行比较。如果匹配，则返回 mid，否则如果小于 mid，则在左半部分搜索，否则在右半部分搜索。

## C++

```
// CPP program to implement Binary Search for strings
#include<bits/stdc++.h>
using namespace std;

    // Returns index of x if it is present in arr[],
    // else return -1
    int binarySearch(string arr[], string x,int n)
    {
        int l = 0 ;
        int r = n - 1;
        while (l <= r)
        {
            int m = l + (r - l) / 2;

        int res = -1000;   //some random value assigned because if res is already 0 then
                             //it will always return 0    
        if (x == (arr[m]))
            res = 0;

            // Check if x is present at mid
            if (res == 0)
                return m;

            // If x greater, ignore left half
            if (x > (arr[m]))
                l = m + 1;

            // If x is smaller, ignore right half
            else
                r = m - 1;
        }

        return -1;
    }

    // Driver code
    int main()
    {
        string arr[] = { "contribute", "geeks", "ide", "practice"};
        string x = "ide";
        int n = 4;
        int result = binarySearch(arr, x,n);

        if (result == -1)
            cout << ("Element not present");
        else
            cout << ("Element found at index ") << result;
    }

// This code is contributed by
// Shashank_Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Binary Search for strings
class GFG {

    // Returns index of x if it is present in arr[],
    // else return -1
    static int binarySearch(String[] arr, String x)
    {
        int l = 0, r = arr.length - 1;
        while (l <= r) {
            int m = l + (r - l) / 2;

            int res = x.compareTo(arr[m]);

            // Check if x is present at mid
            if (res == 0)
                return m;

            // If x greater, ignore left half
            if (res > 0)
                l = m + 1;

            // If x is smaller, ignore right half
            else
                r = m - 1;
        }

        return -1;
    }

    // Driver method to test above
    public static void main(String []args)
    {
        String[] arr = { "contribute", "geeks", "ide", "practice"};
        String x = "ide";
        int result = binarySearch(arr, x);

        if (result == -1)
            System.out.println("Element not present");
        else
            System.out.println("Element found at "
                              + "index " + result);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement Binary
# Search for strings

# Returns index of x if it is present
# in arr[], else return -1
def binarySearch(arr, x):
    l = 0
    r = len(arr)
    while (l <= r):
        m = l + ((r - l) // 2)

        res = (x == arr[m])

        # Check if x is present at mid
        if (res == 0):
            return m - 1

        # If x greater, ignore left half
        if (res > 0):
            l = m + 1

        # If x is smaller, ignore right half
        else:
            r = m - 1

    return -1

# Driver Code
if __name__ == "__main__":

    arr = ["contribute", "geeks",
               "ide", "practice"];
    x = "ide"
    result = binarySearch(arr, x)

    if (result == -1):
        print("Element not present")
    else:
        print("Element found at index" ,
                                 result)

# This code is contributed by ita_c
```

## C#

```
// C# program to implement Binary Search for strings

using System;

class GFG {

    // Returns index of x if it is present in arr[],
    // else return -1
    static int binarySearch(String[] arr, String x)
    {
        int l = 0, r = arr.Length - 1;
        while (l <= r) {
            int m = l + (r - l) / 2;

            int res = x.CompareTo(arr[m]);

            // Check if x is present at mid
            if (res == 0)
                return m;

            // If x greater, ignore left half
            if (res > 0)
                l = m + 1;

            // If x is smaller, ignore right half
            else
                r = m - 1;
        }

        return -1;
    }

    // Driver method to test above
    public static void Main(String []args)
    {
        String[] arr = { "contribute", "geeks", "ide", "practice"};
        String x = "ide";
        int result = binarySearch(arr, x);

        if (result == -1)
            Console.WriteLine("Element not present");
        else
            Console.WriteLine("Element found at "
                            + "index " + result);
    }
// This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement Binary
// Search for strings

// Returns index of x if it is present
// in arr[], else return -1
function binarySearch($arr, $x)
{
    $l = 0;
    $r = count($arr);
    while ($l <= $r)
    {
        $m = $l + (int)(($r - $l) / 2);

        $res = strcmp($x, $arr[$m]);

        // Check if x is present at mid
        if ($res == 0)
            return $m - 1;

        // If x greater, ignore left half
        if ($res > 0)
            $l = $m + 1;

        // If x is smaller, ignore right half
        else
            $r = $m - 1;
    }

    return -1;
}

// Driver Code
$arr = array("contribute", "geeks",
                "ide", "practice");
$x = "ide";
$result = binarySearch($arr, $x);

if ($result == -1)
    print("Element not present");
else
    print("Element found at index " .
                            $result);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to implement Binary Search for strings

// Returns index of x if it is present in arr[],
// else return -1
function binarySearch(arr,x)
{
    let l = 0, r = arr.length - 1;
        while (l <= r) {
            let m = l + Math.floor((r - l) / 2);

            let res = x.localeCompare(arr[m]);

            // Check if x is present at mid
            if (res == 0)
                return m;

            // If x greater, ignore left half
            if (res > 0)
                l = m + 1;

            // If x is smaller, ignore right half
            else
                r = m - 1;
        }

        return -1;
}

// Driver method to test above
let arr=["contribute", "geeks", "ide", "practice"];
let x = "ide";
let result = binarySearch(arr, x);
if (result == -1)
    document.write("Element not present<br>");
else
    document.write("Element found at "
                   + "index " + result+"<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Element found at index 2
```