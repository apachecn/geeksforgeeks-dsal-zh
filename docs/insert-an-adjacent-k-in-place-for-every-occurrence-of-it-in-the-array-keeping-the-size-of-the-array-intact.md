# 在数组中每出现一次，插入与其相邻的 K 的副本

> 原文:[https://www . geeksforgeeks . org/每次在阵列中出现时插入一个相邻的 k-in-place-it-保持阵列大小不变/](https://www.geeksforgeeks.org/insert-an-adjacent-k-in-place-for-every-occurrence-of-it-in-the-array-keeping-the-size-of-the-array-intact/)

给定一个由 **N** 整数和一个整数 **K** 组成的数组 **arr** ，任务是为它在原始序列中的每次出现插入一个相邻的 K，然后使用一个 O(1)辅助空间将数组截断到原始长度。

**示例:**

> **输入:** arr[] = {1，0，2，3，0，4，5，0}，K = 0
> **输出:** {1，0，0，2，3，0，0，0，4}
> **解释:**
> 给定数组{1，0，2，3，0，4，5，0}修改为{1，0， **0** ，2，3，0， **0** ，
> 
> **输入:** arr[] = {7，5，8}，K = 8
> **输出:** {7，5，8}
> **解释:**
> 在数组中插入一个相邻的 8 后，它被截断以恢复数组的原始大小。

**方法一:使用** [**STL 函数**](https://www.geeksforgeeks.org/cpp-stl-tutorial/)
这个问题可以通过使用内置函数 [pop_back()](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) 和 [insert()](https://www.geeksforgeeks.org/vector-insert-function-in-c-stl/) 来解决。

下面是上述方法的实现:

## C++

```
// C++ implementation to update each entry of zero
// with two zero entries adjacent to each other
#include <bits/stdc++.h>
using namespace std;

// Function to update each entry of zero
// with two zero entries adjacent to each other
vector<int> duplicateK(vector<int>& arr)
{
    int N = arr.size();
    for(int i=0;i<N;i++)
    {
        if(arr[i] == 0)
        {
            // Insert an adjacent 0
            arr.insert(arr.begin() + i + 1, 0);

            i++;

            // Pop the last element
            arr.pop_back();
        }
    }

    return arr;
}

// Driver code
int main(int argc, char* argv[])
{
    vector<int> arr
= { 1, 0, 2, 3, 0, 4, 5, 0  };

    vector<int> ans = duplicateK(arr);

    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to update each
// entry of zero with two zero entries
// adjacent to each other
import java.util.*;

class GFG{

// Function to update each entry of
// zero with two zero entries
// adjacent to each other
static Vector<Integer> duplicateK(Vector<Integer> arr)
{
    int N = arr.size();
    for(int i = 0; i < N; i++)
    {
       if(arr.get(i) == 0)
       {

           // Insert an adjacent 0
           arr.add(i + 1, 0);

           i++;

           // Pop the last element
           arr.remove(arr.size() - 1);
       }
    }
    return arr;
}

// Driver code
public static void main(String[] args)
{
    Integer []arr = { 1, 0, 2, 3, 0, 4, 5, 0 };

    Vector<Integer> vec = new Vector<Integer>();;
    for(int i = 0; i < arr.length; i++)
       vec.add(arr[i]);

    Vector<Integer> ans = duplicateK(vec);

    for(int i = 0; i < ans.size(); i++)
       System.out.print(ans.get(i) + " ");
}
}

// This code is contributed by gauravrajput1
```

## C#

```
// C# implementation to update each
// entry of zero with two zero entries
// adjacent to each other
using System;
using System.Collections.Generic;

class GFG{

// Function to update each entry of
// zero with two zero entries
// adjacent to each other
static List<int> duplicateK(List<int> arr)
{
    int N = arr.Count;
    for(int i = 0; i < N; i++)
    {
        if(arr[i] == 0)
        {

            // Insert an adjacent 0
            arr.Insert(i + 1, 0);

            i++;

            // Pop the last element
            arr.RemoveAt(arr.Count - 1);
        }
    }
    return arr;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 2, 3, 0, 4, 5, 0 };

    List<int> vec = new List<int>();;
    for(int i = 0; i < arr.Length; i++)
    vec.Add(arr[i]);

    List<int> ans = duplicateK(vec);

    for(int i = 0; i < ans.Count; i++)
    Console.Write(ans[i] + " ");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation to update each entry of zero
// with two zero entries adjacent to each other

// Function to update each entry of zero
// with two zero entries adjacent to each other
function duplicateK(arr)
{
    var N = arr.length;
    for(var i=0;i<N;i++)
    {
        if(arr[i] == 0)
        {
            // Insert an adjacent 0
            arr.splice(i+1, 0, 0);
            i++;

            // Pop the last element
            arr.pop();
        }
    }

    return arr;
}

// Driver code

var arr=[ 1, 0, 2, 3, 0, 4, 5, 0 ];

var ans = duplicateK(arr);

for (var i = 0; i < ans.length; i++)
    document.write( ans[i] + " ");

</script>
```

**输出:**

```
1 0 0 2 3 0 0 4 
```

**方法二:使用** [**两个指针**](https://www.geeksforgeeks.org/two-pointers-technique/) **手法**

*   由于每个 K 需要用两个相邻的 K 个条目进行更新，**数组的长度将增加一个数量，该数量等于原始数组 arr[]中存在的 K 个**的数量。
*   求 K 的总数，然后我们假设我们有一个有足够空间容纳每个元素的数组。
*   初始化一个变量 *write_idx* ，该变量将指向这个虚数组末尾的索引和当前数组末尾的另一个指针 *curr* ，即 arr[N-1]。
*   从末尾开始迭代，对于每个元素，我们假设我们正在将元素复制到它的当前位置，但是仅当 write_idx < N 时才复制，并且每次都保持更新 write_idx。对于值为零的元素，写两次。

下面是上述方法的实现:

## C++

```
// C++ implementation to update each entry of zero
// with two zero entries adjacent to each other
#include <bits/stdc++.h>
using namespace std;

// Function to update each entry of zero
// with two zero entries adjacent to each other
vector<int> duplicateZeros(vector<int>& arr)
{
    const int N = arr.size();

    // Find the count of total number of zeros
    int cnt = count(arr.begin(), arr.end(), 0);

    // Variable to store index where elements
    // will be written in the final array
    int write_idx = N + cnt - 1;

    // Variable to point the current index
    int curr = N - 1;

    while (curr >= 0 && write_idx >= 0) {
        // Keep the current element to its correct
        // position, if that is within the size N
        if (write_idx < N)
            arr[write_idx] = arr[curr];

        write_idx -= 1;

        // Check if the current element is also
        // zero then again write its duplicate
        if (arr[curr] == 0) {
            if (write_idx < N)
                arr[write_idx] = 0;

            write_idx -= 1;
        }

        --curr;
    }

    // Return the final result
    return arr;
}

// Driver code
int main(int argc, char* argv[])
{
    vector<int> arr = { 1, 0, 2, 3, 0, 4, 5, 0 };

    vector<int> ans = duplicateZeros(arr);

    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to update
// each entry of zero with two zero
// entries adjacent to each other
class GFG{

// Function to update each
// entry of zero with two zero
// entries adjacent to each other
static int[] duplicateZeros(int []arr)
{

    int N = arr.length;

    // Find the count of
    // total number of zeros
    int cnt = count(arr, 0);

    // Variable to store index
    // where elements will be
    // written in the final array
    int write_idx = N + cnt - 1;

    // Variable to point the current index
    int curr = N - 1;

    while (curr >= 0 && write_idx >= 0)
    {

        // Keep the current element
        // to its correctposition, if
        // that is within the size N
        if (write_idx < N)
            arr[write_idx] = arr[curr];

        write_idx -= 1;

        // Check if the current element is also
        // zero then again write its duplicate
        if (arr[curr] == 0)
        {
            if (write_idx < N)
                arr[write_idx] = 0;

            write_idx -= 1;
        }
        --curr;
    }

    // Return the final result
    return arr;
}

static int count(int []arr, int num)
{
    int ans = 0;
    for(int i : arr)

       if(i == num)
          ans++;
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 1, 0, 2, 3, 0, 4, 5, 0 };
    int []ans = duplicateZeros(arr);

    for(int i = 0; i < ans.length; i++)
       System.out.print(ans[i] + " ");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to update each entry of zero
# with two zero entries adjacent to each other

# Function to update each entry of zero
# with two zero entries adjacent to each other
def duplicateZeros(arr):

    N = len(arr)

    # Find the count of total number of zeros
    cnt = arr.count(0)

    # Variable to store index where elements
    # will be written in the final array
    write_idx = N + cnt - 1

    # Variable to point the current index
    curr = N - 1

    while (curr >= 0 and write_idx >= 0):

        # Keep the current element to its correct
        # position, if that is within the size N
        if (write_idx < N):
            arr[write_idx] = arr[curr]

        write_idx -= 1

        # Check if the current element is also
        # zero then again write its duplicate
        if (arr[curr] == 0):
            if (write_idx < N):
                arr[write_idx] = 0

            write_idx -= 1

        curr -= 1

    # Return the final result
    return arr

# Driver Code
arr = [ 1, 0, 2, 3, 0, 4, 5, 0 ]

ans = duplicateZeros(arr)
for i in range(len(ans)):
    print(ans[i], end = " ")

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to update
// each entry of zero with two zero
// entries adjacent to each other
using System;

class GFG{

// Function to update each
// entry of zero with two zero
// entries adjacent to each other
static int[] duplicateZeros(int []arr)
{
    int N = arr.Length;

    // Find the count of
    // total number of zeros
    int cnt = count(arr, 0);

    // Variable to store index
    // where elements will be
    // written in the readonly array
    int write_idx = N + cnt - 1;

    // Variable to point the
    // current index
    int curr = N - 1;

    while (curr >= 0 && write_idx >= 0)
    {

        // Keep the current element
        // to its correctposition, if
        // that is within the size N
        if (write_idx < N)
            arr[write_idx] = arr[curr];

        write_idx -= 1;

        // Check if the current element is also
        // zero then again write its duplicate
        if (arr[curr] == 0)
        {
            if (write_idx < N)
                arr[write_idx] = 0;

            write_idx -= 1;
        }
        --curr;
    }

    // Return the readonly result
    return arr;
}

static int count(int []arr, int num)
{
    int ans = 0;
    foreach(int i in arr)
    {
        if(i == num)
           ans++;
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 2, 3, 0, 4, 5, 0 };
    int []ans = duplicateZeros(arr);

    for(int i = 0; i < ans.Length; i++)
       Console.Write(ans[i] + " ");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript implementation to update each entry of zero
// with two zero entries adjacent to each other

// Function to update each entry of zero
// with two zero entries adjacent to each other
function duplicateZeros(arr)
{
    const N = arr.length;

    // Find the count of total number of zeros
    let cnt = 0;
    for(let i = 0; i < arr.length; ++i){
        if(arr[i] == 0)
            cnt++;
    }

    // Variable to store index where elements
    // will be written in the final array
    let write_idx = N + cnt - 1;

    // Variable to point the current index
    let curr = N - 1;

    while (curr >= 0 && write_idx >= 0) {
        // Keep the current element to its correct
        // position, if that is within the size N
        if (write_idx < N)
            arr[write_idx] = arr[curr];

        write_idx -= 1;

        // Check if the current element is also
        // zero then again write its duplicate
        if (arr[curr] == 0) {
            if (write_idx < N)
                arr[write_idx] = 0;

            write_idx -= 1;
        }

        --curr;
    }

    // Return the final result
    return arr;
}

// Driver code
    let arr = [ 1, 0, 2, 3, 0, 4, 5, 0 ];

    let ans = duplicateZeros(arr);

    for (let i = 0; i < ans.length; i++)
        document.write(ans[i] + " ");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
1 0 0 2 3 0 0 4
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*