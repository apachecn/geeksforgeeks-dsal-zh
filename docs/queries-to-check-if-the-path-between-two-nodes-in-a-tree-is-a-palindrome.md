# 查询以检查树中两个节点之间的路径是否是回文

> 原文:[https://www . geesforgeks . org/query-to-check-如果树中两个节点之间的路径是回文/](https://www.geeksforgeeks.org/queries-to-check-if-the-path-between-two-nodes-in-a-tree-is-a-palindrome/)

给定一棵具有 **N** 节点和**N–1**边的树。树的每条边都用一串小写的英文字母标记。您有**问题**查询。在每个查询中，您会得到两个节点 **x** 和 **y** 。对于 **x** 到 **y** 之间的路径，任务是检查是否有可能制作一个新的回文字符串，该字符串使用从节点 **x** 到节点 **y** 的路径中的所有字符。**注意**可以按照自己喜欢的顺序使用字符，根节点永远是 **1** 。
**举例:**

```
Input:
         1
  (bbc)/   \(ac)
      2     3
Q[][] = {{1, 2}, {2, 3}, {3, 1}, {3, 3}}
Output:
Yes
Yes
No
Yes
Query 1: "bbc" can be arranged into "bcb" 
which is a palindrome.
Query 2: "bbcac" -> "bcacb"
Query 3: No permutation of "ac" is palindrome.
Query 4: "acac" -> "acca"

Input:
          1
     /    |     \
   /(ab)  |(bca)  \(bc)
 2        3         4
  \(ab)
    5
Q[][] = {{1, 5}, {4, 5}, {5, 4}}
Output:
Yes
No
No
```

**方法:**对于每个查询，必须计算路径 x 到 y 的字符数。找到字符数后，使用[这篇](https://www.geeksforgeeks.org/check-characters-given-string-can-rearranged-form-palindrome/)文章中讨论的方法，可以很容易地检查字符是否会形成回文。
获取路径 x 到 y 的字符数的步骤

1.  设置每个节点的初始字符数。
2.  更新根的子节点的字符数，然后对其子节点重复相同的过程。
3.  求 x 和 y 的 LCA ( [最低共同祖先](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/))
4.  通过以下步骤计算路径 x 到 y 的字符数:
    对于每个字符，字符计数[I]=(xNodeCharCount[I]–lcaNodeCharCount[I])+(yNodeCharCount[I]–lcaNodeCharCount[I])

5.  现在检查回文是否可以用当前的字符数组成。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX_SIZE = 100005, MAX_CHAR = 26;
int nodeCharactersCount[MAX_SIZE][MAX_CHAR];

vector<int> tree[MAX_SIZE];

// Function that returns true if a palindromic
// string can be formed using the given characters
bool canFormPalindrome(int* charArray)
{

    // Count odd occurring characters
    int oddCount = 0;
    for (int i = 0; i < MAX_CHAR; i++) {
        if (charArray[i] % 2 == 1)
            oddCount++;
    }
    // Return false if odd count is more than 1,
    if (oddCount >= 2)
        return false;
    else
        return true;
}

// Find to find the Lowest Common
// Ancestor in the tree
int LCA(int currentNode, int x, int y)
{
    // Base case
    if (currentNode == x)
        return x;

    // Base case
    if (currentNode == y)
        return y;
    int xLca, yLca;

    // Initially value -1 denotes that
    // we need to find the ancestor
    xLca = yLca = -1;

    // -1 denotes that we need to find the lca
    // for x and y, values other than x and y
    // will be the LCA of x and y
    int gotLca = -1;

    // Iterating in the child
    // substree of the currentNode
    for (int l = 0; l < tree[currentNode].size(); l++) {

        // Next node that will be checked
        int nextNode = tree[currentNode][l];

        // Look for the next child subtree
        int out_ = LCA(nextNode, x, y);

        if (out_ == x)
            xLca = out_;
        if (out_ == y)
            yLca = out_;

        // Both the nodes exist in the different
        // subtrees, in this case parent node
        // will be the lca
        if (xLca != -1 and yLca != -1)
            return currentNode;

        // Handle the cases where LCA is already
        // calculated or both x and y are present
        // in the same subtree
        if (out_ != -1)
            gotLca = out_;
    }
    return gotLca;
}

// Function to calculate the character count for
// each path from node i to 1 (root node)
void buildTree(int i)
{
    for (int l = 0; l < tree[i].size(); l++) {

        int nextNode = tree[i][l];
        for (int j = 0; j < MAX_CHAR; j++) {

            // Updating the character count
            // for each node
            nodeCharactersCount[nextNode][j]
                += nodeCharactersCount[i][j];
        }

        // Look for the child subtree
        buildTree(nextNode);
    }
}

// Function that returns true if a palindromic path
// is possible between the nodes x and y
bool canFormPalindromicPath(int x, int y)
{

    int lcaNode;

    // If both x and y are same then
    // lca will be the node itself
    if (x == y)
        lcaNode = x;

    // Find the lca of x and y
    else
        lcaNode = LCA(1, x, y);

    int charactersCountFromXtoY[MAX_CHAR] = { 0 };

    // Calculating the character count
    // for path node x to y
    for (int i = 0; i < MAX_CHAR; i++) {
        charactersCountFromXtoY[i]
            = nodeCharactersCount[x][i]
              + nodeCharactersCount[y][i]
              - 2 * nodeCharactersCount[lcaNode][i];
    }

    // Checking if we can form the palindrome
    // string with the all character count
    if (canFormPalindrome(charactersCountFromXtoY))
        return true;
    return false;
}

// Function to update character count at node v
void updateNodeCharactersCount(string str, int v)
{

    // Updating the character count at node v
    for (int i = 0; i < str.length(); i++)
        nodeCharactersCount[v][str[i] - 'a']++;
}

// Function to perform the queries
void performQueries(vector<vector<int> > queries, int q)
{
    int i = 0;
    while (i < q) {

        int x = queries[i][0];
        int y = queries[i][1];

        // If path can be a palindrome
        if (canFormPalindromicPath(x, y))
            cout << "Yes\n";
        else
            cout << "No\n";
        i++;
    }
}

// Driver code
int main()
{

    // Fill the complete array with 0
    memset(nodeCharactersCount, 0,
           sizeof(nodeCharactersCount));

    // Edge between 1 and 2 labelled "bbc"
    tree[1].push_back(2);
    updateNodeCharactersCount("bbc", 2);

    // Edge between 1 and 3 labelled "ac"
    tree[1].push_back(3);
    updateNodeCharactersCount("ac", 3);

    // Update the character count
    // from root to the ith node
    buildTree(1);

    vector<vector<int> > queries{ { 1, 2 },
                                  { 2, 3 },
                                  { 3, 1 },
                                  { 3, 3 } };
    int q = queries.size();

    // Perform the queries
    performQueries(queries, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

@SuppressWarnings("unchecked")
class GFG {

    static int MAX_SIZE = 100005, MAX_CHAR = 26;
    static int[][] nodeCharactersCount = new int[MAX_SIZE][MAX_CHAR];

    static Vector<Integer>[] tree = new Vector[MAX_SIZE];

    // Function that returns true if a palindromic
    // string can be formed using the given characters
    static boolean canFormPalindrome(int[] charArray) {

        // Count odd occurring characters
        int oddCount = 0;
        for (int i = 0; i < MAX_CHAR; i++) {
            if (charArray[i] % 2 == 1)
                oddCount++;
        }
        // Return false if odd count is more than 1,
        if (oddCount >= 2)
            return false;
        else
            return true;
    }

    // Find to find the Lowest Common
    // Ancestor in the tree
    static int LCA(int currentNode, int x, int y) {

        // Base case
        if (currentNode == x)
            return x;

        // Base case
        if (currentNode == y)
            return y;
        int xLca, yLca;

        // Initially value -1 denotes that
        // we need to find the ancestor
        xLca = yLca = -1;

        // -1 denotes that we need to find the lca
        // for x and y, values other than x and y
        // will be the LCA of x and y
        int gotLca = -1;

        // Iterating in the child
        // substree of the currentNode
        for (int l = 0; l < tree[currentNode].size(); l++) {

            // Next node that will be checked
            int nextNode = tree[currentNode].elementAt(l);

            // Look for the next child subtree
            int out_ = LCA(nextNode, x, y);

            if (out_ == x)
                xLca = out_;
            if (out_ == y)
                yLca = out_;

            // Both the nodes exist in the different
            // subtrees, in this case parent node
            // will be the lca
            if (xLca != -1 && yLca != -1)
                return currentNode;

            // Handle the cases where LCA is already
            // calculated or both x and y are present
            // in the same subtree
            if (out_ != -1)
                gotLca = out_;
        }
        return gotLca;
    }

    // Function to calculate the character count for
    // each path from node i to 1 (root node)
    static void buildTree(int i) {
        for (int l = 0; l < tree[i].size(); l++) {

            int nextNode = tree[i].elementAt(l);
            for (int j = 0; j < MAX_CHAR; j++) {

                // Updating the character count
                // for each node
                nodeCharactersCount[nextNode][j] += nodeCharactersCount[i][j];
            }

            // Look for the child subtree
            buildTree(nextNode);
        }
    }

    // Function that returns true if a palindromic path
    // is possible between the nodes x and y
    static boolean canFormPalindromicPath(int x, int y) {

        int lcaNode;

        // If both x and y are same then
        // lca will be the node itself
        if (x == y)
            lcaNode = x;

        // Find the lca of x and y
        else
            lcaNode = LCA(1, x, y);

        int[] charactersCountFromXtoY = new int[MAX_CHAR];
        Arrays.fill(charactersCountFromXtoY, 0);

        // Calculating the character count
        // for path node x to y
        for (int i = 0; i < MAX_CHAR; i++) {
            charactersCountFromXtoY[i] = nodeCharactersCount[x][i] +
                                         nodeCharactersCount[y][i]
                               - 2 * nodeCharactersCount[lcaNode][i];
        }

        // Checking if we can form the palindrome
        // string with the all character count
        if (canFormPalindrome(charactersCountFromXtoY))
            return true;
        return false;
    }

    // Function to update character count at node v
    static void updateNodeCharactersCount(String str, int v) {

        // Updating the character count at node v
        for (int i = 0; i < str.length(); i++)
            nodeCharactersCount[v][str.charAt(i) - 'a']++;
    }

    // Function to perform the queries
    static void performQueries(int[][] queries, int q) {
        int i = 0;
        while (i < q) {

            int x = queries[i][0];
            int y = queries[i][1];

            // If path can be a palindrome
            if (canFormPalindromicPath(x, y))
                System.out.println("Yes");
            else
                System.out.println("No");
            i++;
        }
    }

    // Driver Code
    public static void main(String[] args) {

        // Fill the complete array with 0
        for (int i = 0; i < MAX_SIZE; i++) {
            for (int j = 0; j < MAX_CHAR; j++) {
                nodeCharactersCount[i][j] = 0;
            }
        }
        for (int i = 0; i < MAX_SIZE; i++) {
            tree[i] = new Vector<>();
        }

        // Edge between 1 and 2 labelled "bbc"
        tree[1].add(2);
        updateNodeCharactersCount("bbc", 2);

        // Edge between 1 and 3 labelled "ac"
        tree[1].add(3);
        updateNodeCharactersCount("ac", 3);

        // Update the character count
        // from root to the ith node
        buildTree(1);

        int[][] queries = { { 1, 2 }, { 2, 3 }, { 3, 1 }, { 3, 3 } };
        int q = queries.length;

        // Perform the queries
        performQueries(queries, q);
    }
}

// This code is contributed by
// sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

  static int MAX_SIZE = 100005, MAX_CHAR = 26;
  static int[,] nodecharsCount = new int[MAX_SIZE, MAX_CHAR];
  static List<int>[] tree = new List<int>[MAX_SIZE];

  // Function that returns true if a palindromic
  // string can be formed using the given characters
  static bool canFormPalindrome(int[] charArray)
  {

    // Count odd occurring characters
    int oddCount = 0;
    for (int i = 0; i < MAX_CHAR; i++)
    {
      if (charArray[i] % 2 == 1)
        oddCount++;
    }

    // Return false if odd count is more than 1,
    if (oddCount >= 2)
      return false;
    else
      return true;
  }

  // Find to find the Lowest Common
  // Ancestor in the tree
  static int LCA(int currentNode, int x, int y)
  {

    // Base case
    if (currentNode == x)
      return x;

    // Base case
    if (currentNode == y)
      return y;
    int xLca, yLca;

    // Initially value -1 denotes that
    // we need to find the ancestor
    xLca = yLca = -1;

    // -1 denotes that we need to find the lca
    // for x and y, values other than x and y
    // will be the LCA of x and y
    int gotLca = -1;

    // Iterating in the child
    // substree of the currentNode
    for (int l = 0; l < tree[currentNode].Count; l++)
    {

      // Next node that will be checked
      int nextNode = tree[currentNode][l];

      // Look for the next child subtree
      int out_ = LCA(nextNode, x, y);

      if (out_ == x)
        xLca = out_;
      if (out_ == y)
        yLca = out_;

      // Both the nodes exist in the different
      // subtrees, in this case parent node
      // will be the lca
      if (xLca != -1 && yLca != -1)
        return currentNode;

      // Handle the cases where LCA is already
      // calculated or both x and y are present
      // in the same subtree
      if (out_ != -1)
        gotLca = out_;
    }
    return gotLca;
  }

  // Function to calculate the character count for
  // each path from node i to 1 (root node)
  static void buildTree(int i)
  {
    for (int l = 0; l < tree[i].Count; l++)
    {
      int nextNode = tree[i][l];
      for (int j = 0; j < MAX_CHAR; j++)
      {

        // Updating the character count
        // for each node
        nodecharsCount[nextNode,j] += nodecharsCount[i,j];
      }

      // Look for the child subtree
      buildTree(nextNode);
    }
  }

  // Function that returns true if a palindromic path
  // is possible between the nodes x and y
  static bool canFormPalindromicPath(int x, int y)
  {
    int lcaNode;

    // If both x and y are same then
    // lca will be the node itself
    if (x == y)
      lcaNode = x;

    // Find the lca of x and y
    else
      lcaNode = LCA(1, x, y);
    int[] charactersCountFromXtoY = new int[MAX_CHAR];

    // Calculating the character count
    // for path node x to y
    for (int i = 0; i < MAX_CHAR; i++)
    {
      charactersCountFromXtoY[i] = nodecharsCount[x, i] +
        nodecharsCount[y, i]
        - 2 * nodecharsCount[lcaNode, i];
    }

    // Checking if we can form the palindrome
    // string with the all character count
    if (canFormPalindrome(charactersCountFromXtoY))
      return true;
    return false;
  }

  // Function to update character count at node v
  static void updateNodecharsCount(String str, int v)
  {

    // Updating the character count at node v
    for (int i = 0; i < str.Length; i++)
      nodecharsCount[v, str[i] - 'a']++;
  }

  // Function to perform the queries
  static void performQueries(int[,] queries, int q) {
    int i = 0;
    while (i < q) {

      int x = queries[i, 0];
      int y = queries[i, 1];

      // If path can be a palindrome
      if (canFormPalindromicPath(x, y))
        Console.WriteLine("Yes");
      else
        Console.WriteLine("No");
      i++;
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Fill the complete array with 0
    for (int i = 0; i < MAX_SIZE; i++)
    {
      for (int j = 0; j < MAX_CHAR; j++)
      {
        nodecharsCount[i, j] = 0;
      }
    }
    for (int i = 0; i < MAX_SIZE; i++)
    {
      tree[i] = new List<int>();
    }

    // Edge between 1 and 2 labelled "bbc"
    tree[1].Add(2);
    updateNodecharsCount("bbc", 2);

    // Edge between 1 and 3 labelled "ac"
    tree[1].Add(3);
    updateNodecharsCount("ac", 3);

    // Update the character count
    // from root to the ith node
    buildTree(1);

    int[,] queries = { { 1, 2 }, { 2, 3 }, { 3, 1 }, { 3, 3 } };
    int q = queries.GetLength(0);

    // Perform the queries
    performQueries(queries, q);
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MAX_SIZE = 100005, MAX_CHAR = 26;
    let nodeCharactersCount = new Array(MAX_SIZE);

    let tree = new Array(MAX_SIZE);

    // Function that returns true if a palindromic
    // string can be formed using the given characters
    function canFormPalindrome(charArray) {

        // Count odd occurring characters
        let oddCount = 0;
        for (let i = 0; i < MAX_CHAR; i++) {
            if (charArray[i] % 2 == 1)
                oddCount++;
        }
        // Return false if odd count is more than 1,
        if (oddCount >= 2)
            return false;
        else
            return true;
    }

    // Find to find the Lowest Common
    // Ancestor in the tree
    function LCA(currentNode, x, y) {

        // Base case
        if (currentNode == x)
            return x;

        // Base case
        if (currentNode == y)
            return y;
        let xLca, yLca;

        // Initially value -1 denotes that
        // we need to find the ancestor
        xLca = yLca = -1;

        // -1 denotes that we need to find the lca
        // for x and y, values other than x and y
        // will be the LCA of x and y
        let gotLca = -1;

        // Iterating in the child
        // substree of the currentNode
        for (let l = 0; l < tree[currentNode].length; l++) {

            // Next node that will be checked
            let nextNode = tree[currentNode][l];

            // Look for the next child subtree
            let out_ = LCA(nextNode, x, y);

            if (out_ == x)
                xLca = out_;
            if (out_ == y)
                yLca = out_;

            // Both the nodes exist in the different
            // subtrees, in this case parent node
            // will be the lca
            if (xLca != -1 && yLca != -1)
                return currentNode;

            // Handle the cases where LCA is already
            // calculated or both x and y are present
            // in the same subtree
            if (out_ != -1)
                gotLca = out_;
        }
        return gotLca;
    }

    // Function to calculate the character count for
    // each path from node i to 1 (root node)
    function buildTree(i) {
        for (let l = 0; l < tree[i].length; l++) {

            let nextNode = tree[i][l];
            for (let j = 0; j < MAX_CHAR; j++) {

                // Updating the character count
                // for each node
                nodeCharactersCount[nextNode][j] +=
                nodeCharactersCount[i][j];
            }

            // Look for the child subtree
            buildTree(nextNode);
        }
    }

    // Function that returns true if a palindromic path
    // is possible between the nodes x and y
    function canFormPalindromicPath(x, y) {

        let lcaNode;

        // If both x and y are same then
        // lca will be the node itself
        if (x == y)
            lcaNode = x;

        // Find the lca of x and y
        else
            lcaNode = LCA(1, x, y);

        let charactersCountFromXtoY = new Array(MAX_CHAR);
        charactersCountFromXtoY.fill(0);

        // Calculating the character count
        // for path node x to y
        for (let i = 0; i < MAX_CHAR; i++) {
            charactersCountFromXtoY[i] =
            nodeCharactersCount[x][i] +
            nodeCharactersCount[y][i]
            - 2 * nodeCharactersCount[lcaNode][i];
        }

        // Checking if we can form the palindrome
        // string with the all character count
        if (canFormPalindrome(charactersCountFromXtoY))
            return true;
        return false;
    }

    // Function to update character count at node v
    function updateNodeCharactersCount(str, v) {

        // Updating the character count at node v
        for (let i = 0; i < str.length; i++)
            nodeCharactersCount[v][str[i].charCodeAt() -
            'a'.charCodeAt()]++;
    }

    // Function to perform the queries
    function performQueries(queries, q) {
        let i = 0;
        while (i < q) {

            let x = queries[i][0];
            let y = queries[i][1];

            // If path can be a palindrome
            if (canFormPalindromicPath(x, y))
                document.write("Yes" + "</br>");
            else
                document.write("No" + "</br>");
            i++;
        }
    }

    // Fill the complete array with 0
    for (let i = 0; i < MAX_SIZE; i++) {
      nodeCharactersCount[i] = new Array(MAX_CHAR);
      for (let j = 0; j < MAX_CHAR; j++) {
        nodeCharactersCount[i][j] = 0;
      }
    }
    for (let i = 0; i < MAX_SIZE; i++) {
      tree[i] = [];
    }

    // Edge between 1 and 2 labelled "bbc"
    tree[1].push(2);
    updateNodeCharactersCount("bbc", 2);

    // Edge between 1 and 3 labelled "ac"
    tree[1].push(3);
    updateNodeCharactersCount("ac", 3);

    // Update the character count
    // from root to the ith node
    buildTree(1);

    let queries = [ [ 1, 2 ], [ 2, 3 ], [ 3, 1 ], [ 3, 3 ] ];
    let q = queries.length;

    // Perform the queries
    performQueries(queries, q);

</script>
```

## java 描述语言

```
// JavaScript implementation of the approach

let MAX_SIZE = 1000;

let tree = new Array(MAX_SIZE);

for (let i = 0; i < tree.length; i++) {
    tree[i] = [];
}

function addEdgesWithLabel(a, b, str) {
    tree[a].push([b, str]);
    tree[b].push([a, str]);
}

function dfs(node, parent, label, lev) {
    memo[node][0] = parent;
    level[node] = lev;
    label_array[node][0] = label;
    for (let i = 1; i <= log; i++) {
        if (memo[node][i - 1] != -1) {
            memo[node][i] = memo[memo[node][i - 1]][i - 1];
            label_array[node][i] = label_array[node][i] + label_array[memo[node][i - 1]][i - 1];
        }
    }
    for (let i = 0; i < tree[node].length; i++) {
        if (tree[node][i][0] != parent) {
            dfs(tree[node][i][0], node, tree[node][i][1], level[node] + 1)
        }
    }

}

function findPathString(u, v) {

    let res = '';

    if (level[u] < level[v]) {
        let temp = u;

        u = v;

        v = temp;
    }

    for (let i = log; i >= 0; i--) {
        if (level[u] - Math.pow(2, i) >= level[v]) {
            res = res + label_array[u][i];

            u = memo[u][i];
        }
    }

    if (u == v) {
        return res;
    }

    for (let i = log; i >= 0; i--) {
        if (memo[u][i] != memo[v][i]) {
            res = res + label_array[u][i] + label_array[v][i];

            v = memo[v][i];
            u = memo[u][i];
        }
    }
    res = res + label_array[u][0] + label_array[v][0];
    return res;
}

function checkIfPalindrom(str) {
    // Create a list
    let list = [];
    // For each character in input strings,
    // remove character if list contains
    // else add character to list
    for (let i = 0; i < str.length; i++) {
        if (list.includes(str[i]))
            list.splice(list.indexOf(str[i]), 1);
        else
            list.push(str[i]);
    }
    // If character length is even
    // list is expected to be empty or
    // if character length is odd list size
    // is expected to be 1

    // If string length is even
    if (str.length % 2 == 0 && list.length == 0 ||
        (str.length % 2 == 1 && list.length == 1))
        return 'YES';
    // If string length is odd
    else
        return 'NO';
}

let memo = new Array(MAX_SIZE);

let log = Math.ceil(Math.log(MAX_SIZE) / Math.log(2));

for (let i = 0; i < memo.length; i++) {
    memo[i] = new Array(log + 1);

    for (let j = 0; j < log + 1; j++) {
        memo[i][j] = -1;
    }
}

let label_array = new Array(MAX_SIZE);

for (let i = 0; i < label_array.length; i++) {
    label_array[i] = new Array(log + 1);

    for (let j = 0; j < log + 1; j++) {
        label_array[i][j] = '';
    }
}

let level = new Array(MAX_SIZE);
level.fill(0);
addEdgesWithLabel(1, 2, 'bbc');
addEdgesWithLabel(1, 3, 'ac');
dfs(1, -1, '', 0);
document.write(checkIfPalindrom(findPathString(1, 2)) + '<br>');
document.write(checkIfPalindrom(findPathString(2, 3)) + '<br>');
document.write(checkIfPalindrom(findPathString(3, 1)) + '<br>');
document.write(checkIfPalindrom(findPathString(3, 3)) + '<br>');

// This code is contributed by gaurav2146
```

**Output:** 

```
Yes
Yes
No
Yes
```