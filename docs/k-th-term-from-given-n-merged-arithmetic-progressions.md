# 给定 N 个合并算术级数的第 K 项

> 原文:[https://www . geeksforgeeks . org/k-th-term-from-given-n-merged-算术-progressions/](https://www.geeksforgeeks.org/k-th-term-from-given-n-merged-arithmetic-progressions/)

给定一个整数 **K** 和一个 **N** 整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，每个整数都是一个算术级数[T9】的第一项和公差，任务是找到集合 **S** 的**K<sup>th</sup>T13】元素，集合**S**由 N 个算术级数合并而成。**](https://www.geeksforgeeks.org/program-print-arithmetic-progression-series/)

**示例:**

> **输入:** arr[] = {2，3}，K = 10
> **输出:** 15
> **说明:**
> 有 2 个算术级数。
> 第一学期和第一学期的共同区别是 2。因此 AP1 = {2，4，6，…}
> 第一项和第二项的共同区别是 3。因此 AP2 = {3，6，9，…}
> 集合 S 包含 AP1 和 AP2，即{ 2，3，4，6，8，9，10，12，14，15，16，18，20…}。
> 因此第 10 个学期是:15
> 
> **输入:** arr[] = {2，3，5，7，11}，K = 8
> **输出:** 9
> **说明:**
> 有 5 个算术级数。
> 第一学期和第一学期的共同区别是 2。因此 AP1 = {2，4，6，…}
> 第一项和第二项的共同区别是 3。因此 AP2 = {3，6，9，…}
> 第一学期和第三学期的共同区别是 5。因此 AP3 = {5，10，15，…}
> 第一项和第四项的公差是 7。因此 AP4 = {7，14，21，…}
> 第一学期和第五学期的共同区别是 11。因此 AP5 = {11，22，33，…}
> 这样集合 S 包含{ 2，3，4，5，6，7，8，9，10，…。}.
> 因此第 8 个术语是:9

**方法:**
按照以下步骤解决问题:

*   考虑[1，maxm]的范围，并计算该范围的中间值。
*   检查是否可以通过合并 N 个系列获得 K 个元素。如果条款数量超过 **K** ，则减少 **R** 至**中间**。否则，将 **L** 更新为**中**。现在，继续前进，直到我们找到一个**中间的**，对于这个中间的 **K** 项可以在系列中精确地获得。
*   为了找出在任何特定值之前会出现多少元素，我们需要应用[包含和排除原则](https://www.geeksforgeeks.org/inclusion-exclusion-principle-and-programming-applications/)来获得所有元素的并集

下面是上述方法的实现:

## C++

```
// C++ program to find k-th term of
// N merged Arithmetic Progressions
#include <bits/stdc++.h>
using namespace std;
#define maxm 1000000000

// Function to count and return the
// number of values less than equal
// to N present in the set
int count(vector<int> v, int n)
{
    int i, odd = 0, even = 0;
    int j, d, count;

    int t = (int)1 << v.size();
    int size = v.size();

    for (i = 1; i < t; i++) {
        d = 1, count = 0;
        for (j = 0; j < size; j++) {

            // Check whether j-th bit
            // is set bit or not
            if (i & (1 << j)) {
                d *= v[j];
                count++;
            }
        }
        if (count & 1)
            odd += n / d;
        else
            even += n / d;
    }

    return (odd - even);
}

// Function to implement Binary
// Search to find K-th element
int BinarySearch(int l, int r,
                 vector<int> v,
                 int key)
{
    int mid;

    while (r - l > 1) {

        // Find middle index of
        // the array
        mid = (l + r) / 2;

        // Search in the left half
        if (key <= count(v, mid)) {
            r = mid;
        }

        // Search in the right half
        else {
            l = mid;
        }
    }

    // If exactly K elements
    // are present
    if (key == count(v, l))
        return l;
    else
        return r;
}

// Driver Code
int main()
{
    int N = 2, K = 10;

    vector<int> v = { 2, 3 };

    cout << BinarySearch(1, maxm, v, K)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k-th term of
// N merged Arithmetic Progressions
import java.util.*;
class GFG{
static final int maxm = 1000000000;

// Function to count and return the
// number of values less than equal
// to N present in the set
static int count(int []v, int n)
{
    int i, odd = 0, even = 0;
    int j, d, count;

    int t = (int)1 << v.length;
    int size = v.length;

    for (i = 1; i < t; i++)
    {
        d = 1;
        count = 0;
        for (j = 0; j < size; j++)
        {

            // Check whether j-th bit
            // is set bit or not
            if ((i & (1 << j)) > 0)
            {
                d *= v[j];
                count++;
            }
        }
        if (count % 2 == 1)
            odd += n / d;
        else
            even += n / d;
    }

    return (odd - even);
}

// Function to implement Binary
// Search to find K-th element
static int BinarySearch(int l, int r,
                        int []v,
                        int key)
{
    int mid;

    while (r - l > 1)
    {

        // Find middle index of
        // the array
        mid = (l + r) / 2;

        // Search in the left half
        if (key <= count(v, mid))
        {
            r = mid;
        }

        // Search in the right half
        else
        {
            l = mid;
        }
    }

    // If exactly K elements
    // are present
    if (key == count(v, l))
        return l;
    else
        return r;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, K = 10;

    int []v = { 2, 3 };

    System.out.print(BinarySearch(1, maxm, v, K) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find k-th term of
# N merged Arithmetic Progressions
maxm = 1000000000

# Function to count and return the
# number of values less than equal
# to N present in the set
def count(v, n):

    odd, even = 0, 0

    t = 1 << len(v)
    size = len(v)

    for i in range(1, t):
        d, count = 1, 0

        for j in range(0, size):

            # Check whether j-th bit
            # is set bit or not
            if (i & (1 << j)):
                d *= v[j]
                count += 1

        if (count & 1):
            odd += n // d
        else:
            even += n // d

    return (odd - even)

# Function to implement Binary
# Search to find K-th element
def BinarySearch(l, r, v, key):

    while (r - l > 1):

        # Find middle index of
        # the array
        mid = (l + r) // 2

        # Search in the left half
        if (key <= count(v, mid)):
            r = mid

        # Search in the right half
        else:
            l = mid

    # If exactly K elements
    # are present
    if (key == count(v, l)):
        return l
    else:
        return r

# Driver Code
N, K = 2, 10

v = [ 2, 3 ]

print(BinarySearch(1, maxm, v, K))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find k-th term of
// N merged Arithmetic Progressions
using System;

class GFG{

static readonly int maxm = 1000000000;

// Function to count and return the
// number of values less than equal
// to N present in the set
static int count(int []v, int n)
{
    int i, odd = 0, even = 0;
    int j, d, count;

    int t = (int)1 << v.Length;
    int size = v.Length;

    for(i = 1; i < t; i++)
    {
       d = 1;
       count = 0;
       for(j = 0; j < size; j++)
       {

          // Check whether j-th bit
          // is set bit or not
          if ((i & (1 << j)) > 0)
          {
              d *= v[j];
              count++;
          }
       }

       if (count % 2 == 1)
           odd += n / d;
       else
           even += n / d;
    }
    return (odd - even);
}

// Function to implement Binary
// Search to find K-th element
static int BinarySearch(int l, int r,
                        int []v, int key)
{
    int mid;

    while (r - l > 1)
    {

        // Find middle index of
        // the array
        mid = (l + r) / 2;

        // Search in the left half
        if (key <= count(v, mid))
        {
            r = mid;
        }

        // Search in the right half
        else
        {
            l = mid;
        }
    }

    // If exactly K elements
    // are present
    if (key == count(v, l))
        return l;
    else
        return r;
}

// Driver Code
public static void Main(String[] args)
{
    //int N = 2;
    int K = 10;

    int []v = { 2, 3 };

    Console.Write(BinarySearch(
                  1, maxm, v, K) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to find k-th term of
// N merged Arithmetic Progressions

let maxm = 1000000000;

// Function to count and return the
// number of values less than equal
// to N present in the set
function count(v, n)
{
    let i, odd = 0, even = 0;
    let j, d, count;

    let t = 1 << v.length;
    let size = v.length;

    for (i = 1; i < t; i++)
    {
        d = 1;
        count = 0;
        for (j = 0; j < size; j++)
        {

            // Check whether j-th bit
            // is set bit or not
            if ((i & (1 << j)) > 0)
            {
                d *= v[j];
                count++;
            }
        }
        if (count % 2 == 1)
            odd += n / d;
        else
            even += n / d;
    }

    return (odd - even);
}

// Function to implement Binary
// Search to find K-th element
function BinarySearch(l, r,
                        v, key)
{
    let mid;

    while (r - l > 1)
    {

        // Find middle index of
        // the array
        mid = Math.floor((l + r) / 2);

        // Search in the left half
        if (key <= count(v, mid))
        {
            r = mid;
        }

        // Search in the right half
        else
        {
            l = mid;
        }
    }

    // If exactly K elements
    // are present
    if (key == count(v, l))
        return l;
    else
        return r;
}

    // Driver Code

    let N = 2, K = 10;

    let v = [ 2, 3 ];

    document.write(BinarySearch(1, maxm, v, K) + "\n");

</script>
```

**Output:** 

```
15
```

**时间复杂度:***O(N * 2<sup>N</sup>)*
T7】辅助空间: *O(1)*