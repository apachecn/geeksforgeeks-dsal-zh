# 阵列对的长度，其中一个包含所有不同的元素，另一个包含所有相同的元素

> 原文:[https://www . geeksforgeeks . org/数组对长度-其中一个包含所有不同的元素和其他所有相同的元素/](https://www.geeksforgeeks.org/length-of-array-pair-formed-where-one-contains-all-distinct-elements-and-other-all-same-elements/)

给定一个数组 **arr[]** ，任务是确定使用给定数组元素可以创建的两个相同大小的数组的最大可能大小，这样在一个数组中所有元素都是**不同的**，而在另一个数组中，所有元素都是**相同的**。
***注意:**不是强制使用给定数组的所有元素来构建这两个数组。*

**示例:**

> **输入:** a[] = {4，2，4，1，4，3，4}
> **输出:** 3
> **解释:**
> 最大可能大小为 3 –{ 1 2 3 }和{4 4 4}
> 
> **输入:** a[] = {2，1，5，4，3}
> **输出:** 1
> **解释:**
> 最大可能大小为 1 –{ 1 }和{2}

**方法:**要解决上述问题，请按照下面给出的步骤操作:

*   首先，计算给定数组中所有数字的出现频率，并计算该数组中不同元素的数量。然后统计其中最大频率 *maxfrq*
*   很明显，一个数组(包含相同元素)的最大可能大小是 maxfrq，因为它是一个数的频率的最高可能值。并且，另一个数组(包含所有不同元素)的最大可能大小是 dist，这是不同元素的总数。现在我们必须考虑两种情况:
    1.  如果我们在一个数组中取所有具有频率 maxfrq 的元素(包含相同的元素)，那么剩下的不同元素的总数将是*dist–1*，所以另一个数组只能包含 dist–1 数量的元素。在这种情况下，答案是，**ans1 = min(dist–1，maxfrq)**
    2.  如果我们取除了一个数组中的一个元素(包含相同的元素)之外的所有具有频率 maxfrq 的元素，那么剩下的不同元素的总数将是 dist，所以另一个数组只能包含 dist 数量的元素。在这种情况下，答案是， **ans2 = min(dist，maxfrq–1)**。
*   因此，实际的答案是

> 最大值(距离–1、maxfrq)、最小值(距离、max frq–1)

*   下面是上述方法的实现:

## C++

```
// C++ implementation to Divide the array
// into two arrays having same size,
// one with distinct elements
// and other with same elements

#include <bits/stdc++.h>
using namespace std;

// Function to find the max size possible
int findMaxSize(int a[], int n)
{
    vector<int> frq(n + 1);

    for (int i = 0; i < n; ++i)
        frq[a[i]]++;

    // Counting the maximum frequency
    int maxfrq
        = *max_element(
            frq.begin(), frq.end());

    // Counting total distinct elements
    int dist
        = n + 1 - count(
                      frq.begin(),
                      frq.end(), 0);

    int ans1 = min(maxfrq - 1, dist);

    int ans2 = min(maxfrq, dist - 1);

    // Find max of both the answer
    int ans = max(ans1, ans2);

    return ans;
}

// Driver code
int main()
{

    int arr[] = { 4, 2, 4, 1, 4, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMaxSize(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Divide the array
// into two arrays having same size,
// one with distinct elements
// and other with same elements
import java.io.*;
import java.util.*;

class GFG {

// Function to find the max size possible
static int findMaxSize(int a[], int n)
{
    ArrayList<Integer> frq = new ArrayList<Integer>(n+1);

    for(int i = 0; i <= n; i++)
       frq.add(0);

    for(int i = 0; i < n; ++i)
       frq.set(a[i], frq.get(a[i]) + 1);

    // Counting the maximum frequency
    int maxfrq = Collections.max(frq);

    // Counting total distinct elements
    int dist = n + 1 - Collections.frequency(frq, 0);

    int ans1 = Math.min(maxfrq - 1, dist);
    int ans2 = Math.min(maxfrq, dist - 1);

    // Find max of both the answer
    int ans = Math.max(ans1, ans2);

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 2, 4, 1, 4, 3, 4 };
    int n = arr.length;

    System.out.println(findMaxSize(arr, n));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 implementation to divide the 
# array into two arrays having same 
# size, one with distinct elements
# and other with same elements

# Function to find the max size possible
def findMaxSize(a, n):

    frq = [0] * (n + 1)

    for i in range(n):
        frq[a[i]] += 1

    # Counting the maximum frequency
    maxfrq = max(frq)

    # Counting total distinct elements
    dist = n + 1 - frq.count(0)
    ans1 = min(maxfrq - 1, dist)
    ans2 = min(maxfrq, dist - 1)

    # Find max of both the answer
    ans = max(ans1, ans2)

    return ans

# Driver code
arr = [ 4, 2, 4, 1, 4, 3, 4 ]
n = len(arr)

print(findMaxSize(arr, n))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to Divide the array
// into two arrays having same size,
// one with distinct elements
// and other with same elements
using System;
using System.Collections;
class GFG{

// Function to find the max size possible
static int findMaxSize(int []a, int n)
{
  ArrayList frq = new ArrayList(n + 1);

  for(int i = 0; i <= n; i++)
    frq.Add(0);

  for(int i = 0; i < n; ++i)
    frq[a[i]] = (int)frq[a[i]] + 1;

  // Counting the maximum frequency
  int maxfrq = int.MinValue;
  for(int i = 0; i < frq.Count; i++)
  {
    if(maxfrq < (int)frq[i])
    {
      maxfrq = (int)frq[i];
    }
  }

  // Counting total distinct elements
  int dist = n + 1;
  for(int i = 0; i < frq.Count; i++)
  {
    if((int)frq[i] == 0)
    {
      dist--;
    }
  }

  int ans1 = Math.Min(maxfrq - 1, dist);
  int ans2 = Math.Min(maxfrq, dist - 1);

  // Find max of both the answer
  int ans = Math.Max(ans1, ans2);

  return ans;
}

// Driver code
public static void Main(string[] args)
{
  int []arr = {4, 2, 4, 1, 4, 3, 4};
  int n = arr.Length;
  Console.Write(findMaxSize(arr, n));
}
}

// This code is contributed by Rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to Divide the array
// into two arrays having same size,
// one with distinct elements
// and other with same elements

// Function to find the max size possible
function findMaxSize(a, n)
{
    var frq = Array(n + 1).fill(0);

    for (var i = 0; i < n; ++i)
        frq[a[i]]++;

    // Counting the maximum frequency
    var maxfrq = frq.reduce((a,b)=>Math.max(a,b))

    // Counting total distinct elements
    var dist
        = n + 1 - frq.filter(x=> x ==0).length;

    var ans1 = Math.min(maxfrq - 1, dist);

    var ans2 = Math.min(maxfrq, dist - 1);

    // Find max of both the answer
    var ans = Math.max(ans1, ans2);

    return ans;
}

// Driver code
var arr = [4, 2, 4, 1, 4, 3, 4];
var n = arr.length;
document.write( findMaxSize(arr, n));

</script>
```

**Output:** 

```
3
```