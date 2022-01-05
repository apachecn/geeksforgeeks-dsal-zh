# 未排序数组中的前后搜索

> 原文:[https://www . geesforgeks . org/前后搜索未排序数组/](https://www.geeksforgeeks.org/front-and-back-search-in-unsorted-array/)

给定一个未排序的整数数组和一个元素 x，使用“前”和“后”搜索查找 x 是否出现在数组中。
示例:

```
Input : arr[] = {10, 20, 80, 30, 60, 50, 
                     110, 100, 130, 170}
          x = 110;
Output : Yes

Input : arr[] = {10, 20, 80, 30, 60, 50, 
                     110, 100, 130, 170}
           x = 175;
Output : No
```

一个简单的解决方案是执行[线性搜索](https://www.geeksforgeeks.org/linear-search/)。当要搜索的元素是数组中的最后一个元素时，线性搜索算法总是导致 O(n)的最坏情况复杂度。寻找有值元素的前后搜索算法 *x* 的工作方式如下:

1.  初始化索引*前面的*和*后面的*，分别指向数组的第一个和最后一个元素。
2.  如果*前*大于*后*，返回假。
3.  检查前后索引处的元素 *x* 。
4.  如果找到元素 *x* ，返回真。
5.  否则增加*前*和减少*后*进入步骤 2。

**要点:**

*   当元素在中间或不在数组中时，最差的情况复杂度是 O(n/2)(相当于 O(n))。
*   当元素是数组中的第一个或最后一个元素时，最佳的情况复杂度是 O(1)。

## C++

```
// CPP program to implement front and back
// search
#include<iostream>
using namespace std;

bool search(int arr[], int n, int x)
{
    // Start searching from both ends
    int front = 0, back = n - 1;

    // Keep searching while two indexes
    // do not cross.
    while (front <= back)
    {
        if (arr[front] == x || arr[back] == x)
          return true;
        front++;
        back--;
    }
    return false;
}

int main()
{
   int arr[] = {10, 20, 80, 30, 60, 50,
                     110, 100, 130, 170};
   int x = 130;
   int n = sizeof(arr)/sizeof(arr[0]);
   if (search(arr, n, x))
      cout << "Yes";
   else
      cout << "No";
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement front and back
// search
class GFG {

    static boolean search(int arr[], int n, int x)
    {

        // Start searching from both ends
        int front = 0, back = n - 1;

        // Keep searching while two indexes
        // do not cross.
        while (front <= back)
        {
            if (arr[front] == x || arr[back] == x)
                return true;
            front++;
            back--;
        }

        return false;
    }

    // driver code
    public static void main (String[] args)
    {
        int arr[] = {10, 20, 80, 30, 60, 50,
                        110, 100, 130, 170};
        int x = 130;
        int n = arr.length;

        if (search(arr, n, x))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to implement
# front and back search

def search(arr, n, x):

    # Start searching from both ends
    front = 0; back = n - 1

    # Keep searching while two
    # indexes do not cross.
    while (front <= back):

        if (arr[front] == x or arr[back] == x):
            return True
        front += 1
        back -= 1

    return False

# Driver code
arr = [10, 20, 80, 30, 60,
       50, 110, 100, 130, 170]
x = 130
n = len(arr)

if (search(arr, n, x)):
    print("Yes")
else:
    print("No")

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to implement front and back
// search
using System;

public class GFG {

    static bool search(int []arr, int n, int x)
    {

        // Start searching from both ends
        int front = 0, back = n - 1;

        // Keep searching while two indexes
        // do not cross.
        while (front <= back)
        {
            if (arr[front] == x || arr[back] == x)
                return true;
            front++;
            back--;
        }

        return false;
    }

    static public void Main ()
    {
        int []arr = {10, 20, 80, 30, 60, 50,
                    110, 100, 130, 170};
        int x = 130;
        int n = arr.Length;

        if (search(arr, n, x))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement front and back
// search

function search($arr, $n, $x)
{

    // Start searching from both ends
    $front = 0;
    $back = $n - 1;

    // Keep searching while two
    // indexes do not cross.
    while ($front <= $back)
    {
        if ($arr[$front] == $x ||
            $arr[$back] == $x)
        return true;
        $front++;
        $back--;
    }
    return false;
}

    // Driver Code
    $arr = array(10, 20, 80, 30, 60, 50,
                     110, 100, 130, 170);
    $x = 130;
    $n = sizeof($arr);
    if (search($arr, $n, $x))
        echo "Yes";
    else
        echo "No";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to implement front and back

    function search(arr, n, x)
    {

        // Start searching from both ends
        let front = 0, back = n - 1;

        // Keep searching while two indexes
        // do not cross.
        while (front <= back)
        {
            if (arr[front] == x || arr[back] == x)
                return true;
            front++;
            back--;
        }

        return false;
    }

// Driver Code

        let arr = [10, 20, 80, 30, 60, 50,
                        110, 100, 130, 170];
        let x = 130;
        let n = arr.length;

        if (search(arr, n, x))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by avijitmondal1998.
</script>
```

**Output:** 

```
Yes
```