# 壳牌-迈兹纳分类

> 原文:[https://www.geeksforgeeks.org/shell-metzner-sort/](https://www.geeksforgeeks.org/shell-metzner-sort/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是使用 Shell-Metzner 排序对数组进行排序。

> **输入:** arr[] = {0，-2，8，5，1}
> **输出:** -2 0 1 5 8
> **输入:** arr[] = {4，5，6，1，100000，1000}
> **输出:** 1 4 5 6 1000 100000

**先决条件** : [贝壳类](https://www.geeksforgeeks.org/shellsort/)
贝壳-梅兹纳类是玛琳·梅兹纳对贝壳类的改编。Shell-Metzner 排序使用五个索引来检查交换哪些单元格。Metzner 版本以等于数组长度一半的步长开始，每次传递都以二次方式增加比较次数。
下面是 Shell-Metzner 排序的实现:

## C++

```
// C++ implementation of Shell-Metzner Sort
#include <bits/stdc++.h>
using namespace std;

// Function to swap two elements
void swap(int& a, int& b)
{
    int temp = a;
    a = b;
    b = temp;
}

// Function to sort arr[] using Shell Metzner sort
void sort_shell_metzner(int arr[], int n)
{

    // Declare variables
    int i, j, k, l, m, temp;

    // Set initial step size to
    // the size of the array
    m = n;

    while (m > 0) {

        // Step size decreases by half each time
        m /= 2;

        // k is the upper limit for j
        k = n - m;

        // j is the starting point
        j = 0;

        do {

            // i equals to smaller value
            i = j;

            do {

                // l equals to larger value
                l = i + m;

                // Compare and swap arr[i] with arr[l]
                if (arr[i] > arr[l]) {
                    swap(arr[i], arr[l]);

                    // Decrease smaller value by step size
                    i -= m;
                }
                else
                    break;
            } while (i >= 0);

            // Increment the lower limit of i
            j++;

        } while (j <= k);
    }
}

// Function to print the contents of an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 0, -2, 8, 5, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Sort the array using Shell Metzner Sort
    sort_shell_metzner(arr, n);

    // Print the sorted array
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of Shell-Metzner Sort
class GFG
{

    // Function to swap two elements
    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Function to sort arr[] using Shell Metzner sort
    static void sort_shell_metzner(int arr[], int n)
    {

        // Declare variables
        int i, j, k, l, m, temp;

        // Set initial step size to
        // the size of the array
        m = n;

        while (m > 0)
        {

            // Step size decreases by half each time
            m /= 2;

            // k is the upper limit for j
            k = n - m;

            // j is the starting point
            j = 0;

            do
            {

                // i equals to smaller value
                i = j;

                do
                {

                    // l equals to larger value
                    l = i + m;

                    // Compare and swap arr[i] with arr[l]
                    if (l < n && arr[i] > arr[l])
                    {
                        swap(arr, i, l);

                        // Decrease smaller value by step size
                        i -= m;
                    }
                    else
                    {
                        break;
                    }
                } while (i >= 0);

                // Increment the lower limit of i
                j++;

            } while (j <= k);
        }
    }

    // Function to print the contents of an array
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {0, -2, 8, 5, 1};
        int n = arr.length;

        // Sort the array using Shell Metzner Sort
        sort_shell_metzner(arr, n);

        // Print the sorted array
        printArray(arr, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of Shell-Metzner Sort

# Function to sort arr[] using Shell Metzner sort
def sort_shell_metzner( arr, n):

    # Set initial step size to
    # the size of the array
    m = n;

    while (m > 0):

        # Step size decreases by half each time
        m //= 2

        # k is the upper limit for j
        k = n - m

        # j is the starting point
        j = 0

        while(j < k):

            # i equals to smaller value
            i = j

            while(i >= 0):

                # l equals to larger value
                l = i + m

                # Compare and swap arr[i] with arr[l]
                if (arr[i] > arr[l]):
                    arr[i], arr[l]=arr[l],arr[i]

                    # Decrease smaller value by step size
                    i -= m

                else:
                    break

            # Increment the lower limit of i
            j += 1

# Function to print the contents of an array
def printArray(arr, n):

    for i in range( n):
        print( arr[i], end= " ")

# Driver code
if __name__ =="__main__":
    arr = [ 0, -2, 8, 5, 1 ]
    n = len(arr)

    # Sort the array using Shell Metzner Sort
    sort_shell_metzner(arr, n)

    # Print the sorted array
    printArray(arr, n)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of Shell-Metzner Sort
using System;

class GFG
{

    // Function to swap two elements
    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Function to sort arr[] using Shell Metzner sort
    static void sort_shell_metzner(int []arr, int n)
    {

        // Declare variables
        int i, j, k, l, m, temp;

        // Set initial step size to
        // the size of the array
        m = n;

        while (m > 0)
        {

            // Step size decreases by half each time
            m /= 2;

            // k is the upper limit for j
            k = n - m;

            // j is the starting point
            j = 0;

            do
            {

                // i equals to smaller value
                i = j;

                do
                {

                    // l equals to larger value
                    l = i + m;

                    // Compare and swap arr[i] with arr[l]
                    if (l < n && arr[i] > arr[l])
                    {
                        swap(arr, i, l);

                        // Decrease smaller value by step size
                        i -= m;
                    }
                    else
                    {
                        break;
                    }
                } while (i >= 0);

                // Increment the lower limit of i
                j++;

            } while (j <= k);
        }
    }

    // Function to print the contents of an array
    static void printArray(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {0, -2, 8, 5, 1};
        int n = arr.Length;

        // Sort the array using Shell Metzner Sort
        sort_shell_metzner(arr, n);

        // Print the sorted array
        printArray(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation of Shell-Metzner Sort

// Function to sort arr[] using Shell Metzner sort
function sort_shell_metzner($arr, $n)
{
    // Set initial step size to
    // the size of the array
    $m = $n;

    while ($m > 0)
    {

        // Step size decreases by half each time
        $m = $m / 2;

        // k is the upper limit for j
        $k = $n - $m;

        // j is the starting point
        $j = 0;

        do {

            // i equals to smaller value
            $i = $j;

            do {

                // l equals to larger value
                $l = $i + $m;

                // Compare and swap arr[i] with arr[l]
                if ($arr[$i] > $arr[$l])
                {
                    $temp = $arr[$i];
                    $arr[$i] = $arr[$l];
                    $arr[$l] = $temp;

                    // Decrease smaller value by step size
                    $i -= $m;
                }
                else
                    break;

            } while ($i >= 0);

            // Increment the lower limit of i
            $j++;

        } while ($j <= $k);
    }
    return $arr ;
}

// Function to print the contents of an array
function printArray($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i], " ";
}

// Driver code
$arr = array( 0, -2, 8, 5, 1 );
$n = count($arr);

// Sort the array using Shell Metzner Sort
$result_array = sort_shell_metzner($arr, $n);

// Print the sorted array
printArray($result_array, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of Shell-Metzner Sort

// Function to swap two elements
    function swap(arr,i,j)
    {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Function to sort arr[] using Shell Metzner sort    
    function sort_shell_metzner(arr,n)
    {
        // Declare variables
        let i, j, k, l, m, temp;

        // Set initial step size to
        // the size of the array
        m = n;

        while (m > 0)
        {

            // Step size decreases by half each time
            m = Math.floor(m/2);

            // k is the upper limit for j
            k = n - m;

            // j is the starting point
            j = 0;

            do
            {

                // i equals to smaller value
                i = j;

                do
                {

                    // l equals to larger value
                    l = i + m;

                    // Compare and swap arr[i] with arr[l]
                    if (l < n && arr[i] > arr[l])
                    {
                        swap(arr, i, l);

                        // Decrease smaller value by step size
                        i -= m;
                    }
                    else
                    {
                        break;
                    }
                } while (i >= 0);

                // Increment the lower limit of i
                j++;

            } while (j <= k);
        }
    }

     // Function to print the contents of an array
    function printArray(arr,n)
    {
        for (let i = 0; i < n; i++)
        {
            document.write(arr[i] + " ");
        }
    }

    // Driver code
    let arr=[0, -2, 8, 5, 1];
    let n = arr.length;

    // Sort the array using Shell Metzner Sort
    sort_shell_metzner(arr, n);

    // Print the sorted array
    printArray(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
-2 0 1 5 8
```

**时间复杂度:** O(n <sup>2</sup> )