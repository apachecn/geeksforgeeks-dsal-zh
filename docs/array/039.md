# 根据给定的索引重新排序数组

> 原文： [https://www.geeksforgeeks.org/reorder-a-array-according-to-given-indexes/](https://www.geeksforgeeks.org/reorder-a-array-according-to-given-indexes/)

给定两个大小相同的整数数组`arr[]`和`index[]`，请根据给定的索引数组对`arr[]`中的元素进行重新排序。 不允许指定数组`arr`的长度。

**示例**：

```
Input:  arr[]   = [10, 11, 12];
        index[] = [1, 0, 2];
Output: arr[]   = [11, 10, 12]
        index[] = [0,  1,  2] 

Input:  arr[]   = [50, 40, 70, 60, 90]
        index[] = [3,  0,  4,  1,  2]
Output: arr[]   = [40, 60, 90, 50, 70]
        index[] = [0,  1,  2,  3,   4] 

```

预期时间复杂度`O(n)`和辅助空间`O(1)`。

**简单解决方案**是使用与给定数组大小相同的辅助数组`temp[]`。 遍历给定的数组，并使用`index[]`将所有元素放在`temp[]`中的正确位置。 最后，将`temp[]`复制到`arr[]`并将`index[i]`的所有值设置为`i`。

## C++ 

```cpp

// C++ program to sort an array according to given 
// indexes 
#include<iostream> 

using namespace std; 

// Function to reorder elements of arr[] according 
// to index[] 
void reorder(int arr[], int index[], int n) 
{ 
    int temp[n]; 

    // arr[i] should be present at index[i] index 
    for (int i=0; i<n; i++) 
        temp[index[i]] = arr[i]; 

    // Copy temp[] to arr[] 
    for (int i=0; i<n; i++) 
    {  
       arr[i]   = temp[i]; 
       index[i] = i; 
    } 
} 

// Driver program 
int main() 
{ 
    int arr[] = {50, 40, 70, 60, 90}; 
    int index[] = {3,  0,  4,  1,  2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    reorder(arr, index, n); 

    cout << "Reordered array is: \n"; 
    for (int i=0; i<n; i++) 
        cout << arr[i] << " "; 

    cout << "\nModified Index array is: \n"; 
    for (int i=0; i<n; i++) 
        cout << index[i] << " "; 
    return 0; 
} 

```

## Java

```java
//Java to find positions of zeroes flipping which 
// produces maximum number of consecutive 1's 
  
import java.util.Arrays; 
  
class Test 
{ 
    static int arr[] = new int[]{50, 40, 70, 60, 90}; 
    static int index[] = new int[]{3,  0,  4,  1,  2}; 
      
    // Method to reorder elements of arr[] according 
    // to index[] 
    static void reorder() 
    { 
        int temp[] = new int[arr.length]; 
       
        // arr[i] should be present at index[i] index 
        for (int i=0; i<arr.length; i++) 
            temp[index[i]] = arr[i]; 
       
        // Copy temp[] to arr[] 
        for (int i=0; i<arr.length; i++) 
        {  
           arr[i]   = temp[i]; 
           index[i] = i; 
        } 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
          
        reorder(); 
          
        System.out.println("Reordered array is: "); 
        System.out.println(Arrays.toString(arr)); 
        System.out.println("Modified Index array is:"); 
        System.out.println(Arrays.toString(index)); 
          
    } 
} 
```

## Python3

```py
# Python 3 program to sort 
# an array according to given 
# indexes 
  
# Function to reorder 
# elements of arr[] according 
# to index[] 
def reorder(arr,index, n): 
  
    temp = [0] * n; 
  
    # arr[i] should be 
        # present at index[i] index 
    for i in range(0,n): 
        temp[index[i]] = arr[i] 
  
    # Copy temp[] to arr[] 
    for i in range(0,n): 
        arr[i] = temp[i] 
        index[i] = i 
      
# Driver program 
arr = [50, 40, 70, 60, 90] 
index = [3, 0, 4, 1, 2] 
n = len(arr) 
  
reorder(arr, index, n) 
  
print("Reordered array is:") 
for i in range(0,n): 
    print(arr[i],end = " ") 
  
print("\nModified Index array is:") 
for i in range(0,n): 
    print(index[i],end = " ") 
  
# This code is contributed by 
# Smitha Dinesh Semwal 
```

## C#

```cs
// C# to find positions of zeroes flipping which 
// produces maximum number of consecutive 1's 
using System;  
   
public class Test{ 
      
    static int []arr = new int[]{50, 40, 70, 60, 90}; 
    static int []index = new int[]{3,  0,  4,  1,  2}; 
       
    // Method to reorder elements of arr[] according 
    // to index[] 
    static void reorder() 
    { 
        int []temp = new int[arr.Length]; 
        
        // arr[i] should be present at index[i] index 
        for (int i=0; i<arr.Length; i++) 
            temp[index[i]] = arr[i]; 
        
        // Copy temp[] to arr[] 
        for (int i=0; i<arr.Length; i++) 
        {  
           arr[i]   = temp[i]; 
           index[i] = i; 
        } 
    } 
       
    // Driver method to test the above function 
    public static void Main()  
    { 
           
        reorder(); 
           
        Console.WriteLine("Reordered array is: "); 
        Console.WriteLine(string.Join(",", arr)); 
        Console.WriteLine("Modified Index array is:"); 
        Console.WriteLine(string.Join(",", index)); 
           
    } 
} 
/*This code is contributed by 29AjayKumar*/
```

## PHP

```php
<?php 
// PHP program to sort an array  
// according to given indexes 
  
// Function to reorder elements  
// of arr[] according to index[] 
function reorder($arr, $index, $n) 
{ 
    // $temp[$n]; 
  
    // arr[i] should be present 
    // at index[i] index 
    for ($i = 0; $i < $n; $i++) 
    { 
        $temp[$index[$i]] = $arr[$i]; 
    } 
      
      
    // Copy temp[] to arr[] 
    for ($i = 0; $i < $n; $i++) 
    {  
        $arr[$i] = $temp[$i]; 
        $index[$i] = $i; 
    } 
      
    echo "Reordered array is: \n"; 
for ($i = 0; $i < $n; $i++) 
{ 
    echo $arr[$i] . " "; 
} 
  
echo "\nModified Index array is: \n"; 
for ($i = 0; $i < $n; $i++) 
{ 
    echo $index[$i] . " "; 
} 
} 
  
// Driver Code 
$arr = array(50, 40, 70, 60, 90); 
$index = array(3, 0, 4, 1, 2); 
$n = sizeof($arr); 
  
reorder($arr, $index, $n); 
  
// This code is contributed 
// by Abby_akku 
?> 
```

输出：

```
Reordered array is: 
40 60 90 50 70 
Modified Index array is: 
0 1 2 3 4 
```

感谢 gccode 建议上述解决方案。

我们可以在没有辅助数组的情况下解决它。 下面是算法。

+   对每个元素`arr [i]`执行以下操作：
+   当`index [i]`不等于`i`时：
    1.  存储应放置`arr[i]`的目标（或正确）位置的数组和索引值。 `arr[i]`的正确位置是`index[i]`。
    2.  将`arr[i]`放置在正确的位置。 同时更新正确位置的索引值。
    3.  在`while`循环继续迭代`i`的过程中，复制正确位置的旧值（存储在步骤（1）中）到`arr[i]`和`index[i]`。


下面是上述算法的实现。

## C++

```cpp
// A O(n) time and O(1) extra space C++ program to 
// sort an array according to given indexes 
#include<iostream> 
  
using namespace std; 
  
// Function to reorder elements of arr[] according 
// to index[] 
void reorder(int arr[], int index[], int n) 
{ 
    // Fix all elements one by one 
    for (int i=0; i<n; i++) 
    { 
        // While index[i] and arr[i] are not fixed 
        while (index[i] != i) 
        { 
            // Store values of the target (or correct)  
            // position before placing arr[i] there 
            int  oldTargetI  = index[index[i]]; 
            char oldTargetE  = arr[index[i]]; 
  
            // Place arr[i] at its target (or correct) 
            // position. Also copy corrected index for 
            // new position 
            arr[index[i]] = arr[i]; 
            index[index[i]] = index[i]; 
  
            // Copy old target values to arr[i] and 
            // index[i] 
            index[i] = oldTargetI; 
            arr[i]   = oldTargetE; 
        } 
    } 
} 
  
// Driver program 
int main() 
{ 
    int arr[] = {50, 40, 70, 60, 90}; 
    int index[] = {3,  0,  4,  1,  2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
  
    reorder(arr, index, n); 
  
    cout << "Reordered array is: \n"; 
    for (int i=0; i<n; i++) 
        cout << arr[i] << " "; 
  
    cout << "\nModified Index array is: \n"; 
    for (int i=0; i<n; i++) 
        cout << index[i] << " "; 
    return 0; 
} 
```

## Java

```java
//A O(n) time and O(1) extra space Java program to 
//sort an array according to given indexes 
  
import java.util.Arrays; 
  
class Test 
{ 
    static int arr[] = new int[]{50, 40, 70, 60, 90}; 
    static int index[] = new int[]{3,  0,  4,  1,  2}; 
      
    // Method to reorder elements of arr[] according 
    // to index[] 
    static void reorder() 
    { 
        // Fix all elements one by one 
        for (int i=0; i<arr.length; i++) 
        { 
            // While index[i] and arr[i] are not fixed 
            while (index[i] != i) 
            { 
                // Store values of the target (or correct)  
                // position before placing arr[i] there 
                int  oldTargetI  = index[index[i]]; 
                char oldTargetE  = (char)arr[index[i]]; 
       
                // Place arr[i] at its target (or correct) 
                // position. Also copy corrected index for 
                // new position 
                arr[index[i]] = arr[i]; 
                index[index[i]] = index[i]; 
       
                // Copy old target values to arr[i] and 
                // index[i] 
                index[i] = oldTargetI; 
                arr[i]   = oldTargetE; 
            } 
        } 
    } 
      
    // Driver method to test the above function 
    public static void main(String[] args)  
    { 
          
        reorder(); 
          
        System.out.println("Reordered array is: "); 
        System.out.println(Arrays.toString(arr)); 
        System.out.println("Modified Index array is:"); 
        System.out.println(Arrays.toString(index)); 
          
    } 
} 
```

## Python3

```py
# A O(n) time and O(1) extra space Python3 program to 
# sort an array according to given indexes 
  
# Function to reorder elements of arr[] according 
# to index[] 
def reorder(arr, index, n): 
  
    # Fix all elements one by one 
    for i in range(0,n): 
  
           #  While index[i] and arr[i] are not fixed 
           while (index[i] != i): 
          
               # Store values of the target (or correct)  
               # position before placing arr[i] there 
               oldTargetI = index[index[i]] 
               oldTargetE = arr[index[i]] 
  
               # Place arr[i] at its target (or correct) 
               # position. Also copy corrected index for 
               # new position 
               arr[index[i]] = arr[i] 
               index[index[i]] = index[i] 
  
               # Copy old target values to arr[i] and 
               # index[i] 
               index[i] = oldTargetI 
               arr[i] = oldTargetE 
  
  
# Driver program 
arr = [50, 40, 70, 60, 90] 
index= [3, 0, 4, 1, 2] 
n = len(arr) 
  
reorder(arr, index, n) 
  
print("Reordered array is:") 
for  i in range(0, n): 
    print(arr[i],end=" ") 
  
print("\nModified Index array is:") 
for i in range(0, n): 
    print(index[i] ,end=" ") 
  
# This code is contributed by 
# Smitha Dinesh Semwal 
```

## C#

```cs
//A O(n) time and O(1) extra space C# program to 
//sort an array according to given indexes 
using System;  
  
public class Test 
{ 
    static int []arr = new int[]{50, 40, 70, 60, 90}; 
    static int []index = new int[]{3,  0,  4,  1,  2}; 
       
    // Method to reorder elements of arr[] according 
    // to index[] 
    static void reorder() 
    { 
        // Fix all elements one by one 
        for (int i=0; i<arr.Length; i++) 
        { 
            // While index[i] and arr[i] are not fixed 
            while (index[i] != i) 
            { 
                // Store values of the target (or correct)  
                // position before placing arr[i] there 
                int  oldTargetI  = index[index[i]]; 
                char oldTargetE  = (char)arr[index[i]]; 
        
                // Place arr[i] at its target (or correct) 
                // position. Also copy corrected index for 
                // new position 
                arr[index[i]] = arr[i]; 
                index[index[i]] = index[i]; 
        
                // Copy old target values to arr[i] and 
                // index[i] 
                index[i] = oldTargetI; 
                arr[i]   = oldTargetE; 
            } 
        } 
    } 
       
    // Driver method to test the above function 
    public static void Main()  
    { 
           
        reorder(); 
           
        Console.WriteLine("Reordered array is: "); 
        Console.WriteLine(String.Join(" ",arr)); 
        Console.WriteLine("Modified Index array is:"); 
        Console.WriteLine(String.Join(" ",index)); 
           
    } 
} 
  
// This code is contributed by PrinciRaj1992 
```

输出：

```
Reordered array is: 
40 60 90 50 70 
Modified Index array is: 
0 1 2 3 4 
```

感谢 shyamala_lokre 建议上述解决方案。

不使用辅助数组的另一种方法是对数组进行排序。

对索引数组进行排序并自定义排序，以在每次交换`index[]`数据时交换`arr[]`数据。

```cpp
ter_none
edit
play_arrow

brightness_4
//C++ code to reorder an array according to given indices 
#include <bits/stdc++.h> 
  
using namespace std; 
  
int heapSize; 
  
void swap ( int &a, int &b ) { 
    int temp = a; 
    a = b; 
    b = temp; 
} 
  
void heapify( int arr[], int index[], int i )  
{ 
    int largest = i; 
    // left child in 0 based indexing 
    int left = 2 * i + 1;  
    // right child in 1 based indexing 
    int right = 2 * i + 2;  
    // find largest index from root, left and right child 
    if( left < heapSize && index[left] > index[largest] ) 
    { 
        largest = left; 
    } 
    if( right < heapSize && index[right] > index[largest] )  
    { 
        largest = right; 
    } 
      
    if ( largest != i ) { 
        //swap arr whenever index is swapped 
        swap(arr[largest], arr[i]);  
        swap(index[largest], index[i]); 
        heapify(arr, index, largest); 
    } 
} 
  
void heapSort( int arr[], int index[], int n ) { 
// Build heap 
    for ( int i = ( n - 1 ) / 2 ; i >= 0 ; i-- ) { 
        heapify(arr, index, i); 
    } 
    // Swap the largest element of index(first element) 
    // with the last element 
    for ( int i = n - 1 ; i > 0 ; i-- ) { 
        swap(index[0], index[i]); 
        //swap arr whenever index is swapped 
        swap(arr[0], arr[i]);  
        heapSize--; 
        heapify(arr, index, 0); 
    } 
} 
  
// Driver Code 
int main() { 
    int arr[] = {50, 40, 70, 60, 90}; 
    int index[] = {3,  0,  4,  1,  2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    heapSize = n; 
    heapSort(arr, index, n); 
  
    cout << "Reordered array is: \n"; 
    for ( int i = 0 ; i < n ; i++ ) 
        cout << arr[i] << " "; 
          
        cout << "\nModified Index array is: \n"; 
    for (int i=0; i<n; i++) 
        cout << index[i] << " "; 
  
    return 0; 
} 
```

输出：

```
Reordered array is: 
40 60 90 50 70 
Modified Index array is: 
0 1 2 3 4 
```

时间复杂度：`O(nlogn)`。
