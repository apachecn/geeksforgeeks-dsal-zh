# 大小为 k 的所有子阵列的最小和最大元素之和

> 原文:[https://www . geesforgeks . org/sum-minimum-maximum-elements-subarray-size-k/](https://www.geeksforgeeks.org/sum-minimum-maximum-elements-subarrays-size-k/)

给定一个正整数和负整数的数组，任务是计算大小为 k 的所有子数组的最小和最大元素的和。
示例:

```
Input : arr[] = {2, 5, -1, 7, -3, -1, -2}  
        K = 4
Output : 18
Explanation : Subarrays of size 4 are : 
     {2, 5, -1, 7},   min + max = -1 + 7 = 6
     {5, -1, 7, -3},  min + max = -3 + 7 = 4      
     {-1, 7, -3, -1}, min + max = -3 + 7 = 4
     {7, -3, -1, -2}, min + max = -3 + 7 = 4   
     Sum of all min & max = 6 + 4 + 4 + 4 
                          = 18               
```

这个问题主要是下面问题的延伸。
[大小为 k 的所有子阵列的最大值](https://www.geeksforgeeks.org/maximum-of-all-subarrays-of-size-k/)
**方法 1(简单)**
运行两个循环生成大小为 k 的所有子阵列，并找到最大值和最小值。最后，返回所有最大和最小元素的和。
该溶液所用时间为 O(nk)。
**方法 2(高效使用出列)**
思路是使用出列数据结构和滑动窗口概念。我们创建了两个大小为 k(‘S’，‘G’)的空双端队列，它们只存储当前窗口中并非无用的元素的索引。如果一个元素不能是下一个子阵的最大值或最小值，那么它就是无用的。

```
 a) In deque 'G', we maintain decreasing order of 
    values from front to rear
 b) In deque 'S', we maintain increasing order of 
    values from front to rear

1) First window size K
  1.1) For deque 'G', if current element is greater 
       than rear end element, we remove rear while 
       current is greater.
  1.2) For deque 'S', if current element is smaller 
       than rear end element, we just pop it while 
       current is smaller.
  1.3) insert current element in both deque 'G' 'S'

2) After step 1, front of 'G' contains maximum element
   of first window and front of 'S' contains minimum 
   element of first window. Remaining elements of G
   and S may store maximum/minimum for subsequent 
   windows.

3) After that we do traversal for rest array elements.
  3.1) Front element of deque 'G' is greatest and 'S' 
       is smallest element of previous window 
  3.2) Remove all elements which are out of this 
       window [remove element at front of queue ]
  3.3) Repeat steps 1.1 , 1.2 ,1.3 

4) Return sum of minimum and maximum element of all 
   sub-array size k.
```

以下是上述想法的实现

## C++

```
// C++ program to find sum of all minimum and maximum
// elements Of Sub-array Size k.
#include<bits/stdc++.h>
using namespace std;

// Returns sum of min and max element of all subarrays
// of size k
int SumOfKsubArray(int arr[] , int n , int k)
{
    int sum = 0;  // Initialize result

    // The queue will store indexes of useful elements
    // in every window
    // In deque 'G' we maintain decreasing order of
    // values from front to rear
    // In deque 'S' we  maintain increasing order of
    // values from front to rear
    deque< int > S(k), G(k);

    // Process first window of size K
    int i = 0;
    for (i = 0; i < k; i++)
    {
        // Remove all previous greater elements
        // that are useless.
        while ( (!S.empty()) && arr[S.back()] >= arr[i])
            S.pop_back(); // Remove from rear

        // Remove all previous smaller that are elements
        // are useless.
        while ( (!G.empty()) && arr[G.back()] <= arr[i])
            G.pop_back(); // Remove from rear

        // Add current element at rear of both deque
        G.push_back(i);
        S.push_back(i);
    }

    // Process rest of the Array elements
    for (  ; i < n; i++ )
    {
        // Element at the front of the deque 'G' & 'S'
        // is the largest and smallest
        // element of previous window respectively
        sum += arr[S.front()] + arr[G.front()];

        // Remove all elements which are out of this
        // window
        while ( !S.empty() && S.front() <= i - k)
            S.pop_front();
        while ( !G.empty() && G.front() <= i - k)
            G.pop_front();

        // remove all previous greater element that are
        // useless
        while ( (!S.empty()) && arr[S.back()] >= arr[i])
            S.pop_back(); // Remove from rear

        // remove all previous smaller that are elements
        // are useless
        while ( (!G.empty()) && arr[G.back()] <= arr[i])
            G.pop_back(); // Remove from rear

        // Add current element at rear of both deque
        G.push_back(i);
        S.push_back(i);
    }

    // Sum of minimum and maximum element of last window
    sum += arr[S.front()] + arr[G.front()];

    return sum;
}

// Driver program to test above functions
int main()
{
    int arr[] = {2, 5, -1, 7, -3, -1, -2} ;
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 3;
    cout << SumOfKsubArray(arr, n, k) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of all minimum and maximum
// elements Of Sub-array Size k.
import java.util.Deque;
import java.util.LinkedList;
public class Geeks {

    // Returns sum of min and max element of all subarrays
    // of size k
    public static int SumOfKsubArray(int arr[] , int k)
    {
        int sum = 0;  // Initialize result

        // The queue will store indexes of useful elements
        // in every window
        // In deque 'G' we maintain decreasing order of
        // values from front to rear
        // In deque 'S' we  maintain increasing order of
        // values from front to rear
        Deque<Integer> S=new LinkedList<>(),G=new LinkedList<>();

        // Process first window of size K
        int i = 0;
        for (i = 0; i < k; i++)
        {
            // Remove all previous greater elements
            // that are useless.
            while ( !S.isEmpty() && arr[S.peekLast()] >= arr[i])
                S.removeLast(); // Remove from rear

            // Remove all previous smaller that are elements
            // are useless.
            while ( !G.isEmpty() && arr[G.peekLast()] <= arr[i])
                G.removeLast(); // Remove from rear

            // Add current element at rear of both deque
            G.addLast(i);
            S.addLast(i);
        }

        // Process rest of the Array elements
        for (  ; i < arr.length; i++ )
        {
            // Element at the front of the deque 'G' & 'S'
            // is the largest and smallest
            // element of previous window respectively
            sum += arr[S.peekFirst()] + arr[G.peekFirst()];

            // Remove all elements which are out of this
            // window
            while ( !S.isEmpty() && S.peekFirst() <= i - k)
                S.removeFirst();
            while ( !G.isEmpty() && G.peekFirst() <= i - k)
                G.removeFirst();

            // remove all previous greater element that are
            // useless
            while ( !S.isEmpty() && arr[S.peekLast()] >= arr[i])
                S.removeLast(); // Remove from rear

            // remove all previous smaller that are elements
            // are useless
            while ( !G.isEmpty() && arr[G.peekLast()] <= arr[i])
                G.removeLast(); // Remove from rear

            // Add current element at rear of both deque
            G.addLast(i);
            S.addLast(i);
        }

        // Sum of minimum and maximum element of last window
        sum += arr[S.peekFirst()] + arr[G.peekFirst()];

        return sum;
    }

    public static void main(String args[])
    {
        int arr[] = {2, 5, -1, 7, -3, -1, -2} ;
        int k = 3;
        System.out.println(SumOfKsubArray(arr, k));
    }
}
//This code is contributed by Gaurav Tiwari
```

## 计算机编程语言

```
# Python3 program to find Sum of all minimum and maximum
# elements Of Sub-array Size k.
from collections import deque

# Returns Sum of min and max element of all subarrays
# of size k
def SumOfKsubArray(arr, n , k):

    Sum = 0 # Initialize result

    # The queue will store indexes of useful elements
    # in every window
    # In deque 'G' we maintain decreasing order of
    # values from front to rear
    # In deque 'S' we maintain increasing order of
    # values from front to rear
    S = deque()
    G = deque()

    # Process first window of size K

    for i in range(k):

        # Remove all previous greater elements
        # that are useless.
        while ( len(S) > 0 and arr[S[-1]] >= arr[i]):
            S.pop() # Remove from rear

        # Remove all previous smaller that are elements
        # are useless.
        while ( len(G) > 0 and arr[G[-1]] <= arr[i]):
            G.pop() # Remove from rear

        # Add current element at rear of both deque
        G.append(i)
        S.append(i)

    # Process rest of the Array elements
    for i in range(k, n):

        # Element at the front of the deque 'G' & 'S'
        # is the largest and smallest
        # element of previous window respectively
        Sum += arr[S[0]] + arr[G[0]]

        # Remove all elements which are out of this
        # window
        while ( len(S) > 0 and S[0] <= i - k):
            S.popleft()
        while ( len(G) > 0 and G[0] <= i - k):
            G.popleft()

        # remove all previous greater element that are
        # useless
        while ( len(S) > 0 and arr[S[-1]] >= arr[i]):
            S.pop() # Remove from rear

        # remove all previous smaller that are elements
        # are useless
        while ( len(G) > 0 and arr[G[-1]] <= arr[i]):
            G.pop() # Remove from rear

        # Add current element at rear of both deque
        G.append(i)
        S.append(i)

    # Sum of minimum and maximum element of last window
    Sum += arr[S[0]] + arr[G[0]]

    return Sum

# Driver program to test above functions
arr=[2, 5, -1, 7, -3, -1, -2]
n = len(arr)
k = 3
print(SumOfKsubArray(arr, n, k))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find sum of all minimum and maximum
// elements Of Sub-array Size k.
using System;
using System.Collections.Generic;
class Geeks
{

  // Returns sum of min and max element of all subarrays
  // of size k
  public static int SumOfKsubArray(int []arr , int k)
  {
    int sum = 0;  // Initialize result

    // The queue will store indexes of useful elements
    // in every window
    // In deque 'G' we maintain decreasing order of
    // values from front to rear
    // In deque 'S' we  maintain increasing order of
    // values from front to rear
    List<int> S = new List<int>();
    List<int> G = new List<int>();

    // Process first window of size K
    int i = 0;
    for (i = 0; i < k; i++)
    {

      // Remove all previous greater elements
      // that are useless.
      while ( S.Count != 0 && arr[S[S.Count - 1]] >= arr[i])
        S.RemoveAt(S.Count - 1); // Remove from rear

      // Remove all previous smaller that are elements
      // are useless.
      while ( G.Count != 0 && arr[G[G.Count - 1]] <= arr[i])
        G.RemoveAt(G.Count - 1); // Remove from rear

      // Add current element at rear of both deque
      G.Add(i);
      S.Add(i);
    }

    // Process rest of the Array elements
    for (  ; i < arr.Length; i++ )
    {

      // Element at the front of the deque 'G' & 'S'
      // is the largest and smallest
      // element of previous window respectively
      sum += arr[S[0]] + arr[G[0]];

      // Remove all elements which are out of this
      // window
      while ( S.Count != 0 && S[0] <= i - k)
        S.RemoveAt(0);
      while ( G.Count != 0 && G[0] <= i - k)
        G.RemoveAt(0);

      // remove all previous greater element that are
      // useless
      while ( S.Count != 0 && arr[S[S.Count-1]] >= arr[i])
        S.RemoveAt(S.Count - 1 ); // Remove from rear

      // remove all previous smaller that are elements
      // are useless
      while ( G.Count != 0 && arr[G[G.Count - 1]] <= arr[i])
        G.RemoveAt(G.Count - 1); // Remove from rear

      // Add current element at rear of both deque
      G.Add(i);
      S.Add(i);
    }

    // Sum of minimum and maximum element of last window
    sum += arr[S[0]] + arr[G[0]];  
    return sum;
  }

  // Driver code
  public static void Main(String []args)
  {
    int []arr = {2, 5, -1, 7, -3, -1, -2} ;
    int k = 3;
    Console.WriteLine(SumOfKsubArray(arr, k));
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to find sum of all minimum and maximum
// elements Of Sub-array Size k.

// Returns sum of min and max element of all subarrays
// of size k
function SumOfKsubArray(arr , k)
{
    let sum = 0; // Initialize result

    // The queue will store indexes of useful elements
    // in every window
    // In deque 'G' we maintain decreasing order of
    // values from front to rear
    // In deque 'S' we maintain increasing order of
    // values from front to rear
    let S = [];
    let G = [];

    // Process first window of size K
    let i = 0;
    for (i = 0; i < k; i++)
    {

    // Remove all previous greater elements
    // that are useless.
    while ( S.length != 0 && arr[S[S.length - 1]] >= arr[i])
        S.pop(); // Remove from rear

    // Remove all previous smaller that are elements
    // are useless.
    while ( G.length != 0 && arr[G[G.length - 1]] <= arr[i])
        G.pop(); // Remove from rear

    // Add current element at rear of both deque
    G.push(i);
    S.push(i);
    }

    // Process rest of the Array elements
    for ( ; i < arr.length; i++ )
    {

    // Element at the front of the deque 'G' & 'S'
    // is the largest and smallest
    // element of previous window respectively
    sum += arr[S[0]] + arr[G[0]];

    // Remove all elements which are out of this
    // window
    while ( S.length != 0 && S[0] <= i - k)
        S.shift(0);
    while ( G.length != 0 && G[0] <= i - k)
        G.shift(0);

    // remove all previous greater element that are
    // useless
    while ( S.length != 0 && arr[S[S.length-1]] >= arr[i])
        S.pop(); // Remove from rear

    // remove all previous smaller that are elements
    // are useless
    while ( G.length != 0 && arr[G[G.length - 1]] <= arr[i])
        G.pop(); // Remove from rear

    // Add current element at rear of both deque
    G.push(i);
    S.push(i);
    }

    // Sum of minimum and maximum element of last window
    sum += arr[S[0]] + arr[G[0]];
    return sum;
}

// Driver code

    let arr = [2, 5, -1, 7, -3, -1, -2];
    let k = 3;
    document.write(SumOfKsubArray(arr, k));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
14
```

**时间复杂度:** O(n)
本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。