# 最长正确括号子序列的范围查询

> 原文:[https://www . geesforgeks . org/range-query-最长-正确-括号-subsequence/](https://www.geeksforgeeks.org/range-queries-longest-correct-bracket-subsequence/)

给定一个括号序列，或者换句话说，一个长度为 n 的字符串，由字符“(”和“)”组成。查找给定查询范围的序列的最大正确括号子序列的长度。*注意:正确的括号序列是指具有匹配的括号对或包含另一个嵌套的正确括号序列的序列。例如()、(())、()()都是一些正确的括号顺序。*

示例:

```
Input : S = ())(())(())(
        Start Index of Range = 0, 
        End Index of Range = 11
Output : 10
Explanation:  Longest Correct Bracket Subsequence is ()(())(())

Input : S = ())(())(())(
        Start Index of Range = 1, 
        End Index of Range = 2
Output : 0

```

[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)可以有效解决这个问题

**在段树的每个节点上，我们存储以下内容:**

```
1) a - Number of correctly matched pairs of brackets.
2) b - Number of unused open brackets.  
3) c - Number of unused closed brackets. 
```

**(未使用的开括号–表示它们不能与任何闭括号匹配，未使用的闭括号–表示它们不能与任何开括号匹配，例如 S =)(包含一个未使用的开括号和一个未使用的闭括号)**

**对于每个区间[L，R]，我们可以在区间[MID + 1，R]中匹配 X 个未使用的开括号'('在区间[L，MID]中与未使用的闭括号')'，其中
X =最小值(未使用的数量'('在[L，MID]中，未使用的数量')'在[MID + 1，R])中)
因此，X 也是通过组合构建的正确匹配对的数量。
所以，对于区间[左，右]**

**1)正确匹配对的总数成为左子级中正确匹配对和右子级中正确匹配对的总和，以及分别来自左子级和右子级的未使用'('和未使用')'的组合数。**

```
<font size="3">a<sub>[L, R]</sub> = a<sub>[L, MID]</sub> + a<sub>[MID + 1, R]</sub> + X</font>
```

**2)未使用的开括号总数变成左子括号中未使用的开括号和右子括号中未使用的开括号的总和减去 X(减–因为我们使用了右子括号中的 X unused '('从左子括号开始匹配未使用的')。**

```
<font size="3">a<sub>[L, R]</sub> = b<sub>[L, MID]</sub> + b<sub>[MID + 1, R]</sub> - X</font> 
```

**3)类似地，对于未设置的闭括号，以下关系成立。**

```
<font size="3">a<sub>[L, R]</sub> = c<sub>[L, MID]</sub> + c<sub>[MID + 1, R]</sub> - X</font>
```

**其中 a、b 和 c 是上面针对要存储的每个节点描述的表示。**

**下面是上述方法在 C++中的实现。**

```
/* CPP Program to find the longest correct
   bracket subsequence in a given range */
#include <bits/stdc++.h>
using namespace std;

/* Declaring Structure for storing
   three values in each segment tree node */
struct Node {
    int pairs;
    int open; // unused
    int closed; // unused

    Node()
    {
        pairs = open = closed = 0;
    }
};

// A utility function to get the middle index from corner indexes.
int getMid(int s, int e) { return s + (e - s) / 2; }

// Returns Parent Node after merging its left and right child
Node merge(Node leftChild, Node rightChild)
{
    Node parentNode;
    int minMatched = min(leftChild.open, rightChild.closed);
    parentNode.pairs = leftChild.pairs + rightChild.pairs + minMatched;
    parentNode.open = leftChild.open + rightChild.open - minMatched;
    parentNode.closed = leftChild.closed + rightChild.closed - minMatched;
    return parentNode;
}

// A recursive function that constructs Segment Tree 
// for string[ss..se]. si is index of current node in
// segment tree st
void constructSTUtil(char str[], int ss, int se, Node* st,
                                                 int si)
{
    // If there is one element in string, store it in
    // current node of segment tree and return
    if (ss == se) {

        // since it contains one element, pairs 
        // will be zero
        st[si].pairs = 0;

        // check whether that one element is opening 
        // bracket or not
        st[si].open = (str[ss] == '(' ? 1 : 0);

        // check whether that one element is closing
        // bracket or not
        st[si].closed = (str[ss] == ')' ? 1 : 0);

        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the relation
    // of values in this node
    int mid = getMid(ss, se);
    constructSTUtil(str, ss, mid, st, si * 2 + 1);
    constructSTUtil(str, mid + 1, se, st, si * 2 + 2);

    // Merge left and right child into the Parent Node
    st[si] = merge(st[si * 2 + 1], st[si * 2 + 2]);
}

/* Function to construct segment tree from given
   string. This function allocates memory for segment 
   tree and calls constructSTUtil() to fill the 
   allocated memory */
Node* constructST(char str[], int n)
{
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Declaring array of structure Allocate memory
    Node* st = new Node[max_size];

    // Fill the allocated memory st
    constructSTUtil(str, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

/* A Recursive function to get the desired 
   Maximum Sum Sub-Array,
The following are parameters of the function-

st     --> Pointer to segment tree 
si --> Index of the segment tree Node 
ss & se  --> Starting and ending indexes of the 
             segment represented by
                 current Node, i.e., tree[index]
qs & qe  --> Starting and ending indexes of query range */
Node queryUtil(Node* st, int ss, int se, int qs,
               int qe, int si)
{
    // No overlap
    if (ss > qe || se < qs) {

        // returns a Node for out of bounds condition
        Node nullNode;
        return nullNode;
    }

    // Complete overlap
    if (ss >= qs && se <= qe) {
        return st[si];
    }

    // Partial Overlap Merge results of Left
    // and Right subtrees
    int mid = getMid(ss, se);
    Node left = queryUtil(st, ss, mid, qs, qe, si * 2 + 1);
    Node right = queryUtil(st, mid + 1, se, qs, qe, si * 2 + 2);

    // merge left and right subtree query results
    Node res = merge(left, right);
    return res;
}

/* Returns the maximum length correct bracket 
   subsequencebetween start and end
   It mainly uses queryUtil(). */
int query(Node* st, int qs, int qe, int n)
{
    Node res = queryUtil(st, 0, n - 1, qs, qe, 0);

    // since we are storing numbers pairs
    // and have to return maximum length, hence
    // multiply no of pairs by 2
    return 2 * res.pairs;
}

// Driver Code
int main()
{
    char str[] = "())(())(())(";
    int n = strlen(str);

    // Build segment tree from given string
    Node* st = constructST(str, n);

    int startIndex = 0, endIndex = 11;
    cout << "Maximum Length Correct Bracket"
           " Subsequence between "
         << startIndex << " and " << endIndex << " = "
         << query(st, startIndex, endIndex, n) << endl;

    startIndex = 1, endIndex = 2;
    cout << "Maximum Length Correct Bracket"
           " Subsequence between "
         << startIndex << " and " << endIndex << " = "
         << query(st, startIndex, endIndex, n) << endl;

    return 0;
}
```

****Output:**

```
Maximum Length Correct Bracket Subsequence between 0 and 11 = 10
Maximum Length Correct Bracket Subsequence between 1 and 2 = 0

```** 

**每个查询的时间复杂度为 **O(logN)** ，其中 N 是字符串的大小。**