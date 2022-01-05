# 查询计算 X 与任何不超过 M 的数组元素的最大按位异或

> 原文:[https://www . geeksforgeeks . org/query-to-compute-max-by-xor-of-x-any-array-element-not-exclusive-m/](https://www.geeksforgeeks.org/queries-to-calculate-maximum-bitwise-xor-of-x-with-any-array-element-not-exceeding-m/)

给定一个由非负整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由类型为 **{X，M}** 的查询组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **查询【】【】**，每个查询的任务是找到值最多为 **M** 的任意数组元素的最大[位异或](https://www.geeksforgeeks.org/tag/xor/)。如果无法找到按位异或，则打印**-1”**。

**示例:**

> **输入:** arr[] = {0，1，2，3，4}，查询[][] = {{3，1}，{1，3}，{5，6}}
> **输出:** {3，3，7}
> **解释:**
> **查询 1:** 查询为{3，1}。最大按位异或= 3 ^ 0 = 3。
> **查询 2:** 查询为{1，3}。最大按位异或= 1 ^ 2 = 3。
> **查询 3:** 查询为{5，6}。最大按位异或= 5 ^ 2 = 7。
> 
> **输入:** arr[] = {5，2，4，6，6，3}，查询[][] = {{12，4}，{8，1}，{6，3}}
> **输出:** {15，-1，5}

**天真法:**解决给定问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)进行每个查询 **{X，M}** 并打印 **X** 的**位异或**的最大值，数组元素的值最多为 **M** 。如果不存在小于 **M** 的值，则打印**-1”**进行查询。
***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过使用 [Trie 数据结构](https://www.geeksforgeeks.org/trie-insert-and-search/)来优化，以最多 M 存储所有具有值**的元素。因此，问题简化为寻找一个数组中两个元素的最大异或。按照以下步骤解决问题:**

*   初始化一个变量，说**索引**，到[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   初始化一个存储每个查询结果的数组，比如 **ans[]** 。
*   初始化一个辅助数组，比如 **temp[][3]** ，用每个查询的索引把所有的查询都存储在里面。
*   [根据第二个参数对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **temp[]** 进行排序，即 **temp[1]** (= **M** )。
*   [按升序排列给定数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **temp[]** ，对于每个查询 **{X，M，idx}** ，执行以下步骤:
    *   迭代直到**索引**的值小于 **N** 且 **arr【索引】**至多为 **M** 或不为。如果发现为真，则插入该节点作为 **N** 的二进制表示，并增加**索引**。
    *   完成上述步骤后，如果**索引**的值为**非零**，则[在 Trie](https://www.geeksforgeeks.org/search-in-a-trie-recursively/) 中找到值为 **X** 的节点(说**结果**，将当前查询的最大值更新为**结果**。否则，将当前查询的最大值更新为**-【1】**。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)**ans【】**作为每个查询的最大值。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

// Trie Node Class
class TrieNode {
    TrieNode nums[] = new TrieNode[2];
    int prefixValue;
}

class sol {

    // Function to find the maximum XOR
    // of X with any array element <= M
    // for each query of the type {X, M}
    public void maximizeXor(
        int[] nums, int[][] queries)
    {
        int queriesLength = queries.length;
        int[] ans = new int[queriesLength];
        int[][] temp = new int[queriesLength][3];

        // Stores the queries
        for (int i = 0; i < queriesLength; i++) {
            temp[i][0] = queries[i][0];
            temp[i][1] = queries[i][1];
            temp[i][2] = i;
        }

        // Sort the query
        Arrays.sort(temp,
                    (a, b) -> {
                        return a[1]
                            - b[1];
                    });
        int index = 0;

        // Sort the array
        Arrays.sort(nums);
        TrieNode root = new TrieNode();

        // Traverse the given query
        for (int query[] : temp) {

            // Traverse the array nums[]
            while (index < nums.length
                   && nums[index]
                          <= query[1]) {

                // Insert the node into the Trie
                insert(root, nums[index]);
                index++;
            }

            // Stores the resultant
            // maximum value
            int tempAns = -1;

            // Find the maximum value
            if (index != 0) {

                // Search the node in the Trie
                tempAns = search(root,
                                 query[0]);
            }

            // Update the result
            // for each query
            ans[query[2]] = tempAns;
        }

        // Print the answer
        for (int num : ans) {
            System.out.print(num + " ");
        }
    }

    // Function to insert the
    // root in the trieNode
    public void insert(TrieNode root,
                       int n)
    {
        TrieNode node = root;

        // Iterate from 31 to 0
        for (int i = 31; i >= 0; i--) {

            // Find the bit at i-th position
            int bit = (n >> i) & 1;
            if (node.nums[bit] == null) {
                node.nums[bit]
                    = new TrieNode();
            }
            node = node.nums[bit];
        }

        // Update the value
        node.prefixValue = n;
    }

    // Function to search the root
    // with the value and perform
    // the Bitwise XOR with N
    public int search(TrieNode root,
                      int n)
    {
        TrieNode node = root;

        // Iterate from 31 to 0
        for (int i = 31; i >= 0; i--) {

            // Find the bit at ith
            // position
            int bit = (n >> i) & 1;
            int requiredBit = bit
                                      == 1
                                  ? 0
                                  : 1;

            if (node.nums[requiredBit]
                != null) {
                node = node.nums[requiredBit];
            }
            else {
                node = node.nums[bit];
            }
        }

        // Return the prefixvalue XORed
        // with N
        return node.prefixValue ^ n;
    }
}

class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        sol tt = new sol();
        int[] nums = { 0, 1, 2, 3, 4 };
        int[][] queries = { { 3, 1 },
                            { 1, 3 },
                            { 5, 6 } };

        tt.maximizeXor(nums, queries);
    }
}
```

**Output:**

```
3 3 7

```

***时间复杂度:**O(N * log N+K * log K)*
T5**辅助空间:** O(N)