# 在给定的 N 个范围内搜索元素

> 原文:[https://www . geesforgeks . org/search-给定 n 范围内的元素/](https://www.geeksforgeeks.org/search-an-element-in-given-n-ranges/)

给定一组 **N** 排序范围和一个数字 **K** 。任务是找到 **K** 所在范围的指数。如果 **K** 不在任何给定范围内，则打印 **-1** 。
**注:**给定的范围都不一致。
**举例:**

> **输入:** arr[] = { { 1，3 }，{4，7}，{ 8，11 } }，K = 6
> **输出:** 1
> 6 位于范围{ 4，7 }内，索引= 1
> **输入:** arr[] = { { 1，3 }，{ 4，7 }，{ 9，11 } }，K = 8
> **输出:** -1

**天真的做法:**解决上述问题可以遵循以下步骤。

*   遍历所有范围。
*   检查条件是否**K>= arr【I】。第一&T4【K<= arr【I】。第二**适用于任何迭代。
*   如果数字 **K** 不在任何给定范围内，则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the index of the range
// in which K lies and uses linear search
int findNumber(pair<int, int> a[], int n, int K)
{

    // Iterate and find the element
    for (int i = 0; i < n; i++) {

        // If K lies in the current range
        if (K >= a[i].first && K <= a[i].second)
            return i;
    }

    // K doesn't lie in any of the given ranges
    return -1;
}

// Driver code
int main()
{
    pair<int, int> a[] = { { 1, 3 }, { 4, 7 }, { 8, 11 } };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 6;
    int index = findNumber(a, n, k);
    if (index != -1)
        cout << index;
    else
        cout << -1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return the index
// of the range in which K lies
// and uses linear search
static int findNumber(pair a[],
                      int n, int K)
{

    // Iterate and find the element
    for (int i = 0; i < n; i++)
    {

        // If K lies in the current range
        if (K >= a[i].first &&
            K <= a[i].second)
            return i;
    }

    // K doesn't lie in any
    // of the given ranges
    return -1;
}

// Driver code
public static void main(String[] args)
{
    pair a[] = {new pair(1, 3 ),
                new pair(4, 7 ),
                new pair(8, 11 )};
    int n = a.length;
    int k = 6;
    int index = findNumber(a, n, k);
    if (index != -1)
        System.out.println(index);
    else
        System.out.println(-1);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the index of the range
# in which K lies and uses linear search
def findNumber(a, n, K):

    # Iterate and find the element
    for i in range(0, n, 1):

        # If K lies in the current range
        if (K >= a[i][0] and K <= a[i][1]):
            return i

    # K doesn't lie in any of the
    # given ranges
    return -1

# Driver code
if __name__ == '__main__':
    a = [[1, 3], [4, 7], [8, 11]]
    n = len(a)
    k = 6
    index = findNumber(a, n, k)
    if (index != -1):
        print(index, end = "")
    else:
        print(-1, end = "")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return the index
// of the range in which K lies
// and uses linear search
static int findNumber(pair []a,
                    int n, int K)
{

    // Iterate and find the element
    for (int i = 0; i < n; i++)
    {

        // If K lies in the current range
        if (K >= a[i].first &&
            K <= a[i].second)
            return i;
    }

    // K doesn't lie in any
    // of the given ranges
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    pair []a = {new pair(1, 3 ),
                new pair(4, 7 ),
                new pair(8, 11 )};
    int n = a.Length;
    int k = 6;
    int index = findNumber(a, n, k);
    if (index != -1)
        Console.WriteLine(index);
    else
        Console.WriteLine(-1);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the index of the range
// in which K lies and uses linear search
function findNumber(a, n, K)
{
    // Iterate and find the element
    for (var i = 0; i < n; i++) {

        // If K lies in the current range
        if (K >= a[i][0] && K <= a[i][1])
            return i;
    }

    // K doesn't lie in any of the given ranges
    return -1;
}

// Driver code
var a = [ [ 1, 3 ], [ 4, 7 ], [ 8, 11 ] ];
var n = a.length;
var k = 6;
var index = findNumber(a, n, k);
if (index != -1)
    document.write( index);
else
    document.write( -1);

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)
**高效途径:** [二分搜索法](https://www.geeksforgeeks.org/binary-search/)可用于寻找 O(log N)中的元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the index of the range
// in which K lies and uses binary search
int findNumber(pair<int, int> a[], int n, int K)
{

    int low = 0, high = n - 1;

    // Binary search
    while (low <= high) {

        // Find the mid element
        int mid = (low + high) >> 1;

        // If element is found
        if (K >= a[mid].first && K <= a[mid].second)
            return mid;

        // Check in first half
        else if (K < a[mid].first)
            high = mid - 1;

        // Check in second half
        else
            low = mid + 1;
    }

    // Not found
    return -1;
}

// Driver code
int main()
{
    pair<int, int> a[] = { { 1, 3 }, { 4, 7 }, { 8, 11 } };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 6;
    int index = findNumber(a, n, k);
    if (index != -1)
        cout << index;
    else
        cout << -1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return the index of the range
// in which K lies and uses binary search
static int findNumber(pair a[], int n, int K)
{
    int low = 0, high = n - 1;

    // Binary search
    while (low <= high)
    {

        // Find the mid element
        int mid = (low + high) >> 1;

        // If element is found
        if (K >= a[mid].first &&
            K <= a[mid].second)
            return mid;

        // Check in first half
        else if (K < a[mid].first)
            high = mid - 1;

        // Check in second half
        else
            low = mid + 1;
    }

    // Not found
    return -1;
}

// Driver code
public static void main(String[] args)
{
    pair a[] = { new pair(1, 3),
                 new pair(4, 7),
                 new pair(8, 11) };
    int n = a.length;
    int k = 6;
    int index = findNumber(a, n, k);
    if (index != -1)
        System.out.println(index);
    else
        System.out.println(-1);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the index of the range
# in which K lies and uses binary search
def findNumber(a, n, K):

    low = 0
    high = n - 1

    # Binary search
    while (low <= high):

        # Find the mid element
        mid = (low + high) >> 1

        # If element is found
        if (K >= a[mid][0] and K <= a[mid][1]):
            return mid

        # Check in first half
        elif (K < a[mid][0]):
            high = mid - 1

        # Check in second half
        else:
            low = mid + 1

    # Not found
    return -1

# Driver code
a= [ [ 1, 3 ], [ 4, 7 ], [ 8, 11 ] ]
n = len(a)
k = 6
index = findNumber(a, n, k)
if (index != -1):
    print(index)
else:
    print(-1)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the above approach
using System;
class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return the index of the range
// in which K lies and uses binary search
static int findNumber(pair []a, int n, int K)
{
    int low = 0, high = n - 1;

    // Binary search
    while (low <= high)
    {

        // Find the mid element
        int mid = (low + high) >> 1;

        // If element is found
        if (K >= a[mid].first &&
            K <= a[mid].second)
            return mid;

        // Check in first half
        else if (K < a[mid].first)
            high = mid - 1;

        // Check in second half
        else
            low = mid + 1;
    }

    // Not found
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    pair []a = {new pair(1, 3),
                new pair(4, 7),
                new pair(8, 11)};
    int n = a.Length;
    int k = 6;
    int index = findNumber(a, n, k);
    if (index != -1)
        Console.WriteLine(index);
    else
        Console.WriteLine(-1);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

     class pair {

        constructor(first , second) {
            this.first = first;
            this.second = second;
        }
    }

    // Function to return the index of the range
    // in which K lies and uses binary search
    function findNumber( a , n , K) {
        var low = 0, high = n - 1;

        // Binary search
        while (low <= high) {

            // Find the mid element
            var mid = (low + high) >> 1;

            // If element is found
            if (K >= a[mid].first && K <= a[mid].second)
                return mid;

            // Check in first half
            else if (K < a[mid].first)
                high = mid - 1;

            // Check in second half
            else
                low = mid + 1;
        }

        // Not found
        return -1;
    }

    // Driver code

        var a = [ new pair(1, 3), new pair(4, 7),
                  new pair(8, 11) ];
        var n = a.length;
        var k = 6;
        var index = findNumber(a, n, k);
        if (index != -1)
            document.write(index);
        else
            document.write(-1);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(log N)