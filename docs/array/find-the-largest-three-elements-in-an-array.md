# 查找数组中最大的三个元素

> 原文： [https://www.geeksforgeeks.org/find-the-largest-three-elements-in-an-array/](https://www.geeksforgeeks.org/find-the-largest-three-elements-in-an-array/)

给定一个包含所有不同元素的数组，找到最大的三个元素。 预期时间复杂度为`O(n)`，额外空间为`O(1)`。

**示例**：

```
Input: arr[] = {10, 4, 3, 50, 23, 90}
Output: 90, 50, 23

```



下面是算法：

```
1) Initialize the largest three elements as minus infinite.
    first = second = third = -∞

2) Iterate through all elements of array.
   a) Let current array element be x.
   b) If (x > first)
      {
          // This order of assignment is important
          third = second
          second = first
          first = x   
       }
   c)  Else if (x > second)
      {
          third = second
          second = x 
      }
   d)  Else if (x > third)
      {
          third = x  
      }

3) Print first, second and third.

```

下面是上述算法的实现。

## C

```c

#include <stdio.h> 
#include <limits.h> /* For INT_MIN */ 

/* Function to print three largest elements */
void print3largest(int arr[], int arr_size) 
{ 
    int i, first, second, third; 

    /* There should be atleast three elements */
    if (arr_size < 3) 
    { 
        printf(" Invalid Input "); 
        return; 
    } 

    third = first = second = INT_MIN; 
    for (i = 0; i < arr_size ; i ++) 
    { 
        /* If current element is greater than first*/
        if (arr[i] > first) 
        { 
            third = second; 
            second = first; 
            first = arr[i]; 
        } 

        /* If arr[i] is in between first and second then update second  */
        else if (arr[i] > second) 
        { 
            third = second; 
            second = arr[i]; 
        } 

        else if (arr[i] > third) 
            third = arr[i]; 
    } 

    printf("Three largest elements are %d %d %d\n", first, second, third); 
} 

/* Driver program to test above function */
int main() 
{ 
    int arr[] = {12, 13, 1, 10, 34, 1}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    print3largest(arr, n); 
    return 0; 
} 
/*This code is edited by Ayush Singla(@ayusin51)*/

```

## C

```c
// C program for find the largest  
// three elements in an array 
#include <limits.h> /* For INT_MIN */ 
#include <stdio.h> 
  
/* Function to print three largest elements */
void print3largest(int arr[], int arr_size) 
{ 
    int i, first, second, third; 
  
    /* There should be atleast three elements */
    if (arr_size < 3) { 
        printf(" Invalid Input "); 
        return; 
    } 
  
    third = first = second = INT_MIN; 
    for (i = 0; i < arr_size; i++) { 
        /* If current element is greater than first*/
        if (arr[i] > first) { 
            third = second; 
            second = first; 
            first = arr[i]; 
        } 
  
        /* If arr[i] is in between first and second then update second  */
        else if (arr[i] > second) { 
            third = second; 
            second = arr[i]; 
        } 
  
        else if (arr[i] > third) 
            third = arr[i]; 
    } 
  
    printf("Three largest elements are %d %d %d\n", first, second, third); 
} 
  
/* Driver program to test above function */
int main() 
{ 
    int arr[] = { 12, 13, 1, 10, 34, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    print3largest(arr, n); 
    return 0; 
} 
/*This code is edited by Ayush Singla(@ayusin51)*/
```

## Java

```java
// Java code to find largest three elements 
// in an array 
  
class PrintLargest { 
    /* Function to print three largest elements */
    static void print3largest(int arr[], int arr_size) 
    { 
        int i, first, second, third; 
  
        /* There should be atleast three elements */
        if (arr_size < 3) { 
            System.out.print(" Invalid Input "); 
            return; 
        } 
  
        third = first = second = Integer.MIN_VALUE; 
        for (i = 0; i < arr_size; i++) { 
            /* If current element is greater than 
            first*/
            if (arr[i] > first) { 
                third = second; 
                second = first; 
                first = arr[i]; 
            } 
  
            /* If arr[i] is in between first and 
            second then update second  */
            else if (arr[i] > second) { 
                third = second; 
                second = arr[i]; 
            } 
  
            else if (arr[i] > third) 
                third = arr[i]; 
        } 
  
        System.out.println("Three largest elements are " + first + " " + second + " " + third); 
    } 
  
    /* Driver program to test above function*/
    public static void main(String[] args) 
    { 
        int arr[] = { 12, 13, 1, 10, 34, 1 }; 
        int n = arr.length; 
        print3largest(arr, n); 
    } 
} 
/*This code is contributed by Prakriti Gupta  
and edited by Ayush Singla(@ayusin51)*/
```

## Python3

```py
# Python3 code to find largest three 
# elements in an array 
import sys 
  
# Function to print three largest  
# elements  
def print3largest(arr, arr_size): 
  
    # There should be atleast three 
    # elements  
    if (arr_size < 3): 
      
        print(" Invalid Input ") 
        return
      
    third = first = second = -sys.maxsize 
      
    for i in range(0, arr_size): 
      
        # If current element is greater 
        # than first 
        if (arr[i] > first): 
          
            third = second 
            second = first 
            first = arr[i] 
          
  
        # If arr[i] is in between first 
        # and second then update second  
        elif (arr[i] > second): 
          
            third = second 
            second = arr[i] 
          
        elif (arr[i] > third): 
            third = arr[i] 
      
    print("Three largest elements are", 
                  first, second, third) 
  
# Driver program to test above function  
arr = [12, 13, 1, 10, 34, 1] 
n = len(arr) 
print3largest(arr, n) 
  
# This code is contributed by Smitha Dinesh Semwal  
# and edited by Ayush Singla(@ayusin51). 
```

## C#

```cs
// C# code to find largest 
// three elements in an array 
using System; 
  
class PrintLargest { 
  
    // Function to print three 
    // largest elements 
    static void print3largest(int[] arr, 
                              int arr_size) 
    { 
        int i, first, second, third; 
  
        // There should be atleast three elements 
        if (arr_size < 3) { 
            Console.WriteLine("Invalid Input"); 
            return; 
        } 
  
        third = first = second = 000; 
        for (i = 0; i < arr_size; i++) { 
            // If current element is 
            // greater than first 
            if (arr[i] > first) { 
                third = second; 
                second = first; 
                first = arr[i]; 
            } 
  
            // If arr[i] is in between first 
            // and second then update second 
            else if (arr[i] > second) { 
                third = second; 
                second = arr[i]; 
            } 
  
            else if (arr[i] > third) 
                third = arr[i]; 
        } 
  
        Console.WriteLine("Three largest elements are " + first + " " + second + " " + third); 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = new int[] { 12, 13, 1, 10, 34, 1 }; 
        int n = arr.Length; 
        print3largest(arr, n); 
    } 
} 
  
// This code is contributed by KRV and edited by Ayush Singla(@ayusin51). 
```

## PHP

```php
<?php 
// PHP code to find largest  
// three elements in an array 
  
// Function to print  
// three largest elements 
function print3largest($arr, $arr_size) 
{ 
    $i; $first; $second; $third; 
  
    // There should be atleast 
    // three elements  
    if ($arr_size < 3) 
    { 
        echo " Invalid Input "; 
        return; 
    } 
  
    $third = $first = $second = PHP_INT_MIN; 
    for ($i = 0; $i < $arr_size ; $i ++) 
    { 
        // If current element is 
        // greater than first 
        if ($arr[$i] > $first) 
        { 
            $third = $second; 
            $second = $first; 
            $first = $arr[$i]; 
        } 
  
        // If arr[i] is in between first  
        // and second then update second  
        else if ($arr[$i] > $second) 
        { 
            $third = $second; 
            $second = $arr[$i]; 
        } 
  
        else if ($arr[$i] > $third) 
            $third = $arr[$i]; 
    } 
  
    echo "Three largest elements are ",  
       $first, " ", $second, " ", $third; 
} 
  
  
// Driver Code 
$arr = array(12, 13, 1,  
             10, 34, 1); 
$n = count($arr); 
print3largest($arr, $n); 
  
// This code is contributed by anuj_67 and edited by Ayush Singla(@ayusin51). 
?> 
```

输出：

```
Three largest elements are 34 13 12
```

方法二：

解决此问题的有效方法是使用任何`O(nLogn)`排序算法并简单地返回最后 3 个最大元素。

## C++

```cpp
// C++ code to find largest 
// three elements in an array 
#include <bits/stdc++.h> 
using namespace std; 
  
void find3largest(int arr[], int n) 
{ 
    sort(arr, arr + n); // It uses Tuned Quicksort with 
    // avg. case Time complexity = O(nLogn) 
  
    int check = 0, count = 1; 
  
    for (int i = 1; i <= n; i++) { 
  
        if (count < 4) { 
            if (check != arr[n - i]) { 
                // to handle duplicate values 
                cout << arr[n - i] << " "; 
                check = arr[n - i]; 
                count++; 
            } 
        } 
        else
            break; 
    } 
} 
  
// Driver code 
int main() 
{ 
    int arr[] = { 12, 45, 1, -1, 45, 54, 23, 5, 0, -10 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    find3largest(arr, n); 
} 
  
// This code is contibuted by Rajput-Ji 
```

## Java

```java
// Java code to find largest 
// three elements in an array 
  
import java.io.*; 
import java.util.Arrays; 
  
class GFG { 
    void find3largest(int[] arr) 
    { 
        Arrays.sort(arr); // It uses Tuned Quicksort with 
        // avg. case Time complexity = O(nLogn) 
        int n = arr.length; 
        int check = 0, count = 1; 
  
        for (int i = 1; i <= n; i++) { 
  
            if (count < 4) { 
                if (check != arr[n - i]) { 
                    // to handle duplicate values 
                    System.out.print(arr[n - i] + " "); 
                    check = arr[n - i]; 
                    count++; 
                } 
            } 
            else
                break; 
        } 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        GFG obj = new GFG(); 
        int[] arr = { 12, 45, 1, -1, 45, 54, 23, 5, 0, -10 }; 
        obj.find3largest(arr); 
    } 
} 
// This code is contibuted by Prashant Malik 
```

## Python3

```py
# Python3 code to find largest 
# three elements in an array 
def find3largest(arr, n): 
    arr = sorted(arr) # It uses Tuned Quicksort with 
                      # avg. case Time complexity = O(nLogn) 
  
    check = 0
    count = 1
  
    for i in range(1, n + 1): 
  
        if(count < 4): 
            if(check != arr[n - i]): 
                  
                # to handle duplicate values 
                print(arr[n - i], end = " ") 
                check = arr[n - i] 
                count += 1
        else: 
            break
  
# Driver code 
arr = [12, 45, 1, -1, 45,  
       54, 23, 5, 0, -10] 
n = len(arr) 
find3largest(arr, n) 
  
# This code is contibuted by mohit kumar 
```

## C#

```cs
// C# code to find largest 
// three elements in an array 
using System; 
  
class GFG { 
    void find3largest(int[] arr) 
    { 
        Array.Sort(arr); // It uses Tuned Quicksort with 
        // avg. case Time complexity = O(nLogn) 
        int n = arr.Length; 
        int check = 0, count = 1; 
  
        for (int i = 1; i <= n; i++) { 
            if (count < 4) { 
                if (check != arr[n - i]) { 
                    // to handle duplicate values 
                    Console.Write(arr[n - i] + " "); 
                    check = arr[n - i]; 
                    count++; 
                } 
            } 
            else
                break; 
        } 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        GFG obj = new GFG(); 
        int[] arr = { 12, 45, 1, -1, 45, 
                      54, 23, 5, 0, -10 }; 
        obj.find3largest(arr); 
    } 
} 
  
// This code is contibuted by Code_Mech 
```

输出：

```
 54 45 23 
```

方法 3：

我们可以使用 C++ STL 的部分排序。 `partial_sort`使用`Heapselect`，对于小型`M`，它的性能比`Quickselect`更好。作为副作用，`Heapselect`的最终状态为您留下了一个堆，这意味着您“免费”获得了`Heapsort`算法的前半部分。 复杂度是“大约” `O(N log(M))`，其中`M`是距离（中间优先）。

## C++

```cpp
#include <bits/stdc++.h> 
using namespace std; 
int main() 
{ 
    vector<int> V = { 11, 65, 193, 36, 209, 664, 32 }; 
    partial_sort(V.begin(), V.begin() + 3, V.end(), greater<int>()); 
  
    cout << "first = " << V[0] << "\n"; 
    cout << "second = " << V[1] << "\n"; 
    cout << "third = " << V[2] << "\n"; 
    return 0; 
} 
```

输出：

```
first = 664
second = 209
third = 193
```

