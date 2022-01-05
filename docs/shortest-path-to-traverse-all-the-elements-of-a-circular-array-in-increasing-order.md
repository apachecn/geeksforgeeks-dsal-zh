# 按递增顺序遍历圆形数组所有元素的最短路径

> 原文:[https://www . geeksforgeeks . org/最短路径遍历递增顺序循环数组的所有元素/](https://www.geeksforgeeks.org/shortest-path-to-traverse-all-the-elements-of-a-circular-array-in-increasing-order/)

一个圆上排列着 **N** 个不同的整数。任意两个相邻数字之间的距离为 **1** 。任务是在这个圆上行进，从最小的数字开始，然后移动到第二小、第三小，以此类推，直到最大的数字并打印最小的行进距离。
**例:**

> **输入:** arr[] = {3，6，5，1，2，4 }
> T3】输出: 8
> 1 - > 2(从左到右)
> 2 - > 3(从左到右)
> 3 - > 4(从右到左)
> 4 - > 5(从左到右或从右到左)
> 5 - > 6(从右到左)
> **输入:【T0**

**方法:**如果我们想在两个有指数的元素之间旅行 **i** 和 **j** ，我们有两条可能的路径，一条是长度**| I–j |**另一条是长度**n –| I–j |**，我们会选择距离最小的一条。
最初，我们构建一个对**(元素，索引)**的数组，并按照元素的递增顺序对其进行排序。然后我们可以每两个连续的对，找到这两个元素之间最短的旅行方式。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Function to return the minimum distance
int min_distance(int n, vector<int> arr)
{

    // Declare a Pair[] array of size n
    vector<pair<int,int>> val(n);

    // Store all the (element, index) pairs
    for ( int i = 0; i < n; i++)
        val[i] = {arr[i], i};

    // Sort the pairs in ascending order of the value
    sort(val.begin(), val.end());

    int min_dist = 0;
    for (int i = 1; i < n; i++)
    {

        // Choose the minimum distance path
        // of the two available
        min_dist += min(abs(val[i].second - val[i - 1].second),
                    n - abs(val[i].second - val[i - 1].second));
    }

    return min_dist;
}

// Driver Code
int main()
{
    vector<int> arr = {3, 6, 5, 1, 2, 4};
    int n = arr.size();
    cout << (min_distance(n, arr));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the minimum distance
    static int min_distance(int n, int[] arr)
    {

        // Declare a Pair[] array of size n
        Pair[] val = new Pair[n];

        // Store all the (element, index) pairs
        for (int i = 0; i < n; i++)
            val[i] = new Pair(arr[i], i);

        // Sort the pairs in ascending order of the value
        Arrays.sort(val, com);

        int min_dist = 0;
        for (int i = 1; i < n; i++) {

            // Choose the minimum distance path
            // of the two available
            min_dist
                += Math.min(Math.abs(val[i].y - val[i - 1].y),
                            n - Math.abs(val[i].y - val[i - 1].y));
        }

        return min_dist;
    }

    // Comparator to be used in the
    // sorting of pairs based on the values
    static final Comparator<Pair> com = new Comparator<Pair>() {
        public int compare(Pair a, Pair b)
        {
            if (Integer.compare(a.x, b.x) != 0)
                return Integer.compare(a.x, b.x);
            else
                return Integer.compare(a.y, b.y);
        }
    };

    // Class to represent a pair
    static class Pair {
        int x, y;
        Pair(int p, int q)
        {
            x = p;
            y = q;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 3, 6, 5, 1, 2, 4 };
        int n = arr.length;

        System.out.println(min_distance(n, arr));
    }
}
```

## 计算机编程语言

```
# Python implementation of the approach

# Function to return the minimum distance
def min_distance(n, arr):

    # Declare a Pair[] array of size n
    val = [None] * n

    # Store all the (element, index) pairs
    for i in range(0, n):
        val[i] = (arr[i], i)

    # Sort the pairs in ascending order of the value
    val.sort()

    min_dist = 0
    for i in range(1, n):

        # Choose the minimum distance path
        # of the two available
        min_dist += min(abs(val[i][1] - val[i - 1][1]),
                        n - abs(val[i][1] - val[i - 1][1]))

    return min_dist

# Driver code
if __name__ == "__main__":

    arr = [3, 6, 5, 1, 2, 4]
    n = len(arr)

    print(min_distance(n, arr))

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum distance
function min_distance(n,arr)
{
    // Declare a Pair[] array of size n
        let val = new Array(n);

        // Store all the (element, index) pairs
        for (let i = 0; i < n; i++)
            val[i] = [arr[i], i];

        // Sort the pairs in ascending order of the value
        val.sort(function(a,b){return a[0]-b[0];});

        let min_dist = 0;
        for (let i = 1; i < n; i++) {

            // Choose the minimum distance path
            // of the two available
            min_dist
                += Math.min(Math.abs(val[i][1] - val[i - 1][1]),
                         n - Math.abs(val[i][1] - val[i - 1][1]));
        }

        return min_dist;
}

// Driver code
let arr=[3, 6, 5, 1, 2, 4];
let n=arr.length;
document.write(min_distance(n, arr))

// This code is contributed by patel2127

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(n * log(n))*

***辅助空间:** O(n)*