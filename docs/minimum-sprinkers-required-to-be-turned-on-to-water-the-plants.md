# 给植物浇水所需开启的最小喷洒器

> 原文:[https://www . geesforgeks . org/minist-sprinkers-需要打开才能给植物浇水/](https://www.geeksforgeeks.org/minimum-sprinkers-required-to-be-turned-on-to-water-the-plants/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，其中 **i <sup>第</sup>个元素**代表喷水器的范围，即**【I-arr[I]，I+arr[I]】**它可以喷水，任务是找到最少数量的要打开的喷水器来给画廊中的每一株植物喷水。如果不可能给每一株植物浇水，那么打印 **-1。**
***注意:**如果 **arr[i] = -1** ，则不能开启洒水车。*

**示例:**

> **输入:** arr[ ] = {-1，2，2，-1，0，0}
> **输出:** 2
> **解释:**
> 可能的方式之一是:
> 
> *   在索引 2 处打开喷水器，它可以给范围[0，4]内的植物浇水。
> *   在索引 5 处打开喷水器，它可以给范围[5，5]内的植物浇水。
> 
> 因此，打开两个喷头可以给所有的植物浇水。此外，这是开启喷头的最小可能数量。
> 
> **输入:** arr[ ] = {2，3，4，-1，2，0，0，-1，0}
> **输出:** -1

**进场:**以上问题可以使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是首先[通过左边界对范围进行排序](https://www.geeksforgeeks.org/sort-c-stl/)，然后从左开始遍历范围，并在每次迭代中选择洒水喷头可以覆盖的最右边的边界，使左边界在当前范围内。按照以下步骤解决问题:

*   初始化一个[向量<对< int，int > >](https://www.geeksforgeeks.org/store-data-triplet-vector-c/) 说 **V** 将每个洒水车的射程存储为一对。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果 **arr[i]** 不等于 **-1** ，则推矢量 **V** 中的对 **(i-arr[i]，i+arr[i])** 。
*   [按第一个元素对成对向量进行升序排序。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   初始化 **2** 变量表示 **res** ，和 **maxRight** 来存储要打开的最小洒水喷头和存储阵列的最右边界。
*   初始化一个变量，比如说 **i** 为 **0** 来迭代 **V.**
*   重复直到**最大值**小于 **N** ，并执行以下步骤:
    *   如果 **i** 等于 **V.size()** 或**V【I】。首先**大于 **maxRight** 然后打印**-1**[返回](https://www.geeksforgeeks.org/return-0-vs-return-1-in-c/)。
    *   将当前洒水喷头的右边界存储在变量中，比如 **currMax** 。
    *   现在迭代直到 **i+1** 小于 **V.size()** 和 **V[i+1]。首先**小于或等于 **maxRight** ，然后在每次迭代中以 **1** 递增 **i** ，并将 **currMax** 更新为**curr max**=**min(curr max，V[i]。第二)。**
    *   如果**电流最大值**小于**最大值**，则打印**-1**[并返回](https://www.geeksforgeeks.org/return-0-vs-return-1-in-c/)。
    *   将**最大权限**更新为**最大权限** = **当前最大+1** ，然后将 **res** 和 **i** 增加 **1** 。
*   最后，完成上述步骤后，打印 **res** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// sprinkler to be turned on
int minSprinklers(int arr[], int N)
{
    // Stores the leftmost and rightmost
    // point of every sprinklers
    vector<pair<int, int> > V;
    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        if (arr[i] > -1) {
            V.push_back(
                pair<int, int>(i - arr[i], i + arr[i]));
        }
    }
    // Sort the array sprinklers in
    // ascending order by first element
    sort(V.begin(), V.end());

    // Stores the rightmost range
    // of a sprinkler
    int maxRight = 0;
    // Stores minimum sprinklers
    // to be turned on
    int res = 0;

    int i = 0;

    // Iterate until maxRight is
    // less than N
    while (maxRight < N) {

        // If i is equal to V.size()
        // or V[i].first is greater
        // than maxRight

        if (i == V.size() || V[i].first > maxRight) {
            return -1;
        }
        // Stores the rightmost boundary
        // of current sprinkler
        int currMax = V[i].second;

        // Iterate until i+1 is less
        // than V.size() and V[i+1].first
        // is less than or equal to maxRight
        while (i + 1 < V.size()
               && V[i + 1].first <= maxRight) {

            // Increment i by 1
            i++;
            // Update currMax
            currMax = max(currMax, V[i].second);
        }

        // If currMax is less than the maxRight
        if (currMax < maxRight) {
            // Return -1
            return -1;
        }
        // Increment res by 1
        res++;

        // Update maxRight
        maxRight = currMax + 1;

        // Increment i by 1
        i++;
    }
    // Return res as answer
    return res;
}

// Drive code.
int main()
{
    // Input
    int arr[] = { -1, 2, 2, -1, 0, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << minSprinklers(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class pair
{
    int x;
    int y;
    pair(int x1,int y1)
    {
        x = x1;
        y = y1;
    }
}

class GFG
{

    // Function to find minimum number of
    // sprinkler to be turned on
    static int minSprinklers(int arr[], int N)
    {

        // Stores the leftmost and rightmost
        // point of every sprinklers
        ArrayList<pair> V= new ArrayList<pair>();

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {
            if (arr[i] > -1) {
                V.add(new pair(i - arr[i], i + arr[i]));
            }
        }

        // Sort the array sprinklers in
        // ascending order by first element
        Collections.sort(V, new Comparator<pair>() {
            @Override public int compare(pair p1, pair p2)
            {
                return p1.x - p2.x;
            }
        });

        // Stores the rightmost range
        // of a sprinkler
        int maxRight = 0;

        // Stores minimum sprinklers
        // to be turned on
        int res = 0;

        int i = 0;

        // Iterate until maxRight is
        // less than N
        while (maxRight < N) {

            // If i is equal to V.size()
            // or V[i].first is greater
            // than maxRight

            if (i == V.size() || V.get(i).x > maxRight) {
                return -1;
            }
            // Stores the rightmost boundary
            // of current sprinkler
            int currMax = V.get(i).y;

            // Iterate until i+1 is less
            // than V.size() and V[i+1].first
            // is less than or equal to maxRight
            while (i + 1 < V.size()
                   && V.get(i+1).x <= maxRight) {

                // Increment i by 1
                i++;

                // Update currMax
                currMax = Math.max(currMax, V.get(i).y);
            }

            // If currMax is less than the maxRight
            if (currMax < maxRight) {
                // Return -1
                return -1;
            }

            // Increment res by 1
            res++;

            // Update maxRight
            maxRight = currMax + 1;

            // Increment i by 1
            i++;
        }

        // Return res as answer
        return res;
    }

  // Driver code
    public static void main (String[] args)
    {
        int arr[] = { -1, 2, 2, -1, 0, 0 };
        int N = 6 ;

        // Function call
        System.out.println(minSprinklers(arr, N));
    }
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find minimum number of
# sprinkler to be turned on
def minSprinklers(arr, N):

    # Stores the leftmost and rightmost
    # point of every sprinklers
    V = [];

    # Traverse the array arr[]
    for i in range(N):
        if (arr[i] > -1):
            V.append([i - arr[i], i + arr[i]]);

    # Sort the array sprinklers in
    # ascending order by first element
    V.sort();

    # Stores the rightmost range
    # of a sprinkler
    maxRight = 0;

    # Stores minimum sprinklers
    # to be turned on
    res = 0;

    i = 0;

    # Iterate until maxRight is
    # less than N
    while (maxRight < N):

        # If i is equal to V.size()
        # or V[i][0] is greater
        # than maxRight

        if (i == len(V) or V[i][0] > maxRight):
            return -1;

        # Stores the rightmost boundary
        # of current sprinkler
        currMax = V[i][1];

        # Iterate until i+1 is less
        # than V.size() and V[i+1][0]
        # is less than or equal to maxRight
        while (i + 1 < len(V) and V[i + 1][0] <= maxRight):

            # Increment i by 1
            i += 1;
            # Update currMax
            currMax = max(currMax, V[i][1]);

        # If currMax is less than the maxRight
        if (currMax < maxRight):
            # Return -1
            return -1;

        # Increment res by 1
        res += 1;

        # Update maxRight
        maxRight = currMax + 1;

        # Increment i by 1
        i += 1;
    # Return res as answer
    return res;

# Drive code.

# Input
arr = [-1, 2, 2, -1, 0, 0];
N = len(arr);

# Function call
print(minSprinklers(arr, N));

# This code is contributed by _saurabh_jaiswal.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum number of
// sprinkler to be turned on
function minSprinklers(arr, N) {
    // Stores the leftmost and rightmost
    // point of every sprinklers
    let V = [];
    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {
        if (arr[i] > -1) {
            V.push([i - arr[i], i + arr[i]]);
        }
    }
    // Sort the array sprinklers in
    // ascending order by first element
    V.sort((a, b) => a - b);

    // Stores the rightmost range
    // of a sprinkler
    let maxRight = 0;
    // Stores minimum sprinklers
    // to be turned on
    let res = 0;

    let i = 0;

    // Iterate until maxRight is
    // less than N
    while (maxRight < N) {

        // If i is equal to V.size()
        // or V[i][0] is greater
        // than maxRight

        if (i == V.length || V[i][0] > maxRight) {
            return -1;
        }
        // Stores the rightmost boundary
        // of current sprinkler
        let currMax = V[i][1];

        // Iterate until i+1 is less
        // than V.size() and V[i+1][0]
        // is less than or equal to maxRight
        while (i + 1 < V.length
            && V[i + 1][0] <= maxRight) {

            // Increment i by 1
            i++;
            // Update currMax
            currMax = Math.max(currMax, V[i][1]);
        }

        // If currMax is less than the maxRight
        if (currMax < maxRight) {
            // Return -1
            return -1;
        }
        // Increment res by 1
        res++;

        // Update maxRight
        maxRight = currMax + 1;

        // Increment i by 1
        i++;
    }
    // Return res as answer
    return res;
}

// Drive code.

// Input
let arr = [-1, 2, 2, -1, 0, 0];
let N = arr.length;

// Function call
document.write(minSprinklers(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*