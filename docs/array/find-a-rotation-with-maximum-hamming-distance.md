# 查找具有最大汉明距离的旋转

> 原文： [https://www.geeksforgeeks.org/find-a-rotation-with-maximum-hamming-distance/](https://www.geeksforgeeks.org/find-a-rotation-with-maximum-hamming-distance/)

给定`n`个元素的数组，请创建一个新数组，该数组是给定数组的旋转，并且两个数组之间的汉明距离最大。

[两个长度相等的数组或字符串之间的汉明距离](https://en.wikipedia.org/wiki/Hamming_distance)是相应字符（元素）不同的位置数。

**注意**：对于给定的输入，可以有多个输出。

例子：

```
Input :  1 4 1
Output :  2
Explanation:  
Maximum hamming distance = 2.
We get this hamming distance with 4 1 1 
or 1 1 4 

input :  N = 4
         2 4 8 0
output :  4
Explanation: 
Maximum hamming distance = 4
We get this hamming distance with 4 8 0 2.
All the places can be occupied by another digit.
Other solutions can be 8 0 2 4, 4 0 2 8 etc.  

```



创建另一个数组，该数组的大小是原始数组的两倍，以使此新数组（复制数组）的元素只是原始数组的元素，并按相同顺序重复两次。 例如，如果原始数组为`1 4 1`，则副本数组为`1 4 1 1 4 1`。

现在，遍历副本数组并查找每次移位（或旋转）的汉明距离。 因此，我们检查`4 1 1, 1 1 4, 1 4 1`，选择汉明距离最大的输出。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to Find another array 
// such that the hamming distance  
// from the original array is maximum 
#include <bits/stdc++.h> 
using namespace std; 

// Return the maximum hamming distance of a rotation 
int maxHamming(int arr[], int n) 
{ 
    // arr[] to brr[] two times so that 
    // we can traverse through all rotations. 
    int brr[2 *n + 1]; 
    for (int i = 0; i < n; i++) 
        brr[i] = arr[i]; 
    for (int i = 0; i < n; i++)  
        brr[n+i] = arr[i]; 

    // We know hamming distance with 0 rotation 
    // would be 0\. 
    int maxHam = 0;     

    // We try other rotations one by one and compute 
    // Hamming distance of every rotation 
    for (int i = 1; i < n; i++) 
    { 
        int currHam = 0; 
        for (int j = i, k=0; j < (i + n); j++,k++)  
            if (brr[j] != arr[k]) 
                 currHam++; 

        // We can never get more than n.  
        if (currHam == n) 
            return n; 

        maxHam = max(maxHam, currHam); 
    } 

    return maxHam; 
} 

// driver program 
int main()  
{ 
    int arr[] = {2, 4, 6, 8};     
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << maxHamming(arr, n);     
    return 0; 
} 

```

## Java

```java
// Java program to Find another array 
// such that the hamming distance  
// from the original array is maximum 
class GFG  
{ 
// Return the maximum hamming 
// distance of a rotation 
static int maxHamming(int arr[], int n) 
{ 
    // arr[] to brr[] two times so that 
    // we can traverse through all rotations. 
    int brr[]=new int[2 *n + 1]; 
    for (int i = 0; i < n; i++) 
        brr[i] = arr[i]; 
    for (int i = 0; i < n; i++)  
        brr[n+i] = arr[i]; 
  
    // We know hamming distance with  
    // 0 rotation would be 0. 
    int maxHam = 0;  
  
    // We try other rotations one by one  
    // and compute Hamming distance 
    // of every rotation 
    for (int i = 1; i < n; i++) 
    { 
        int currHam = 0; 
        for (int j = i, k=0; j < (i + n); j++, 
                                          k++)  
            if (brr[j] != arr[k]) 
                currHam++; 
  
        // We can never get more than n.  
        if (currHam == n) 
            return n; 
  
        maxHam = Math.max(maxHam, currHam); 
    } 
  
    return maxHam; 
}  
  
// driver code 
public static void main (String[] args) 
{ 
    int arr[] = {2, 4, 6, 8};  
    int n = arr.length; 
    System.out.print(maxHamming(arr, n));      
} 
} 
  
// This code is contributed by Anant Agarwal. 
```

## Python3

```py
# Python3 code to Find another array 
# such that the hamming distance  
# from the original array is maximum 
  
# Return the maximum hamming  
# distance of a rotation 
def maxHamming( arr , n ): 
  
    # arr[] to brr[] two times so 
    # that we can traverse through  
    # all rotations. 
    brr = [0] * (2 * n + 1) 
    for i in range(n): 
        brr[i] = arr[i] 
    for i in range(n): 
        brr[n+i] = arr[i] 
      
    # We know hamming distance  
    # with 0 rotation would be 0. 
    maxHam = 0
      
    # We try other rotations one by 
    # one and compute Hamming  
    # distance of every rotation 
    for i in range(1, n): 
        currHam = 0
        k = 0
        for j in range(i, i + n): 
            if brr[j] != arr[k]: 
                currHam += 1
                k = k + 1
          
        # We can never get more than n. 
        if currHam == n: 
            return n 
          
        maxHam = max(maxHam, currHam) 
      
    return maxHam 
  
# driver program 
arr = [2, 4, 6, 8] 
n = len(arr) 
print(maxHamming(arr, n)) 
  
# This code is contributed by "Sharad_Bhardwaj". 
```

## C#

```cs
// C# program to Find another array 
// such that the hamming distance  
// from the original array is maximum 
using System; 
  
class GFG { 
      
    // Return the maximum hamming 
    // distance of a rotation 
    static int maxHamming(int []arr, int n) 
    { 
          
        // arr[] to brr[] two times so that 
        // we can traverse through all rotations. 
        int []brr=new int[2 * n + 1]; 
          
        for (int i = 0; i < n; i++) 
            brr[i] = arr[i]; 
        for (int i = 0; i < n; i++)  
            brr[n+i] = arr[i]; 
      
        // We know hamming distance with  
        // 0 rotation would be 0. 
        int maxHam = 0;  
      
        // We try other rotations one by one  
        // and compute Hamming distance 
        // of every rotation 
        for (int i = 1; i < n; i++) 
        { 
            int currHam = 0; 
            for (int j = i, k=0; j < (i + n);  
                                    j++, k++)  
                if (brr[j] != arr[k]) 
                    currHam++; 
      
            // We can never get more than n.  
            if (currHam == n) 
                return n; 
      
            maxHam = Math.Max(maxHam, currHam); 
        } 
      
        return maxHam; 
    }  
      
    // driver code 
    public static void Main () 
    { 
        int []arr = {2, 4, 6, 8};  
        int n = arr.Length; 
        Console.Write(maxHamming(arr, n));  
    } 
} 
  
// This code is contributed by vt_m. 
```

## PHP

```php
<?php 
// PHP program to Find another array 
// such that the hamming distance  
// from the original array is maximum 
  
// Return the maximum hamming 
// distance of a rotation 
function maxHamming($arr, $n) 
{ 
      
    // arr[] to brr[] two times so that 
    // we can traverse through all rotations. 
    $brr = array(); 
    for ($i = 0; $i < $n; $i++) 
        $brr[$i] = $arr[$i]; 
    for ($i = 0; $i < $n; $i++)  
        $brr[$n+$i] = $arr[$i]; 
  
    // We know hamming distance 
    // with 0 rotation would be 0. 
    $maxHam = 0;  
  
    // We try other rotations one  
    // by one and compute Hamming  
    // distance of every rotation 
    for ($i = 1; $i < $n; $i++) 
    { 
        $currHam = 0; 
        for ( $j = $i, $k = 0; $j < ($i + $n); 
                                  $j++, $k++)  
            if ($brr[$j] != $arr[$k]) 
                $currHam++; 
  
        // We can never get more than n.  
        if ($currHam == $n) 
            return $n; 
  
        $maxHam = max($maxHam, $currHam); 
    } 
  
    return $maxHam; 
} 
  
    // Driver Code 
    $arr = array(2, 4, 6, 80);  
    $n = count($arr); 
    echo maxHamming($arr, $n);  
  
// This code is contributed by anuj_67. 
?> 
```

输出：

```
4
```

时间复杂度：`O(n*n)`。

