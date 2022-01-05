# 检查一个数组是否包含给定范围的所有元素

> 原文:[https://www . geeksforgeeks . org/check-如果数组包含给定范围的所有元素/](https://www.geeksforgeeks.org/check-if-an-array-contains-all-elements-of-a-given-range/)

给出了一个包含正元素的数组。“a”和“B”是定义一个范围的两个数字。编写一个函数来检查数组是否包含给定范围内的所有元素。
**例:**

```
Input : arr[] = {1 4 5 2 7 8 3}
           A : 2, B : 5
Output : Yes

Input : arr[] = {1 4 5 2 7 8 3}
          A : 2, B : 6
Output : No
```

**方法一:(直观)**
最直观的方法是对数组进行排序，从大于‘A’的元素检查到大于‘B’的元素。如果这些元素按连续顺序排列，则数组中存在该范围内的所有元素。
时间复杂度:O(n log n)
辅助空间:O(1)
**方法 2 : (Hashing)**
我们可以维护一个计数数组或哈希表，存储数组中所有在 A…B 范围内的数字的计数，然后我们可以简单的检查每个数字是否至少出现一次。
时间复杂度:O(n)
辅助空间:O(max_element)
**方法三:(最佳)**
做数组的线性遍历。如果在给定范围内找到一个元素，即|arr[i]| > = A 和|arr[i]| < =B

## C++

```
#include <iostream>
using namespace std;

// Function to check the array for elements in
// given range
bool check_elements(int arr[], int n, int A, int B)
{
    // Range is the no. of elements that are
    // to be checked
    int range = B - A;

    // Traversing the array
    for (int i = 0; i < n; i++) {

        // If an element is in range
        if (abs(arr[i]) >= A && abs(arr[i]) <= B) {

            // Negating at index ‘element – A’
            int z = abs(arr[i]) - A;
            if (arr[z] > 0) {
                arr[z] = arr[z] * -1;
            }
        }
    }

    // Checking whether elements in range 0-range
    // are negative
    int count=0;
    for (int i = 0; i <= range && i<n; i++) {

        // Element from range is missing from array
        if (arr[i] > 0)
            return false;
        else
            count++;
    }
     if(count!= (range+1))
        return false;
    // All range elements are present
    return true;
}

// Driver code
int main()
{
    // Defining Array and size
    int arr[] = { 1, 4, 5, 2, 7, 8, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // A is lower limit and B is the upper limit
    // of range
    int A = 2, B = 5;

    // True denotes all elements were present
    if (check_elements(arr, n, A, B))
        cout << "Yes";

    // False denotes any element was not present
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Check if an array contains
// all elements of a given range
import java.util.*;

class GFG {

    // Function to check the array for elements in
    // given range
     public static boolean check_elements(int arr[], int n,
                                             int A, int B)
    {
        // Range is the no. of elements that are
        // to be checked
        int range = B - A;

        // Traversing the array
        for (int i = 0; i < n; i++) {

            // If an element is in range
            if (Math.abs(arr[i]) >= A &&
                           Math.abs(arr[i]) <= B) {

                int z = Math.abs(arr[i]) - A;
                if (arr[z] > 0) {
                    arr[z] = arr[z] * -1;
                }
            }
        }

        // Checking whether elements in range 0-range
        // are negative
        int count=0;

        for (int i = 0; i <= range && i<n; i++) {

            // Element from range is missing from array
            if (arr[i] > 0)
                return false;
            else
                count++;
        }

        if(count!= (range+1))
            return false;

        // All range elements are present
        return true;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        // Defining Array and size
        int arr[] = { 1, 4, 5, 2, 7, 8, 3 };
        int n = arr.length;

        // A is lower limit and B is the upper limit
        // of range
        int A = 2, B = 5;

        // True denotes all elements were present
        if (check_elements(arr, n, A, B))
            System.out.println("Yes");

        // False denotes any element was not present
        else
            System.out.println("No");
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Function to check the array for
# elements in given range
def check_elements(arr, n, A, B) :

    # Range is the no. of elements
    # that are to be checked
    rangeV = B - A

    # Traversing the array
    for i in range(0, n):

        # If an element is in range
        if (abs(arr[i]) >= A and
            abs(arr[i]) <= B) :

            # Negating at index ‘element – A’
            z = abs(arr[i]) - A
            if (arr[z] > 0) :
                arr[z] = arr[z] * -1

    # Checking whether elements in
    # range 0-range are negative
    count = 0
    for i in range(0, rangeV + 1):
        if i >= n:
            break

        # Element from range is
        # missing from array
        if (arr[i] > 0):
            return False
        else:
            count = count + 1

    if(count != (rangeV + 1)):
        return False

    # All range elements are present
    return True

# Driver code

# Defining Array and size
arr = [ 1, 4, 5, 2, 7, 8, 3 ]
n = len(arr)

# A is lower limit and B is
# the upper limit of range
A = 2
B = 5

# True denotes all elements
# were present
if (check_elements(arr, n, A, B)) :
    print("Yes")

# False denotes any element
# was not present
else:
    print("No")

# This code is contributed
# by Yatin Gupta
```

## C#

```
// C# Code for Check if an array contains
// all elements of a given range
using System;

class GFG {

    // Function to check the array for
    // elements in given range
    public static bool check_elements(int []arr, int n,
                                      int A, int B)
    {
        // Range is the no. of elements
        // that are to be checked
        int range = B - A;

        // Traversing the array
        for (int i = 0; i < n; i++)
        {

            // If an element is in range
            if (Math.Abs(arr[i]) >= A &&
                Math.Abs(arr[i]) <= B)
                {
                    int z = Math.Abs(arr[i]) - A;
                    if (arr[z] > 0)
                    {
                      arr[z] = arr[z] * - 1;
                    }
                }
        }

        // Checking whether elements in
        // range 0-range are negative
        int count=0;

        for (int i = 0; i <= range
             && i < n; i++)
        {

            // Element from range is
            // missing from array
            if (arr[i] > 0)
                return false;
            else
                count++;
        }

        if(count != (range + 1))
            return false;

        // All range elements are present
        return true;
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Defining Array and size
        int []arr = {1, 4, 5, 2, 7, 8, 3};
        int n = arr.Length;

        // A is lower limit and B is
        // the upper limit of range
        int A = 2, B = 5;

        // True denotes all elements were present
        if (check_elements(arr, n, A, B))
         Console.WriteLine("Yes");

        // False denotes any element was not present
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to check the
// array for elements in
// given range
function check_elements($arr, $n,
                        $A, $B)
{
    // Range is the no. of
    // elements that are to
    // be checked
    $range = $B - $A;

    // Traversing the array
    for ($i = 0; $i < $n; $i++)
    {

        // If an element is in range
        if (abs($arr[$i]) >= $A &&
            abs($arr[$i]) <= $B)
        {

            // Negating at index
            // ‘element – A’
            $z = abs($arr[$i]) - $A;
            if ($arr[$z] > 0)
            {
                $arr[$z] = $arr[$z] * -1;
            }
        }
    }

    // Checking whether elements
    // in range 0-range are negative
    $count = 0;
    for ($i = 0; $i <= $range &&
                 $i< $n; $i++)
    {

        // Element from range is
        // missing from array
        if ($arr[$i] > 0)
            return -1;
        else
            $count++;
    }
    if($count!= ($range + 1))
        return -1;
    // All range elements
    // are present
    return true;
}

// Driver code

// Defining Array and size
$arr = array(1, 4, 5, 2,
             7, 8, 3);
$n = sizeof($arr);

// A is lower limit and
// B is the upper limit
// of range
$A = 2; $B = 5;

// True denotes all
// elements were present
if ((check_elements($arr, $n,
                    $A, $B)) == true)

    echo "Yes";

// False denotes any
// element was not present
else
    echo "No";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript Code for Check
    // if an array contains
    // all elements of a given range

    // Function to check the array for
    // elements in given range
    function check_elements(arr, n, A, B)
    {
        // Range is the no. of elements
        // that are to be checked
        let range = B - A;

        // Traversing the array
        for (let i = 0; i < n; i++)
        {

            // If an element is in range
            if (Math.abs(arr[i]) >= A &&
                Math.abs(arr[i]) <= B)
                {
                    let z = Math.abs(arr[i]) - A;
                    if (arr[z] > 0)
                    {
                      arr[z] = arr[z] * - 1;
                    }
                }
        }

        // Checking whether elements in
        // range 0-range are negative
        let count=0;

        for (let i = 0; i <= range &&
        i < n; i++)
        {

            // Element from range is
            // missing from array
            if (arr[i] > 0)
                return false;
            else
                count++;
        }

        if(count != (range + 1))
            return false;

        // All range elements are present
        return true;
    }

    // Defining Array and size
    let arr = [1, 4, 5, 2, 7, 8, 3];
    let n = arr.length;

    // A is lower limit and B is
    // the upper limit of range
    let A = 2, B = 5;

    // True denotes all elements were present
    if (check_elements(arr, n, A, B))
      document.write("Yes");

    // False denotes any element was not present
    else
      document.write("No");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。