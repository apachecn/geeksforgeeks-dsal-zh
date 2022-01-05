# 将一个盒子放入另一个盒子后的可见盒子数量

> 原文:[https://www . geesforgeks . org/number-visible-box-put-one-in-other/](https://www.geeksforgeeks.org/number-visible-boxes-putting-one-inside-another/)

给定 **N** 个盒子和它们在一个数组中的大小。只有当装盒子的盒子是空的，并且盒子的大小至少是盒子大小的两倍时，才允许将盒子放在另一个盒子里。任务是找到最小数量的可见框。
**示例–**

```
Input : arr[] = { 1, 3, 4, 5 }
Output : 3
Put box of size 1 in box of size 3.

Input : arr[] = { 4, 2, 1, 8 }
Output : 1
Put box of size 1 in box of size 2 
and box of size 2 in box of size 4.
And put box of size 4 in box of size 8.
```

想法是对数组进行排序。现在，创建一个队列并插入排序数组的第一个元素。现在从第一个元素开始遍历数组，并将每个元素插入队列，同时检查队列的前一个元素是否小于或等于当前遍历元素的一半。因此，可见框的数量将是遍历排序数组后队列中的元素数量。基本上，我们尝试在大于或等于 2*x 的最小盒子中放置一个大小为的盒子。
例如，如果 arr[] = { 2，3，4，6 }，那么我们尝试将大小为 2 的盒子放在大小为 4 的盒子中，而不是大小为 6 的盒子中，因为如果我们将大小为 2 的盒子放在大小为 6 的盒子中，那么大小为 3 的盒子不能保存在任何其他盒子中，并且我们需要最小化可见盒子的数量。

## C++

```
// CPP program to count number of visible boxes.
#include <bits/stdc++.h>
using namespace std;

// return the minimum number of visible boxes
int minimumBox(int arr[], int n)
{
    queue<int> q;

    // sorting the array
    sort(arr, arr + n);

    q.push(arr[0]);

    // traversing the array
    for (int i = 1; i < n; i++)  {

        int now = q.front();

        // checking if current element
        // is greater than or equal to
        // twice of front element
        if (arr[i] >= 2 * now)
            q.pop();

        // Pushing each element of array
        q.push(arr[i]);
    }

    return q.size();
}

// driver Program
int main()
{
    int arr[] = { 4, 1, 2, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minimumBox(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of visible
// boxes.

import java.util.LinkedList;
import java.util.Queue;
import java.util.Arrays;

public class GFG {

    // return the minimum number of visible
    // boxes
    static int minimumBox(int []arr, int n)
    {

        // New Queue of integers.
        Queue<Integer> q = new LinkedList<>();

        // sorting the array
        Arrays.sort(arr);

        q.add(arr[0]);

        // traversing the array
        for (int i = 1; i < n; i++)
        {
            int now = q.element();

            // checking if current element
            // is greater than or equal to
            // twice of front element
            if (arr[i] >= 2 * now)
            q.remove();

            // Pushing each element of array
            q.add(arr[i]);
        }

        return q.size();
    }

    // Driver code
    public static void main(String args[])
    {
        int [] arr = { 4, 1, 2, 8 };
        int n = arr.length;

        System.out.println(minimumBox(arr, n));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python3 program to count number
# of visible boxes.

import collections

# return the minimum number of visible boxes
def minimumBox(arr, n):

    q = collections.deque([])

    # sorting the array
    arr.sort()

    q.append(arr[0])

    # traversing the array
    for i in range(1, n):

        now = q[0]

        # checking if current element
        # is greater than or equal to
        # twice of front element
        if(arr[i] >= 2 * now):
            q.popleft()

        # Pushing each element of array
        q.append(arr[i])

    return len(q)

# driver Program
if __name__=='__main__':
    arr = [4, 1, 2, 8 ]
    n = len(arr)
    print(minimumBox(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count number of visible
// boxes.
using System;
using System.Collections.Generic;

class GFG {

    // return the minimum number of visible
    // boxes
    static int minimumBox(int []arr, int n)
    {

        // New Queue of integers.
        Queue<int> q = new Queue<int>();

        // sorting the array
        Array.Sort(arr);

        q.Enqueue(arr[0]);

        // traversing the array
        for (int i = 1; i < n; i++)
        {
            int now = q.Peek();

            // checking if current element
            // is greater than or equal to
            // twice of front element
            if (arr[i] >= 2 * now)
            q.Dequeue();

            // Pushing each element of array
            q.Enqueue(arr[i]);
        }

        return q.Count;
    }

    // Driver code
    public static void Main()
    {
        int [] arr = { 4, 1, 2, 8 };
        int n = arr.Length;

        Console.WriteLine(minimumBox(arr, n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of visible boxes.

// return the minimum number of visible boxes
function minimumBox($arr, $n)
{
    $q = array();

    // sorting the array
    sort($arr);

    array_push($q, $arr[0]);

    // traversing the array
    for ($i = 1; $i < $n; $i++)
    {

        $now = $q[0];

        // checking if current element
        // is greater than or equal to
        // twice of front element
        if ($arr[$i] >= 2 * $now)
            array_pop($q);

        // Pushing each element of array
        array_push($q,$arr[$i]);
    }

    return count($q);
}

// Driver Code
$arr = array( 4, 1, 2, 8 );
$n = count($arr);
echo minimumBox($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count
// number of visible boxes.

// return the minimum number
// of visible boxes
function minimumBox(arr, n)
{
    var q = [];

    // sorting the array
    arr.sort((a,b)=> a-b)

    q.push(arr[0]);

    // traversing the array
    for (var i = 1; i < n; i++)  {

        var now = q[0];

        // checking if current element
        // is greater than or equal to
        // twice of front element
        if (arr[i] >= 2 * now)
            q.pop(0);

        // Pushing each element of array
        q.push(arr[i]);
    }

    return q.length;
}

// driver Program
var arr = [ 4, 1, 2, 8 ];
var n = arr.length;
document.write( minimumBox(arr, n));

</script>
```

**输出:**

```
1
```

**时间复杂度:** O(nlogn)