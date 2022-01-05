# 找到在排序数组中出现一次的元素

> 原文:[https://www . geeksforgeeks . org/find-一次出现的元素排序数组/](https://www.geeksforgeeks.org/find-the-element-that-appears-once-in-a-sorted-array/)

给定一个排序数组，其中所有元素出现两次(一个接一个)，一个元素只出现一次。求 O(log n)复杂度中的那个元素。

**示例:**

```
Input:   arr[] = {1, 1, 3, 3, 4, 5, 5, 7, 7, 8, 8}
Output:  4

Input:   arr[] = {1, 1, 3, 3, 4, 4, 5, 5, 7, 7, 8}
Output:  8
```

一个**简单的解决方案**是从左到右遍历数组。由于数组是排序的，我们可以很容易地计算出所需的元素。

下面是上述方法的实现。

## C++

```
// C++ program to find the element that
// appears only once
#include <bits/stdc++.h>
using namespace std;

// A Linear Search based function to find
// the element that appears only once
void search(int arr[], int n)
{
    int ans = -1;
    for (int i = 0; i < n; i += 2) {
        if (arr[i] != arr[i + 1]) {
            ans = arr[i];
            break;
        }
    }

    if (arr[n - 2] != arr[n - 1])
            ans = arr[n-1];

    // ans = -1 if no such element is present.
    cout << "The required element is " << ans << "\n";
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
    int len = sizeof(arr) / sizeof(arr[0]);

    search(arr, len);

    return 0;
}

// This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element that
// appears only once
import java.io.*;

class GFG {
    // A Linear Search based function to find
    // the element that appears only once
    static void search(int arr[], int n)
    {
        int ans = -1;
        for (int i = 0; i < n; i += 2) {
            if (arr[i] != arr[i + 1]) {
                ans = arr[i];
                break;
            }
        }

        if (arr[n - 2] != arr[n - 1])
            ans = arr[n-1];

        // ans = -1 if no such element is present.
        System.out.println("The required element is "
                           + ans);
    }
    public static void main(String[] args)
    {
        int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
        int len = arr.length;

        search(arr, len);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the element that
# appears only once

# A Linear Search based function to find
# the element that appears only once

def search(arr, n):

    ans = -1
    for i in range(0, n, 2):
        if (arr[i] != arr[i + 1]):
            ans = arr[i]
            break
    if(arr[n-2] != arr[n-1]):
        ans = arr[n-1]

    # ans = -1 if no such element is present.
    print("The required element is", ans)

# Driver code
arr = [1, 1, 2, 4, 4, 5, 5, 6, 6]
Len = len(arr)

search(arr, Len)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the element that
// appears only once
using System;

class GFG {
    // A Linear Search based function to find
    // the element that appears only once
    static void search(int[] arr, int n)
    {
        int ans = -1;
        for (int i = 0; i < n; i += 2) {
            if (arr[i] != arr[i + 1]) {
                ans = arr[i];
                break;
            }
        }

        if (arr[n - 2] != arr[n - 1])
            ans = arr[n-1];

        // ans = -1 if no such element is present.
        Console.Write("The required element is "
                        + ans);
    }
    public static void Main(String[] args)
    {
        int[] arr = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
        int len = arr.Length;

        search(arr, len);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program to find the element that
// appears only once

// A Linear Search based function to find
// the element that appears only once
function search(arr, n)
{
    let ans = -1;
    for (let i = 0; i < n; i += 2) {
        if (arr[i] != arr[i + 1]) {
            ans = arr[i];
            break;
        }
    }

    if (arr[n - 2] != arr[n - 1])
            ans = arr[n-1];

    // ans = -1 if no such element is present.
    document.write("The required element is " + ans + "<br>");
}

// Driver code
    let arr = [ 1, 1, 2, 4, 4, 5, 5, 6, 6 ];
    let len = arr.length;

    search(arr, len);

// This code is contributed by Surbhi Tyagi

</script>
```

**Output**

```
The required element is 2
```

**时间复杂度:**O(n)
T3】空间复杂度 : O(1)

另一个**简单的解决方案**是使用 **XOR** 的属性(a ^ a = 0 & a ^ 0 = a)。想法是找到完整数组的**异或**。数组的**异或**就是需要的答案。

下面是上述方法的实现。

## C++

```
// C++ program to find the element that
// appears only once
#include <bits/stdc++.h>
using namespace std;

// A XOR based function to find
// the element that appears only once
void search(int arr[], int n)
{
    int XOR = 0;
    for (int i = 0; i < n; i++) {
        XOR = XOR ^ arr[i];
    }
    cout << "The required element is " << XOR << "\n";
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
    int len = sizeof(arr) / sizeof(arr[0]);

    search(arr, len);

    return 0;
}

// This code is contributed by yashbeersingh42
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element that
// appears only once
import java.io.*;

class GFG {
    // A XOR based function to find
    // the element that appears only once
    static void search(int arr[], int n)
    {
        int XOR = 0;
        for (int i = 0; i < n; i++) {
            XOR = XOR ^ arr[i];
        }
        System.out.println("The required element is "
                           + XOR);
    }
    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
        int len = arr.length;

        search(arr, len);
    }
}

// This code is contributed by yashbeersingh42
```

## 蟒蛇 3

```
# Python3 program to find the element that
# appears only once

# A XOR based function to find
# the element that appears only once
def search(arr, n) :

    XOR = 0
    for i in range(n) :
        XOR = XOR ^ arr[i]

    print("The required element is", XOR)

# Driver code
arr = [ 1, 1, 2, 4, 4, 5, 5, 6, 6 ]
Len = len(arr)

search(arr, Len)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the element that
// appears only once
using System;

class GFG{

// A XOR based function to find
// the element that appears only once
static void search(int []arr, int n)
{
    int XOR = 0;

    for(int i = 0; i < n; i++)
    {
        XOR = XOR ^ arr[i];
    }
    Console.Write("The required element is " + XOR);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
    int len = arr.Length;

    search(arr, len);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program to find the element that
// appears only once

// A XOR based function to find
// the element that appears only once
function search(arr, n)
{
    let XOR = 0;
    for (let i = 0; i < n; i++) {
        XOR = XOR ^ arr[i];
    }
    document.write("The required element is " + XOR + "<br>");
}

// Driver code
    let arr = [ 1, 1, 2, 4, 4, 5, 5, 6, 6 ];
    let len = arr.length;

    search(arr, len);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output**

```
The required element is 2
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)

一个**高效解**可以在 O(Log n)时间内找到需要的元素。想法是用[二分搜索法](http://geeksquiz.com/binary-search/)。下面是对输入数组的观察。
要求之前的所有元素在偶数索引(0，2，..)和奇数索引(1，3，…)处的下一次出现。所需元素之后的所有元素在奇数索引处第一次出现，在偶数索引处第二次出现。
1)找到中间指标，说‘中间’。
2)如果‘mid’为偶数，则比较 arr[mid]和 arr[mid + 1]。如果两者相同，则所需元素在“mid”之后，否则在 mid 之前。
3)如果‘中间’是奇数，则比较 arr[中间]和 arr[中间–1]。如果两者相同，则所需元素在“mid”之后，否则在 mid 之前。

下面是基于上述思想的实现:

## C++

```
// C++ program to find the element that
// appears only once
#include <iostream>
using namespace std;

// A Binary Search based function to find
// the element that appears only once
void search(int arr[], int low, int high)
{

    // Base cases
    if (low > high)
        return;

    if (low == high) {
        cout << "The required element is " << arr[low];
        return;
    }

    // Find the middle point
    int mid = (low + high) / 2;

    // If mid is even and element next to mid is
    // same as mid, then output element lies on
    // right side, else on left side
    if (mid % 2 == 0) {
        if (arr[mid] == arr[mid + 1])
            search(arr, mid + 2, high);
        else
            search(arr, low, mid);
    }

    // If mid is odd
    else {
        if (arr[mid] == arr[mid - 1])
            search(arr, mid + 1, high);
        else
            search(arr, low, mid - 1);
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
    int len = sizeof(arr) / sizeof(arr[0]);

    search(arr, 0, len - 1);

    return 0;
}

// This code is contributed by ShubhamCoder
```

## C

```
// C program to find the element that appears only once
#include <stdio.h>

// A Binary Search based function to find the element
// that appears only once
void search(int* arr, int low, int high)
{
    // Base cases
    if (low > high)
        return;

    if (low == high) {
        printf("The required element is %d ", arr[low]);
        return;
    }

    // Find the middle point
    int mid = (low + high) / 2;

    // If mid is even and element next to mid is
    // same as mid, then output element lies on
    // right side, else on left side
    if (mid % 2 == 0) {
        if (arr[mid] == arr[mid + 1])
            search(arr, mid + 2, high);
        else
            search(arr, low, mid);
    }
    else // If mid is odd
    {
        if (arr[mid] == arr[mid - 1])
            search(arr, mid + 1, high);
        else
            search(arr, low, mid - 1);
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
    int len = sizeof(arr) / sizeof(arr[0]);
    search(arr, 0, len - 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element that appears only once

public class Main {
    // A Binary Search based method to find the element
    // that appears only once
    public static void search(int[] arr, int low, int high)
    {
        if (low > high)
            return;
        if (low == high) {
            System.out.println("The required element is "
                               + arr[low]);
            return;
        }

        // Find the middle point
        int mid = (low + high) / 2;

        // If mid is even and element next to mid is
        // same as mid, then output element lies on
        // right side, else on left side
        if (mid % 2 == 0) {
            if (arr[mid] == arr[mid + 1])
                search(arr, mid + 2, high);
            else
                search(arr, low, mid);
        }
        // If mid is odd
        else if (mid % 2 == 1) {
            if (arr[mid] == arr[mid - 1])
                search(arr, mid + 1, high);
            else
                search(arr, low, mid - 1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
        search(arr, 0, arr.length - 1);
    }
}
// This code is contributed by Tanisha Mittal
```

## 计算机编程语言

```
# A Binary search based function to find
# the element that appears only once

def search(arr, low, high):

    # Base cases
    if low > high:
        return None

    if low == high:
        return arr[low]

    # Find the middle point
    mid = low + (high - low)/2

    # If mid is even and element next to mid is
    # same as mid, then output element lies on
    # right side, else on left side
    if mid % 2 == 0:

        if arr[mid] == arr[mid+1]:
            return search(arr, mid+2, high)
        else:
            return search(arr, low, mid)

    else:
        # if mid is odd
        if arr[mid] == arr[mid-1]:
            return search(arr, mid+1, high)
        else:
            return search(arr, low, mid-1)

# Driver Code
# Test Array
arr = [1, 1, 2, 4, 4, 5, 5, 6, 6]

# Function call
result = search(arr, 0, len(arr)-1)

if result is not None:
    print "The required element is %d" % result
else:
    print "Invalid Array"
```

## C#

```
// C# program to find the element
// that appears only once
using System;

class GFG {

    // A Binary Search based
    // method to find the element
    // that appears only once
    public static void search(int[] arr, int low, int high)
    {

        if (low > high)
            return;
        if (low == high) {
            Console.WriteLine("The required element is "
                              + arr[low]);
            return;
        }

        // Find the middle point
        int mid = (low + high) / 2;

        // If mid is even and element
        // next to mid is same as mid
        // then output element lies on
        // right side, else on left side
        if (mid % 2 == 0) {
            if (arr[mid] == arr[mid + 1])
                search(arr, mid + 2, high);
            else
                search(arr, low, mid);
        }

        // If mid is odd
        else if (mid % 2 == 1) {
            if (arr[mid] == arr[mid - 1])
                search(arr, mid + 1, high);
            else
                search(arr, low, mid - 1);
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
        search(arr, 0, arr.Length - 1);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the element
// that appears only once

// A Binary Search based function
// to find the element that
// appears only once
function search($arr, $low, $high)
{

    // Base cases
    if ($low > $high)
        return;

    if ($low==$high)
    {
        echo("The required element is " );
        echo $arr[$low] ;
        return;
    }

    // Find the middle point
    $mid = ($low + $high) / 2;

    // If mid is even and element
    // next to mid is same as mid,
    // then output element lies on
    // right side, else on left side
    if ($mid % 2 == 0)
    {
        if ($arr[$mid] == $arr[$mid + 1])
            search($arr, $mid + 2, $high);
        else
            search($arr, $low, $mid);
    }

    // If mid is odd
    else
    {
        if ($arr[$mid] == $arr[$mid - 1])
            search($arr, $mid + 1, $high);
        else
            search($arr, $low, $mid - 1);
    }
}

    // Driver Code
    $arr = array(1, 1, 2, 4, 4, 5, 5, 6, 6);
    $len = sizeof($arr);
    search($arr, 0, $len - 1);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript implementation

// A Binary Search based function to find
// the element that appears only once
function search( arr, low, high)
{

    // Base cases
    if (low > high)
        return;

    if (low == high) {
        document.write("The required element is " + arr[low]);
        return;
    }

    // Find the middle point
    var mid = Math.floor((low + high) / 2);

    // If mid is even and element next to mid is
    // same as mid, then output element lies on
    // right side, else on left side
    if (mid % 2 == 0) {
        if (arr[mid] == arr[mid + 1])
            search(arr, mid + 2, high);
        else
            search(arr, low, mid);
    }

    // If mid is odd
    else {
        if (arr[mid] == arr[mid - 1])
            search(arr, mid + 1, high);
        else
            search(arr, low, mid - 1);
    }
}

// Driver Code
var arr = [1, 1, 2, 4, 4, 5, 5, 6, 6];
var len = arr.length;

search(arr, 0, len - 1)

// This is code is contributed
// by shubhamsingh10
</script>
```

**Output**

```
The required element is 2
```

**时间复杂度:** O(Log n)
**注:**这个问题的其他**解决方案**是 [**这个**](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) 帖子中讨论的方法的微小变化。

**另一种方法:**高效的解决方案可以在 O(Log n)时间内找到所需的元素。想法是不用递归使用二分搜索法。所需之前的所有元素在偶数索引(0，2，..等等)和奇数索引(1，3，..等等)。

方法如下:

使用开始指针和结束指针找到假定为中间的中间索引。并在以下情况下检查中间元素

**情况 1)** 如果 mid 元素不等于 mid+1 元素和 mid-1 元素。**这个案例返回了答案。**

**情况 2)** 当 mid 元素为偶数且等于 mid+1 元素时，这意味着数组左侧不存在数字。在这种情况下**开始指针将变为中间+1。**

**情况 3)** 当 mid 元素为奇数且等于 mid-1 元素时，这意味着数组左侧不存在数字。在这种情况下**开始指针将变为中间+1。**

**情况 4)** 当 mid 元素为奇数且等于 mid+1 元素时，这意味着数组右侧不存在数字。在这种情况下**的结束指针将变为中间 1。**

**情况 5)** 当 mid 元素为偶数且等于 mid-1 元素时，这意味着数组右侧不存在数字。在这种情况下**的结束指针将变为中间 1。**

检查所有情况下中间到开始< =结束的可能值..

如果所有检查都失败，则不存在这样的元素。

此解决方案需要对边缘案例进行额外检查。

**边缘情况 1)** 如果数组中只有一个元素。因此**返回数组的唯一元素。**

**边缘情况 2)** 如果数组的最后一个元素是必需元素。因此**返回数组的最后一个元素。**

**边缘情况 3)** 如果数组的第一个元素是需要的元素。因此**返回数组的第一个元素。**

下面是基于上述思想的实现:

## C++

```
#include <iostream>
using namespace std;
int search(int nums[], int n)
{

    // A Binary Search based method to find the element
    // that appears only once
    int start = 0, end = n - 1, mid;

    // For Edge Cases
    if (n == 1) // If only one element is in the array
        return nums[0];

    if (nums[start]
        != nums[start + 1]) // If the first element
                            // is the element that
                            // appears only once
        return nums[start];

    if (nums[end]
        != nums[end - 1]) // If Last element is the element
                          // that appears only once
        return nums[end];

    // Binary Search
    while (start <= end)
    {
        mid = start + (end - start) / 2;

        // CASE 1
        if (nums[mid] != nums[mid - 1]
            && nums[mid] != nums[mid + 1])
            return nums[mid];

        // CASE 2 and CASE 3
        else if ((nums[mid] == nums[mid + 1]
                  && mid % 2 == 0)
                 || (nums[mid] == nums[mid - 1]
                     && mid % 2 != 0))
            start = mid + 1;

        // CASE 4 and CASE 5
        else
            end = mid - 1;
    }

    // If no such element found
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int element = search(arr, n);

    if (element != -1)
        cout << "The required element is " << element;
    else
        cout << "There is no such element";
}

// This code is contributed by umadevi9616
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {
    public static int search(int[] nums)
    {
        // A Binary Search based method to find the element
        // that appears only once
        int start = 0, end = nums.length - 1, mid;

        // For Edge Cases
        if (nums.length
            == 1) // If only one element is in the array
            return nums[0];

        if (nums[start]
            != nums[start + 1]) // If the first element
                                // is the element that
                                // appears only once
            return nums[start];

        if (nums[end]
            != nums[end
                    - 1]) // If Last element is the element
                          // that appears only once
            return nums[end];

        // Binary Search
        while (start <= end) {
            mid = start + (end - start) / 2;
            // CASE 1
            if (nums[mid] != nums[mid - 1]
                && nums[mid] != nums[mid + 1])
                return nums[mid];
            // CASE 2 and CASE 3
            else if ((nums[mid] == nums[mid + 1]
                      && mid % 2 == 0)
                     || (nums[mid] == nums[mid - 1]
                         && mid % 2 != 0))
                start = mid + 1;
            // CASE 4 and CASE 5
            else
                end = mid - 1;
        }
        // If no such element found
        return -1;
    }
    public static void main(String[] args)
    {
        int[] arr = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };

        int element = search(arr);

        if (element != -1)
            System.out.println("The required element is "
                               + element);
        else
            System.out.println("There is no such element");
    }
}

// Code Contributed by Arnav Sharma
```

## 蟒蛇 3

```
def search(nums):
    # A Binary Search based method to find the element
    # that appears only once
    start = 0;
    end = len(nums)-1;
    mid = 0;

    # For Edge Cases
    if (len(nums) == 1): # If only one element is in the array
        return nums[0];

    if (nums[start] != nums[start + 1]): # If the first element
                                        # is the element that
                                        # appears only once
        return nums[start];

    if (nums[end] != nums[end - 1]): # If Last element is the element
                                    # that appears only once
        return nums[end];

    # Binary Search
    while (start <= end):
        mid = start + (end - start) // 2;

        # CASE 1
        if (nums[mid] != nums[mid - 1] and nums[mid] != nums[mid + 1]):

            return nums[mid];
        # CASE 2 and CASE 3
        elif((nums[mid] == nums[mid + 1] and mid % 2 == 0) or (nums[mid] == nums[mid - 1] and mid % 2 != 0)):
            start = mid + 1;

        # CASE 4 and CASE 5
        else:
            end = mid - 1;

    # If no such element found
    return -1;

# Driver code
if __name__ == '__main__':
    arr = [ 1, 1, 2, 4, 4, 5, 5, 6, 6 ];

    element = search(arr);

    if (element != -1):
        print("The required element is " , element);
    else:
        print("There is no such element");

# This code is contributed by umadevi9616
```

## C#

```
using System;
public class GFG {
    public static int search(int[] nums)
    {

        // A Binary Search based method to find the element
        // that appears only once
        int start = 0, end = nums.Length - 1, mid;

        // For Edge Cases
        if (nums.Length
            == 1) // If only one element is in the array
            return nums[0];

        if (nums[start]
            != nums[start + 1]) // If the first element
                                // is the element that
                                // appears only once
            return nums[start];

        if (nums[end]
            != nums[end
                    - 1]) // If Last element is the element
                          // that appears only once
            return nums[end];

        // Binary Search
        while (start <= end)
        {
            mid = start + (end - start) / 2;

            // CASE 1
            if (nums[mid] != nums[mid - 1]
                && nums[mid] != nums[mid + 1])
                return nums[mid];

            // CASE 2 and CASE 3
            else if ((nums[mid] == nums[mid + 1]
                      && mid % 2 == 0)
                     || (nums[mid] == nums[mid - 1]
                         && mid % 2 != 0))
                start = mid + 1;

            // CASE 4 and CASE 5
            else
                end = mid - 1;
        }

        // If no such element found
        return -1;
    }
    public static void Main(String[] args)
    {
        int[] arr = { 1, 1, 2, 4, 4, 5, 5, 6, 6 };

        int element = search(arr);

        if (element != -1)
            Console.WriteLine("The required element is "
                               + element);
        else
            Console.WriteLine("There is no such element");
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
   function search(nums)
    {

        // A Binary Search based method to find the element
        // that appears only once
        var start = 0, end = nums.length - 1, mid;

        // For Edge Cases
        if (nums.length
            == 1) // If only one element is in the array
            return nums[0];

        if (nums[start]
            != nums[start + 1]) // If the first element
                                // is the element that
                                // appears only once
            return nums[start];

        if (nums[end]
            != nums[end
                    - 1]) // If Last element is the element
                          // that appears only once
            return nums[end];

        // Binary Search
        while (start <= end)
        {
            mid = start + (end - start) / 2;

            // CASE 1
            if (nums[mid] != nums[mid - 1]
                && nums[mid] != nums[mid + 1])
                return nums[mid];

            // CASE 2 and CASE 3
            else if ((nums[mid] == nums[mid + 1]
                      && mid % 2 == 0)
                     || (nums[mid] == nums[mid - 1]
                         && mid % 2 != 0))
                start = mid + 1;

            // CASE 4 and CASE 5
            else
                end = mid - 1;
        }

        // If no such element found
        return -1;
    }

        var arr = [ 1, 1, 2, 4, 4, 5, 5, 6, 6 ];
        var element = search(arr);
        if (element = 2)
            document.write("The required element is "
                               + element);
        else
            document.write("There is no such element");

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
The required element is 2
```

这个解决方案是由 Arnav Sharma 贡献的。

**时间复杂度:**O(logn)
T3】辅助空间: O(1)

本文由 Mehboob Elahi 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。