# 由不同元件子阵列形成的计数对

> 原文:[https://www . geesforgeks . org/count-all-distinct-pairs-by-continuous-sub-array/](https://www.geeksforgeeks.org/count-all-distinct-pairs-formed-by-contiguous-sub-array/)

给定一个数组，计算由包含不同数字的所有可能的连续子数组组成的对的数量。数组包含 0 到 n-1 之间的正数，其中 n 是数组的大小。
**例:**

```
Input:  [1, 4, 2, 4, 3, 2]
Output: 8
The subarrays with distinct elements 
are [1, 4, 2], [2, 4, 3] and [4, 3, 2].
There are 8 pairs that can be formed 
from above array.
(1, 4), (1, 2), (4, 2), (2, 4), (2, 3),
(4, 3), (4, 2), (3, 2)

Input:  [1, 2, 2, 3]
Output: 2
There are 2 pairs that can be formed
from above array.
(1, 2), (2, 3)
```

想法是对给定的数组使用滑动窗口。让我们使用一个从索引左到索引右的窗口覆盖和一个被访问的布尔数组来标记当前窗口中的元素。窗口不变量是窗口内的所有元素都是不同的。我们继续向右扩展窗口，如果发现重复，我们从左收缩窗口，直到所有元素再次不同。我们一路上更新当前窗口中的对的计数。观察表明，在扩展窗口中，对的数量可以增加等于窗口大小-1 的值。例如

```
Expanding Window   Count

[1]              Count = 0

[1, 2]           Count += 1 pair  
                 i.e. (1, 2)

[1, 2, 3]        Count += 2 pairs 
                 i.e. (1, 3) and (2, 3)

[1, 2, 3, 4]     Count += 3 pairs 
                 i.e. (1, 4), (2, 4) 
                 and (3, 4)
```

因此，上述包含不同元素的大小为 4 的窗口的总计数为 6。当窗户缩小时，什么也不需要做。
下面是想法的实现。

## C++

```
// C++ program to count number of distinct pairs
// that can be formed from all possible contiguous
// sub-arrays containing distinct numbers
#include <bits/stdc++.h>
using namespace std;

int countPairs(int arr[], int n)
{
    // initialize number of pairs to zero
    int count = 0;

    //Left and right indexes of current window
    int right = 0, left = 0;

    // Boolean array visited to mark elements in
    // current window. Initialized as false
    vector<bool> visited(n, false);

    // While right boundary of current window
    // doesn't cross right end
    while (right < n)
    {
        // If current window contains all distinct
        // elements, widen the window toward right
        while (right < n && !visited[arr[right]])
        {
            count += (right - left);
            visited[arr[right]] = true;
            right++;
        }

        // If duplicate is found in current window,
        // then reduce the window from left
        while (left < right && (right != n &&
               visited[arr[right]]))
        {
            visited[arr[left]] = false;
            left++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = {1, 4, 2, 4, 3, 2};
    int n = sizeof arr / sizeof arr[0];

    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of distinct pairs
// that can be formed from all possible contiguous
// sub-arrays containing distinct numbers
class GFG
{

static int countPairs(int arr[], int n)
{
    // initialize number of pairs to zero
    int count = 0;

    //Left and right indexes of current window
    int right = 0, left = 0;

    // Boolean array visited to mark elements in
    // current window. Initialized as false
    boolean visited[] = new boolean[n];

    for(int i = 0; i < n; i++)
        visited[i] = false;

    // While right boundary of current window
    // doesn't cross right end
    while (right < n)
    {
        // If current window contains all distinct
        // elements, widen the window toward right
        while (right < n && !visited[arr[right]])
        {
            count += (right - left);
            visited[arr[right]] = true;
            right++;
        }

        // If duplicate is found in current window,
        // then reduce the window from left
        while (left < right && (right != n &&
            visited[arr[right]]))
        {
            visited[arr[left]] = false;
            left++;
        }
    }

    return count;
}

// Driver code
public static void main(String args[])
{
    int arr[] = {1, 4, 2, 4, 3, 2};
    int n = arr.length;

    System.out.println( countPairs(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to count number of distinct
# pairs that can be formed from all possible
# contiguous sub-arrays containing distinct numbers

def countPairs(arr, n):

    # initialize number of pairs to zero
    count = 0

    # Left and right indexes of
    # current window
    right = 0
    left = 0

    # Boolean array visited to mark elements
    # in current window. Initialized as false
    visited = [False for i in range(n)]

    # While right boundary of current
    # window doesn't cross right end
    while (right < n):

        # If current window contains all distinct
        # elements, widen the window toward right
        while (right < n and
               visited[arr[right]] == False):
            count += (right - left)
            visited[arr[right]] = True
            right += 1

        # If duplicate is found in current window,
        # then reduce the window from left
        while (left < right and (right != n and
               visited[arr[right]] == True)):
            visited[arr[left]] = False
            left += 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [1, 4, 2, 4, 3, 2]
    n = len(arr)

    print(countPairs(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count number of distinct pairs
// that can be formed from all possible contiguous
// sub-arrays containing distinct numbers
using System;

class GFG
{

static int countPairs(int []arr, int n)
{
    // initialize number of pairs to zero
    int count = 0;

    //Left and right indexes of current window
    int right = 0, left = 0;

    // Boolean array visited to mark elements in
    // current window. Initialized as false
    bool [] visited = new bool[n];

    for(int i = 0; i < n; i++)
        visited[i] = false;

    // While right boundary of current window
    // doesn't cross right end
    while (right < n)
    {
        // If current window contains all distinct
        // elements, widen the window toward right
        while (right < n && !visited[arr[right]])
        {
            count += (right - left);
            visited[arr[right]] = true;
            right++;
        }

        // If duplicate is found in current window,
        // then reduce the window from left
        while (left < right && (right != n &&
            visited[arr[right]]))
        {
            visited[arr[left]] = false;
            left++;
        }
    }

    return count;
}

// Driver code
public static void Main()
{
    int [] arr = {1, 4, 2, 4, 3, 2};
    int n = arr.Length;

    Console.Write( countPairs(arr, n));
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program to count number of distinct pairs
// that can be formed from all possible contiguous
// sub-arrays containing distinct numbers

    function countPairs(arr,n)
    {
        // initialize number of pairs to zero
    let count = 0;

    //Left and right indexes of current window
    let right = 0, left = 0;

    // Boolean array visited to mark elements in
    // current window. Initialized as false
    let visited = new Array(n);

    for(let i = 0; i < n; i++)
        visited[i] = false;

    // While right boundary of current window
    // doesn't cross right end
    while (right < n)
    {
        // If current window contains all distinct
        // elements, widen the window toward right
        while (right < n && !visited[arr[right]])
        {
            count += (right - left);
            visited[arr[right]] = true;
            right++;
        }

        // If duplicate is found in current window,
        // then reduce the window from left
        while (left < right && (right != n &&
            visited[arr[right]]))
        {
            visited[arr[left]] = false;
            left++;
        }
    }

    return count;
    }

    // Driver code
    let arr=[1, 4, 2, 4, 3, 2];
    let n = arr.length;
    document.write( countPairs(arr, n));

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
8
```

**时间复杂度:**当涉及循环时，复杂度可能看起来像 o(n^2)2，但是注意左索引和右索引从 0 变化到 N-1。所以整体复杂度是 O(n + n) = O(n)。上述解决方案中需要的辅助空间是 O(n)，因为我们使用访问数组来标记当前窗口的元素。
本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息