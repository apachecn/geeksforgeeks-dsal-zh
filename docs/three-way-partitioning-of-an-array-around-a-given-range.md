# 数组在给定范围内的三路分区

> 原文： [https://www.geeksforgeeks.org/three-way-partitioning-of-an-array-around-a-given-range/](https://www.geeksforgeeks.org/three-way-partitioning-of-an-array-around-a-given-range/)

给定一个数组和一个范围`[lowVal, highVal]`，围绕该范围划分数组，以便将数组分为三部分。

1.  所有小于`lowVal`的元素都在前面。

2.  接下来是`lowVal`至`highVVal`范围内的所有元素。

3.  最后是所有大于`highVVal`的元素。

三组中的各个元素可以按任何顺序出现。

**示例**：

```
Input: arr[] = {1, 14, 5, 20, 4, 2, 54, 20, 87, 98, 3, 1, 32}  
        lowVal = 14, highVal = 20
Output: arr[] = {1, 5, 4, 2, 1, 3, 14, 20, 20, 98, 87, 32, 54}

Input: arr[] = {1, 14, 5, 20, 4, 2, 54, 20, 87, 98, 3, 1, 32}  
       lowVal = 20, highVal = 20       
Output: arr[] = {1, 14, 5, 4, 2, 1, 3, 20, 20, 98, 87, 32, 54} 

```

![](img/880f272932267da219b4546df1821d9e.png)



**简单解决方案**是对数组进行排序。 此解决方案做了很多额外的重新安排，并且需要`O(n Log n)`时间。

**有效解决方案**基于[荷兰国旗的快速排序](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)。 我们从左遍历给定的数组元素。 我们跟踪两个指针，第一个（在下面的代码中称为`start`）从头开始存储较小元素（小于范围）的下一个位置； 第二个（在下面的代码中称为`end`）存储从`end`开始更大元素的下一个位置。

## C/C++ 

```cpp

// C++ program to implement three way partitioning 
// around a given range. 
#include<iostream> 
using namespace std; 

// Partitions arr[0..n-1] around [lowVal..highVal] 
void threeWayPartition(int arr[], int n, 
                int lowVal, int highVal) 
{ 
    // Initialize ext available positions for 
    // smaller (than range) and greater lements 
    int start = 0, end = n-1; 

    // Traverse elements from left 
    for (int i=0; i<=end;) 
    { 
        // If current element is smaller than 
        // range, put it on next available smaller 
        // position. 
        if (arr[i] < lowVal) 
            swap(arr[i++], arr[start++]); 

        // If current element is greater than 
        // range, put it on next available greater 
        // position. 
        else if (arr[i] > highVal) 
            swap(arr[i], arr[end--]); 

        else
            i++; 
    } 
} 

// Driver code 
int main() 
{ 
    int arr[] = {1, 14, 5, 20, 4, 2, 54, 20, 87, 
                98, 3, 1, 32}; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    threeWayPartition(arr, n, 10, 20); 

    cout << "Modified array \n"; 
    for (int i=0; i<n; i++) 
        cout << arr[i] << " "; 
} 

```

## Java

```java
import java.io.*; 
  
class GFG  
{ 
      
    // Partitions arr[0..n-1] around [lowVal..highVal] 
    public static void threeWayPartition(int[] arr, int lowVal, int highVal) 
    { 
          
        int  n = arr.length; 
          
        // Initialize ext available positions for 
        // smaller (than range) and greater lements 
        int start = 0, end = n-1; 
          
         // Traverse elements from left 
        for(int i = 0; i <= end;) 
        { 
              
            // If current element is smaller than 
            // range, put it on next available smaller 
            // position. 
              
            if(arr[i] < lowVal) 
            { 
                  
                int temp = arr[start]; 
                arr[start] = arr[i]; 
                arr[i] = temp; 
                start++; 
                i++; 
                  
            } 
              
            // If current element is greater than 
            // range, put it on next available greater 
            // position. 
            else if(arr[i] > highVal) 
            { 
                  
                int temp = arr[end]; 
                arr[end] = arr[i]; 
                arr[i] = temp; 
                end--; 
                   
            } 
              
            else
               i++; 
        } 
          
    } 
      
    public static void main (String[] args)  
    { 
      
      
        int arr[] = {1, 14, 5, 20, 4, 2, 54, 20, 87, 98, 3, 1, 32}; 
          
        threeWayPartition(arr, 10, 20); 
   
        System.out.println("Modified array "); 
        for (int i=0; i < arr.length; i++) 
        { 
            System.out.print(arr[i] + " "); 
      
        }     
    } 
} 
  
//This code is contributed by Dheerendra Singh 
```

## Python3

```py
# Python3 program to implement three way  
# partitioning around a given range. 
  
# Partitions arr[0..n-1] around [lowVal..highVal] 
def threeWayPartition(arr, n, lowVal, highVal): 
  
    # Initialize ext available positions for 
    # smaller (than range) and greater lements 
    start = 0
    end = n - 1
    i = 0
  
    # Traverse elements from left 
    while i <= end: 
  
        # If current element is smaller than 
        # range, put it on next available smaller 
        # position. 
        if arr[i] < lowVal: 
            temp = arr[i] 
            arr[i] = arr[start] 
            arr[start] = temp 
            i += 1
            start += 1
  
        # If current element is greater than 
        # range, put it on next available greater 
        # position. 
        elif arr[i] > highVal: 
            temp = arr[i] 
            arr[i] = arr[end] 
            arr[end] = temp 
            end -= 1
  
        else: 
            i += 1
  
# Driver code 
if __name__ == "__main__": 
    arr = [1, 14, 5, 20, 4, 2, 54,  
           20, 87, 98, 3, 1, 32] 
    n = len(arr) 
  
    threeWayPartition(arr, n, 10, 20) 
  
    print("Modified array") 
    for i in range(n): 
        print(arr[i], end = " ") 
  
# This code is contributed by 
# sanjeev2552 
```

## C#

```cs
// C# program to implement three way  
// partitioning around a given range. 
using System; 
  
class GFG { 
  
    // Partitions arr[0..n-1]  
    // around [lowVal..highVal] 
    public static void threeWayPartition(int[] arr, 
                           int lowVal, int highVal) 
    { 
        int n = arr.Length; 
  
        // Initialize ext available positions for 
        // smaller (than range) and greater lements 
        int start = 0, end = n - 1; 
  
        // Traverse elements from left 
        for (int i = 0; i <= end;) { 
  
            // If current element is smaller than 
            // range, put it on next available smaller 
            // position. 
  
            if (arr[i] < lowVal) { 
  
                int temp = arr[start]; 
                arr[start] = arr[i]; 
                arr[i] = temp; 
                start++; 
                i++; 
            } 
  
            // If current element is greater than 
            // range, put it on next available greater 
            // position. 
            else if (arr[i] > highVal) { 
  
                int temp = arr[end]; 
                arr[end] = arr[i]; 
                arr[i] = temp; 
                end--; 
            } 
  
            else
                i++; 
        } 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 14, 5, 20, 4, 2, 54,  
                      20, 87, 98, 3, 1, 32 }; 
  
        threeWayPartition(arr, 10, 20); 
  
        Console.WriteLine("Modified array "); 
        for (int i = 0; i < arr.Length; i++) { 
            Console.Write(arr[i] + " "); 
        } 
    } 
} 
  
// This article is contributed by vt_m. 
```

输出：

```
Modified array 
1 5 4 2 1 3 14 20 20 98 87 32 54 
```

时间复杂度：`O(n)`。

辅助空间：`O(1)`。