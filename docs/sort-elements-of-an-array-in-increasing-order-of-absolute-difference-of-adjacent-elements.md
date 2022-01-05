# 按照相邻元素绝对差的递增顺序对数组的元素进行排序

> 原文:[https://www . geeksforgeeks . org/按相邻元素绝对差递增顺序对数组元素进行排序/](https://www.geeksforgeeks.org/sort-elements-of-an-array-in-increasing-order-of-absolute-difference-of-adjacent-elements/)

给定一个数组 **arr[]** ，任务是以相邻元素之间的绝对差按递增顺序排列数组。

**示例:**

> **输入:** arr[] = {8，1，2，3，0}
> **输出:**2 3 1 8 0
> T6】解释:
> |2-3| = 1，|3-1| = 2，|1-8| = 7，|8-0| = 8
> 相邻元素的绝对差按递增顺序排列。
> 
> **输入:** -1 -2 3 4 5
> **输出:** 3 4 -1 5 -2
> **解释:**
> |3-4| = 1，|4-(-1)| = 5，|-1-5| = 6，|5-(-2)| = 7

**做法:**思路是先对数组的元素进行排序，然后取数组的中间元素，再重复这一步，直到数组不为空。下面通过一个例子说明了这种方法:

```
Given Array be - {8, 1, 2, 3, 0}

After Sorting the array - {0, 1, 2, 3, 8}

     Array          Middle Ele     Output Array
---------------    -------------  ---------------
{0, 1, 2, 3, 8}    5//2 = 2, 2          2
{0, 1, 3, 8}       4//2 = 2, 3        2, 3
{0, 1, 8}          3//2 = 1, 1       1, 2, 3
{0, 8}             2//2 = 1, 8      1, 2, 3, 8
{0}                1//2 = 0, 0     1, 2, 3, 8, 0
```

## C++

```
// C++ implementation to sort
// the elements of the array in
// such a way that absolute
// difference between the adjacent
// elements are in increasing order
#include<bits/stdc++.h>
using namespace std;

// Function to sort the elements
// of the array by difference
void sortDiff(vector<int> arr,
              int n)
{  
    // Sorting the array
    sort(arr.begin(), arr.end());

    // Array to store the
    // elements of the array
    vector<int> out;

    // Iterating over the length
    // of the array to include
    // each middle element of array
    while(n > 0)
    {     
        // Appending the middle
        // element of the array
        out.push_back(arr[n / 2]);
        arr.erase(arr.begin() + n / 2);
        n = n - 1;
    }
    for(auto i : out)
        cout << i << " ";
}

// Driver Code
int main()
{
  vector<int> a = {8, 1, 2, 3, 0};
  int n = 5;
  sortDiff(a, n);
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort
// the elements of the array in
// such a way that absolute
// difference between the adjacent
// elements are in increasing order
import java.util.*;

class GFG{

// Function to sort the elements
// of the array by difference
static void sortDiff(Vector<Integer> arr, int n)
{

    // Sorting the array
    Collections.sort(arr);

    // Array to store the
    // elements of the array
    Vector<Integer> out = new Vector<Integer>();

    // Iterating over the length
    // of the array to include
    // each middle element of array
    while(n > 0)
    {

        // Appending the middle
        // element of the array
        out.add(arr.get(n / 2));
        arr.remove(n / 2);
        n = n - 1;
    }
    for(int i : out)
        System.out.print(i + " ");
}

// Driver Code
public static void main(String[] args)
{
    Integer []a = { 8, 1, 2, 3, 0 };
    Vector<Integer> arr = new Vector<Integer>(Arrays.asList(a));
    int n = 5;
    sortDiff(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation to sort
# the elements of the array in
# such a way that absolute
# difference between the adjacent
# elements are in increasing order

# Function to sort the elements
# of the array by difference
def sortDiff(arr, n):

    # Sorting the array
    arr.sort()

    # Array to store the
    # elements of the array
    out = []

    # Iterating over the length
    # of the array to include
    # each middle element of array
    while n:

        # Appending the middle
        # element of the array
        out.append(arr.pop(n//2))
        n=n-1

    print(*out)
    return out

# Driver Code
if __name__ == "__main__":
    arr = [8, 1, 2, 3, 0]

    n = 5
    sortDiff(arr, n)
```

## C#

```
// C# implementation to sort
// the elements of the array in
// such a way that absolute
// difference between the adjacent
// elements are in increasing order
using System;
using System.Collections.Generic;
class GFG{

// Function to sort the elements
// of the array by difference
static void sortDiff(List<int> arr, int n)
{

    // Sorting the array
    arr.Sort();

    // Array to store the
    // elements of the array
    List<int> Out = new List<int>();

    // Iterating over the length
    // of the array to include
    // each middle element of array
    while(n > 0)
    {

        // Appending the middle
        // element of the array
        Out.Add(arr[n / 2]);
        arr.RemoveAt(n / 2);
        n = n - 1;
    }
    foreach(int i in Out)
        Console.Write(i + " ");
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 8, 1, 2, 3, 0 };
    List<int> arr = new List<int>(a);
    int n = 5;
    sortDiff(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript implementation to sort
// the elements of the array in
// such a way that absolute
// difference between the adjacent
// elements are in increasing order

// Function to sort the elements
// of the array by difference
function sortDiff(arr,n)
{
    // Sorting the array
    arr.sort(function(a,b){return a-b;});

    // Array to store the
    // elements of the array
    let out = [];

    // Iterating over the length
    // of the array to include
    // each middle element of array
    while(n > 0)
    {

        // Appending the middle
        // element of the array
        out.push(arr[Math.floor(n / 2)]);
        arr.splice(Math.floor(n / 2),1);
        n = n - 1;
    }
    for(let i=0;i< out.length;i++)
        document.write(out[i] + " ");
}

// Driver Code
let arr=[8, 1, 2, 3, 0 ];
let n = 5;
sortDiff(arr, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2 3 1 8 0
```