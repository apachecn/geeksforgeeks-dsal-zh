# 将数组中的 0 和 1 分开

> 原文： [https://www.geeksforgeeks.org/segregate-0s-and-1s-in-an-array-by-traversing-array-once/](https://www.geeksforgeeks.org/segregate-0s-and-1s-in-an-array-by-traversing-array-once/)

系统会以随机顺序为您提供 0 和 1 的数组。 分隔数组左侧的 0 和右侧的 1。 遍历数组仅一次。

```
Input array   =  [0, 1, 0, 1, 0, 0, 1, 1, 1, 0] 
Output array =  [0, 0, 0, 0, 0, 1, 1, 1, 1, 1] 

```



**方法 1（计数 0s 或 1s）**：

感谢 Naveen 建议使用此方法。

1.  计算 0 的数量。 令数量为`C`。

2.  一旦有了计数，就可以在数组的`C`位置的开头放置 0，在其余的`n – C`位置放置 1。

**时间复杂度**：`O(n)`。

## C++ 

```cpp

// C++ code to Segregate 0s and 1s in an array 
#include <bits/stdc++.h> 
using namespace std; 

// Function to segregate 0s and 1s 
void segregate0and1(int arr[], int n) 
{ 
    int count = 0; // Counts the no of zeros in arr 

    for (int i = 0; i < n; i++) { 
        if (arr[i] == 0) 
            count++; 
    } 

    // Loop fills the arr with 0 until count 
    for (int i = 0; i < count; i++) 
        arr[i] = 0; 

    // Loop fills remaining arr space with 1 
    for (int i = count; i < n; i++) 
        arr[i] = 1; 
} 

// Function to print segregated array 
void print(int arr[], int n) 
{ 
    cout << "Array after segregation is "; 

    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver function 
int main() 
{ 
    int arr[] = { 0, 1, 0, 1, 1, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    segregate0and1(arr, n); 
    print(arr, n); 

    return 0; 
} 

// This code is contributed by Sahil_Bansall 

```

## Java

```java
// Java code to Segregate 0s and 1s in an array 
class GFG { 
      
    // function to segregate 0s and 1s 
    static void segregate0and1(int arr[], int n) 
    { 
        int count = 0; // counts the no of zeros in arr 
      
        for (int i = 0; i < n; i++) { 
            if (arr[i] == 0) 
                count++; 
        } 
  
        // loop fills the arr with 0 until count 
        for (int i = 0; i < count; i++) 
            arr[i] = 0; 
  
        // loop fills remaining arr space with 1 
        for (int i = count; i < n; i++) 
            arr[i] = 1; 
    } 
      
    // function to print segregated array 
    static void print(int arr[], int n) 
    { 
        System.out.print("Array after segregation is "); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " ");     
    } 
      
    // driver function 
    public static void main(String[] args) 
    { 
        int arr[] = new int[]{ 0, 1, 0, 1, 1, 1 }; 
        int n = arr.length; 
  
        segregate0and1(arr, n); 
        print(arr, n); 
          
    } 
} 
  
// This code is contributed by Kamal Rawal 
```

## Python3

```py
# Python 3 code to Segregate 
# 0s and 1s in an array 
  
# Function to segregate 0s and 1s 
def segregate0and1(arr, n) : 
      
    # Counts the no of zeros in arr 
    count = 0 
  
    for i in range(0, n) : 
        if (arr[i] == 0) : 
            count = count + 1
  
    # Loop fills the arr with 0 until count 
    for i in range(0, count) : 
        arr[i] = 0
  
    # Loop fills remaining arr space with 1 
    for i in range(count, n) : 
        arr[i] = 1
          
  
# Function to print segregated array 
def print_arr(arr , n) : 
    print( "Array after segregation is ",end = "") 
  
    for i in range(0, n) : 
        print(arr[i] , end = " ") 
          
  
# Driver function 
arr = [ 0, 1, 0, 1, 1, 1 ] 
n = len(arr) 
      
segregate0and1(arr, n) 
print_arr(arr, n) 
  
  
          
# This code is contributed by Nikita Tiwari. 
```

## C#

```cs
// C# code to Segregate 0s and 1s in an array 
using System; 
  
class GFG { 
      
    // function to segregate 0s and 1s 
    static void segregate0and1(int []arr, int n) 
    {    
        // counts the no of zeros in arr 
        int count = 0;  
      
        for (int i = 0; i < n; i++) { 
            if (arr[i] == 0) 
                count++; 
        } 
  
        // loop fills the arr with 0 until count 
        for (int i = 0; i < count; i++) 
            arr[i] = 0; 
  
        // loop fills remaining arr space with 1 
        for (int i = count; i < n; i++) 
            arr[i] = 1; 
    } 
      
    // function to print segregated array 
    static void print(int []arr, int n) 
    { 
        Console.WriteLine("Array after segregation is "); 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " ");  
    } 
      
    // driver function 
    public static void Main() 
    { 
        int []arr = new int[]{ 0, 1, 0, 1, 1, 1 }; 
        int n = arr.Length; 
  
        segregate0and1(arr, n); 
        print(arr, n); 
          
    } 
} 
  
//This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// PHP code to Segregate   
// 0s and 1s in an array  
  
// Function to segregate  
// 0s and 1s 
function segregate0and1(&$arr, $n) 
{ 
    $count = 0; // Counts the no  
                // of zeros in arr 
  
    for ($i = 0; $i < $n; $i++)  
    { 
        if ($arr[$i] == 0) 
            $count++; 
    } 
  
    // Loop fills the arr 
    // with 0 until count 
    for ($i = 0; $i < $count; $i++) 
        $arr[$i] = 0; 
  
    // Loop fills remaining  
    // arr space with 1 
    for ($i = $count; $i < $n; $i++) 
        $arr[$i] = 1; 
} 
  
// Function to print 
// segregated array 
function toprint(&$arr , $n) 
{ 
    echo ("Array after segregation is "); 
  
    for ($i = 0; $i < $n; $i++) 
        echo ( $arr[$i] . " "); 
} 
  
// Driver Code 
$arr = array(0, 1, 0, 1, 1, 1 ); 
$n = sizeof($arr); 
  
segregate0and1($arr, $n); 
toprint($arr, $n); 
      
// This code is contributed 
// by Shivi_Aggarwal 
?> 
```

输出：

```
Array after segregation is 0 0 1 1 1 1 
```

方法 1 遍历两次数组。 方法 2 一次完成相同的操作。

方法 2（使用两个索引进行遍历）：

维护两个索引。 将第一个索引`left`初始化为 0，将第二个索引`right`初始化为`n-1`。

在`left < right`的同时执行以下操作：

+   当`left`索引为 0 时，请继续递增。
+   当`right`索引为 1 时，请继续递增。
+   如果`left < right`，则交换`arr[left]`和`arr[right]`。

实现方式：

## C++

```cpp
// C++ program to sort a binary array in one pass  
#include <bits/stdc++.h> 
using namespace std; 
  
/*Function to put all 0s on left and all 1s on right*/
void segregate0and1(int arr[], int size)  
{  
    /* Initialize left and right indexes */
    int left = 0, right = size-1;  
  
    while (left < right)  
    {  
        /* Increment left index while we see 0 at left */
        while (arr[left] == 0 && left < right)  
            left++;  
  
        /* Decrement right index while we see 1 at right */
        while (arr[right] == 1 && left < right)  
            right--;  
  
        /* If left is smaller than right then there is a 1 at left  
        and a 0 at right. Exchange arr[left] and arr[right]*/
        if (left < right)  
        {  
            arr[left] = 0;  
            arr[right] = 1;  
            left++;  
            right--;  
        }  
    }  
}  
  
/* Driver code */
int main()  
{  
    int arr[] = {0, 1, 0, 1, 1, 1};  
    int i, arr_size = sizeof(arr)/sizeof(arr[0]);  
  
    segregate0and1(arr, arr_size);  
  
    cout << "Array after segregation ";  
    for (i = 0; i < 6; i++)  
        cout << arr[i] << " ";  
    return 0;  
}  
  
// This is code is contributed by rathbhupendra 
```

## C

```c
// C program to sort a binary array in one pass 
#include<stdio.h> 
  
/*Function to put all 0s on left and all 1s on right*/
void segregate0and1(int arr[], int size) 
{ 
    /* Initialize left and right indexes */
    int left = 0, right = size-1; 
  
    while (left < right) 
    { 
        /* Increment left index while we see 0 at left */
        while (arr[left] == 0 && left < right) 
            left++; 
  
        /* Decrement right index while we see 1 at right */
        while (arr[right] == 1 && left < right) 
            right--; 
  
        /* If left is smaller than right then there is a 1 at left 
          and a 0 at right.  Exchange arr[left] and arr[right]*/
        if (left < right) 
        { 
            arr[left] = 0; 
            arr[right] = 1; 
            left++; 
            right--; 
        } 
    } 
} 
  
/* driver program to test */
int main() 
{ 
    int arr[] = {0, 1, 0, 1, 1, 1}; 
    int i, arr_size = sizeof(arr)/sizeof(arr[0]); 
  
    segregate0and1(arr, arr_size); 
  
    printf("Array after segregation "); 
    for (i = 0; i < 6; i++) 
        printf("%d ", arr[i]); 
  
    getchar(); 
    return 0; 
} 
```

## Java

```java
class Segregate  
{ 
    /*Function to put all 0s on left and all 1s on right*/
    void segregate0and1(int arr[], int size)  
    { 
        /* Initialize left and right indexes */
        int left = 0, right = size - 1; 
  
        while (left < right)  
        { 
            /* Increment left index while we see 0 at left */
            while (arr[left] == 0 && left < right) 
               left++; 
  
            /* Decrement right index while we see 1 at right */
            while (arr[right] == 1 && left < right) 
                right--; 
  
            /* If left is smaller than right then there is a 1 at left 
               and a 0 at right.  Exchange arr[left] and arr[right]*/
            if (left < right)  
            { 
                arr[left] = 0; 
                arr[right] = 1; 
                left++; 
                right--; 
            } 
        } 
    } 
      
    /* Driver Program to test above functions */
    public static void main(String[] args)  
    { 
        Segregate seg = new Segregate(); 
        int arr[] = new int[]{0, 1, 0, 1, 1, 1}; 
        int i, arr_size = arr.length; 
  
        seg.segregate0and1(arr, arr_size); 
  
        System.out.print("Array after segregation is "); 
        for (i = 0; i < 6; i++) 
            System.out.print(arr[i] + " "); 
    } 
} 
```

## Python

```py
# Python program to sort a binary array in one pass 
  
# Function to put all 0s on left and all 1s on right 
def segregate0and1(arr, size): 
    # Initialize left and right indexes 
    left, right = 0, size-1
      
    while left < right: 
        # Increment left index while we see 0 at left 
        while arr[left] == 0 and left < right: 
            left += 1
  
        # Decrement right index while we see 1 at right 
        while arr[right] == 1 and left < right: 
            right -= 1
  
        # If left is smaller than right then there is a 1 at left 
        # and a 0 at right. Exchange arr[left] and arr[right] 
        if left < right: 
            arr[left] = 0
            arr[right] = 1
            left += 1
            right -= 1
  
    return arr 
  
# driver program to test 
arr = [0, 1, 0, 1, 1, 1] 
arr_size = len(arr) 
print("Array after segregation") 
print(segregate0and1(arr, arr_size)) 
  
# This code is contributed by Pratik Chhajer 
```

## C#

```cs
// C# program to sort a binary array in one pass 
using System; 
  
class Segregate  
{ 
    /*Function to put all 0s on 
      left and all 1s on right*/
    void segregate0and1(int []arr, int size)  
    { 
        /* Initialize left and right indexes */
        int left = 0, right = size - 1; 
  
        while (left < right)  
        { 
            /* Increment left index while 
               we see 0 at left */
            while (arr[left] == 0 && left < right) 
            left++; 
  
            /* Decrement right index while  
               we see 1 at right */
            while (arr[right] == 1 && left < right) 
                right--; 
  
            /* If left is smaller than right then 
               there is a 1 at left and a 0 at right.  
               Exchange arr[left] and arr[right]*/
            if (left < right)  
            { 
                arr[left] = 0; 
                arr[right] = 1; 
                left++; 
                right--; 
            } 
        } 
    } 
      
    /* Driver Program to test above functions */
    public static void Main()  
    { 
        Segregate seg = new Segregate(); 
        int []arr = new int[]{0, 1, 0, 1, 1, 1}; 
        int i, arr_size = arr.Length; 
  
        seg.segregate0and1(arr, arr_size); 
  
        Console.WriteLine("Array after segregation is "); 
        for (i = 0; i < 6; i++) 
            Console.Write(arr[i] + " "); 
    } 
} 
  
//This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// PHP program to sort a 
// binary array in one pass 
  
// Function to put all 0s on 
// left and all 1s on right 
function segregate0and1(&$arr, $size) 
{ 
    // Initialize left and 
    // right indexes  
    $left = 0; 
    $right = $size - 1; 
  
    while ($left < $right) 
    { 
        // Increment left index  
        // while we see 0 at left  
        while ($arr[$left] == 0 &&  
               $left < $right) 
            $left++; 
  
        // Decrement right index  
        // while we see 1 at right  
        while ($arr[$right] == 1 &&  
               $left < $right) 
            $right--; 
  
        // If left is smaller than right  
        // then there is a 1 at left 
        // and a 0 at right. Exchange  
        // arr[left] and arr[right] 
        if ($left < $right) 
        { 
            $arr[$left] = 0; 
            $arr[$right] = 1; 
            $left++; 

$right--; 
        } 
    } 
} 
  
// Driver code 
$arr = array(0, 1, 0, 1, 1, 1); 
$arr_size = sizeof($arr); 
  
segregate0and1($arr, $arr_size); 
  
printf("Array after segregation is "); 
for ($i = 0; $i < 6; $i++) 
    echo ($arr[$i]. " "); 
  
// This code is contributed  
// by Shivi_Aggarwal 
?> 
```

输出：

```
Array after segregation is 0 0 1 1 1 1 
```

事件复杂度：`O(n)`。

另一种方法：

1.  从开头（`index = 0`）开始取指针`type0`（对于元素 0），从结尾开始取指针`type1`（对于元素 1）（`index = array.length - 1`）。
初始化`type0 = 0`和`type1 = array.length - 1`。
2.  打算将 1 放在数组的右侧。 一旦完成，则 0 肯定会朝向数组的左侧。

## C++

```cpp
// C++ program to sort a  
// binary array in one pass 
#include <bits/stdc++.h> 
using namespace std; 
  
/*Function to put all 0s on  
left and all 1s on right*/
void segregate0and1(int arr[],  
                    int size) 
{ 
    int type0 = 0; 
    int type1 = size - 1; 
      
    while(type0 < type1) 
    { 
        if(arr[type0] == 1) 
        { 
            swap(arr[type0],  
                 arr[type1]); 
            type1--; 
        } 
        else
        type0++; 
    } 
} 
  
// Driver Code 
int main() 
{ 
    int arr[] = {0, 1, 0, 1, 1, 1}; 
    int i, arr_size = sizeof(arr) /  
                      sizeof(arr[0]); 
  
    segregate0and1(arr, arr_size); 
  
    cout << "Array after segregation is "; 
    for (i = 0; i < arr_size; i++) 
        cout << arr[i] << " "; 
  
    return 0; 
} 
```

## Java

```java
// Java code to segregate 0 and 1 
import java.util.*; 
  
class GFG{ 
/** 
Method for segregation 0 and 1 given input array 
*/
static void segregate0and1(int arr[]) { 
        int type0 = 0; 
        int type1 = arr.length - 1; 
          
        while (type0 < type1) { 
            if (arr[type0] == 1) { 
                // swap 
                arr[type1] = arr[type1]+ arr[type0]; 
                arr[type0] = arr[type1]-arr[type0]; 
                arr[type1] = arr[type1]-arr[type0]; 
                type1--; 
            } else { 
                type0++; 
            } 
        } 
  
    } 
      
// Driver program 
public static void main(String[] args) {      
          
        int[] array = {0, 1, 0, 1, 1, 1}; 
          
        segregate0and1(array); 
          
        for(int a : array){ 
            System.out.print(a+" "); 
        } 
    } 
} 
```

## Python 3

```py
# Python program to sort a  
# binary array in one pass 
  
# Function to put all 0s on  
# left and all 1s on right 
def segregate0and1(arr, size): 
  
    type0 = 0
    type1 = size - 1
      
    while(type0 < type1): 
        if(arr[type0] == 1): 
            (arr[type0],  
             arr[type1]) = (arr[type1], 
                            arr[type0]) 
            type1 -= 1
        else: 
            type0 += 1
      
# Driver Code 
arr = [0, 1, 0, 1, 1, 1] 
arr_size = len(arr) 
segregate0and1(arr, arr_size) 
print("Array after segregation is",  
                         end = " ") 
for i in range(0, arr_size): 
        print(arr[i], end = " ") 
  
# This code is contributed 
# by Shivi_Aggarwal
```

## C#

```cs
// C# code to segregate 0 and 1  
using System; 
  
class GFG { 
  
// Method for segregation 0  
// and 1 given input array  
static void segregate0and1(int[] arr) 
{ 
    int type0 = 0; 
    int type1 = arr.Length - 1; 
  
    while (type0 < type1) 
    { 
        if (arr[type0] == 1) 
        { 
            // swap  
            arr[type1] = arr[type1] + arr[type0]; 
            arr[type0] = arr[type1] - arr[type0]; 
            arr[type1] = arr[type1] - arr[type0]; 
            type1--; 
        } 
          
        else
        { 
            type0++; 
        } 
    } 
  
} 
  
// Driver Code  
public static void Main(string[] args) 
{ 
  
    int[] array = new int[] {0, 1, 0, 1, 1, 1}; 
    segregate0and1(array); 
  
    Console.Write("Array after segregation is "); 
    foreach (int a in array) 
    { 
        Console.Write(a + " "); 
    } 
} 
} 
  
// This code is contributed by Shrikant13 
```

## PHP

```php
<?php 
// PHP program to sort a  
// binary array in one pass 
  
// Function to put all 0s on  
// left and all 1s on right 
function segregate0and1(&$arr , $size) 
{ 
    $type0 = 0; 
    $type1 = $size - 1; 
      
    while($type0 < $type1) 
    { 
        if($arr[$type0] == 1) 
        { 
            $temp = $arr[$type0]; 
            $arr[$type0] = $arr[$type1]; 
            $arr[$type1] = $temp; 
            $type1--; 
        } 
        else
        $type0++; 
    } 
} 
  
// Driver Code 
$arr = array(0, 1, 0, 1, 1, 1); 
$arr_size = sizeof($arr); 
  
segregate0and1($arr, $arr_size); 
  
echo ("Array after segregation is "); 
for ($i = 0; $i < $arr_size; $i++) 
    echo ($arr[$i] . " "); 
  
// This code is contributed  
// by Shivi_Aggarwal 
?> 
```

输出：

```
Array after segregation is 0 0 1 1 1 1 
```

时间复杂度：`O(n)`。