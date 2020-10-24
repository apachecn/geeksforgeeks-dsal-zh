# 最长递增子序列的构造（`N log N`）

> 原文： [https://www.geeksforgeeks.org/construction-of-longest-monotonically-increasing-subsequence-n-log-n/](https://www.geeksforgeeks.org/construction-of-longest-monotonically-increasing-subsequence-n-log-n/)

在上一篇文章中，我详细解释了最长[递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)（LIS）问题。 但是，该帖子仅涵盖了与 LIS 查询大小有关的代码，而没有涵盖 LIS 的构造。 我把它留作练习。 如果您解决了，那就加油。 如果不是，那么您并不孤单，这里是代码。

如果您尚未阅读我的上一篇文章，请在[这里](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)阅读。 请注意，以下代码以相反的顺序打印 LIS。 我们可以使用栈（显式栈或系统栈）修改打印顺序。 我将解释作为练习（简单）进行。

## C++ 

```cpp

// C++ implementation to find longest increasing subsequence 
// in O(n Log n) time. 
#include <bits/stdc++.h> 
using namespace std; 

// Binary search 
int GetCeilIndex(int arr[], vector<int>& T, int l, int r, 
                 int key) 
{ 
    while (r - l > 1) { 
        int m = l + (r - l) / 2; 
        if (arr[T[m]] >= key) 
            r = m; 
        else
            l = m; 
    } 

    return r; 
} 

int LongestIncreasingSubsequence(int arr[], int n) 
{ 
    // Add boundary case, when array n is zero 
    // Depend on smart pointers 

    vector<int> tailIndices(n, 0); // Initialized with 0 
    vector<int> prevIndices(n, -1); // initialized with -1 

    int len = 1; // it will always point to empty location 
    for (int i = 1; i < n; i++) { 
        if (arr[i] < arr[tailIndices[0]]) { 
            // new smallest value 
            tailIndices[0] = i; 
        } 
        else if (arr[i] > arr[tailIndices[len - 1]]) { 
            // arr[i] wants to extend largest subsequence 
            prevIndices[i] = tailIndices[len - 1]; 
            tailIndices[len++] = i; 
        } 
        else { 
            // arr[i] wants to be a potential condidate of 
            // future subsequence 
            // It will replace ceil value in tailIndices 
            int pos = GetCeilIndex(arr, tailIndices, -1, 
                                   len - 1, arr[i]); 

            prevIndices[i] = tailIndices[pos - 1]; 
            tailIndices[pos] = i; 
        } 
    } 

    cout << "LIS of given input" << endl; 
    for (int i = tailIndices[len - 1]; i >= 0; i = prevIndices[i]) 
        cout << arr[i] << " "; 
    cout << endl; 

    return len; 
} 

int main() 
{ 
    int arr[] = { 2, 5, 3, 7, 11, 8, 10, 13, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    printf("LIS size %d\n", LongestIncreasingSubsequence(arr, n)); 

    return 0; 
} 

```

## Java

```java
// Java implementation to find longest 
// increasing subsequence in O(n Log n) 
// time. 
import java.util.Arrays; 
  
class GFG { 
  
    // Binary search 
    static int GetCeilIndex(int arr[], 
                            int T[], int l, 
                            int r, int key) 
    { 
  
        while (r - l > 1) { 
  
            int m = l + (r - l) / 2; 
            if (arr[T[m]] >= key) 
                r = m; 
            else
                l = m; 
        } 
  
        return r; 
    } 
  
    static int LongestIncreasingSubsequence( 
        int arr[], int n) 
    { 
  
        // Add boundary case, when array n is zero 
        // Depend on smart pointers 
  
        int tailIndices[] = new int[n]; 
  
        // Initialized with 0 
        Arrays.fill(tailIndices, 0); 
  
        int prevIndices[] = new int[n]; 
  
        // initialized with -1 
        Arrays.fill(prevIndices, -1); 
  
        // it will always point to empty 
        // location 
        int len = 1; 
  
        for (int i = 1; i < n; i++) { 
            if (arr[i] < arr[tailIndices[0]]) 
  
                // new smallest value 
                tailIndices[0] = i; 
  
            else if (arr[i] > arr[tailIndices[len - 1]]) { 
  
                // arr[i] wants to extend 
                // largest subsequence 
                prevIndices[i] = tailIndices[len - 1]; 
                tailIndices[len++] = i; 
            } 
            else { 
  
                // arr[i] wants to be a potential 
                // condidate of future subsequence 
                // It will replace ceil value in 
                // tailIndices 
                int pos = GetCeilIndex(arr, 
                                       tailIndices, -1, len - 1, arr[i]); 
  
                prevIndices[i] = tailIndices[pos - 1]; 
                tailIndices[pos] = i; 
            } 
        } 
  
        System.out.println("LIS of given input"); 
  
        for (int i = tailIndices[len - 1]; i >= 0; 
             i = prevIndices[i]) 
            System.out.print(arr[i] + " "); 
  
        System.out.println(); 
  
        return len; 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 2, 5, 3, 7, 11, 8, 10, 13, 6 }; 
        int n = arr.length; 
  
        System.out.print("LIS size\n" + LongestIncreasingSubsequence(arr, n)); 
    } 
} 
  
// This code is contributed by Anant Agarwal. 
```

## Python3

```py
# Python implementation to 
# find longest increasing 
# subsequence 
# in O(n Log n) time. 
  
# Binary search 
def GetCeilIndex(arr, T, l, r, key): 
  
    while (r - l > 1): 
      
        m = l + (r - l)//2
        if (arr[T[m]] >= key): 
            r = m 
        else: 
            l = m 
  
    return r 
   
def LongestIncreasingSubsequence(arr, n): 
  
    # Add boundary case, 
    # when array n is zero 
    # Depend on smart pointers 
      
    # Initialized with 0 
    tailIndices =[0 for i in range(n + 1)]   
  
    # Initialized with -1 
    prevIndices =[-1 for i in range(n + 1)]   
      
    # it will always point 
    # to empty location 
    len = 1 
    for i in range(1, n): 
      
        if (arr[i] < arr[tailIndices[0]]): 
          
            # new smallest value 
            tailIndices[0] = i 
          
        elif (arr[i] > arr[tailIndices[len-1]]): 
          
            # arr[i] wants to extend 
            # largest subsequence 
            prevIndices[i] = tailIndices[len-1] 
            tailIndices[len] = i 
            len += 1
          
        else: 
          
            # arr[i] wants to be a 
            # potential condidate of 
            # future subsequence 
            # It will replace ceil 
            # value in tailIndices 
            pos = GetCeilIndex(arr, tailIndices, -1, 
                                   len-1, arr[i]) 
   
            prevIndices[i] = tailIndices[pos-1] 
            tailIndices[pos] = i 
          
    print("LIS of given input") 
    i = tailIndices[len-1] 
    while(i >= 0): 
        print(arr[i], " ", end ="") 
        i = prevIndices[i] 
    print() 
   
    return len
  
# driver code 
arr = [ 2, 5, 3, 7, 11, 8, 10, 13, 6 ] 
n = len(arr) 
   
print("LIS size\n", LongestIncreasingSubsequence(arr, n)) 
  
# This code is contributed 
# by Anant Agarwal. 
```

## C#

```cs
// C# implementation to find longest 
// increasing subsequence in O(n Log n) 
// time. 
using System; 
  
class GFG { 
  
    // Binary search 
    static int GetCeilIndex(int[] arr, int[] T, int l, 
                            int r, int key) 
    { 
  
        while (r - l > 1) { 
            int m = l + (r - l) / 2; 
  
            if (arr[T[m]] >= key) 
                r = m; 
            else
                l = m; 
        } 
  
        return r; 
    } 
  
    static int LongestIncreasingSubsequence( 
        int[] arr, int n) 
    { 
  
        // Add boundary case, when array n is zero 
        // Depend on smart pointers 
  
        int[] tailIndices = new int[n]; 
  
        // Initialized with 0 
        for (int i = 0; i < n; i++) 
            tailIndices[i] = 0; 
  
        int[] prevIndices = new int[n]; 
  
        // initialized with -1 
        for (int i = 0; i < n; i++) 
            prevIndices[i] = -1; 
  
        // it will always point to empty 
        // location 
        int len = 1; 
  
        for (int i = 1; i < n; i++) { 
            if (arr[i] < arr[tailIndices[0]]) 
  
                // new smallest value 
                tailIndices[0] = i; 
  
            else if (arr[i] > arr[tailIndices[len - 1]]) { 
  
                // arr[i] wants to extend 
                // largest subsequence 
                prevIndices[i] = tailIndices[len - 1]; 
                tailIndices[len++] = i; 
            } 
            else { 
  
                // arr[i] wants to be a potential 
                // condidate of future subsequence 
                // It will replace ceil value in 
                // tailIndices 
                int pos = GetCeilIndex(arr, 
                                       tailIndices, -1, len - 1, arr[i]); 
  
                prevIndices[i] = tailIndices[pos - 1]; 
                tailIndices[pos] = i; 
            } 
        } 
  
        Console.Write("LIS of given input"); 
  
        for (int i = tailIndices[len - 1]; i >= 0; 
             i = prevIndices[i]) 
            Console.Write(arr[i] + " "); 
  
        Console.WriteLine(); 
  
        return len; 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 2, 5, 3, 7, 11, 8, 10, 13, 6 }; 
        int n = arr.Length; 
  
        Console.Write("LIS size\n" + LongestIncreasingSubsequence(arr, n)); 
    } 
} 
  
// This code is contributed by nitin mittal. 
```

## PHP

```php
<?php 
// PHP implementation to find longest increasing  
// subsequence in O(n Log n) time. 
  
// Binary search 
function GetCeilIndex($arr, $T, $l, $r, $key) 
{ 
    while ($r - $l > 1) 
    { 
        $m = (int)($l + ($r - $l)/2); 
        if ($arr[$T[$m]] >= $key) 
            $r = $m; 
        else
            $l = $m; 
    } 
  
    return $r; 
} 
  
function LongestIncreasingSubsequence($arr, $n) 
{ 
    // Add boundary case, when array n is zero 
    // Depend on smart pointers 
  
    $tailIndices=array_fill(0, $n+1, 0); // Initialized with 0  
    $prevIndices=array_fill(0, $n+1, -1); // initialized with -1 
  
    $len = 1; // it will always point to empty location 
    for ($i = 1; $i < $n; $i++) 
    { 
        if ($arr[$i] < $arr[$tailIndices[0]]) 
        { 
            // new smallest value 
            $tailIndices[0] = $i; 
        } 
        else if ($arr[$i] > $arr[$tailIndices[$len-1]]) 
        { 
            // arr[i] wants to extend largest subsequence 
            $prevIndices[$i] = $tailIndices[$len-1]; 
            $tailIndices[$len++] = $i; 
        } 
        else
        { 
            // arr[i] wants to be a potential condidate of 
            // future subsequence 
            // It will replace ceil value in tailIndices 
            $pos = GetCeilIndex($arr, $tailIndices, -1, 
                                $len-1, $arr[$i]); 
  
            $prevIndices[$i] = $tailIndices[$pos-1]; 
            $tailIndices[$pos] = $i; 
        } 
    } 
  
    echo "LIS of given input\n"; 
    for ($i = $tailIndices[$len-1]; $i >= 0; $i = $prevIndices[$i]) 
        echo $arr[$i]." "; 
    echo "\n"; 
  
    return $len; 
} 
  
// Driver code 
$arr = array( 2, 5, 3, 7, 11, 8, 10, 13, 6 ); 
$n = count($arr); 
  
print("LIS size ".LongestIncreasingSubsequence($arr, $n)); 
  
// This code is contributed by chandan_jnu 
?> 
```

输出：

```
LIS of given input
13 10 8 7 3 2 
LIS size 6
```

练习：

1.  您知道 [Kadane](http://en.wikipedia.org/wiki/Maximum_subarray_problem) 的算法，可以找到[最大和子数组](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。 修改 Kadane 的算法，以跟踪最大和子数组的开始和结束位置。

2.  修改 [Kadane](http://en.wikipedia.org/wiki/Maximum_subarray_problem) 的算法，以在圆形数组中找到最大和子数组。 有关这个问题的许多评论，请参考 GFG 论坛。

3.  给定两个整数`A`和`B`作为输入。 查找这两个数字（包括`A`和`B`）之间存在的斐波那契数。 例如，`A = 3`且`B = 18`，则`{3, 5, 8, 13}`之间有4个斐波那契数。 在O`(log K)`时间执行，其中`K`为`max(A, B)`。 你的观察是什么？