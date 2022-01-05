# 数组类型及其最大元素

> 原文:[https://www.geeksforgeeks.org/type-array-maximum-element/](https://www.geeksforgeeks.org/type-array-maximum-element/)

给定一个数组，它可以有 4 种类型。
(a)上升
(b)下降
(c)上升旋转
(d)下降旋转
找出是哪种数组，返回该数组的最大值。

**示例:**

```
Input :  arr[] = { 2, 1, 5, 4, 3}
Output : Descending rotated with maximum element 5

Input :  arr[] = { 3, 4, 5, 1, 2}
Output : Ascending rotated with maximum element 5
```

问于:[亚马逊采访](https://www.geeksforgeeks.org/amazon-interview-experience-set-327-off-campus-sde-1/)

**实施:**

```
1- First, check if the whole array is in 
   increasing order, if yes then print arr[n-1].
   and return.

2- If above statement doesn't run even single
   time that means an array is in decreasing 
   order from starting. Two cases arise:

      a) Check if the whole array is in 
         decreasing order, if yes then 
         print arr[0] and return.
     (b) Otherwise, the array is descending
         rotated and the maximum element will
         be the index before which array was 
         decreasing.

3- If first point partially satisfies that 
   means the whole array is not in increasing 
   order that means an array is ascending 
   rotated and the maximum element will be the
   point from where it starts decreasing.
```

## C++

```
// C++ program to find type of array, ascending
// descending, clockwise rotated or anti-clockwise
// rotated.
#include <bits/stdc++.h>
using namespace std;

// Function to find the type of an array
// and maximum element in it.
void findType(int arr[], int n)
{
    int i = 0;

    // Check if the array is in ascending order
    while (i < n - 1 && arr[i] <= arr[i + 1])
        i++;

    // If i reaches to last index that means
    // all elements are in increasing order
    if (i == n - 1) {
        cout << "Ascending with maximum element = "
             << arr[n - 1] << endl;
        return;
    }

    // If first element is greater than next one
    if (i == 0) {
        while (i < n - 1 && arr[i] >= arr[i + 1])
            i++;

        // If i reaches to last index
        if (i == n - 1) {
            cout << "Descending with maximum element =  "
                 << arr[0] << endl;
            return;
        }

        // If the whole array is not in decreasing order
        // that means it is first decreasing then
        // increasing, i.e., descending rotated, so
        // its maximum element will be the point breaking
        // the order i.e. i so, max will be i+1
        if (arr[0] < arr[i + 1]) {
            cout << "Descending rotated with maximum element = "
                 << max(arr[0], arr[i + 1]) << endl;
            return;
        }
        else {
            cout << "Ascending rotated with maximum element = "
                 << max(arr[0], arr[i + 1]) << endl;
            return;
        }
    }

    // If whole array is not increasing that means at some
    // point it is decreasing, which makes it ascending rotated
    // with max element as the decreasing point
    if (i < n - 1 && arr[0] > arr[i + 1]) {
        cout << "Ascending rotated with maximum element =  "
             << max(arr[i], arr[0]) << endl;
        return;
    }

    cout << "Descending rotated with maximum element "
         << max(arr[i], arr[0]) << endl;
}

// Driver code
int main()
{
    int arr1[] = { 4, 5, 6, 1, 2, 3 }; // Ascending rotated
    int n = sizeof(arr1) / sizeof(arr1[0]);
    findType(arr1, n);

    int arr2[] = { 2, 1, 7, 5, 4, 3 }; // Descending rotated
    n = sizeof(arr2) / sizeof(arr2[0]);
    findType(arr2, n);

    int arr3[] = { 1, 2, 3, 4, 5, 8 }; // Ascending
    n = sizeof(arr3) / sizeof(arr3[0]);
    findType(arr3, n);

    int arr4[] = { 9, 5, 4, 3, 2, 1 }; // Descending
    n = sizeof(arr4) / sizeof(arr4[0]);
    findType(arr4, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find type of array, ascending
// descending, clockwise rotated or anti-clockwise
// rotated.
import java.io.*;
class GFG {
    public static int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    // Function to find the type of an array
    // and maximum element in it
    public static void findType(int arr[])
    {
        int i = 0;
        int n = arr.length;

        // Check if the array is in ascending order
        while (i < n - 1 && arr[i] <= arr[i + 1])
            i++;

        // If i reaches to last index that means
        // all elements are in increasing order
        if (i == n - 1) {
            System.out.println("Ascending with maximum element = " + arr[n - 1]);
            return;
        }

        // If first element is greater than next one
        if (i == 0) {
            while (i < n - 1 && arr[i] >= arr[i + 1])
                i++;

            // If i reaches to last index
            if (i == n - 1) {
                System.out.println("Descending with maximum "
                                   + "element =  " + arr[0]);
                return;
            }

            // If the whole array is not in decreasing order
            // that means it is first decreasing then
            // increasing, i.e., descending rotated, so
            // its maximum element will be the point breaking
            // the order i.e. i so, max will be i+1
            if (arr[0] < arr[i + 1]) {
                System.out.println("Descending rotated with"
                                   + " maximum element = " + max(arr[0], arr[i + 1]));
                return;
            }
            else {
                System.out.println("Ascending rotated with"
                                   + " maximum element = " + max(arr[0], arr[i + 1]));
                return;
            }
        }

        // If whole array is not increasing that means at some
        // point it is decreasing, which makes it ascending rotated
        // with max element as the decreasing point
        if (i < n - 1 && arr[0] > arr[i + 1]) {

            System.out.println("Ascending rotated with maximum"
                               + " element =  " + max(arr[i], arr[0]));
            return;
        }

        System.out.println("Descending rotated with maximum "
                           + "element " + max(arr[i], arr[0]));
    }

    public static void main(String[] args)
    {
        int arr1[] = { 4, 5, 6, 1, 2, 3 }; // Ascending rotated
        findType(arr1);

        int arr2[] = { 2, 1, 7, 5, 4, 3 }; // Descending rotated
        findType(arr2);

        int arr3[] = { 1, 2, 3, 4, 5, 8 }; // Ascending
        findType(arr3);

        int arr4[] = { 9, 5, 4, 3, 2, 1 }; // Descending
        findType(arr4);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find type of array, ascending
# descending, clockwise rotated or anti-clockwise
# rotated.

def findType(arr, n) :

    i = 0;

    # Check if the array is in ascending order
    while (i < n-1 and arr[i] <= arr[i + 1]) :
        i = i + 1

    # If i reaches to last index that means
    # all elements are in increasing order
    if (i == n-1):
        print(("Ascending with maximum element = "
              + str(arr[n-1])))
        return None

    # If first element is greater than next one
    if (i == 0):
        while (i < n-1 and arr[i] >= arr[i + 1]):
            i = i + 1;

        # If i reaches to last index
        if (i == n - 1):
            print(("Descending with maximum element = "
                  + str(arr[0])))
            return None

        # If the whole array is not in decreasing order
        # that means it is first decreasing then
        # increasing, i.e., descending rotated, so
        # its maximum element will be the point breaking
        # the order i.e. i so, max will be i + 1
        if (arr[0] < arr[i + 1]):
            print(("Descending rotated with maximum element = "
                  + str(max(arr[0], arr[i + 1]))))
            return None
        else:

            print(("Ascending rotated with maximum element = "
                  + str(max(arr[0], arr[i + 1]))))

            return None

    # If whole array is not increasing that means at some
    # point it is decreasing, which makes it ascending rotated
    # with max element as the decreasing point
    if (i < n -1 and arr[0] > arr[i + 1]):

        print(("Ascending rotated with maximum element = "
             + str(max(arr[i], arr[0]))))
        return None

    print(("Descending rotated with maximum element "
          + str(max(arr[i], arr[0]))))

# Driver code
if __name__=='__main__':
    arr1 = [ 4, 5, 6, 1, 2, 3] # Ascending rotated
    n = len(arr1)
    findType(arr1, n);

    arr2 = [ 2, 1, 7, 5, 4, 3] # Descending rotated
    n = len(arr2)
    findType(arr2, n);

    arr3 = [ 1, 2, 3, 4, 5, 8] # Ascending
    n = len(arr3)
    findType(arr3, n);

    arr4 = [ 9, 5, 4, 3, 2, 1] # Descending
    n = len(arr4)
    findType(arr4, n);

# this code is contributed by YatinGupta
```

## C#

```
// C# program to find type of array, ascending
// descending, clockwise rotated or anti-clockwise
// rotated.
using System;

class GFG {

    public static int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    // Function to find the type of an array
    // and maximum element in it
    public static void findType(int[] arr)
    {
        int i = 0;
        int n = arr.Length;

        // Check if the array is in ascending
        // order
        while (i < n - 1 && arr[i] <= arr[i + 1])
            i++;

        // If i reaches to last index that means
        // all elements are in increasing order
        if (i == n - 1) {
            Console.WriteLine("Ascending with "
                              + "maximum element = " + arr[n - 1]);
            return;
        }

        // If first element is greater than
        // next one
        if (i == 0) {
            while (i < n - 1 && arr[i] >= arr[i + 1])
                i++;

            // If i reaches to last index
            if (i == n - 1) {
                Console.WriteLine("Descending with"
                                  + " maximum element = " + arr[0]);
                return;
            }

            // If the whole array is not in
            // decreasing order that means it is
            // first decreasing then increasing,
            // i.e., descending rotated, so its
            // maximum element will be the point
            // breaking the order i.e. i so, max
            // will be i+1
            if (arr[0] < arr[i + 1]) {
                Console.WriteLine("Descending rotated"
                                  + " with maximum element = "
                                  + max(arr[0], arr[i + 1]));
                return;
            }
            else {
                Console.WriteLine("Ascending rotated"
                                  + " with maximum element = "
                                  + max(arr[0], arr[i + 1]));
                return;
            }
        }

        // If whole array is not increasing that
        // means at some point it is decreasing,
        // which makes it ascending rotated with
        // max element as the decreasing point
        if (i < n - 1 && arr[0] > arr[i + 1]) {

            Console.WriteLine("Ascending rotated"
                              + " with maximum element = "
                              + max(arr[i], arr[0]));
            return;
        }

        Console.WriteLine("Descending rotated with"
                          + " maximum element "
                          + max(arr[i], arr[0]));
    }

    // Driver code
    public static void Main()
    {

        // Ascending rotated
        int[] arr1 = { 4, 5, 6, 1, 2, 3 };
        findType(arr1);

        // Descending rotated
        int[] arr2 = { 2, 1, 7, 5, 4, 3 };
        findType(arr2);

        // Ascending
        int[] arr3 = { 1, 2, 3, 4, 5, 8 };
        findType(arr3);

        // Descending
        int[] arr4 = { 9, 5, 4, 3, 2, 1 };
        findType(arr4);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find type
// of array, ascending descending,
// clockwise rotated or anti-clockwise
// rotated.

// Function to find the type
// of an array and maximum
// element in it.
function findType($arr, $n)
{
    $i = 0;

    // Check if the array is
    // in ascending order
    while ($i < $n - 1 and
           $arr[$i] <= $arr[$i + 1])
        $i++;

    // If i reaches to last index
    // that means all elements are
    // in increasing order
    if ($i == $n - 1)
    {
        echo "Ascending with maximum ".
                         "element = ",
                    $arr[$n - 1], "\n";
        return ;
    }

    // If first element is
    // greater than next one
    if ($i == 0)
    {
        while ($i < $n - 1 and
               $arr[$i] >= $arr[$i + 1])
            $i++;

        // If i reaches to last index
        if ($i == $n - 1)
        {
            echo "Descending with maximum ".
                              "element = ",
                              $arr[0], "\n";
            return ;
        }

        // If the whole array is not in
        // decreasing order that means
        // it is first decreasing then
        // increasing, i.e., descending
        // rotated, so its maximum element
        // will be the point breaking the
        // order i.e. i so, max will be i+1
        if ($arr[0] < $arr[$i + 1])
        {
            echo "Descending rotated with ".
                      "maximum element = ",
                                max($arr[0],
                        $arr[$i + 1]), "\n";
            return ;
        }
        else
        {
            echo "Ascending rotated with " .
                       "maximum element = ",
                                max($arr[0],
                       $arr[$i + 1]), "\n";
            return ;
        }
    }

    // If whole array is not increasing
    // that means at some point it is
    // decreasing, which makes it
    // ascending rotated with max element
    // as the decreasing point
    if ($i < $n - 1 and $arr[0] > $arr[$i + 1])
    {
        echo "Ascending rotated with maximum ".
                   "element = ", max($arr[$i],
                                $arr[0]), "\n";
        return;
    }

    echo "Descending rotated with maximum " .
                   "element ", max($arr[$i],
                              $arr[0]), "\n";
}

// Driver code

// Ascending rotated
$arr1 = array( 4, 5, 6, 1, 2, 3);
$n = count($arr1);
findType($arr1, $n);

// Descending rotated
$arr2 = array( 2, 1, 7, 5, 4, 3);
$n = count($arr2);
findType($arr2, $n);

// Ascending
$arr3 = array( 1, 2, 3, 4, 5, 8);
$n = count($arr3);
findType($arr3, $n);

// Descending
$arr4 = array( 9, 5, 4, 3, 2, 1);
$n = count($arr4);
findType($arr4, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find type of array, ascending
    // descending, clockwise rotated or anti-clockwise
    // rotated.

    function max(a, b)
    {
        return (a > b) ? a : b;
    }

    // Function to find the type of an array
    // and maximum element in it
    function findType(arr)
    {
        let i = 0;
        let n = arr.length;

        // Check if the array is in ascending
        // order
        while (i < n - 1 && arr[i] <= arr[i + 1])
            i++;

        // If i reaches to last index that means
        // all elements are in increasing order
        if (i == n - 1) {
            document.write("Ascending with "
                              + "maximum element = " + arr[n - 1] + "</br>");
            return;
        }

        // If first element is greater than
        // next one
        if (i == 0) {
            while (i < n - 1 && arr[i] >= arr[i + 1])
                i++;

            // If i reaches to last index
            if (i == n - 1) {
                document.write("Descending with"
                                  + " maximum element = " + arr[0]);
                return;
            }

            // If the whole array is not in
            // decreasing order that means it is
            // first decreasing then increasing,
            // i.e., descending rotated, so its
            // maximum element will be the point
            // breaking the order i.e. i so, max
            // will be i+1
            if (arr[0] < arr[i + 1]) {
                document.write("Descending rotated"
                                  + " with maximum element = "
                                  + max(arr[0], arr[i + 1]) + "</br>");
                return;
            }
            else {
                document.write("Ascending rotated"
                                  + " with maximum element = "
                                  + max(arr[0], arr[i + 1]) + "</br>");
                return;
            }
        }

        // If whole array is not increasing that
        // means at some point it is decreasing,
        // which makes it ascending rotated with
        // max element as the decreasing point
        if (i < n - 1 && arr[0] > arr[i + 1]) {

            document.write("Ascending rotated"
                              + " with maximum element = "
                              + max(arr[i], arr[0]) + "</br>");
            return;
        }

        document.write("Descending rotated with"
                          + " maximum element "
                          + max(arr[i], arr[0]) + "</br>");
    }

    // Ascending rotated
    let arr1 = [ 4, 5, 6, 1, 2, 3 ];
    findType(arr1);

    // Descending rotated
    let arr2 = [ 2, 1, 7, 5, 4, 3 ];
    findType(arr2);

    // Ascending
    let arr3 = [ 1, 2, 3, 4, 5, 8 ];
    findType(arr3);

    // Descending
    let arr4 = [ 9, 5, 4, 3, 2, 1 ];
    findType(arr4);

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Ascending rotated with maximum element = 6
Descending rotated with maximum element = 7
Ascending with maximum element = 8
Descending with maximum element = 9
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**另一种方法:**遍历数组一次，并存储数组最小和最大元素的第一次和最后一次出现的索引。现在有四种情况:

1.  如果最小元素的第一次出现在数组的开头，最大元素的最后一次出现在数组的末尾，则数组按升序排列。例如，{1，1，1，2，3，4，5，6，6，6}。
2.  如果最大元素的第一次出现在数组的开头，最小元素的最后一次出现在数组的末尾，则数组按降序排列。例如，{6，6，6，5，4，3，2，1，1，1}。
3.  如果最大元素的第一次出现等于最小元素的最后一次出现+ 1，则数组按降序旋转。例如，{3，2，1，1，1，6，6，6，5，4}。
4.  如果最小元素的第一次出现等于最大元素的最后一次出现+ 1，则数组按升序旋转。例如，{4，5，6，6，6，1，1，1，2，3}。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the type of an array
// and maximum element in it
void findType(int arr[], int n)
{

    // To store the minimum and the maximum
    // element from the array
    int min_element = INT_MAX, max_element = INT_MIN;

    // To store the first and the last occurrences
    // of the minimum and the maximum
    // element from the array
    int min_index1, max_index1, max_index2, min_index2;

    for (int i = 0; i < n; i++) {

        // If new minimum is found
        if (arr[i] < min_element) {

            // Update the minimum so far
            // and its occurrences
            min_element = arr[i];
            min_index1 = i;
            min_index2 = i;
        }

        // If current element is equal the found
        // minimum so far then update the last
        // occurrence of the minimum element
        else if (arr[i] == min_element)
            min_index2 = i;

        // If new maximum is found
        if (arr[i] > max_element) {

            // Update the maximum so far
            // and its occurrences
            max_element = arr[i];
            max_index1 = i;
            max_index2 = i;
        }

        // If current element is equal the found
        // maximum so far then update the last
        // occurrence of the maximum element
        else if (arr[i] == max_element)
            max_index2 = i;
    }

    // First occurrence of minimum element is at the
    // beginning of the array and the last occurrence
    // of the maximum element is at the end of the
    // array then the array is sorted in ascending
    // For example, {1, 1, 1, 2, 3, 4, 5, 6, 6, 6}
    if (min_index1 == 0 && max_index2 == n - 1) {
        cout << "Ascending with maximum element = "
             << max_element << endl;
    }

    // First occurrence of maximum element is at the
    // beginning of the array and the last occurrence
    // of the minimum element is at the end of the
    // array then the array is sorted in descending
    // For example, {6, 6, 6, 5, 4, 3, 2, 1, 1, 1}
    else if (min_index2 == n - 1 && max_index1 == 0) {
        cout << "Descending with maximum element = "
             << max_element << endl;
    }

    // First occurrence of maximum element is equal
    // to the last occurrence of the minimum element + 1
    // then the array is descending and rotated
    // For example, {3, 2, 1, 1, 1, 6, 6, 6, 5, 4}
    else if (max_index1 == min_index2 + 1) {
        cout << "Descending rotated with maximum element = "
             << max_element << endl;
    }

    // First occurrence of minimum element is equal
    // to the last occurrence of the maximum element + 1
    // then the array is ascending and rotated
    // For example, {4, 5, 6, 6, 6, 1, 1, 1, 2, 3}
    else {
        cout << "Ascending rotated with maximum element = "
             << max_element << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 6, 6, 6, 1, 1, 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findType(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the type of an array
// and maximum element in it
static void findType(int arr[], int n)
{

    // To store the minimum and the maximum
    // element from the array
    int min_element = Integer.MAX_VALUE,
        max_element = Integer.MIN_VALUE;

    // To store the first and the last occurrences
    // of the minimum and the maximum
    // element from the array
    int min_index1 = -1, max_index1 = -1,
        max_index2 = -1, min_index2 = -1;

    for (int i = 0; i < n; i++)
    {

        // If new minimum is found
        if (arr[i] < min_element)
        {

            // Update the minimum so far
            // and its occurrences
            min_element = arr[i];
            min_index1 = i;
            min_index2 = i;
        }

        // If current element is equal the found
        // minimum so far then update the last
        // occurrence of the minimum element
        else if (arr[i] == min_element)
            min_index2 = i;

        // If new maximum is found
        if (arr[i] > max_element)
        {

            // Update the maximum so far
            // and its occurrences
            max_element = arr[i];
            max_index1 = i;
            max_index2 = i;
        }

        // If current element is equal the found
        // maximum so far then update the last
        // occurrence of the maximum element
        else if (arr[i] == max_element)
            max_index2 = i;
    }

    // First occurrence of minimum element is at the
    // beginning of the array and the last occurrence
    // of the maximum element is at the end of the
    // array then the array is sorted in ascending
    // For example, {1, 1, 1, 2, 3, 4, 5, 6, 6, 6}
    if (min_index1 == 0 && max_index2 == n - 1)
    {
        System.out.println("Ascending with maximum" +  
                        " element = " + max_element);
    }

    // First occurrence of maximum element is at the
    // beginning of the array and the last occurrence
    // of the minimum element is at the end of the
    // array then the array is sorted in descending
    // For example, {6, 6, 6, 5, 4, 3, 2, 1, 1, 1}
    else if (min_index2 == n - 1 && max_index1 == 0)
    {
        System.out.println("Descending with maximum" +
                         " element = " + max_element);
    }

    // First occurrence of maximum element is equal
    // to the last occurrence of the minimum element + 1
    // then the array is descending and rotated
    // For example, {3, 2, 1, 1, 1, 6, 6, 6, 5, 4}
    else if (max_index1 == min_index2 + 1)
    {
        System.out.println("Descending rotated with " +
                   "maximum element = " + max_element);
    }

    // First occurrence of minimum element is equal
    // to the last occurrence of the maximum element + 1
    // then the array is ascending and rotated
    // For example, {4, 5, 6, 6, 6, 1, 1, 1, 2, 3}
    else
    {
        System.out.println("Ascending rotated with " +
                  "maximum element = " + max_element);
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 5, 6, 6, 6, 1, 1, 1, 2, 3 };
    int n = arr.length;

    findType(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to find the type of an array
# and maximum element in it
import sys

def findType(arr, n):

    # To store the minimum and the maximum
    # element from the array
    min_element = sys.maxsize;
    max_element = -sys.maxsize;

    # To store the first and the last occurrences
    # of the minimum and the maximum
    # element from the array
    min_index1 = -1; max_index1 = -1,
    max_index2 = -1; min_index2 = -1;

    for i in range(n):

        # If new minimum is found
        if (arr[i] < min_element):

            # Update the minimum so far
            # and its occurrences
            min_element = arr[i];
            min_index1 = i;
            min_index2 = i;

        # If current element is equal the found
        # minimum so far then update the last
        # occurrence of the minimum element
        elif (arr[i] == min_element):
            min_index2 = i;

        # If new maximum is found
        if (arr[i] > max_element):

            # Update the maximum so far
            # and its occurrences
            max_element = arr[i];
            max_index1 = i;
            max_index2 = i;

        # If current element is equal the found
        # maximum so far then update the last
        # occurrence of the maximum element
        elif (arr[i] == max_element):
            max_index2 = i;

    # First occurrence of minimum element is at the
    # beginning of the array and the last occurrence
    # of the maximum element is at the end of the
    # array then the array is sorted in ascending
    # For example, 1, 1, 1, 2, 3, 4, 5, 6, 6, 6
    if (min_index1 == 0 and max_index2 == n - 1):

        print("Ascending with maximum",
                          "element = ", max_element);

    # First occurrence of maximum element is at the
    # beginning of the array and the last occurrence
    # of the minimum element is at the end of the
    # array then the array is sorted in descending
    # For example, 6, 6, 6, 5, 4, 3, 2, 1, 1, 1
    elif (min_index2 == n - 1 and max_index1 == 0):

        print("Descending with maximum",
                           "element = ", max_element);

    # First occurrence of maximum element is equal
    # to the last occurrence of the minimum element + 1
    # then the array is descending and rotated
    # For example, [3, 2, 1, 1, 1, 6, 6, 6, 5, 4]
    elif (max_index1 == min_index2 , 1):

        print("Descending rotated with",
                   "maximum element = ", max_element);

    # First occurrence of minimum element is equal
    # to the last occurrence of the maximum element + 1
    # then the array is ascending and rotated
    # For example, [4, 5, 6, 6, 6, 1, 1, 1, 2, 3]
    else:

        print("Ascending rotated with",
                  "maximum element = ", max_element);

# Driver code
arr = [4, 5, 6, 6, 6, 1, 1, 1, 2, 3];
n = len(arr);

findType(arr, n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the type of an array
// and maximum element in it
static void findType(int []arr, int n)
{

    // To store the minimum and the maximum
    // element from the array
    int min_element = int.MaxValue,
        max_element = int.MinValue;

    // To store the first and the last occurrences
    // of the minimum and the maximum
    // element from the array
    int min_index1 = -1, max_index1 = -1,
        max_index2 = -1, min_index2 = -1;

    for (int i = 0; i < n; i++)
    {

        // If new minimum is found
        if (arr[i] < min_element)
        {

            // Update the minimum so far
            // and its occurrences
            min_element = arr[i];
            min_index1 = i;
            min_index2 = i;
        }

        // If current element is equal the found
        // minimum so far then update the last
        // occurrence of the minimum element
        else if (arr[i] == min_element)
            min_index2 = i;

        // If new maximum is found
        if (arr[i] > max_element)
        {

            // Update the maximum so far
            // and its occurrences
            max_element = arr[i];
            max_index1 = i;
            max_index2 = i;
        }

        // If current element is equal the found
        // maximum so far then update the last
        // occurrence of the maximum element
        else if (arr[i] == max_element)
            max_index2 = i;
    }

    // First occurrence of minimum element is at the
    // beginning of the array and the last occurrence
    // of the maximum element is at the end of the
    // array then the array is sorted in ascending
    // For example, {1, 1, 1, 2, 3, 4, 5, 6, 6, 6}
    if (min_index1 == 0 && max_index2 == n - 1)
    {
        Console.Write("Ascending with maximum" +
                   " element = " + max_element);
    }

    // First occurrence of maximum element is at the
    // beginning of the array and the last occurrence
    // of the minimum element is at the end of the
    // array then the array is sorted in descending
    // For example, {6, 6, 6, 5, 4, 3, 2, 1, 1, 1}
    else if (min_index2 == n - 1 && max_index1 == 0)
    {
        Console.Write("Descending with maximum" +
                    " element = " + max_element);
    }

    // First occurrence of maximum element is equal
    // to the last occurrence of the minimum element + 1
    // then the array is descending and rotated
    // For example, {3, 2, 1, 1, 1, 6, 6, 6, 5, 4}
    else if (max_index1 == min_index2 + 1)
    {
        Console.Write("Descending rotated with " +
              "maximum element = " + max_element);
    }

    // First occurrence of minimum element is equal
    // to the last occurrence of the maximum element + 1
    // then the array is ascending and rotated
    // For example, {4, 5, 6, 6, 6, 1, 1, 1, 2, 3}
    else
    {
        Console.Write("Ascending rotated with " +
             "maximum element = " + max_element);
    }
}

// Driver code
static public void Main ()
{
    int []arr = { 4, 5, 6, 6, 6, 1, 1, 1, 2, 3 };
    int n = arr.Length;

    findType(arr, n);
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to find the type of an array
    // and maximum element in it
    function findType(arr, n)
    {

        // To store the minimum and the maximum
        // element from the array
        let min_element = Number.MAX_VALUE,
            max_element = Number.MIN_VALUE;

        // To store the first and the last occurrences
        // of the minimum and the maximum
        // element from the array
        let min_index1 = -1, max_index1 = -1,
            max_index2 = -1, min_index2 = -1;

        for (let i = 0; i < n; i++)
        {

            // If new minimum is found
            if (arr[i] < min_element)
            {

                // Update the minimum so far
                // and its occurrences
                min_element = arr[i];
                min_index1 = i;
                min_index2 = i;
            }

            // If current element is equal the found
            // minimum so far then update the last
            // occurrence of the minimum element
            else if (arr[i] == min_element)
                min_index2 = i;

            // If new maximum is found
            if (arr[i] > max_element)
            {

                // Update the maximum so far
                // and its occurrences
                max_element = arr[i];
                max_index1 = i;
                max_index2 = i;
            }

            // If current element is equal the found
            // maximum so far then update the last
            // occurrence of the maximum element
            else if (arr[i] == max_element)
                max_index2 = i;
        }

        // First occurrence of minimum element is at the
        // beginning of the array and the last occurrence
        // of the maximum element is at the end of the
        // array then the array is sorted in ascending
        // For example, {1, 1, 1, 2, 3, 4, 5, 6, 6, 6}
        if (min_index1 == 0 && max_index2 == n - 1)
        {
            document.write("Ascending with maximum" +
                       " element = " + max_element);
        }

        // First occurrence of maximum element is at the
        // beginning of the array and the last occurrence
        // of the minimum element is at the end of the
        // array then the array is sorted in descending
        // For example, {6, 6, 6, 5, 4, 3, 2, 1, 1, 1}
        else if (min_index2 == n - 1 && max_index1 == 0)
        {
            document.write("Descending with maximum" +
                        " element = " + max_element);
        }

        // First occurrence of maximum element is equal
        // to the last occurrence of the minimum element + 1
        // then the array is descending and rotated
        // For example, {3, 2, 1, 1, 1, 6, 6, 6, 5, 4}
        else if (max_index1 == min_index2 + 1)
        {
            document.write("Descending rotated with " +
                  "maximum element = " + max_element);
        }

        // First occurrence of minimum element is equal
        // to the last occurrence of the maximum element + 1
        // then the array is ascending and rotated
        // For example, {4, 5, 6, 6, 6, 1, 1, 1, 2, 3}
        else
        {
            document.write("Ascending rotated with " +
                 "maximum element = " + max_element);
        }
    }

    let arr = [ 4, 5, 6, 6, 6, 1, 1, 1, 2, 3 ];
    let n = arr.length;

    findType(arr, n);

</script>
```

**输出:**

```
Ascending rotated with maximum element = 6
```