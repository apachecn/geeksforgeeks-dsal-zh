# 找到给定每个节点的子 id 和的树根

> 原文:[https://www . geesforgeks . org/find-root-tree-children-id-sum-ever-node-given/](https://www.geeksforgeeks.org/find-root-tree-children-id-sum-every-node-given/)

考虑一棵二叉树，其节点的 id 从 1 到 n，其中 n 是树中的节点数。给定的树是 n 对的集合，其中每对代表节点 id 和子 id 的总和。
**例:**

```
Input : 1 5
        2 0
        3 0
        4 0
        5 5
        6 5
Output: 6
Explanation: In this case, two trees can 
be made as follows and 6 is the root node.
   6          6
   \         / \
    5       1   4
   / \       \
  1   4       5
 / \         / \
2   3       2   3

Input : 4 0
Output: 4
Explanation: Clearly 4 does 
not have any children and is the
only node i.e., the root node.
```

乍一看，这个问题似乎是一个典型的树数据结构问题，但它
可以通过以下方式解决。
除了根，每个节点 id 都出现在子总和中。所以如果我们对所有的 id 求和，然后从所有子和的和中减去它，我们就得到根。

## C++

```
// Find root of tree where children
// sum for every node id is given.
#include<bits/stdc++.h>
using namespace std;

int findRoot(pair<int, int> arr[], int n)
{
   // Every node appears once as an id, and
   // every node except for the root appears
   // once in a sum.  So if we subtract all
   // the sums from all the ids, we're left
   // with the root id.
   int root = 0;
   for (int i=0; i<n; i++)
     root += (arr[i].first - arr[i].second);

   return root;
}

// Driver code
int main()
{
    pair<int, int> arr[] = {{1, 5}, {2, 0},
           {3, 0}, {4, 0}, {5, 5}, {6, 5}};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("%d\n", findRoot(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Find root of tree where children
// sum for every node id is given.

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

    static int findRoot(pair arr[], int n)
    {
        // Every node appears once as an id, and
        // every node except for the root appears
        // once in a sum. So if we subtract all
        // the sums from all the ids, we're left
        // with the root id.
        int root = 0;
        for (int i = 0; i < n; i++)
        {
            root += (arr[i].first - arr[i].second);
        }

        return root;
    }

    // Driver code
    public static void main(String[] args)
    {
        pair arr[] = {new pair(1, 5), new pair(2, 0),
                    new pair(3, 0), new pair(4, 0),
                    new pair(5, 5), new pair(6, 5)};
        int n = arr.length;
        System.out.printf("%d\n", findRoot(arr, n));
    }

}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
"""Find root of tree where children
sum for every node id is given"""

def findRoot(arr, n) :

    # Every node appears once as an id, and
    # every node except for the root appears
    # once in a sum. So if we subtract all
    # the sums from all the ids, we're left
    # with the root id.
    root = 0
    for i in range(n):
        root += (arr[i][0] - arr[i][1])
    return root

# Driver Code
if __name__ == '__main__':

    arr = [[1, 5], [2, 0],
           [3, 0], [4, 0],
           [5, 5], [6, 5]]
    n = len(arr)
    print(findRoot(arr, n))

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# Find root of tree where children
// sum for every node id is given.
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

    static int findRoot(pair []arr, int n)
    {
        // Every node appears once as an id, and
        // every node except for the root appears
        // once in a sum. So if we subtract all
        // the sums from all the ids, we're left
        // with the root id.
        int root = 0;
        for (int i = 0; i < n; i++)
        {
            root += (arr[i].first - arr[i].second);
        }

        return root;
    }

    // Driver code
    public static void Main(String[] args)
    {
        pair []arr = {new pair(1, 5), new pair(2, 0),
                    new pair(3, 0), new pair(4, 0),
                    new pair(5, 5), new pair(6, 5)};
        int n = arr.Length;
        Console.Write("{0}\n", findRoot(arr, n));
    }

}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript: Find root of tree where children
// sum for every node id is given.

/*Every node appears once as an id, and
every node except for the root appears
once in a sum. So if we subtract all
the sums from all the ids, we're left
with the root id. */

const findRoot = (nodeList) => {
    let root = 0;
    nodeList.forEach(element =>
    root+=(Number(element[0]) - Number(element[1])));
    return root ;
}

let nodeList = [[1, 5], [2, 0],
                [3, 0], [4, 0],
                [5, 5], [6, 5]];
let root = findRoot(nodeList);
document.write(root);

// This code is contributed by bharathmkulkarni

</script>
```

**输出:**

```
6
```

本文由**苏尼迪·乔德里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。