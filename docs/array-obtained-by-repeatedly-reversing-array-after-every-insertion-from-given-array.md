# 从给定数组中每次插入后通过重复反转数组获得的数组

> 原文:[https://www . geeksforgeeks . org/array-通过从给定数组每次插入后重复反转数组获得/](https://www.geeksforgeeks.org/array-obtained-by-repeatedly-reversing-array-after-every-insertion-from-given-array/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是将**arr【】**的元素一个一个地插入到一个初始为空的数组中，比如说**arr 1【】**，每次插入后[反转数组**arr 1【】**](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 4 2 1 3
> **解释:**
> 对数组 arr1[]执行的操作如下:
> **步骤 1:** 将 1 追加到数组中并反转。arr1[] = {1}
> **第 2 步:**将 2 追加到数组中并反转。arr1[] = {2，1}
> **第 3 步:**将 3 追加到数组中并反转。arr1[] = {3，1，2}
> **步骤 3:** 将 4 追加到数组中并反转。arr1[] = {4，2，1，3}
> 
> **输入:** arr[] = {1，2，3}
> **输出:** 3 1 2
> **解释:**
> 对数组 arr1[]执行的操作如下:
> **步骤 1:** 将 1 追加到数组中并反转。arr1[] = {1}
> **第 2 步:**将 2 追加到数组中并反转。arr1[] = {2，1}
> **第 3 步:**将 3 追加到数组中并反转。arr1[] = {3，1，2}

**天真法:**解决问题最简单的方法是[迭代数组**arr【】**T5】并在每次插入后将 arr【】的每个元素逐一插入数组**arr 1【】**和](https://www.geeksforgeeks.org/iterating-arrays-java/)[反向数组**arr 1【】**T11】。](https://www.geeksforgeeks.org/reverse-an-array-in-java/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是使用[双端队列(Deque)](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/) 在两端追加元素。按照以下步骤解决问题:

*   初始化一个[双端队列](https://www.geeksforgeeks.org/deque-cpp-stl/)，用于存储转换后数组的元素。
*   [迭代数组的元素](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**，如果元素的索引和元素的长度具有相同的奇偶性，则将元素推到德格的[前面。否则，将其推到德清](https://www.geeksforgeeks.org/dequefront-dequeback-c-stl/)的[后面。](https://www.geeksforgeeks.org/dequefront-dequeback-c-stl/)
*   最后，在完成数组**arr【】**的[迭代后，按照输出的要求排列打印出德格的内容。](https://www.geeksforgeeks.org/iterating-arrays-java/)

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate the array by
// inserting array elements one by one
// followed by reversing the array
void generateArray(int arr[], int n)
{

    // Doubly ended Queue
    deque<int> ans;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        // Push array elements
        // alternately to the front
        // and back
        if (i & 1)
            ans.push_front(arr[i]);
        else
            ans.push_back(arr[i]);
    }

    // If size of list is odd
    if (n & 1) {

        // Reverse the list
        reverse(ans.begin(),
                ans.end());
    }

    // Print the elements
    // of the array
    for (auto x : ans) {
        cout << x << " ";
    }
    cout << endl;
}

// Driver Code
int32_t main()
{
    int n = 4;
    int arr[n] = { 1, 2, 3, 4 };
    generateArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to generate the array by
// inserting array elements one by one
// followed by reversing the array
static void generateArray(int arr[], int n)
{

    // Doubly ended Queue
    Deque<Integer> ans = new LinkedList<>();

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {

        // Push array elements
        // alternately to the front
        // and back
        if ((i & 1) != 0)
            ans.addFirst(arr[i]);
        else
            ans.add(arr[i]);
    }

    // If size of list is odd
    if ((n & 1) != 0)
    {

        // Reverse the list
        Collections.reverse(Arrays.asList(ans));
    }

    // Print the elements
    // of the array
    for(int x : ans)
    {
        System.out.print(x + " ");
    }
    System.out.println();
}

// Driver Code
public static void main (String[] args)
{
    int n = 4;
    int arr[] = { 1, 2, 3, 4 };

    generateArray(arr, n);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program of the above approach
from collections import deque

# Function to generate the array by
# inserting array elements one by one
# followed by reversing the array
def generateArray(arr, n):

    # Doubly ended Queue
    ans = deque()

    # Iterate over the array
    for i in range(n):

        # Push array elements
        # alternately to the front
        # and back
        if (i & 1 != 0):
            ans.appendleft(arr[i])
        else:
            ans.append(arr[i])

    # If size of list is odd
    if (n & 1 != 0):

        # Reverse the list
        ans.reverse()

    # Print the elements
    # of the array
    for x in ans:
        print(x, end = " ")

    print()

# Driver Code
n = 4
arr = [ 1, 2, 3, 4 ]

generateArray(arr, n)

# This code is contributed by code_hunt
```

## C#

```
// C# program of
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to generate the array
// by inserting array elements
// one by one followed by
// reversing the array
static void generateArray(int []arr,
                          int n)
{   
  // Doubly ended Queue
  List<int> ans = new List<int>();

  // Iterate over the array
  for(int i = 0; i < n; i++)
  {
    // Push array elements
    // alternately to the front
    // and back
    if ((i & 1) != 0)
      ans.Insert(0, arr[i]);
    else
      ans.Add(arr[i]);
  }

  // If size of list is odd
  if ((n & 1) != 0)
  {
    // Reverse the list
    ans.Reverse();
  }

  // Print the elements
  // of the array
  foreach(int x in ans)
  {
    Console.Write(x + " ");
  }
  Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
  int n = 4;
  int []arr = {1, 2, 3, 4};
  generateArray(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to generate the array by
// inserting array elements one by one
// followed by reversing the array
function generateArray(arr, n)
{

    // Doubly ended Queue
    var ans = [];

    // Iterate over the array
    for (var i = 0; i < n; i++) {

        // Push array elements
        // alternately to the front
        // and back
        if (i & 1)
            ans.splice(0,0,arr[i]);
        else
            ans.push(arr[i]);
    }

    // If size of list is odd
    if (n & 1) {

        // Reverse the list
        ans.reverse();
    }

    // Print the elements
    // of the array
    ans.forEach(x => {

        document.write( x + " ");
    });
}

// Driver Code
var n = 4;
var arr =  [1, 2, 3, 4];
generateArray(arr, n);

</script>
```

**Output:** 

```
4 2 1 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)