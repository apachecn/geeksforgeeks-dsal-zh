# 求大小为 k 的子阵列的最大异或值

> 原文:[https://www . geesforgeks . org/find-maximum-xor-value-sub-array-size-k/](https://www.geeksforgeeks.org/find-maximum-xor-value-sub-array-size-k/)

给定一个整数数组，任务是找到大小为 k 的子数组的最大异或值。
**示例:**

```
Input  : arr[] = {2, 5, 8 ,1 , 1 ,3} k = 3
Output : 15
Explanation : All subarrays of size k (=3) and
              their XOR values are:
 {2, 5, 8} => XOR value =  15
 {5, 8, 1} => XOR value =  12
 {8, 1, 1} => XOR value =  8
 {1, 1, 3} => XOR value =  3
Maximum of all XOR values = 15

Input  : arr[] = {1, 2, 4, 5, 6}
Output : 6
```

一个**简单的解决方案**是将 k 大小的所有子阵逐一考虑，计算 XOR 值。最后返回所有异或值的最大值。该解决方案需要 0(n * k)时间
高效解决方案需要 0(n)时间。思路很简单，通过去掉前一个子阵的第一个元素，加上当前子阵的最后一个元素，就可以求出 k 大小的当前子阵的 XOR 值。我们可以通过再次对一个元素进行异或运算来从当前 XOR 中移除该元素，因为 XOR 的属性是 a ^ x ^ x = a。
算法:

```
Let input array be 'arr[]' and size of array be 'n'

max_xor ;  // user to store maximum xor value
current_xor; //  user to store xor value of current subarray 
            // of size k 

// First compute xor value of first subarray of size k  
// (i goes from 0 to k)
corrent_xor = current_xor ^ arr[i] 

// Initialize maximum XOR
max_xor = current_xor 

Traversal rest array (i goes from k to n-1 )
 a).  remove first element of previous subarray 
      current_xor = current_xor ^ arr[i-k] 

 b).  add new element to subarray  
      current_xor = current_xor ^ arr[i]

 c). update max_xor = max(max_xor, current_xor)

return max_xor 

```

下面是以上步骤的实现。

## C++

```
// C++/C program to find maximum xor value of subarray of
// size k
#include<iostream>
using namespace std;

// Returns maximum XOR value of subarray of size k
int maximumXOR(int arr[] , int n , int k)
{
    // Compute XOR value of first subarray of size k
    int current_xor = 0 ;
    for (int i = 0 ; i < k ; i++)
        current_xor  = current_xor ^ arr[i];

    // Traverse rest of the array
    int max_xor = current_xor;
    for (int i = k ; i < n; i++)
    {
        // First remove previous subarray's first
        // element
        current_xor = current_xor ^ arr[i-k];

        // add new element
        current_xor = current_xor ^ arr[i];

        // Update maximum xor value
        max_xor = max(max_xor, current_xor);
    }

    return max_xor;
}

// Driver program
int main()
{
    int arr[] = {2, 5, 8 ,1 , 1 ,3} ;
    int k = 3;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Maximum XOR : " << maximumXOR(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum xor value of
// subarray of size k
import java.io.*;

class GFG {

    // Returns maximum XOR value of subarray of size k
    static int maximumXOR(int arr[] , int n , int k)
    {

        // Compute XOR value of first subarray of size k
        int current_xor = 0 ;
        for (int i = 0 ; i < k ; i++)
            current_xor = current_xor ^ arr[i];

        // Traverse rest of the array
        int max_xor = current_xor;

        for (int i = k ; i < n; i++)
        {

            // First remove previous subarray's first
            // element
            current_xor = current_xor ^ arr[i-k];

            // add new element
            current_xor = current_xor ^ arr[i];

            // Update maximum xor value
            max_xor = Math.max(max_xor, current_xor);
        }

        return max_xor;
    }

    // Driver program
    public static void main (String[] args)
    {
        int arr[] = {2, 5, 8 ,1 , 1 ,3} ;
        int k = 3;
        int n = arr.length;
        System.out.println( "Maximum XOR : "
                   + maximumXOR(arr, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# xor value of subarray of
# size

# Returns maximum XOR value
# of subarray of size k
def maximumXOR(arr , n , k):

    # Compute XOR value of first
    # subarray of size k
    current_xor = 0
    for i in range ( k):
        current_xor = current_xor ^ arr[i]

    # Traverse rest of the array
    max_xor = current_xor
    for i in range( k,n):

        # First remove previous subarray's first
        # element
        current_xor = current_xor ^ arr[i-k]

        # add new element
        current_xor = current_xor ^ arr[i]

        # Update maximum xor value
        max_xor = max(max_xor, current_xor)

    return max_xor

# Driver program
if __name__ =="__main__":

    arr = [2, 5, 8 ,1 , 1 ,3]
    k = 3
    n = len(arr)
    print ("Maximum XOR : "
          ,maximumXOR(arr, n, k))

# This code is contributed by
# ChitraNayal
```

## C#

```
// C# program to find maximum
// xor value of subarray of
// size k
using System;
class GFG {

    // Returns maximum XOR value
    // of subarray of size k
    static int maximumXOR(int []arr,
                      int n, int k)
    {

        // Compute XOR value of first
        // subarray of size k
        int current_xor = 0 ;
        for (int i = 0; i < k; i++)
            current_xor = current_xor ^ arr[i];

        // Traverse rest of the array
        int max_xor = current_xor;

        for (int i = k ; i < n; i++)
        {

            // First remove previous
            // subarray's first
            // element
            current_xor = current_xor ^ arr[i-k];

            // add new element
            current_xor = current_xor ^ arr[i];

            // Update maximum xor value
            max_xor = Math.Max(max_xor, current_xor);
        }

        return max_xor;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {2, 5, 8 ,1 , 1 ,3} ;
        int k = 3;
        int n = arr.Length;
        Console.WriteLine("Maximum XOR : "
                  + maximumXOR(arr, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// xor value of subarray of size k

// Returns maximum XOR value
// of subarray of size k

function maximumXOR($arr, $n, $k)
{
    // Compute XOR value of
    // first subarray of size k
    $current_xor = 0 ;
    for ($i = 0 ; $i < $k ; $i++)
        $current_xor = $current_xor ^
                       $arr[$i];

    // Traverse rest of the array
    $max_xor = $current_xor;
    for ($i = $k ; $i < $n; $i++)
    {
        // First remove previous
        // subarray's first element
        $current_xor = $current_xor ^
                       $arr[$i - $k];

        // add new element
        $current_xor = $current_xor ^
                       $arr[$i];

        // Update maximum xor value
        $max_xor = max($max_xor,
                       $current_xor);
    }

    return $max_xor;
}

// Driver Code
$arr = array(2, 5, 8, 1, 1, 3) ;
$k = 3;
$n = sizeof($arr);
echo "Maximum XOR : ",
      maximumXOR($arr, $n, $k);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// Javascript program to find maximum xor value of
// subarray of size k

    // Returns maximum XOR value of subarray of size k   
    function maximumXOR(arr,n,k)
    {
        // Compute XOR value of first subarray of size k
        let current_xor = 0 ;
        for (let i = 0 ; i < k ; i++)
            current_xor = current_xor ^ arr[i];

        // Traverse rest of the array
        let max_xor = current_xor;

        for (let i = k ; i < n; i++)
        {

            // First remove previous subarray's first
            // element
            current_xor = current_xor ^ arr[i-k];

            // add new element
            current_xor = current_xor ^ arr[i];

            // Update maximum xor value
            max_xor = Math.max(max_xor, current_xor);
        }

        return max_xor;
    }

    // Driver program
    let arr=[2, 5, 8 ,1 , 1 ,3];
    let k = 3;
    let  n = arr.length;
    document.write( "Maximum XOR : "
                   + maximumXOR(arr, n, k));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Maximum XOR : 15
```

**时间复杂度:** O(n)
本文由 **Nishant_Singh(Pintu)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。