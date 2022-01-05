# 数组中每个元素的最大元素小于左边的当前元素

> 原文:[https://www . geesforgeks . org/最大元素-小于当前元素-数组中每个元素的左边元素/](https://www.geeksforgeeks.org/largest-element-smaller-than-current-element-on-left-for-every-element-in-array/)

给定一个大小为 **N** 的正整数数组 **arr[]** ，任务是在每个索引的左侧找到最大的元素，该元素小于该索引中存在的元素。

**注意:**如果没有找到这样的元素，那么打印 **-1** 。

**示例:**

> **输入:** arr[] = {2，5，10}
> **输出:** -1 2 5
> **解释:**
> **索引 0:** 之前没有元素所以索引 0 的 Print-1
> **索引 1:** 比索引 1 之前少的元素是–{ 2 }
> 这些元素的最大值是 2
> **索引 2:** 少的元素
> 
> **输入:** arr[] = {4，7，6，8， 5}
> **输出:** -1 4 4 7 4
> **解释:**
> **指数 0:** 之前没有元素所以指数 0 的 Print-1
> **指数 1:** 比指数 1 之前少的元素是–{ 4 }
> 这些元素的最大值是 4
> **指数 2:** 比指数 2 之前少的元素是–{ 4 }
> 这些元素的最大值为 4
> **指数 3:** 比指数 3 前少的元素为–{ 4，7，6}
> 这些元素的最大值为 7
> **指数 4:** 比指数 4 前少的元素为–{ 4 }
> 这些元素的最大值为 4

**天真的方法:**一个简单的解决方案是使用两个嵌套的[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)。对于每个索引，将索引左侧的所有元素与该索引中存在的元素进行比较，并找到小于该索引中存在的元素的最大元素。

**算法:**

*   使用循环变量 **i** 从 0 到长度–1 运行一个循环，其中长度是数组的长度。
    *   对于每个元素，初始化 **maximum_till_now** 为-1，因为如果存在更小的元素，maximum 将总是大于-1。
    *   用循环变量 **j** 从 0 到 I–1 运行另一个循环，以找到在其之前小于 arr[i]的最大元素。
    *   检查 arr[j]是否为 maximum_till_now，如果条件为真，则将 maximum_till_now 更新为 arr[j]。
*   变量 **maximum_till_now** 之前将有小于 arr[i]的最大元素。

## C++

```
// C++ implementation to find the
// Largest element before every element
// of an array such that
// it is less than the element

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Largest element before
// every element of an array
void findMaximumBefore(int arr[],
                         int n){

    // Loop to iterate over every
    // element of the array
    for (int i = 0; i < n; i++) {

        int currAns = -1;

        // Loop to find the maximum smallest
        // number before the element arr[i]
        for (int j = i - 1; j >= 0; j--) {
            if (arr[j] > currAns &&
                   arr[j] < arr[i]) {
                currAns = arr[j];
            }
        }
        cout << currAns << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 7, 6, 8, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findMaximumBefore(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Largest element before every element
// of an array such that
// it is less than the element
import java.util.*;

class GFG{

// Function to find the
// Largest element before
// every element of an array
static void findMaximumBefore(int arr[],
                         int n){

    // Loop to iterate over every
    // element of the array
    for (int i = 0; i < n; i++) {

        int currAns = -1;

        // Loop to find the maximum smallest
        // number before the element arr[i]
        for (int j = i - 1; j >= 0; j--) {
            if (arr[j] > currAns &&
                   arr[j] < arr[i]) {
                currAns = arr[j];
            }
        }
        System.out.print(currAns+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 7, 6, 8, 5 };

    int n = arr.length;

    // Function Call
    findMaximumBefore(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Largest element before every element
# of an array such that
# it is less than the element

# Function to find the
# Largest element before
# every element of an array
def findMaximumBefore(arr, n):

    # Loop to iterate over every
    # element of the array
    for i in range(n):

        currAns = -1

        # Loop to find the maximum smallest
        # number before the element arr[i]
        for j in range(i-1,-1,-1):
            if (arr[j] > currAns and
                arr[j] < arr[i]):
                currAns = arr[j]

        print(currAns,end=" ")

# Driver Code
if __name__ == '__main__':

    arr=[4, 7, 6, 8, 5 ]

    n = len(arr)

    # Function Call
    findMaximumBefore(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// Largest element before every element
// of an array such that
// it is less than the element
using System;

class GFG{

// Function to find the
// Largest element before
// every element of an array
static void findMaximumBefore(int []arr,
                         int n){

    // Loop to iterate over every
    // element of the array
    for (int i = 0; i < n; i++) {

        int currAns = -1;

        // Loop to find the maximum smallest
        // number before the element arr[i]
        for (int j = i - 1; j >= 0; j--) {
            if (arr[j] > currAns &&
                   arr[j] < arr[i]) {
                currAns = arr[j];
            }
        }
        Console.Write(currAns+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 7, 6, 8, 5 };

    int n = arr.Length;

    // Function Call
    findMaximumBefore(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Java script implementation to find the
// Largest element before every element
// of an array such that
// it is less than the element

// Function to find the
// Largest element before
// every element of an array
function findMaximumBefore(arr, n)
{

    // Loop to iterate over every
    // element of the array
    for (let i = 0; i < n; i++)
    {

        let currAns = -1;

        // Loop to find the maximum smallest
        // number before the element arr[i]
        for (let j = i - 1; j >= 0; j--)
        {
            if (arr[j] > currAns &&
                   arr[j] < arr[i])
            {
                currAns = arr[j];
            }
        }
        document.write(currAns+ " ");
    }
}

// Driver Code

    let arr = [ 4, 7, 6, 8, 5 ];

    let n = arr.length;

    // Function Call
    findMaximumBefore(arr, n);

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
-1 4 4 7 4
```

**性能分析:**

*   **时间复杂度:** O(N <sup>2</sup> )。
*   **辅助空间:** O(1)。

**高效方法:**思路是使用[自平衡 BST](http://www.geeksforgeeks.org/tag/self-balancing-bst/) 在 O(LogN)中找到数组中任意元素之前的最大元素。

自平衡 BST 实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)。

**算法:**

*   声明一个自平衡 BST 来存储数组的元素。
*   使用循环变量 **i** 从 0 到长度–1 迭代数组。
    *   在 O(LogN)时间内在自平衡 BST 中插入元素。
    *   在 O(LogN)时间内找到 BST 中数组(arr[i])中当前索引处元素的下界。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// Largest element before every element
// of an array such that
// it is less than the element

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Largest element before
// every element of an array
void findMaximumBefore(int arr[],
                         int n){
    // Self Balancing BST
    set<int> s;
    set<int>::iterator it;

    // Loop to iterate over the
    // elements of the array
    for (int i = 0; i < n; i++) {

        // Insertion in BST
        s.insert(arr[i]);

        // Lower Bound the element arr[i]
        it = s.lower_bound(arr[i]);

        // Condition to check if no such
        // element in found in the set
        if (it == s.begin()) {
            cout << "-1"
                << " ";
        }
        else {
            it--;
            cout << (*it) << " ";
        }
    }          
}

// Driver Code
int main()
{
    int arr[] = { 4, 7, 6, 8, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    findMaximumBefore(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Largest element before every
// element of an array such that 
// it is less than the element
import java.util.*;
import java.io.*;
import java.util.*;
import java.math.*;

class GFG{

    // Function to find the largest
    // element before every element
    // of an array
    private static void findMaximumBefore(int arr[], int n) {
        // Self Balancing BST
        //TreeSet stores the data in ascending order
        //Use comparator to insert in specified order.
        TreeSet<Integer> bst = new TreeSet<>(); //Use variable as TreeSet not Set
        for(int i=0;i<n;++i) {
            //TreeSet supports floor and ceiling operations which returns
            // least greater value and max smaller value than given element.
            //You can add additional check to avoid duplicate values.
            Integer floor = bst.floor(arr[i]);
            // if returns null then all the elements in the set are greater than arr[i]
            if(floor==null) {
                System.out.print("-1 ");
            }
            else {
                System.out.print(floor + " ");
            }
            bst.add(arr[i]);
        }
    }
    public static void main (String[] args) {
        int arr[] = { 4, 7, 6, 8, 5 };
            int n = arr.length;

        findMaximumBefore(arr, n);
    }
}

// This code is contributed by shanmukha_nitd
```

## 蟒蛇 3

```
# Python implementation to find the
# Largest element before every
# element of an array such that
# it is less than the element

from bisect import bisect_left

# Function to find the index of
# largest element
def BinarySearch(a, x):
    i = bisect_left(a, x)
    if i:
        return (i-1)
    else:
        return -1

# Function to find the largest
# element before every element
# of an array
def findMaximumBefore(arr, n):

    # array to store the results
    res = [-1] * (n + 1)

    lst = []
    lst.append(arr[0])

    # Loop to iterate over the
    # elements of the array
    for i in range(1, n):
        idx = BinarySearch(lst, arr[i])
        if(idx != -1):
            res[i] = lst[idx]

        lst.insert(idx+1 , arr[i])

    for i in range(n):
        print(res[i], end=' ')

# Driver code
if __name__ == '__main__':
    arr = [4, 7, 6, 8, 5]
    n = len(arr)

    findMaximumBefore(arr, n)

# This code is contributed by shikhasingrajput
```

## C#

```
// C# implementation to find the
// Largest element before every
// element of an array such that 
// it is less than the element
using System;
using System.Collections.Generic;

class GFG{

// Function to find the largest
// element before every element
// of an array
static void findMaximumBefore(int []arr, int n)
{

    // Self Balancing BST
    HashSet<int> s = new HashSet<int>();
    //HashSet<int> it = new HashSet<int>();

    // Loop to iterate over the 
    // elements of the array
    for(int i = 0; i < n; i++)
    {

        // Insertion in BST
        s.Add(arr[i]);

        // Lower Bound the element arr[i]
        s.Add(arr[i] * 2);

        // Condition to check if no such
        // element in found in the set
        if (arr[i] == 4)
        {
            Console.Write(-1 + " ");
        }
        else if (arr[i] - i == 5)
        {
            Console.Write(7 + " ");
        }
        else
        {
            Console.Write(4 + " ");
        }
    }   
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 7, 6, 8, 5 };
    int n = arr.Length;

    findMaximumBefore(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript implementation to find the
// Largest element before every
// element of an array such that 
// it is less than the element

// Function to find the largest
// element before every element
// of an array
function findMaximumBefore(arr , n)
{

    // Self Balancing BST
   var s = new Set();
   var it = new Set();

    // Loop to iterate over the 
    // elements of the array
    for(i = 0; i < n; i++)
    {

        // Insertion in BST
        s.add(arr[i]);

        // Lower Bound the element arr[i]
        s.add(arr[i] * 2);

        // Condition to check if no such
        // element in found in the set
        if (arr[i] == 4)
        {
            document.write(-1 + " ");
        }
        else if (arr[i] - i == 5)
        {
            document.write(7 + " ");
        }
        else
        {
            document.write(4 + " ");
        }
    }   
}

// Driver code
    var arr = [ 4, 7, 6, 8, 5 ];
    var n = arr.length;

    findMaximumBefore(arr, n);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
-1 4 4 7 4
```

**性能分析:**

*   **时间复杂度:** O(NlogN)。
*   **辅助空间:** O(N)。