# 使任意区间等于给定集合的并集所需的最小清除量

> 原文:[https://www . geeksforgeeks . org/最小清除-要求使任意间隔等于给定集合的并集/](https://www.geeksforgeeks.org/minimum-removals-required-to-make-any-interval-equal-to-the-union-of-the-given-set/)

给定一个由区间组成的大小为 **N** ( *1 ≤ N ≤ 1e5* )的集合 **S** ，任务是找到需要从该集合中移除的最小区间，使得剩余区间中的任何一个都等于该集合的并集。

**例:**

> **输入:** S = {[1，3]，[4，12]，[5，8]，[13，20]}
> **输出:** 2
> **解释:**
> 删除间隔[1，3]和[13，20]将设置修改为{ [4，12]，[5，8]}。区间[4，12]是集合的并集。
> 
> **输入:** S = {[1，2]，[1，10]，[4，8]，[3，7]}
> **输出:** 0
> **解释:**
> 给定集合的并集= {[1，10]}，该集合已经存在。因此，不需要移除。

**方法:**根据以下观察可以解决问题:

> **观察:**要使任何区间等于集合的并集，集合必须包含一个区间**【L，R】**，使得所有剩余区间的左边界大于等于 **L** ，右边界小于等于 **R** 。

按照以下步骤解决问题:

1.  遍历给定的一组区间。
2.  对于集合中的每个区间，找出其左边界大于或等于其左边界以及其右边界小于或等于其右边界的所有区间。将这些间隔的计数存储在一个变量中，比如**计数**。
3.  找出每个间隔的所有**N–计数**值的最小值(因为**N–计数**会给出删除的间隔数)。
4.  打印获得的最小值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of removals
// required to make an interval equal to the
// union of the given Set
int findMinDeletions(vector<pair<int, int> >& v,
                     int n)
{
    // Stores the minimum number of removals
    int minDel = INT_MAX;

    // Traverse the Set
    for (int i = 0; i < n; i++) {

        // Left Boundary
        int L = v[i].first;

        // Right Boundary
        int R = v[i].second;

        // Stores count of intervals
        // lying within current interval
        int Count = 0;

        // Traverse over all remaining intervals
        for (int j = 0; j < n; j++) {

            // Check if interval lies within
            // the current interval
            if (v[j].first >= L && v[j].second <= R) {

                // Increase count
                Count += 1;
            }
        }

        // Update minimum removals required
        minDel = min(minDel, n - Count);
    }
    return minDel;
}

// Driver Code
int main()
{
    vector<pair<int, int> > v;
    v.push_back({ 1, 3 });
    v.push_back({ 4, 12 });
    v.push_back({ 5, 8 });
    v.push_back({ 13, 20 });

    int N = v.size();

    // Returns the minimum removals
    cout << findMinDeletions(v, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG{

// Function to count minimum number of removals
// required to make an interval equal to the
// union of the given Set
static int findMinDeletions(int [][]v,
                            int n)
{

    // Stores the minimum number of removals
    int minDel = Integer.MAX_VALUE;

    // Traverse the Set
    for (int i = 0; i < n; i++)
    {

        // Left Boundary
        int L = v[i][0];

        // Right Boundary
        int R = v[i][1];

        // Stores count of intervals
        // lying within current interval
        int Count = 0;

        // Traverse over all remaining intervals
        for (int j = 0; j < n; j++)
        {

            // Check if interval lies within
            // the current interval
            if (v[j][0] >= L && v[j][1] <= R)
            {

                // Increase count
                Count += 1;
            }
        }

        // Update minimum removals required
        minDel = Math.min(minDel, n - Count);
    }
    return minDel;
}

// Driver Code
public static void main(String[] args)
{
    int [][]v = {{ 1, 3 },
                 { 4, 12 },
                 { 5, 8 },
                 { 13, 20 }};

    int N = v.length;

    // Returns the minimum removals
    System.out.print(findMinDeletions(v, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count minimum number of removals
# required to make an interval equal to the
# union of the given Set
def findMinDeletions(v, n):

    # Stores the minimum number of removals
    minDel = 10**18

    # Traverse the Set
    for i in range(n):

        # Left Boundary
        L = v[i][0]

        # Right Boundary
        R = v[i][1]

        # Stores count of intervals
        # lying within current interval
        Count = 0

        # Traverse over all remaining intervals
        for j in range(n):

            # Check if interval lies within
            # the current interval
            if (v[j][1] >= L and v[j][0] <= R):

                # Increase count
                Count += 1

        # Update minimum removals required
        minDel = min(minDel, n - Count)
    return minDel

# Driver Code
if __name__ == '__main__':
    v = []
    v.append([1, 3])
    v.append([4, 12])
    v.append([5, 8])
    v.append([13, 2])

    N = len(v)

    # Returns the minimum removals
    print (findMinDeletions(v, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG{

// Function to count minimum number of removals
// required to make an interval equal to the
// union of the given Set
static int findMinDeletions(int [,]v,
                            int n)
{

    // Stores the minimum number of removals
    int minDel = int.MaxValue;

    // Traverse the Set
    for (int i = 0; i < n; i++)
    {

        // Left Boundary
        int L = v[i,0];

        // Right Boundary
        int R = v[i,1];

        // Stores count of intervals
        // lying within current interval
        int Count = 0;

        // Traverse over all remaining intervals
        for (int j = 0; j < n; j++)
        {

            // Check if interval lies within
            // the current interval
            if (v[j,0] >= L && v[j,1] <= R)
            {

                // Increase count
                Count += 1;
            }
        }

        // Update minimum removals required
        minDel = Math.Min(minDel, n - Count);
    }
    return minDel;
}

// Driver Code
public static void Main(String[] args)
{
    int [,]v = {{ 1, 3 },
                 { 4, 12 },
                 { 5, 8 },
                 { 13, 20 }};

    int N = v.GetLength(0);

    // Returns the minimum removals
    Console.Write(findMinDeletions(v, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to count minimum number of removals
// required to make an interval equal to the
// union of the given Set
function findMinDeletions(v, n)
{

    // Stores the minimum number of removals
    let minDel = Number.MAX_VALUE;

    // Traverse the Set
    for (let i = 0; i < n; i++)
    {

        // Left Boundary
        let L = v[i][0];

        // Right Boundary
        let R = v[i][1];

        // Stores count of intervals
        // lying within current interval
        let Count = 0;

        // Traverse over all remaining intervals
        for (let j = 0; j < n; j++)
        {

            // Check if interval lies within
            // the current interval
            if (v[j][0] >= L && v[j][1] <= R)
            {

                // Increase count
                Count += 1;
            }
        }

        // Update minimum removals required
        minDel = Math.min(minDel, n - Count);
    }
    return minDel;
}

// Driver Code

    let v = [[ 1, 3 ],
                 [ 4, 12 ],
                 [ 5, 8 ],
                 [ 13, 20 ]];

    let N = v.length;

    // Returns the minimum removals
    document.write(findMinDeletions(v, N));

 // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*