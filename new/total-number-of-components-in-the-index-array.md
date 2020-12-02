# 索引数组

中的组件总数

> 原文： [https://www.geeksforgeeks.org/total-number-of-components-in-the-index-array/](https://www.geeksforgeeks.org/total-number-of-components-in-the-index-array/)

给定 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 的整数，值从 **0 到 N** ，则任务是计算 索引数组。

> **索引数组**表示如果我们处于**第**个索引，则它会导致 arr [i]。
> 索引数组的**分量**在形成循环时会被计数。 如果没有循环持续或数组包含单个元素，那么我们也将其视为一个组件。
> 例如：
> 令数组 arr [] = {1,2,0,3}
> {1,2,0}将形成一个分量，因为从索引 0 开始，我们再次到达索引 0，如下所示： ：
> 1-> 2（arr [1]）-> 0（arr [2]）-> 1（arr [0]）

**示例：**

> **输入：** arr [] = {1、2、3、5、0、4、6}
> **输出：** 2
> **说明：**
> 以下是 2 个组件的遍历：
> 组件 1：从 0 开始遍历，然后通过以下方式给出遍历的路径：
> 1-> 2（arr [1]）-> 3（arr [2]）-> 5（arr [3]）-> 4（arr [5]）-> 0（arr [4]）-> 1（arr [0 ]）。
> 组件 2：仅访问了 6 个组件，它又创建了一个组件。
> 因此，组件总数= 2。
> 
> **输入：** arr [] = {1,2,0,3}
> **输出：** 2
> **说明：** 遍历 2 个组件：
> 组件 1：从 0 开始遍历，然后遍历的路径为：
> 1-> 2（arr [1]）-> 0（arr [2 ]）-> 1（arr [0]）
> 组件 2：仅访问了 3 个，它又创建了一个组件。
> 因此，组件总数= 2。

**方法：**的想法是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)的概念。 步骤如下：

1.  从第一个未访问的索引开始，该索引将是其中具有整数 0 的索引。
2.  在**期间，DFS 遍历**在数组中标记访问的元素，直到元素形成一个循环为止。
3.  如果形成一个循环，则意味着我们只有一个组件，因此增加了组件数量。
4.  对数组中所有未访问的索引重复上述所有步骤，并计算给定索引数组中的总数。
5.  如果访问了数组的所有索引，则打印已连接组件的总数。

下面是上述方法的实现：

## C ++

```

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function for DFS traversal
void dfs(int i, int a[],
         map<int, int>& m)
{
    // Check if not visited then
    // recurr for the next index
    if (m[i] == 0) {
        m[i] = 1;

        // DFS Traversal for next index
        dfs(a[i], a, m);
    }

    return;
}

// Function for checking which
// indexes are remaining
int allvisited(int a[], int n,
               map<int, int>& m)
{
    for (int i = 0; i < n; i++) {

        // Marks that the ith
        // index is not visited
        if (m[i] == 0)
            return i;
    }
    return -1;
}

// Function for counting components
int count(int a[], int n)
{
    int c = 0;

    // To mark the visited index
    // during DFS Traversal
    map<int, int> m;

    // Function call
    int x = allvisited(a, n, m);

    while (x != -1) {

        // Count number of components
        c++;

        // DFS call
        dfs(x, a, m);

        x = allvisited(a, n, m);
    }

    // Print the total count of components
    cout << c << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 4, 3, 5, 0, 2, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    count(arr, N);

    return 0;
}

```

## Python3

```

# Python3 program for the above approach

# Function for DFS traversal
def dfs(i, a, m):

    # Check if not visited then
    # recurr for the next index
    if i in m:
        if m[i] == 0:
            m[i] = 1

            # DFS Traversal for next index
            dfs(a[i], a, m)
    else:
        m[i] = 1

        # DFS Traversal for next index
        dfs(a[i], a, m)

    return

# Function for checking which
# indexes are remaining
def allvisited(a, n, m):

    for i in range(n):

        # Marks that the ith
        # index is not visited
        if i in m:
            if m[i] == 0:
                return i

        else:
            return i

    return -1

# Function for counting components
def count(a, n):

    c = 0

    # To mark the visited index
    # during DFS Traversal
    m = dict()

    # Function call
    x = allvisited(a, n, m)

    while (x != -1):

        # Count number of components
        c += 1

        # DFS call
        dfs(x, a, m)

        x = allvisited(a, n, m)

    # Print the total count of components
    print(c)

# Driver Code
if __name__=='__main__':

    # Given array arr[]
    arr = [ 1, 4, 3, 5, 0, 2, 6 ]

    N = len(arr)

    # Function Call
    count(arr, N)

# This code is contributed by rutvik_56

```

**Output:** 

```
3

```

**时间复杂度：** *O（N）*辅助空间： *O（N）*

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。