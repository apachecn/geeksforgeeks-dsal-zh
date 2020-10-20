# 整个数组中最小的较大元素

> 原文： [https://www.geeksforgeeks.org/smallest-greater-elements-in-whole-array/](https://www.geeksforgeeks.org/smallest-greater-elements-in-whole-array/)

给定一个长度为`n`的数组，我们需要为给定数组中的每个元素计算下一个更大的元素。 如果下一个更大的元素在给定数组中不可用，那么我们需要在该索引位置填充`_`。

**示例**：

```
Input :  6 3 9 8 10 2 1 15 7 
Output : 7 6 10 9 15 3 2 _ 8
Here every element of array has next greater 
element but at index 7,
15 is the greatest element of given array
and no other element is greater from 15 
so at the index of 15 we fill with '_' .

Input  : 13 6 7 12
Output : _ 7 12 13
Here, at index 0, 13 is the greatest 
value in given array and no other 
array element is greater from 13 so
at index 0 we fill '_'.

```



**简单解决方案**是使用两个嵌套的循环。 外循环一个接一个地选择所有元素，内循环通过从头到尾线性搜索找到下一个更大的元素。

## C++ 

```cpp

// Simple CPP program to find smallest 
// greater element in whole array for  
// every element. 
#include <bits/stdc++.h> 
using namespace std; 

void smallestGreater(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) { 

        // Find the closest greater element  
        // for arr[j] in the entire array. 
        int diff = INT_MAX, closest = -1; 
        for (int j = 0; j < n; j++) { 
            if ( arr[i] < arr[j] &&  
                 arr[j] - arr[i] < diff) 
            { 
                diff = arr[j] - arr[i]; 
                closest = j;             
            } 
        } 

        // Check if arr[i] is largest 
        (closest == -1)?  cout << "_ "  :  
              cout << arr[closest] << " "; 
     } 
} 

// Driver code 
int main() 
{ 
    int ar[] = { 6, 3, 9, 8, 10, 2, 1, 15, 7 }; 
    int n = sizeof(ar) / sizeof(ar[0]); 
    smallestGreater(ar, n); 
    return 0; 
} 

```

## Python3

```
# Simple Python program to find smallest 
# greater element in whole array for  
# every element. 
def smallestGreater(arr, n) : 
    for i in range(0, n) : 
  
        # Find the closest greater element  
        # for arr[j] in the entire array. 
        diff = 1000;  
        closest = -1; 
        for j in range(0, n) : 
            if ( arr[i] < arr[j] and 
                  arr[j] - arr[i] < diff) : 
                diff = arr[j] - arr[i]; 
                closest = j;      
          
        # Check if arr[i] is largest 
        if (closest == -1) : 
            print ("_ ", end = ""); 
        else : 
            print ("{} ".format(arr[closest]), 
                                    end = ""); 
  
# Driver code 
ar = [6, 3, 9, 8, 10, 2, 1, 15, 7]; 
n = len(ar) ; 
smallestGreater(ar, n); 
  
# This code is contributed by Manish Shaw 
# (manishshaw1)
```

## C#

```
// Simple C# program to find 
// smallest greater element in  
// whole array for every element. 
using System; 
  
class GFG  
{ 
static void smallestGreater(int []arr,  
                            int n) 
{ 
    for (int i = 0; i < n; i++)  
    { 
  
        // Find the closest greater 
        // element for arr[j] in  
        // the entire array. 
        int diff = int.MaxValue; 
        int closest = -1; 
        for (int j = 0; j < n; j++)  
        { 
            if (arr[i] < arr[j] &&  
                arr[j] - arr[i] < diff) 
            { 
                diff = arr[j] - arr[i]; 
                closest = j;          
            } 
        } 
          
        // Check if arr[i] is largest 
        if(closest == -1) 
        Console.Write( "_ " ); 
        else
        Console.Write(arr[closest] + " "); 
    } 
} 
  
// Driver code 
public static void Main()  
{ 
    int []ar = {6, 3, 9, 8, 10,  
                2, 1, 15, 7}; 
    int n = ar.Length; 
    smallestGreater(ar, n); 
} 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```
<?php 
// Simple PHP program to find smallest 
// greater element in whole array for  
// every element. 
  
function smallestGreater($arr, $n) 
{ 
    for ( $i = 0; $i < $n; $i++) { 
  
        // Find the closest greater element  
        // for arr[j] in the entire array. 
        $diff = PHP_INT_MAX; $closest = -1; 
        for ( $j = 0; $j < $n; $j++) { 
            if ( $arr[$i] < $arr[$j] &&  
                $arr[$j] - $arr[$i] < $diff) 
            { 
                $diff = $arr[$j] - $arr[$i]; 
                $closest = $j;      
            } 
        } 
          
        // Check if arr[i] is largest 
        if ($closest == -1) 
        echo "_ " ; 
        else
            echo $arr[$closest] , " "; 
    } 
} 
  
    // Driver code 
    $ar = array (6, 3, 9, 8, 10, 2, 1, 15, 7); 
    $n = sizeof($ar) ; 
    smallestGreater($ar, $n); 
  
// This code is contributed by ajit 
?>
```

输出：

```
7 6 10 9 15 3 2 _ 8
```

时间复杂度：`O(n * n)`。

辅助空间：`O(1)`。