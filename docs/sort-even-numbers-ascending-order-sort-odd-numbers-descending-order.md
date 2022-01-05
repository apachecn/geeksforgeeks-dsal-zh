# 将所有偶数按升序排序，然后将所有奇数按降序排序

> 原文:[https://www . geesforgeks . org/sort-偶数-升序-排序-奇数-降序/](https://www.geeksforgeeks.org/sort-even-numbers-ascending-order-sort-odd-numbers-descending-order/)

给定一个整数数组(奇数和偶数)，对它们进行排序，使数组的第一部分包含按降序排序的奇数，其余部分包含按升序排序的偶数。

**示例:**

```
Input  : arr[] = {1, 2, 3, 5, 4, 7, 10}
Output : arr[] = {7, 5, 3, 1, 2, 4, 10}

Input  : arr[] = {0, 4, 5, 3, 7, 2, 1}
Output : arr[] = {7, 5, 3, 1, 0, 2, 4} 
```

**方法 1(使用分区)**

1.  [对输入数组](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)进行分区，使所有奇数元素向左移动，所有偶数元素向右移动。这一步需要 0(n)。
2.  一旦数组被分区，分别对左右部分进行排序。这一步需要 O(n Log n)。

以下是上述想法的实现。

## C++

```
// C++ program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order
#include <bits/stdc++.h>
using namespace std;

// To do two way sort. First sort even numbers in
// ascending order, then odd numbers in descending
// order.
void twoWaySort(int arr[], int n)
{

    // Current indexes from left and right
    int l = 0, r = n - 1;

    // Count of odd numbers
    int k = 0;

    while (l < r)
    {

        // Find first even number
        // from left side.
        while (arr[l] % 2 != 0)
        {
            l++;
            k++;
        }

        // Find first odd number
        // from right side.
        while (arr[r] % 2 == 0 && l < r)
            r--;

        // Swap even number present on left and odd
        // number right.
        if (l < r)
            swap(arr[l], arr[r]);
    }

    // Sort odd number in descending order
    sort(arr, arr + k, greater<int>());

    // Sort even number in ascending order
    sort(arr + k, arr + n);
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 7, 5, 4 };
    int n = sizeof(arr) / sizeof(int);
    twoWaySort(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order

import java.util.Arrays;
import java.util.Collections;

public class GFG {
    // To do two way sort. First sort even numbers in
    // ascending order, then odd numbers in descending
    // order.
    static void twoWaySort(Integer arr[], int n)
    {
        // Current indexes from left and right
        int l = 0, r = n - 1;

        // Count of odd numbers
        int k = 0;

        while (l < r)
        {

            // Find first even number from left side.
            while (arr[l] % 2 != 0)
            {
                l++;
                k++;
            }

            // Find first odd number from right side.
            while (arr[r] % 2 == 0 && l < r)
                r--;

            // Swap even number present on left and odd
            // number right.
            if (l < r)
            {

                // swap arr[l] arr[r]
                int temp = arr[l];
                arr[l] = arr[r];
                arr[r] = temp;
            }
        }

        // Sort odd number in descending order
        Arrays.sort(arr, 0, k, Collections.
                                  reverseOrder());

        // Sort even number in ascending order
        Arrays.sort(arr, k, n);
    }

    // Driver Method
    public static void main(String[] args)
    {
        Integer arr[] = { 1, 3, 2, 7, 5, 4 };

        twoWaySort(arr, arr.length);

        System.out.println(Arrays.toString(arr));
    }
}
```

## 计算机编程语言

```
# Python program to sort array
# in even and odd manner
# The odd numbers are to be
# sorted in descending order
# and the even numbers in
# ascending order

# To do two way sort. First
# sort even numbers in ascending
# order, then odd numbers in
# descending order.
def two_way_sort(arr, arr_len):

    # Current indexes l->left
    # and r->right
    l, r = 0, arr_len - 1

    # Count of number of
    # odd numbers, used in
    # slicing the array later.
    k = 0

    # Run till left(l) < right(r)
    while(l < r):

        # While left(l) is odd, if yes
        # increment the left(l) plus
        # odd count(k) if not break the
        # while for even number found
        # here to be swaped
        while(arr[l] % 2 != 0):
            l += 1
            k += 1

        # While right(r) is even,
        # if yes decrement right(r)
        # if not break the while for
        # odd number found here to
        # be swaped    
        while(arr[r] % 2 == 0 and l < r):
            r -= 1

        # Swap the left(l) and right(r),
        # which is even and odd numbers
        # encountered in above loops
        if(l < r):
            arr[l], arr[r] = arr[r], arr[l]

    # Slice the number on the
    # basis of odd count(k)
    odd = arr[:k]
    even = arr[k:]

    # Sort the odd and
    # even array accordingly
    odd.sort(reverse = True)
    even.sort()

    # Extend the odd array with
    # even values and return it.
    odd.extend(even)

    return odd

# Driver code
arr_len = 6
arr = [1, 3, 2, 7, 5, 4]
result = two_way_sort(arr, arr_len)
for i in result:
    print(str(i) + " "),

# This code is contributed
# by JaySiyaRam
```

## C#

```
// C# program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order
using System;
using System.Linq;

class GFG {
    // To do two way sort. First sort even numbers in
    // ascending order, then odd numbers in descending
    // order.
    static void twoWaySort(int[] arr, int n)
    {
        // Current indexes from left and right
        int l = 0, r = n - 1;

        // Count of odd numbers
        int k = 0;

        while (l < r)
        {

            // Find first even number
            // from left side.
            while (arr[l] % 2 != 0)
            {
                l++;
                k++;
            }

            // Find first odd number from right side.
            while (arr[r] % 2 == 0 && l < r)
                r--;

            // Swap even number present
            // on left and odd
            // number right.
            if (l < r) {
                // swap arr[l] arr[r]
                int temp = arr[l];
                arr[l] = arr[r];
                arr[r] = temp;
            }
        }

        // Sort odd number in descending order
        Array.Sort(arr, 0, k);
        Array.Reverse(arr, 0, k);

        // Sort even number in ascending order
        Array.Sort(arr, k, n - k);
    }

    // Driver Method
    public static void Main(String[] args)
    {
        int[] arr = { 1, 3, 2, 7, 5, 4 };

        twoWaySort(arr, arr.Length);

        Console.WriteLine(String.Join(" ", arr));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program sort array
// in even and odd manner.
// The odd numbers are to be
// sorted in descending
// order and the even numbers in
// ascending order

    // To do two way sort.
    // First sort even numbers in
    // ascending order, then odd
    // numbers in descending
    // order.
    function twoWaySort(arr,n)
    {
        // Current indexes from
        // left and right
        let l = 0, r = n - 1;

        // Count of odd numbers
        let k = 0;

        while (l < r)
        {

            // Find first even number
            // from left side.
            while (arr[l] % 2 != 0)
            {
                l++;
                k++;
            }

            // Find first odd number
            // from right side.
            while (arr[r] % 2 == 0 && l < r)
                r--;

            // Swap even number present
            // on left and odd
            // number right.
            if (l < r)
            {

                // swap arr[l] arr[r]
                let temp = arr[l];
                arr[l] = arr[r];
                arr[r] = temp;
            }
        }

        let odd=new Array(k);
        for(let i=0;i<k;i++)
        {
            odd[i]=arr[i];
        }
        let even=new Array(n-k);
        for(let i=0;i<n-k;i++)
        {
            even[i]=arr[k+i];
        }
        // Sort odd number in descending order
        odd.sort(function(a,b){return b-a;});
        // Sort even number in ascending order
        even.sort(function(a,b){return a-b;});

        return odd.concat(even);

    }
    // Driver Method
    let arr=[1, 3, 2, 7, 5, 4 ];
    let ans=twoWaySort(arr, arr.length);
    for(let i=0;i<ans.length;i++)
    {
        document.write(ans[i]+" ");
    }

    // This code is contributed by rag2127

</script>
```

**输出:**

```
7 5 3 1 2 4 
```

**时间复杂度:**O(n log n)
T3】空间复杂度: O(1)

**方法 2(使用负乘法):**

1.  把所有奇数都变成负数。
2.  对所有数字进行排序。
3.  恢复步骤 1 中所做的更改，以恢复原始元素。

## C++

```
// C++ program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order
#include <bits/stdc++.h>
using namespace std;

// To do two way sort. First sort even numbers in
// ascending order, then odd numbers in descending
// order.
void twoWaySort(int arr[], int n)
{
    // Make all odd numbers negative
    for (int i = 0; i < n; i++)
        if (arr[i] & 1) // Check for odd
            arr[i] *= -1;

    // Sort all numbers
    sort(arr, arr + n);

    // Retaining original array
    for (int i = 0; i < n; i++)
        if (arr[i] & 1)
            arr[i] *= -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 7, 5, 4 };
    int n = sizeof(arr) / sizeof(int);
    twoWaySort(arr, n);
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order

import java.util.Arrays;

public class GFG
{
    // To do two way sort. First sort even numbers in
    // ascending order, then odd numbers in descending
    // order.
    static void twoWaySort(int arr[], int n)
    {
        // Make all odd numbers negative
        for (int i = 0; i < n; i++)
            if ((arr[i] & 1) != 0) // Check for odd
                arr[i] *= -1;

        // Sort all numbers
        Arrays.sort(arr);

        // Retaining original array
        for (int i = 0; i < n; i++)
            if ((arr[i] & 1) != 0)
                arr[i] *= -1;
    }

    // Driver Method
    public static void main(String[] args)
    {
        int arr[] = { 1, 3, 2, 7, 5, 4 };

        twoWaySort(arr, arr.length);

        System.out.println(Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to sort array in
# even and odd manner. The odd
# numkbers are to be sorted in
# descending order and the even
# numbers in ascending order

# To do two way sort. First sort
# even numbers in ascending order,
# then odd numbers in descending order.
def twoWaySort(arr, n):

    # Make all odd numbers negative
    for i in range(0, n):

        # Check for odd
        if (arr[i] & 1):
            arr[i] *= -1

    # Sort all numbers
    arr.sort()

    # Retaining original array
    for i in range(0, n):
        if (arr[i] & 1):
            arr[i] *= -1

# Driver code
arr = [1, 3, 2, 7, 5, 4]
n = len(arr)
twoWaySort(arr, n);
for i in range(0, n):
    print(arr[i], end = " ")

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Java program sort array in even and
// odd manner. The odd numbers are to
// be sorted in descending order and
// the even numbers in ascending order
using System;

public class GFG
{

    // To do two way sort. First sort
    // even numbers in ascending order,
    // then odd numbers in descending
    // order.
    static void twoWaySort(int[] arr, int n)
    {

        // Make all odd numbers negative
        for (int i = 0; i < n; i++)

            // Check for odd
            if ((arr[i] & 1) != 0)
                arr[i] *= -1;

        // Sort all numbers
        Array.Sort(arr);

        // Retaining original array
        for (int i = 0; i < n; i++)
            if ((arr[i] & 1) != 0)
                arr[i] *= -1;
    }

    // Driver Method
    public static void Main()
    {
        int[] arr = { 1, 3, 2, 7, 5, 4 };

        twoWaySort(arr, arr.Length);

        for (int i = 0; i < arr.Length; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order

// To do two way sort. First sort even numbers in
// ascending order, then odd numbers in descending
// order.
function twoWaySort(&$arr, $n)
{
    // Make all odd numbers negative
    for ($i = 0 ; $i < $n; $i++)
        if ($arr[$i] & 1) // Check for odd
            $arr[$i] *= -1;

    // Sort all numbers
    sort($arr);

    // Retaining original array
    for ($i = 0 ; $i < $n; $i++)
        if ($arr[$i] & 1)
            $arr[$i] *= -1;
}

// Driver code
$arr = array(1, 3, 2, 7, 5, 4);
$n = sizeof($arr);
twoWaySort($arr, $n);
for ($i = 0; $i < $n; $i++)
    echo $arr[$i] . " ";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program sort array in even and odd manner.
// The odd numbers are to be sorted in descending
// order and the even numbers in ascending order

// To do two way sort. First sort even numbers in
// ascending order, then odd numbers in descending
// order.
function twoWaySort(arr, n)
{
    // Make all odd numbers negative
    for (let i = 0; i < n; i++)
        if (arr[i] & 1) // Check for odd
            arr[i] *= -1;

    // Sort all numbers
    arr.sort((a,b) => a-b);

    // Retaining original array
    for (let i = 0; i < n; i++)
        if (arr[i] & 1)
            arr[i] *= -1;
}

// Driver code

    let arr = [ 1, 3, 2, 7, 5, 4 ];
    let n = arr.length;
    twoWaySort(arr, n);
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");

//This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
7 5 3 1 2 4 
```

**时间复杂度:**O(n log n)
T3】空间复杂度: O(n)
当输入数组包含负数时，该方法可能不起作用。但是，有一种方法可以解决这个问题。我们计算输入数组中的奇数正整数，然后再次排序。读者可参考[本](https://ide.geeksforgeeks.org/xXobxp)执行。

**方法 3(使用比较器):**
这个问题可以通过使用内置的排序函数和自定义的比较方法来轻松解决。在比较任何两个要素时，会有三种情况:

1.  **当两个元素都是偶数时:**在这种情况下，较小的元素必须出现在排序数组中较大元素的左侧。
2.  **当两个元素都是奇数时:**较大的元素必须出现在较小元素的左边。
3.  **一个奇数，一个偶数:**奇数的元素必须出现在偶数元素的左边。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print
// the contents of the array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// To do two way sort. Make comparator function
// for the inbuilt sort function of c++ such that
// odd numbers are placed before even in descending
// and ascending order respectively
bool compare(int a, int b)
{

    // If both numbers are even,
    // smaller number should
    // be placed at lower index
    if (a % 2 == 0 && b % 2 == 0)
        return a < b;

    // If both numbers are odd larger number
    // should be placed at lower index
    if (a % 2 != 0 && b % 2 != 0)
        return b < a;

    // If a is odd and b is even,
    // a should be placed before b
    if (a % 2 != 0)
        return true;

    // If b is odd and a is even,
    // b should be placed before a
    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 7, 5, 4 };
    int n = sizeof(arr) / sizeof(int);

    // Sort the array
    sort(arr, arr + n, compare);

    // Print the sorted array
    printArr(arr, n);

    return 0;
}

// This code is contributed by Nikhil Yadav
```

## java 描述语言

```
<script>
        // JavaScript implementation of the approach

        // Utility function to print
        // the contents of the array
        function printArr(arr, n)
        {
            for (let i = 0; i < n; i++)
                document.write(arr[i] + " ");
        }

        // To do two way sort. Make comparator function
        // for the inbuilt sort function of c++ such that
        // odd numbers are placed before even in descending
        // and ascending order respectively
        function compare(a, b) {

            // If both numbers are even,
            // smaller number should
            // be placed at lower index
            if (a % 2 == 0 && b % 2 == 0 && a < b)
                return -1;

            // If both numbers are odd larger number
            // should be placed at lower index
            if (a % 2 != 0 && b % 2 != 0 && b > a)
                return 1;

            // If a is odd and b is even,
            // a should be placed before b
            if (a % 2 != 0)
                return -1;

            // If b is odd and a is even,
            // b should be placed before a
            return 1;
        }

        // Driver code
        var arr = [1, 3, 2, 7, 5, 4];
        var n = arr.length;

        // Sort the array
        arr.sort(compare);

        // Print the sorted array
        printArr(arr, n);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
7 5 3 1 2 4 
```

感谢**阿曼迪辛格**提出这个解决方案。
本文由 [**丹麦语 _ 拉扎**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。