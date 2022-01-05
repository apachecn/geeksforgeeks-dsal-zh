# 大小为 K 的最大连续子阵列

> 原文:[https://www . geesforgeks . org/maximum-continuous-sub-array-of-size-k/](https://www.geeksforgeeks.org/greatest-contiguous-sub-array-of-size-k/)

给定一个整数数组 **arr[]** 和一个整数 **K** ，任务是找到大小最大的连续子数组 **K** 。如果两个子阵列中的第一个非匹配元素在 **X** 中的值大于在 **Y** 中的值，则称子阵列 **X** 大于子阵列 **Y** 。

**示例:**

> **输入:** arr[] = {1，4，3，2，5}，K = 4
> **输出:** 4 3 2 5
> 两个子阵分别为{1，4，3，2}和{4，3，2，5}。
> 因此，较大的一个是{4，3，2，5}
> 
> **输入:** arr[] = {1，9，2，7，9，3}，K = 3
> T3】输出: 9 2 7

**方法:**生成所有大小为 **K** 的子数组，并将它们存储在任何数据结构中。对所有子数组进行排序，答案将是排序后的数据结构中的最后一个子数组。在 C++中，我们可以使用向量的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储大小为 **K** 的子数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the sub-array
vector<int> findSubarray(int a[], int k, int n)
{

    // Data-structure to store all
    // the sub-arrays of size K
    vector<vector<int> > vec;

    // Iterate to find all the sub-arrays
    for (int i = 0; i < n - k + 1; i++) {
        vector<int> temp;

        // Store the sub-array elements in the array
        for (int j = i; j < i + k; j++) {
            temp.push_back(a[j]);
        }

        // Push the vector in the container
        vec.push_back(temp);
    }

    // Sort the vector of elements
    sort(vec.begin(), vec.end());

    // The last sub-array in the sorted order
    // will be the answer
    return vec[vec.size() - 1];
}

// Driver code
int main()
{
    int a[] = { 1, 4, 3, 2, 5 };
    int k = 4;
    int n = sizeof(a) / sizeof(a[0]);

    // Get the sub-array
    vector<int> ans = findSubarray(a, k, n);

    for (auto it : ans)
        cout << it << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function that returns the sub-array
static ArrayList<Integer> findSubarray(int a[],
                                       int k, int n)
{

    // Data-structure to store all
    // the sub-arrays of size K
    ArrayList<
    ArrayList<Integer>> vec = new ArrayList<
                                  ArrayList<Integer>>();

    // Iterate to find all the sub-arrays
    for(int i = 0; i < n - k + 1; i++)
    {
        ArrayList<Integer> temp = new ArrayList<Integer>();

        // Store the sub-array elements in the array
        for(int j = i; j < i + k; j++)
        {
            temp.add(a[j]);
        }

        // Push the vector in the container
        vec.add(temp);
    }

     // Sort the vector of elements
    Collections.sort(vec, new Comparator<ArrayList<Integer>>()
    {   
        @Override
        public int compare(ArrayList<Integer> o1,
                           ArrayList<Integer> o2)
        {
            return o1.get(0).compareTo(o2.get(0));
        }              
    });

    // The last sub-array in the sorted order
    // will be the answer
    return vec.get(vec.size() - 1);
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 4, 3, 2, 5 };
    int k = 4;
    int n = a.length;

    // Get the sub-array
    ArrayList<Integer> ans = findSubarray(a, k, n);

    for(int it: ans)
    {
        System.out.print(it + " ");
    }
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the sub-array
def findSubarray(a, k, n):

    # Data-structure to store all
    # the sub-arrays of size K
    vec=[]

    # Iterate to find all the sub-arrays
    for i in range(n-k+1):
        temp=[]

        # Store the sub-array elements in the array
        for j in range(i,i+k):
            temp.append(a[j])

        # Push the vector in the container
        vec.append(temp)

    # Sort the vector of elements
    vec=sorted(vec)

    # The last sub-array in the sorted order
    # will be the answer
    return vec[len(vec) - 1]

# Driver code

a =[ 1, 4, 3, 2, 5 ]
k = 4
n = len(a)

# Get the sub-array
ans = findSubarray(a, k, n)

for it in ans:
    print(it,end=" ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG
{

  // Function that returns the sub-array
  static List<int> findSubarray(int[] a, int k, int n)
  {
    // Data-structure to store all
    // the sub-arrays of size K
    List<List<int>> vec = new List<List<int>>();

    // Iterate to find all the sub-arrays
    for(int i = 0; i < n - k + 1; i++)
    {
      List<int> temp = new List<int>();

      // Store the sub-array elements in the array
      for(int j = i; j < i + k; j++)
      {
        temp.Add(a[j]);
      }

      // Push the vector in the container
      vec.Add(temp);
    }

    // Sort the vector of elements
    vec.OrderBy( l => l[0]);

    // The last sub-array in the sorted order
    // will be the answer
    return vec[vec.Count - 1];
  }

  // Driver code
  static public void Main (){
    int[] a = { 1, 4, 3, 2, 5 };
    int k = 4;
    int n = a.Length;

    // Get the sub-array
    List<int> ans = findSubarray(a, k, n);
    foreach(int it in ans)
    {
      Console.Write(it + " ");
    }
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns the sub-array
function findSubarray(a, k, n)
{

    // Data-structure to store all
    // the sub-arrays of size K
    var vec = [];

    // Iterate to find all the sub-arrays
    for (var i = 0; i < n - k + 1; i++) {
        var temp = [];

        // Store the sub-array elements in the array
        for (var j = i; j < i + k; j++) {
            temp.push(a[j]);
        }

        // Push the vector in the container
        vec.push(temp);
    }

    // Sort the vector of elements
    vec.sort()

    // The last sub-array in the sorted order
    // will be the answer
    return vec[vec.length - 1];
}

// Driver code
var a = [1, 4, 3, 2, 5];
var k = 4;
var n = a.length;

// Get the sub-array
var ans = findSubarray(a, k, n);
ans.forEach(it => {
    document.write(it+ " ")
});

// This coe is contributed by noob2000.
</script>
```

**Output:** 

```
4 3 2 5
```