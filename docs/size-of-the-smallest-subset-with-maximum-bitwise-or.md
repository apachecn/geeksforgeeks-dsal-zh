# 具有最大位“或”的最小子集的大小

> 原文:[https://www . geeksforgeeks . org/按位最大或最小子集大小/](https://www.geeksforgeeks.org/size-of-the-smallest-subset-with-maximum-bitwise-or/)

给定一个正整数数组。任务是找到最小子集的大小，使得该集合的**位“或”**为最大可能。

**示例**:

```
Input : arr[] = {5, 1, 3, 4, 2}
Output : 2
7 is the maximum value possible of OR, 
5|2 = 7 and 5|3 = 7

Input : arr[] = {2, 6, 2, 8, 4, 5}
Output : 3
15 is the maximum value of OR and set
elements are 8, 6, 5 
```

**来源** : [校园实习期 Sprinklr](https://www.geeksforgeeks.org/sprinklr-on-campus-internship/)

对具有某个值的数字进行按位“或”运算不会减少其值。它要么保持不变，要么增加。如果我们仔细研究这个问题，我们可以注意到，我们可以得到的最大“或”值是通过对所有数组元素进行按位“或”运算得到的。但这包括所有元素，这里想知道最小的子集。所以我们做以下工作。
I)查找所有数组元素的按位“或”。这就是我们要找的手术室。
II)现在我们需要用这个按位 OR 找到最小的子集。这个问题类似于子集和问题，我们可以用两种方法来解决:

1.  我们生成所有子集，并用给定的或返回最小的大小
2.  我们使用动态规划来解决这个问题。这个解决方案将非常类似于给定总和的[最大尺寸子集](https://www.geeksforgeeks.org/maximum-size-subset-given-sum/)

第一个解的时间复杂度是 O(2 <sup>n</sup> )，动态规划解的时间复杂度是 O(OR * n)，其中 OR 是所有数组元素的 OR，n 是输入数组的大小。

**使用方法 1 :** (生成所有子集并返回给定 OR 的最小大小)

## C++

```
// CPP Code for above approach
#include <bits/stdc++.h>
using namespace std;

// Compute bitwise or of all elements
// in array of size sz
int OR(int data[], int sz)
{
    int mOR = 0;
      for (int i = 0; i < sz; ++i) {
        mOR |= data[i];
    }

      return mOR;
}

// calculate the size of
// minimum subset with maximum or
int minSubset(int data[], int sz,int maxOR)
{
  // store the minimum size of
  // the subset with maximum OR
      int minSZ=sz;

      // generates all subsets
    for(int mask=0;mask<(1<<sz);mask++)
    {
      // stores the size of the current subset
      int curSZ=0;
      // stores the OR of all the elements
      // in the current subset
      int curOR=0;

      for(int i=0;i<sz;i++)
      {
        if(mask&(1<<i))
        {
          curSZ++;
          curOR|=data[i];
        }
      }
      if(curOR==maxOR)
        minSZ=min(minSZ,curSZ);
    }

  return minSZ;
}

// Driver code
int main()
{
    int data[] = { 5, 1, 3, 4, 2 };
    int sz = sizeof(data) / sizeof(0);
    int maxOR = OR(data, sz);

    // Function Call
    cout << minSubset(data, sz,maxOR) << '\n' ;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.io.*;
import java.util.*;

class Solution
{

  // Compute bitwise or of all elements
  // in array of size sz
  private static int OR(int[] arr)
  {
    int mOR = 0;
    for (int i = 0; i < arr.length; ++i)
    {
      mOR |= arr[i];
    }
    return mOR;
  }

  // Recursively calculating the size of
  // minimum subset with maximum or
  private static int maxSubset(int[] arr, int i,
                int curOr, int curSize, int maxOr)
  {

    // If i is arr.length
    if (i == arr.length)
    {

      // If curOr is equal to maxOr
      if (curOr == maxOr)
      {
          return curSize;
      }

      // Return arr.length
      else
      {
          return arr.length;
      }
    }

    // Try the current element in the subset
    int take = maxSubset(arr, i + 1, curOr |
                          arr[i], curSize + 1, maxOr);

    // Skip the current element
    int notTake = maxSubset(arr, i + 1, curOr,
                                      curSize, maxOr);

    // Return minimum of take and notTake
    return Math.min(take, notTake);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] data = {5, 1, 3, 4, 2};

    int maxOr = OR(data);

    // Function Call
    int maxSubsetSize = maxSubset(data, 0, 0, 0, maxOr);
    System.out.println(maxSubsetSize);
  }
}

// Code contributed by Abdelaziz EROUI
```

## C#

```
// C# Program for above approach
using System;
class Solution
{

  // Compute bitwise or of all elements
  // in array of size sz
  private static int OR(int[] arr)
  {
    int mOR = 0;
    for (int i = 0; i < arr.Length; ++i)
    {
      mOR |= arr[i];
    }
    return mOR;
  }

  // Recursively calculating the size of
  // minimum subset with maximum or
  private static int maxSubset(int[] arr, int i,
                int curOr, int curSize, int maxOr)
  {

    // If i is arr.length
    if (i == arr.Length)
    {

      // If curOr is equal to maxOr
      if (curOr == maxOr)
      {
          return curSize;
      }

      // Return arr.length
      else
      {
          return arr.Length;
      }
    }

    // Try the current element in the subset
    int take = maxSubset(arr, i + 1, curOr |
                          arr[i], curSize + 1, maxOr);

    // Skip the current element
    int notTake = maxSubset(arr, i + 1, curOr,
                                      curSize, maxOr);

    // Return minimum of take and notTake
    return Math.Min(take, notTake);
  }

  // Driver Code
  static void Main()
  {
    int[] data = {5, 1, 3, 4, 2};

    int maxOr = OR(data);

    // Function Call
    int maxSubsetSize = maxSubset(data, 0, 0, 0, maxOr);
     Console.WriteLine(maxSubsetSize);
  }
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript Program for above approach

// Compute bitwise or of all elements
  // in array of size sz
function OR(arr)
{
    let mOR = 0;
    for (let i = 0; i < arr.length; ++i)
    {
      mOR |= arr[i];
    }
    return mOR;
}

// Recursively calculating the size of
  // minimum subset with maximum or
function maxSubset(arr,i,curOr,curSize,maxOr)
{
    // If i is arr.length
    if (i == arr.length)
    {

      // If curOr is equal to maxOr
      if (curOr == maxOr)
      {
          return curSize;
      }

      // Return arr.length
      else
      {
          return arr.length;
      }
    }

    // Try the current element in the subset
    let take = maxSubset(arr, i + 1, curOr |
                          arr[i], curSize + 1, maxOr);

    // Skip the current element
    let notTake = maxSubset(arr, i + 1, curOr,
                                      curSize, maxOr);

    // Return minimum of take and notTake
    return Math.min(take, notTake);
}

// Driver Code
let data=[5, 1, 3, 4, 2];
let maxOr = OR(data);

// Function Call
let maxSubsetSize = maxSubset(data, 0, 0, 0, maxOr);
document.write(maxSubsetSize);

// This code is contributed by rag2127

</script>
```

## 蟒蛇 3

```
# Python3 Code for above approach

# Compute bitwise or of all elements
# in array of size sz
def OR(data, sz):
    mOR = 0
    for i in range(sz) :
        mOR |= data[i]

    return mOR

# calculate the size of
# minimum subset with maximum or
def minSubset(data, sz,maxOR):
  # store the minimum size of
  # the subset with maximum OR
    minSZ=sz

    # generates all subsets
    for mask in range(1<<sz):
        # stores the size of the current subset
        curSZ=0
        # stores the OR of all the elements
        # in the current subset
        curOR=0

        for i in range(sz):
            if(mask&(1<<i)):
                curSZ+=1
                curOR|=data[i]

        if(curOR==maxOR):
            minSZ=min(minSZ,curSZ)     

    return minSZ

# Driver code
if __name__ == '__main__':
    data =[5, 1, 3, 4, 2]
    sz = len(data)
    maxOR = OR(data, sz)

    # Function Call
    print(minSubset(data, sz,maxOR))
```

**Output**

```
2
```

**时间复杂度:**O(2<sup>n</sup>)
T5】辅助空间: O(n)

**使用方法 2:**

我们首先找到给定数组所有元素的或。现在我们需要用这个按位“或”找到最小的子集。

为此，使用类似于 [<u>子集和问题</u>](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/) 中给出的动态规划方法。count[i][j]表示最小大小子集，直到第一个元素的 OR 为 j

## C++

```
// CPP Code for above approach
#include <bits/stdc++.h>
using namespace std;

// Compute bitwise or of all elements
// in array of size sz
int OR(int data[], int sz)
{
    int mOR = 0;
    for (int i = 0; i < sz; ++i) {
        mOR |= data[i];
    }

    return mOR;
}

// calculate the size of
// minimum subset with maximum or
int minSubset(int data[], int sz, int maxOR)
{
    // count table where
      // count[i][j] => minimum size subset till ith element
      // whose OR is j
    vector<vector<int> > count(sz + 1, vector<int>(maxOR + 1, 1e9));

    count[0][0] = 0;

    for (int i = 0; i < sz; i++) {
        for (int j = 0; j <= maxOR; j++) {
            // Do not consider ith element.
            count[i + 1][j] = min(count[i + 1][j], count[i][j]);

            // Consider the ith element.
            if (count[i][j] != 1e9) {
                count[i + 1][j | data[i]] = min(
                    count[i + 1][j | data[i]], count[i][j] + 1);
            }
        }
    }

    return count[sz][maxOR];
}

// Driver code
int main()
{
    int data[] = { 5, 1, 3, 4, 2 };
    int sz = sizeof(data) / sizeof(0);
    int maxOR = OR(data, sz);

    // Function Call
    cout << minSubset(data, sz, maxOR) << '\n';
}
```

## 蟒蛇 3

```
# Python3 Code for above approach

# Compute bitwise or of all elements
# in array of size sz
def OR(data, sz):
    mOR = 0
    for i in range(sz):
        mOR |= data[i]
    return mOR

# calculate the size of
# minimum subset with maximum or
def minSubset(data, sz, maxOR):
    # count table where
      # count[i][j] => minimum size subset till ith element
      # whose OR is j
    count=[[1e9 for _ in range(maxOR+1)]for _ in range(sz+1)]

    count[0][0] = 0

    for i in range(sz) :
        for j in range(maxOR) :
            # Do not consider ith element.
            count[i + 1][j] = min(count[i + 1][j], count[i][j])

            # Consider the ith element.
            if (count[i][j] != 1e9) :
                count[i + 1][j | data[i]] = min(
                    count[i + 1][j | data[i]], count[i][j] + 1)

    return count[sz][maxOR]

# Driver code
if __name__ == '__main__':
    data = [5, 1, 3, 4, 2]
    sz = len(data)
    maxOR = OR(data, sz)

    # Function Call
    print(minSubset(data, sz, maxOR))
```

**Output**

```
2
```

**时间复杂度:** O(n*maxOR)其中 n 是数组的大小，maxOR 是可以得到的最大 OR。
**辅助空间:** O(n*maxOR)