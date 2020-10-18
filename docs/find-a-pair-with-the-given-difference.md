# 找到具有给定差异的一对

> 原文： [https://www.geeksforgeeks.org/find-a-pair-with-the-given-difference/](https://www.geeksforgeeks.org/find-a-pair-with-the-given-difference/)

给定一个未排序的数组和一个数字`n`，请查找数组中是否存在一对差为`n`的元素。

**示例**：

```
Input: arr[] = {5, 20, 3, 2, 50, 80}, n = 78
Output: Pair Found: (2, 80)

Input: arr[] = {90, 70, 20, 80, 50}, n = 45
Output: No Such Pair

```



最简单的方法是运行两个循环，外循环选择第一个元素（较小的元素），内循环查找外循环加上`n`拾取的元素。 该方法的时间复杂度为`O(n ^ 2)`。

我们可以使用排序和二分搜索将时间复杂度提高到`O(nLogn)`。 第一步是按升序对数组进行排序。 数组排序后，从左到右遍历该数组，对于每个元素`arr[i]`，在`arr[i + 1..n-1]`中对`arr[i] + n`进行二分搜索。 如果找到该元素，则返回该对。

第一步和第二步都采用`O(nLogn)`。 因此，总体复杂度为`O(nLogn)`。

上述算法的第二步可以提高到`O(n)`。 第一步保持不变。 第二步的想法是采用两个索引变量`i`和`j`，分别将它们初始化为 0 和 1。 现在运行一个线性循环。 如果`arr[j] – arr[i]`小于`n`，我们需要寻找更大的`arr[j]`，因此增加`j`。 如果`arr[j] – arr[i]`大于`n`，则需要寻找更大的`arr[i]`，因此增加`i`。 感谢 Aashish Barnwal 提出了这种方法。

以下代码仅用于算法的第二步，它假定数组已经排序。

## C++ 

```cpp

// C++ program to find a pair with the given difference  
#include <bits/stdc++.h> 
using namespace std; 

// The function assumes that the array is sorted  
bool findPair(int arr[], int size, int n)  
{  
    // Initialize positions of two elements  
    int i = 0;  
    int j = 1;  

    // Search for a pair  
    while (i < size && j < size)  
    {  
        if (i != j && arr[j] - arr[i] == n)  
        {  
            cout << "Pair Found: (" << arr[i] << 
                        ", " << arr[j] << ")";  
            return true;  
        }  
        else if (arr[j]-arr[i] < n)  
            j++;  
        else
            i++;  
    }  

    cout << "No such pair";  
    return false;  
}  

// Driver program to test above function  
int main()  
{  
    int arr[] = {1, 8, 30, 40, 100};  
    int size = sizeof(arr)/sizeof(arr[0]);  
    int n = 60;  
    findPair(arr, size, n);  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```
// C program to find a pair with the given difference 
#include <stdio.h> 
  
// The function assumes that the array is sorted  
bool findPair(int arr[], int size, int n) 
{ 
    // Initialize positions of two elements 
    int i = 0;   
    int j = 1; 
  
    // Search for a pair 
    while (i<size && j<size) 
    { 
        if (i != j && arr[j]-arr[i] == n) 
        { 
            printf("Pair Found: (%d, %d)", arr[i], arr[j]); 
            return true; 
        } 
        else if (arr[j]-arr[i] < n) 
            j++; 
        else
            i++; 
    } 
  
    printf("No such pair"); 
    return false; 
} 
  
// Driver program to test above function 
int main() 
{ 
    int arr[] = {1, 8, 30, 40, 100}; 
    int size = sizeof(arr)/sizeof(arr[0]); 
    int n = 60; 
    findPair(arr, size, n); 
    return 0; 
}
```

## Java

```
// Java program to find a pair with the given difference 
import java.io.*; 
  
class PairDifference 
{ 
    // The function assumes that the array is sorted 
    static boolean findPair(int arr[],int n) 
    { 
        int size = arr.length; 
  
        // Initialize positions of two elements 
        int i = 0, j = 1; 
  
        // Search for a pair 
        while (i < size && j < size) 
        { 
            if (i != j && arr[j]-arr[i] == n) 
            { 
                System.out.print("Pair Found: "+ 
                                 "( "+arr[i]+", "+ arr[j]+" )"); 
                return true; 
            } 
            else if (arr[j] - arr[i] < n) 
                j++; 
            else
                i++; 
        } 
  
        System.out.print("No such pair"); 
        return false; 
    } 
  
    // Driver program to test above function 
    public static void main (String[] args) 
    { 
        int arr[] = {1, 8, 30, 40, 100}; 
        int n = 60; 
        findPair(arr,n); 
    } 
} 
/*This code is contributed by Devesh Agrawal*/
```

## Python

```
# Python program to find a pair with the given difference 
  
# The function assumes that the array is sorted 
def findPair(arr,n): 
  
    size = len(arr) 
  
    # Initialize positions of two elements 
    i,j = 0,1
  
    # Search for a pair 
    while i < size and j < size: 
  
        if i != j and arr[j]-arr[i] == n: 
            print "Pair found (",arr[i],",",arr[j],")"
            return True
  
        elif arr[j] - arr[i] < n: 
            j+=1
        else: 
            i+=1
    print "No pair found"
    return False
  
# Driver function to test above function 
arr = [1, 8, 30, 40, 100] 
n = 60
findPair(arr, n) 
  
# This code is contributed by Devesh Agrawal
```

## C#

```
// C# program to find a pair with the given difference 
using System; 
  
class GFG { 
      
    // The function assumes that the array is sorted 
    static bool findPair(int []arr, int n) 
    { 
        int size = arr.Length; 
  
        // Initialize positions of two elements 
        int i = 0, j = 1; 
  
        // Search for a pair 
        while (i < size && j < size) 
        { 
            if (i != j && arr[j] - arr[i] == n) 
            { 
                Console.Write("Pair Found: " 
                + "( " + arr[i] + ", " + arr[j] +" )"); 
                  
                return true; 
            } 
            else if (arr[j] - arr[i] < n) 
                j++; 
            else
                i++; 
        } 
  
        Console.Write("No such pair"); 
          
        return false; 
    } 
  
    // Driver program to test above function 
    public static void Main () 
    { 
        int []arr = {1, 8, 30, 40, 100}; 
        int n = 60; 
          
        findPair(arr, n); 
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```
<?php  
// PHP program to find a pair with 
// the given difference 
  
// The function assumes that the  
// array is sorted  
function findPair(&$arr, $size, $n) 
{ 
    // Initialize positions of  
    // two elements 
    $i = 0;  
    $j = 1; 
  
    // Search for a pair 
    while ($i < $size && $j < $size) 
    { 
        if ($i != $j && $arr[$j] -  
                        $arr[$i] == $n) 
        { 
            echo "Pair Found: " . "(" .  
                  $arr[$i] . ", " . $arr[$j] . ")"; 
            return true; 
        } 
        else if ($arr[$j] - $arr[$i] < $n) 
            $j++; 
        else
            $i++; 
    } 
  
    echo "No such pair"; 
    return false; 
} 
  
// Driver Code 
$arr = array(1, 8, 30, 40, 100); 
$size = sizeof($arr); 
$n = 60; 
findPair($arr, $size, $n); 
  
// This code is contributed  
// by ChitraNayal 
?>
```

输出：

```
Pair Found: (40, 100)
```

散列也可以用来解决此问题。 创建一个空的哈希表`HT`。 遍历数组，将数组元素用作哈希键，然后将它们输入`HT`。 再次遍历数组，寻找`HT`中的值`n + arr[i]`。