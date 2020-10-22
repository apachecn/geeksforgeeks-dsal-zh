# 找到要翻转的零，以使连续的 1 的数目最大化

> 原文： [https://www.geeksforgeeks.org/find-zeroes-to-be-flipped-so-that-number-of-consecutive-1s-is-maximized/](https://www.geeksforgeeks.org/find-zeroes-to-be-flipped-so-that-number-of-consecutive-1s-is-maximized/)

给定一个二进制数组和一个整数`m`，找到零翻转的位置，这将创建数组中连续的 1 的最大数量。

**示例**：

```
Input:   arr[] = {1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1}
         m = 2
Output:  5 7
We are allowed to flip maximum 2 zeroes. If we flip
arr[5] and arr[7], we get 8 consecutive 1's which is
maximum possible under given constraints 

Input:   arr[] = {1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1}
         m = 1
Output:  7
We are allowed to flip maximum 1 zero. If we flip 
arr[7], we get 5 consecutive 1's which is maximum 
possible under given constraints.

Input:   arr[] = {0, 0, 0, 1}
         m = 4
Output:  0 1 2
Since m is more than number of zeroes, we can flip
all zeroes.

```

来源： [http://www.careercup.com/question?id=5106425965576192](http://www.careercup.com/question?id=5106425965576192)



**简单解决方案**是通过运行两个循环来考虑每个子数组。 对于每个子数组，计数其中的零个数。 返回具有`m`个或更少零个的最大大小子数组。 该解决方案的时间复杂度为 `O(n^2)`。

**更好的解决方案**是使用辅助空间解决`O(n)`时间的问题。

对于 0 的所有位置，分别计算`left[]`和`right[]`，它们分别定义`i`的左侧和`i`的右侧连续 1 的数量。

例如，对于`arr[] = {1, 1, 0, 1, 1, 0, 0, 1, 1, 1}`和`m = 1`，`left[2] = 2`和`right[2] = 2`，`left[5] = 2`，`right[5] = 0`，`left[6] = 0`，`right[6] = 3`。

可以通过遍历一次数组并跟踪最后一次看到的 1 和最后一次看到的 0 来填充`left[]`和`right[]`的时间为`O(n)`。在填充`left[]`和`right[]`的同时，我们还将全零的索引存储在第三个数组，`zeroes[]`。 对于上面的示例，此第三个数组存储`{2, 5, 6}`。

现在遍历`zeros[]`，对于该数组中的所有连续`m`个条目，计算可产生的 1s 之和。 可以使用`left[]`和`right[]`在`O(n)`中完成此步骤。

有效的**解决方案**可以解决`O(n)`时间和`O(1)`空间中的问题。 这个想法是对给定的数组使用滑动窗口。 解决方案取自[这里](http://www.careercup.com/question?id=5106425965576192)。

让我们使用一个覆盖从索引`wL`到索引`wR`的窗口。 设窗口内的零数为`zeroCount`。 我们维护的窗口中最多包含`m`个零。

主要步骤是：

+   当`zeroCount`不超过`m`时：向右扩展窗口（`wR++`）并更新`count zeroCount`。

+   当`zeroCount`超过` m `时，从左侧缩小窗口（`wL++`），更新`zeroCount`；

+   一路更新最宽的窗口。 输出零的位置在最佳窗口内。

以下是该想法的实现。

## C++ 

```cpp

// C++ program to find positions of zeroes flipping which 
// produces maximum number of xonsecutive 1's 
#include<bits/stdc++.h> 
using namespace std; 

// m is maximum of number zeroes allowed to flip 
// n is size of array 
void findZeroes(int arr[], int n, int m) 
{ 
    // Left and right indexes of current window 
    int wL = 0, wR = 0;  

    // Left index and size of the widest window  
    int bestL = 0, bestWindow = 0;  

    // Count of zeroes in current window 
    int zeroCount = 0;  

    // While right boundary of current window doesn't cross  
    // right end 
    while (wR < n) 
    { 
        // If zero count of current window is less than m, 
        // widen the window toward right 
        if (zeroCount <= m) 
        { 
            if (arr[wR] == 0) 
              zeroCount++; 
            wR++; 
        } 

        // If zero count of current window is more than m, 
        // reduce the window from left 
        if (zeroCount > m) 
        { 
            if (arr[wL] == 0) 
              zeroCount--; 
            wL++; 
        } 

        // Updqate widest window if this window size is more 
        if ((wR-wL > bestWindow) && (zeroCount<=m)) 
        { 
            bestWindow = wR-wL; 
            bestL = wL; 
        } 
    } 

    // Print positions of zeroes in the widest window 
    for (int i=0; i<bestWindow; i++) 
    { 
        if (arr[bestL+i] == 0) 
           cout << bestL+i << " "; 
    } 
} 

// Driver program 
int main() 
{ 
   int arr[] = {1, 0, 0, 1, 1, 0, 1, 0, 1, 1}; 
   int m = 2; 
   int n =  sizeof(arr)/sizeof(arr[0]); 
   cout << "Indexes of zeroes to be flipped are "; 
   findZeroes(arr, n, m); 
   return 0; 
} 

```

## Python3

```py
# Python3 program to find positions 
# of zeroes flipping which produces 
# maximum number of xonsecutive 1's 
  
# m is maximum of number zeroes allowed  
# to flip, n is size of array 
def findZeroes(arr, n, m) : 
      
    # Left and right indexes of current window 
    wL = wR = 0
  
    # Left index and size of the widest window  
    bestL = bestWindow = 0
  
    # Count of zeroes in current window 
    zeroCount = 0
  
    # While right boundary of current  
    # window doesn't cross right end 
    while wR < n: 
          
        # If zero count of current window is less than m, 
        # widen the window toward right 
        if zeroCount <= m : 
            if arr[wR] == 0 : 
                zeroCount += 1
            wR += 1
  
        # If zero count of current window is more than m, 
        # reduce the window from left 
        if zeroCount > m : 
            if arr[wL] == 0 : 
                zeroCount -= 1
            wL += 1
  
        # Updqate widest window if 
        # this window size is more 
        if (wR-wL > bestWindow) and (zeroCount<=m) : 
            bestWindow = wR - wL 
            bestL = wL 
  
    # Print positions of zeroes  
    # in the widest window 
    for i in range(0, bestWindow): 
        if arr[bestL + i] == 0: 
            print (bestL + i, end = " ") 
  
# Driver program 
arr = [1, 0, 0, 1, 1, 0, 1, 0, 1, 1] 
m = 2
n = len(arr) 
print ("Indexes of zeroes to be flipped are", end = " ") 
findZeroes(arr, n, m) 
  
# This code is contributed by Shreyanshi Arun.
```

## C#

```cs
// C# to find positions of zeroes flipping which 
// produces maximum number of consecutive 1's 
using System; 
  
class Test 
{ 
    static int []arr = new int[]{1, 0, 0, 1, 1, 
                                0, 1, 0, 1, 1}; 
      
    // m is maximum of number zeroes allowed to flip 
    static void findZeroes(int m) 
    { 
        // Left and right indexes of current window 
        int wL = 0, wR = 0;  
      
        // Left index and size of the widest window  
        int bestL = 0, bestWindow = 0;  
      
        // Count of zeroes in current window 
        int zeroCount = 0;  
      
        // While right boundary of current  
        // window doesn't cross right end 
        while (wR < arr.Length) 
        { 
            // If zero count of current window is less 
            // than m, widen the window toward right 
            if (zeroCount <= m) 
            { 
                if (arr[wR] == 0) 
                zeroCount++; 
                wR++; 
            } 
      
            // If zero count of current window is more than m, 
            // reduce the window from left 
            if (zeroCount > m) 
            { 
                if (arr[wL] == 0) 
                zeroCount--; 
                wL++; 
            } 
      
            // Update widest window if this window size is more 
            if ((wR-wL > bestWindow) && (zeroCount<=m)) 
            { 
                bestWindow = wR-wL; 
                bestL = wL; 
            } 
        } 
      
        // Print positions of zeroes in the widest window 
        for (int i = 0; i < bestWindow; i++) 
        { 
            if (arr[bestL + i] == 0) 
            Console.Write(bestL + i + " "); 
        } 
    } 
      
    // Driver method to test the above function 
    public static void Main(String[] args)  
    { 
        int m = 2; 
        Console.Write("Indexes of zeroes to be flipped are "); 
        findZeroes(m); 
    } 
} 
  
// This code is contributed by parashar
```

## PHP

```php
<?php 
// PHP program to find positions of 
// zeroes flipping which produces  
// maximum number of xonsecutive 1's 
  
// m is maximum of number zeroes 
// allowed to flip n is size of array 
function findZeroes($arr, $n, $m) 
{ 
      
    // Left and right indexes 
    // of current window 
    $wL = 0; 
    $wR = 0;  
  
    // Left index and size of  
    // the widest window  
    $bestL = 0;  
    $bestWindow = 0;  
  
    // Count of zeroes in 
    // current window 
    $zeroCount = 0;  
  
    // While right boundary of  
    // current window doesn't cross  
    // right end 
    while ($wR < $n) 
    { 
          
        // If zero count of current  
        // window is less than m, 
        // widen the window toward right 
        if ($zeroCount <= $m) 
        { 
            if ($arr[$wR] == 0) 
            $zeroCount++; 
            $wR++; 
        } 
  
        // If zero count of current 
        // window is more than m, 
        // reduce the window from left 
        if ($zeroCount > $m) 
        { 
            if ($arr[$wL] == 0) 
            $zeroCount--; 
            $wL++; 
        } 
  
        // Updqate widest window if 
        // this window size is more 
        if (($wR-$wL > $bestWindow) && ($zeroCount<=$m)) 
        { 
            $bestWindow = $wR - $wL; 
            $bestL = $wL; 
        } 
    } 
  
    // Print positions of zeroes 
    // in the widest window 
    for($i = 0; $i < $bestWindow; $i++) 
    { 
        if ($arr[$bestL + $i] == 0) 
        echo $bestL + $i . " "; 
    } 
} 
  
    // Driver Code 
    $arr = array(1, 0, 0, 1, 1, 0, 1, 0, 1, 1); 
    $m = 2; 
    $n = sizeof($arr)/sizeof($arr[0]); 
    echo "Indexes of zeroes to be flipped are "; 
    findZeroes($arr, $n, $m); 
    return 0; 
  
// This code is contributed by nitin mittal. 
?>
```

输出：

```
Indexes of zeroes to be flipped are 5 7
```

