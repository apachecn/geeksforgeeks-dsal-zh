# 使用给定的操作检查给定的 1 到`N`的排列是否可行

> 原文：[https://www.geeksforgeeks.org/check-if-given-permutation-of-1-to-n-is-feasible-using-given-operations/](https://www.geeksforgeeks.org/check-if-given-permutation-of-1-to-n-is-feasible-using-given-operations/)

给定大小为`N`的数组`arr[]`，检查此数组是否在以下约束下构建的任务：

1.  该数组只能包含 1 到`N`之间的数字。

2.  我们必须按顺序构建数组。 这意味着首先我们放置 1，然后放置 2，依此类推，直到`N`。

3.  如果数组为空，那么我们可以在任何位置放置一个数字。

4.  如果不为空，则可以将下一个元素放置在上一个元素的下一个位置。 如果下一个位置超出数组大小或已经被填满，那么我们可以选择任何未被占用的位置并放置编号。

**示例**：

> **输入**：`arr[] = {2, 3, 4, 5, 1}`
>
> **输出**：`Yes`
>
> **说明**：最初数组为空。 因此我们可以将 1 放置在任何位置。
>
> 我们位于位置 5（基于 1 的索引）。
>
> 下一个位置超出数组大小，所以我们可以在任意位置放置 2。 我们将其放置在第一位置。
>
> 然后，将 3 放置在第二位置，将 4 放置在第三位置，将 5 放置在第四位置。
>
> 因此，我们可以构建这样的数组。
> 
> **输入**：`arr [] = {1, 5, 2, 4, 3}`
>
> **输出**：`NO`
>
> **说明**：首先，我们可以将 1 放在第一位置。 
>
> 然后我们必须将 2 放置在第二个位置，因为第二个位置为空，但是 2 放置在给定数组中的位置 3 处。
>
> 因此无法构建这种数组。

**方法**：

1.  首先，将每个数组元素的索引存储在[**映射**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 中。

2.  将下一个元素的位置存储在`next`中。 最初，由于数组为空，因此`next`包含`1`的位置。

3.  遍历`[1, N]`并检查当前元素是否存在于下一个索引处。 如果不是，则返回 -1。

4.  在每次迭代中，将当前位置标记为已访问，然后将`next`更新为下一个值的可能索引。 如果未访问当前索引的下一个索引`i + 1`，则将`next`更新为`i + 1`。 否则，如果下一个可能的索引超出数组索引范围，则存储映射中下一个元素的位置，因为可以将其放置在映射中当前索引之前的任何索引处。

5.  数组的完整遍历后，返回`true`，因为所有索引均已放置在其各自的`next`索引处。

下面是上述方法的实现。

## C++

```cpp

// C++ program to Check If we
// can build the given array
// under given constraints.

#include <bits/stdc++.h>
using namespace std;

// Function return true if we
// can build the array
bool CheckArray(int a[], int n)
{
    int i, f = 0, next;

    // First one is to keep position
    // of each element
    // Second one is for marking
    // the current position
    map<int, int> pos, vis;

    for (i = 0; i < n; i++) {
        pos[a[i]] = i;
    }

    // Initially next contains
    // the position of 1.
    next = pos[1];

    for (i = 1; i <= n; i++) {
        // Mark the current
        // position.
        vis[next] = 1;

        // If the element is not
        // present at that position
        // then it is impossible
        // to build
        if (i != a[next]) {
            return false;
        }

        // Updating the next
        if (next + 1 == n
            || vis[next + 1]) {

            // If the next position is
            // out of array size or next
            // position is not empty then
            // we use the map to find the
            // position of the next element
            next = pos[i + 1];
        }
        else
            // Else just increment it
            next++;
    }

    return true;
}

// Driver code
int main()
{

    int arr[] = { 2, 3, 4, 5, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    if (CheckArray(arr, N)) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }

    return 0;
}

```

## Java

```java

// Java program to check If we
// can build the given array
// under given constraints.
import java.io.*;
import java.util.*;

class GFG{

// Function return true if we
// can build the array
static boolean CheckArray(int[] a, int n)
{
    int i, f = 0, next;

    // First one is to keep position
    // of each element
    // Second one is for marking
    // the current position
    HashMap<Integer, 
            Integer> pos = new HashMap<Integer, 
                                       Integer>();
    HashMap<Integer, 
            Integer> vis = new HashMap<Integer,
                                       Integer>();
    vis.put(0, 0);

    for(i = 0; i < n; i++) 
    {
        pos.put(a[i], i);
    }

    // Initially next contains
    // the position of 1.
    next = pos.getOrDefault(1, 0);

    for(i = 1; i <= n; i++)
    {

        // Mark the current
        // position.
        vis.put(next, 1);

        // If the element is not
        // present at that position
        // then it is impossible
        // to build
        if (i != a[next])
        {
            return false;
        }

        // Updating the next
        if (next + 1 == n || 
            vis.getOrDefault(next + 1, 0) != 0)
        {

            // If the next position is
            // out of array size or next
            // position is not empty then
            // we use the map to find the
            // position of the next element
            next = pos.getOrDefault(i + 1, 0);
        }
        else

            // Else just increment it
            next++;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 2, 3, 4, 5, 1 };
    int N = arr.length;

    if (CheckArray(arr, N) == true) 
    {
        System.out.println("YES");
    }
    else
    {
        System.out.println("NO");
    }
}
}

// This code is contributed by akhilsaini

```

## Python3

```py

# Python3 program to check if we 
# can build the given array 
# under given constraints. 

# Function return true if we 
# can build the array 
def CheckArray(a, n):

    f = 0

    # First one is to keep position 
    # of each element 
    # Second one is for marking 
    # the current position 
    pos = {}
    vis = {}

    for i in range(n):
        pos[a[i]] = i

    # Initially next contains 
    # the position of 1\. 
    next = pos[1]

    for i in range(1, n + 1):

        # Mark the current 
        # position. 
        vis[next] = 1

        # If the element is not 
        # present at that position 
        # then it is impossible 
        # to build 
        if (i != a[next]):
            return False

        # Updating the next
        if (next + 1 == n or
           (next + 1 in vis and
                        vis[next + 1])):

            # If the next position is 
            # out of array size or next 
            # position is not empty then 
            # we use the map to find the 
            # position of the next element 
            if(i + 1 in pos):
                next = pos[i + 1]
        else:

            # Else just increment it 
            next += 1

    return True

# Driver code 
arr = [ 2, 3, 4, 5, 1 ]
N = len(arr)

if (CheckArray(arr, N)):
    print('YES')
else:
    print('NO')

# This code is contributed by yatinagg

```

## C#

```cs

// C# program to check If we
// can build the given array
// under given constraints.
using System;
using System.Collections;

class GFG{

// Function return true if we
// can build the array
static bool CheckArray(int[] a, int n)
{
    int i, next;

    // First one is to keep position
    // of each element
    // Second one is for marking
    // the current position
    Hashtable pos = new Hashtable(); 
      Hashtable vis = new Hashtable(); 

    for(i = 0; i < n; i++)
    {
        pos.Add(a[i], i);
    }

    // Initially next contains
    // the position of 1.
      if (pos.Contains(1))
        next = (int)pos[1];
      else
        next = 0;  

    for(i = 1; i <= n; i++) 
    {

        // Mark the current
        // position.
        vis.Add(next, 1);

        // If the element is not
        // present at that position
        // then it is impossible
        // to build
        if (i != a[next])
        {
            return false;
        }

        // Updating the next
        if (next + 1 == n || 
           (vis.Contains(next + 1) && 
                (int)vis[next + 1] != 0))
        {

            // If the next position is
            // out of array size or next
            // position is not empty then
            // we use the map to find the
            // position of the next element
              if (pos.Contains(i + 1))
                next = (int)pos[i + 1];
              else
                next = 0;  
        }
        else

            // Else just increment it
            next++;
    }
    return true;
}

// Driver code
static public void Main()
{
    int[] arr = { 2, 3, 4, 5, 1 };
    int N = arr.Length;

    if (CheckArray(arr, N) == true)
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by akhilsaini

```

**输出**： 

```
YES

```



* * *

* * *



