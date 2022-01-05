# 通过更新计算子串字符 ASCII 值平方和的查询

> 原文:[https://www . geeksforgeeks . org/查询-计算带更新的子字符串的 ascii 字符值平方和/](https://www.geeksforgeeks.org/queries-to-calculate-sum-of-squares-of-ascii-values-of-characters-of-a-substring-with-updates/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)T2 S 和由以下类型的 **M** 查询组成的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **Q[][]** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/):

*   **查询(“U”、“I”、“X”):**用字符 **X** 更新索引 **I** 处的字符。
*   **查询(“S”、“L”、“R”):**打印子串 **{S[L]，…中字符位置的平方和。，S[R]}** 按英文字母排序。

**示例:**

> **输入:**S =“geeks forgeeks”，Q[][]= {“S”、“0”、“2”}、{“S”、“1”、“2”}、{“U”、“1”、“a”}、{“S”、“0”、“2”}、{“S”、“4”、“5”}
> T3】输出:T5】99
> 50
> 75
> 397
> **解释:**
> 为**查询(】
> 对于**查询(“S”、“1”、“2”)**，子串“ee”中字符位置的平方和= 5*5 + 5*5 = 50。
> 对于查询(“U”、“1”、“a”):将 S[1]替换为“a”将 S 修改为“gaeksforgeeks”。
> 对于**查询(“S”、“0”、“2”)**，子串“gae”中字符位置的平方和= 7*7 + 1*1 + 5*5 = 75。
> 对于**查询(“S”、“4”、“5”)**，子串“ks”中字符位置的平方和= 19*19 + 36 = 397**
> 
> **输入:** S = 【极客 forgeeks】，Q[][]= { {“S”，“1”，“2”} }
> **输出:** 50

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** 对于每个查询和类型为**‘S’**的查询，只需[遍历子串{S[L]，…，S[R]}](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) 并打印英文字母中字符位置的平方和。在每次迭代执行**‘U’**类型的查询时，只需将 **X** 分配给 **S[I]。**

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过使用[段树数据结构](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)进行优化。按照以下步骤解决问题:

*   初始化一个段树，比如**树[]** ，其中每个节点存储其子树中英文字母字符位置的平方和。
*   对于**查询(“U”、“I”、“X”)**，定义一个更新函数，类似于求和范围查询的[更新函数。更新 **S[i] = X** 然后调用 **update()** 函数更新段树。](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
*   对于**查询(“S”、“L”、“R”)**，定义一个函数**查询()**，类似于[求和范围查询](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，然后对子串 **{S[L]，…，打印调用**查询()**函数得到的和。，S[R]}** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a node
// of a Segment Tree
struct treeNode {
    int square_sum;
};

// Function to construct the Segment Tree
void buildTree(string s, treeNode* tree,
               int start, int end,
               int treeNode)
{
    // If start and end are equal
    if (start == end) {

        // Assign squares of positions
        // of the characters
        tree[treeNode].square_sum
            = pow(s[start] - 'a' + 1, 2);

        return;
    }

    // Stores the mid value of
    // the range [start, end]
    int mid = start + ((end - start) / 2);

    // Recursive call to left subtree
    buildTree(s, tree, start,
              mid, 2 * treeNode);

    // Recursive call to right subtree
    buildTree(s, tree, mid + 1,
              end, 1 + 2 * treeNode);

    // Update the current node
    tree[treeNode].square_sum
        = tree[(2 * treeNode)].square_sum
          + tree[(2 * treeNode) + 1].square_sum;
}

// Function to perform the queries of type 2
int querySquareSum(treeNode* tree, int start,
                   int end, int treeNode,
                   int l, int r)
{
    // No overlap
    if ((l > end) || (r < start)) {
        return 0;
    }

    // If l <= start and r >= end
    if ((l <= start) && (r >= end)) {

        // Return the value of treeNode
        return tree[treeNode].square_sum;
    }

    // Calculate middle of the range [start, end]
    int mid = start + ((end - start) / 2);

    // Function call to left subtree
    int X = querySquareSum(tree, start,
                           mid, 2 * treeNode,
                           l, r);

    // Function call to right subtree
    int Y = +querySquareSum(tree, mid + 1, end,
                            1 + 2 * treeNode, l, r);

    // Return the sum of X and Y
    return X + Y;
}

// Function to perform update
// queries on a Segment Tree
void updateTree(string s, treeNode* tree,
                int start, int end,
                int treeNode, int idx, char X)
{
    // If start is equal to end
    // and idx is equal to start
    if ((start == end) && (idx == start)) {

        // Base Case
        s[idx] = X;
        tree[treeNode].square_sum
            = pow(X - 'a' + 1, 2);

        return;
    }

    // Calculate middle of the range [start, end]
    int mid = start + ((end - start) / 2);

    // If idx <=  mid
    if (idx <= mid) {

        // Function call to left subtree
        updateTree(s, tree, start, mid,
                   (2 * treeNode), idx, X);
    }

    // Otherwise
    else {

        // Function call to the right subtree
        updateTree(s, tree, mid + 1, end,
                   (2 * treeNode) + 1, idx, X);
    }

    // Update the current node
    tree[treeNode].square_sum
        = tree[(2 * treeNode)].square_sum
          + tree[(2 * treeNode) + 1].square_sum;
}

// Function to perform the given queries
void PerformQuery(string S,
                  vector<vector<string> > Q)
{
    int n = S.size();

    // Stores the segment tree
    treeNode* tree = new treeNode[(4 * n) + 1];

    // Traverse the segment tree
    for (int i = 0; i <= (4 * n); i = i + 1) {

        // Assign 0 to each node
        tree[i].square_sum = 0;
    }

    // Builds segment tree
    buildTree(S, tree, 0, n - 1, 1);

    // Traverse the query array Q[][]
    for (int i = 0; i < Q.size(); i++) {

        // If query is of type S
        if (Q[i][0] == "S") {

            // Stores the left boundary
            int L = stoi(Q[i][1]);

            // Stores the right boundary
            int R = stoi(Q[i][2]);

            // Prints the sum of squares of the
            // alphabetic positions of the characters
            cout << querySquareSum(tree, 0,
                                   n - 1, 1, L, R)
                 << endl;
        }

        // Otherwise
        else if (Q[i][0] == "U") {

            // Stores the index of the
            // character to be updated
            int I = stoi(Q[i][1]);

            // Update the segment tree
            updateTree(S, tree, 0, n - 1,
                       1, I, Q[i][2][0]);
        }
    }
}

// Driver Code
int main()
{
    // Input
    string S = "geeksforgeeks";
    vector<vector<string> > Q = { { "S", "0", "2" },
                                  { "S", "1", "2" },
                                  { "U", "1", "a" },
                                  { "S", "0", "2" },
                                  { "S", "4", "5" } };
    // Function call
    PerformQuery(S, Q);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Structure of a node
// of a Segment Tree
static class treeNode
{
    int square_sum;

    treeNode(int square_sum)
    {
        this.square_sum = square_sum;
    }
};

// Function to construct the Segment Tree
static void buildTree(char s[], treeNode tree[],
                      int start, int end, int treenode)
{

    // If start and end are equal
    if (start == end)
    {

        // Assign squares of positions
        // of the characters
        tree[treenode].square_sum = (int)Math.pow(
            s[start] - 'a' + 1, 2);

        return;
    }

    // Stores the mid value of
    // the range [start, end]
    int mid = start + ((end - start) / 2);

    // Recursive call to left subtree
    buildTree(s, tree, start, mid, 2 * treenode);

    // Recursive call to right subtree
    buildTree(s, tree, mid + 1, end, 1 + 2 * treenode);

    // Update the current node
    tree[treenode].square_sum = tree[(2 * treenode)].square_sum +
                                tree[(2 * treenode) + 1].square_sum;
}

// Function to perform the queries of type 2
static int querySquareSum(treeNode tree[], int start,
                          int end, int treenode, int l,
                          int r)
{

    // No overlap
    if ((l > end) || (r < start))
    {
        return 0;
    }

    // If l <= start and r >= end
    if ((l <= start) && (r >= end))
    {

        // Return the value of treeNode
        return tree[treenode].square_sum;
    }

    // Calculate middle of the range [start, end]
    int mid = start + ((end - start) / 2);

    // Function call to left subtree
    int X = querySquareSum(tree, start, mid,
                           2 * treenode, l, r);

    // Function call to right subtree
    int Y = +querySquareSum(tree, mid + 1, end,
                            1 + 2 * treenode, l, r);

    // Return the sum of X and Y
    return X + Y;
}

// Function to perform update
// queries on a Segment Tree
static void updateTree(char s[], treeNode tree[],
                       int start, int end, int treenode,
                       int idx, char X)
{

    // If start is equal to end
    // and idx is equal to start
    if ((start == end) && (idx == start))
    {

        // Base Case
        s[idx] = X;
        tree[treenode].square_sum = (int)Math.pow(
            X - 'a' + 1, 2);

        return;
    }

    // Calculate middle of the range [start, end]
    int mid = start + ((end - start) / 2);

    // If idx <=  mid
    if (idx <= mid)
    {

        // Function call to left subtree
        updateTree(s, tree, start, mid, (2 * treenode),
                   idx, X);
    }

    // Otherwise
    else
    {

        // Function call to the right subtree
        updateTree(s, tree, mid + 1, end,
                 (2 * treenode) + 1, idx, X);
    }

    // Update the current node
    tree[treenode].square_sum = tree[(2 * treenode)].square_sum +
                                tree[(2 * treenode) + 1].square_sum;
}

// Function to perform the given queries
static void PerformQuery(String S, String Q[][])
{
    int n = S.length();

    // Stores the segment tree
    treeNode tree[] = new treeNode[(4 * n) + 1];

    // Traverse the segment tree
    for(int i = 0; i <= (4 * n); i = i + 1)
    {

        // Assign 0 to each node
        tree[i] = new treeNode(0);
    }

    char s[] = S.toCharArray();

    // Builds segment tree
    buildTree(s, tree, 0, n - 1, 1);

    // Traverse the query array Q[][]
    for(int i = 0; i < Q.length; i++)
    {

        // If query is of type S
        if (Q[i][0] == "S")
        {

            // Stores the left boundary
            int L = Integer.parseInt(Q[i][1]);

            // Stores the right boundary
            int R = Integer.parseInt(Q[i][2]);

            // Prints the sum of squares of the
            // alphabetic positions of the characters
            System.out.println(querySquareSum(
                tree, 0, n - 1, 1, L, R));
        }

        // Otherwise
        else if (Q[i][0] == "U")
        {

            // Stores the index of the
            // character to be updated
            int I = Integer.parseInt(Q[i][1]);

            // Update the segment tree
            updateTree(s, tree, 0, n - 1, 1, I,
                       Q[i][2].charAt(0));
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String S = "geeksforgeeks";
    String Q[][] = { { "S", "0", "2" },
                     { "S", "1", "2" },
                     { "U", "1", "a" },
                     { "S", "0", "2" },
                     { "S", "4", "5" } };
    // Function call
    PerformQuery(S, Q);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Structure of a node
# of a Segment Tree
class treeNode:

    def __init__(self, x):

        self.square_sum = x

# Function to construct the Segment Tree
def buildTree(s, tree, start, end, treeNode):

    # If start and end are equa
    if (start == end):

        # Assign squares of positions
        # of the characters
        tree[treeNode].square_sum = pow(ord(s[start]) -
                                        ord('a') + 1, 2)

        return

    # Stores the mid value of
    # the range [start, end]
    mid = start + ((end - start) // 2)

    # Recursive call to left subtree
    buildTree(s, tree, start, mid, 2 * treeNode)

    # Recursive call to right subtree
    buildTree(s, tree, mid + 1, end,
                         1 + 2 * treeNode)

    # Update the current node
    tree[treeNode].square_sum = (tree[(2 * treeNode)].square_sum +
                                 tree[(2 * treeNode) + 1].square_sum)

# Function to perform the queries of type 2
def querySquareSum(tree, start, end, treeNode, l, r):

    # No overlap
    if ((l > end) or (r < start)):
        return 0

    # If l <= start and r >= end
    if ((l <= start) and (r >= end)):

        # Return the value of treeNode
        return tree[treeNode].square_sum

    # Calculate middle of the range [start, end]
    mid = start + ((end - start) // 2)

    # Function call to left subtree
    X = querySquareSum(tree, start, mid,
                       2 * treeNode, l, r)

    # Function call to right subtree
    Y = +querySquareSum(tree, mid + 1, end,
                                1 + 2 * treeNode, l, r)

    # Return the sum of X and Y
    return X + Y

# Function to perform update
# queries on a Segment Tree
def updateTree(s, tree, start, end, treeNode, idx, X):

    # If start is equal to end
    # and idx is equal to start
    if ((start == end) and (idx == start)):

        # Base Case
        s[idx] = X
        tree[treeNode].square_sum = pow(ord(X) -
                                       ord('a') + 1, 2)
        return

    # Calculate middle of the range [start, end]
    mid = start + ((end - start) // 2)

    # If idx <=  mid
    if (idx <= mid):

        # Function call to left subtree
        updateTree(s, tree, start, mid,
                  (2 * treeNode), idx, X)

    # Otherwise
    else:

        # Function call to the right subtree
        updateTree(s, tree, mid + 1, end,
                  (2 * treeNode) + 1, idx, X)

    # Update the current node
    tree[treeNode].square_sum = (tree[(2 * treeNode)].square_sum +
                                 tree[(2 * treeNode) + 1].square_sum)

# Function to perform the given queries
def PerformQuery(S, Q):

    n = len(S)

    # Stores the segment tree
    tree = [treeNode(0) for i in range((4 * n) + 1)]

    # Traverse the segment tree
    for i in range(4 * n + 1):

        # Assign 0 to each node
        tree[i].square_sum = 0

    # Builds segment tree
    buildTree(S, tree, 0, n - 1, 1)

    # Traverse the query array Q[][]
    for i in range(len(Q)):

        # If query is of type S
        if (Q[i][0] == "S"):

            # Stores the left boundary
            L = int(Q[i][1])

            # Stores the right boundary
            R = int(Q[i][2])

            # Prints the sum of squares of the
            # alphabetic positions of the characters
            print(querySquareSum(tree, 0, n - 1,
                                 1, L, R))

        # Otherwise
        elif (Q[i][0] == "U"):

            # Stores the index of the
            # character to be updated
            I = int(Q[i][1])

            # Update the segment tree
            updateTree(S, tree, 0, n - 1,
                       1, I, Q[i][2][0])

# Driver Code
if __name__ == '__main__':

    # Input
    S = "geeksforgeeks"
    Q = [ [ "S", "0", "2" ],
          [ "S", "1", "2" ],
          [ "U", "1", "a" ],
          [ "S", "0", "2" ],
          [ "S", "4", "5" ] ]

    # Function call
    PerformQuery([i for i in S], Q)

# This code is contributed by mohit kumar 29
```

## C#

```
using System;

public class treeNode
{
    public int square_sum;

    public treeNode(int square_sum)
    {
        this.square_sum = square_sum;
    }
};

public class GFG{

    // Function to construct the Segment Tree
static void buildTree(char[] s, treeNode[] tree,
                      int start, int end, int treenode)
{

    // If start and end are equal
    if (start == end)
    {

        // Assign squares of positions
        // of the characters
        tree[treenode].square_sum = (int)Math.Pow(
            s[start] - 'a' + 1, 2);

        return;
    }

    // Stores the mid value of
    // the range [start, end]
    int mid = start + ((end - start) / 2);

    // Recursive call to left subtree
    buildTree(s, tree, start, mid, 2 * treenode);

    // Recursive call to right subtree
    buildTree(s, tree, mid + 1, end, 1 + 2 * treenode);

    // Update the current node
    tree[treenode].square_sum = tree[(2 * treenode)].square_sum +
                                tree[(2 * treenode) + 1].square_sum;
}

// Function to perform the queries of type 2
static int querySquareSum(treeNode[] tree, int start,
                          int end, int treenode, int l,
                          int r)
{

    // No overlap
    if ((l > end) || (r < start))
    {
        return 0;
    }

    // If l <= start and r >= end
    if ((l <= start) && (r >= end))
    {

        // Return the value of treeNode
        return tree[treenode].square_sum;
    }

    // Calculate middle of the range [start, end]
    int mid = start + ((end - start) / 2);

    // Function call to left subtree
    int X = querySquareSum(tree, start, mid,
                           2 * treenode, l, r);

    // Function call to right subtree
    int Y = +querySquareSum(tree, mid + 1, end,
                            1 + 2 * treenode, l, r);

    // Return the sum of X and Y
    return X + Y;
}

// Function to perform update
// queries on a Segment Tree
static void updateTree(char[] s, treeNode[] tree,
                       int start, int end, int treenode,
                       int idx, char X)
{

    // If start is equal to end
    // and idx is equal to start
    if ((start == end) && (idx == start))
    {

        // Base Case
        s[idx] = X;
        tree[treenode].square_sum = (int)Math.Pow(
            X - 'a' + 1, 2);

        return;
    }

    // Calculate middle of the range [start, end]
    int mid = start + ((end - start) / 2);

    // If idx <=  mid
    if (idx <= mid)
    {

        // Function call to left subtree
        updateTree(s, tree, start, mid, (2 * treenode),
                   idx, X);
    }

    // Otherwise
    else
    {

        // Function call to the right subtree
        updateTree(s, tree, mid + 1, end,
                 (2 * treenode) + 1, idx, X);
    }

    // Update the current node
    tree[treenode].square_sum = tree[(2 * treenode)].square_sum +
                                tree[(2 * treenode) + 1].square_sum;
}

// Function to perform the given queries
static void PerformQuery(String S, String[,] Q)
{
    int n = S.Length;

    // Stores the segment tree
    treeNode[] tree = new treeNode[(4 * n) + 1];

    // Traverse the segment tree
    for(int i = 0; i <= (4 * n); i = i + 1)
    {

        // Assign 0 to each node
        tree[i] = new treeNode(0);
    }

    char[] s = S.ToCharArray();

    // Builds segment tree
    buildTree(s, tree, 0, n - 1, 1);

    // Traverse the query array Q[][]
    for(int i = 0; i < Q.GetLength(0); i++)
    {

        // If query is of type S
        if (Q[i,0] == "S")
        {

            // Stores the left boundary
            int L = Int32.Parse(Q[i,1]);

            // Stores the right boundary
            int R = Int32.Parse(Q[i,2]);

            // Prints the sum of squares of the
            // alphabetic positions of the characters
            Console.WriteLine(querySquareSum(
                tree, 0, n - 1, 1, L, R));
        }

        // Otherwise
        else if (Q[i,0] == "U")
        {

            // Stores the index of the
            // character to be updated
            int I = Int32.Parse(Q[i,1]);

            // Update the segment tree
            updateTree(s, tree, 0, n - 1, 1, I,
                       Q[i,2][0]);
        }
    }
}

// Driver Code

    static public void Main (){

        // Input
    string S = "geeksforgeeks";
    string[,] Q = { { "S", "0", "2" },
                     { "S", "1", "2" },
                     { "U", "1", "a" },
                     { "S", "0", "2" },
                     { "S", "4", "5" } };
    // Function call
    PerformQuery(S, Q);

    }
}

// This code is contributed by unknown2108.
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Structure of a node
// of a Segment Tree
class treeNode
{
    constructor( square_sum)
    {
        this.square_sum = square_sum;
    }
}

// Function to construct the Segment Tree
function buildTree(s,tree,start,end,treenode)
{
    // If start and end are equal
    if (start == end)
    {

        // Assign squares of positions
        // of the characters
        tree[treenode].square_sum = Math.pow(
            s[start].charCodeAt(0) - 'a'.charCodeAt(0) + 1, 2);

        return;
    }

    // Stores the mid value of
    // the range [start, end]
    let mid = start + Math.floor((end - start) / 2);

    // Recursive call to left subtree
    buildTree(s, tree, start, mid, 2 * treenode);

    // Recursive call to right subtree
    buildTree(s, tree, mid + 1, end, 1 + 2 * treenode);

    // Update the current node
    tree[treenode].square_sum = tree[(2 * treenode)].square_sum +
                                tree[(2 * treenode) + 1].square_sum;
}

// Function to perform the queries of type 2
function  querySquareSum(tree,start,end,treenode,l,r)
{
    // No overlap
    if ((l > end) || (r < start))
    {
        return 0;
    }

    // If l <= start and r >= end
    if ((l <= start) && (r >= end))
    {

        // Return the value of treeNode
        return tree[treenode].square_sum;
    }

    // Calculate middle of the range [start, end]
    let mid = start + Math.floor((end - start) / 2);

    // Function call to left subtree
    let X = querySquareSum(tree, start, mid,
                           2 * treenode, l, r);

    // Function call to right subtree
    let Y = +querySquareSum(tree, mid + 1, end,
                            1 + 2 * treenode, l, r);

    // Return the sum of X and Y
    return X + Y;
}

// Function to perform update
// queries on a Segment Tree
function updateTree(s,tree,start,end,treenode,idx,X)
{
    // If start is equal to end
    // and idx is equal to start
    if ((start == end) && (idx == start))
    {

        // Base Case
        s[idx] = X;
        tree[treenode].square_sum = Math.pow(
            X.charCodeAt(0) - 'a'.charCodeAt(0) + 1, 2);

        return;
    }

    // Calculate middle of the range [start, end]
    let mid = start + Math.floor((end - start) / 2);

    // If idx <=  mid
    if (idx <= mid)
    {

        // Function call to left subtree
        updateTree(s, tree, start, mid, (2 * treenode),
                   idx, X);
    }

    // Otherwise
    else
    {

        // Function call to the right subtree
        updateTree(s, tree, mid + 1, end,
                 (2 * treenode) + 1, idx, X);
    }

    // Update the current node
    tree[treenode].square_sum = tree[(2 * treenode)].square_sum +
                                tree[(2 * treenode) + 1].square_sum;
}

// Function to perform the given queries
function PerformQuery(S,Q)
{
     let n = S.length;

    // Stores the segment tree
    let tree = new Array((4 * n) + 1);

    // Traverse the segment tree
    for(let i = 0; i <= (4 * n); i = i + 1)
    {

        // Assign 0 to each node
        tree[i] = new treeNode(0);
    }

    let s = S.split("");

    // Builds segment tree
    buildTree(s, tree, 0, n - 1, 1);

    // Traverse the query array Q[][]
    for(let i = 0; i < Q.length; i++)
    {

        // If query is of type S
        if (Q[i][0] == "S")
        {

            // Stores the left boundary
            let L = parseInt(Q[i][1]);

            // Stores the right boundary
            let R = parseInt(Q[i][2]);

            // Prints the sum of squares of the
            // alphabetic positions of the characters
            document.write(querySquareSum(
                tree, 0, n - 1, 1, L, R)+"<br>");
        }

        // Otherwise
        else if (Q[i][0] == "U")
        {

            // Stores the index of the
            // character to be updated
            let I = parseInt(Q[i][1]);

            // Update the segment tree
            updateTree(s, tree, 0, n - 1, 1, I,
                       Q[i][2][0]);
        }
    }
}

// Driver Code
let S = "geeksforgeeks";

let Q=[[ "S", "0", "2" ],
                     [ "S", "1", "2" ],
                     [ "U", "1", "a" ],
                     [ "S", "0", "2" ],
                     [ "S", "4", "5" ]]
// Function call
PerformQuery(S, Q);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
99
50
75
397
```

***时间复杂度:**O((N+M)* log N)*
***辅助空间:** O(N)*