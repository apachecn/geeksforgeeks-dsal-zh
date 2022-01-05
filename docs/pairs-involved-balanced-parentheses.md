# 平衡括号中涉及的对

> 原文:[https://www . geesforgeks . org/pairs-涉案-平衡-括号/](https://www.geeksforgeeks.org/pairs-involved-balanced-parentheses/)

给定一串括号，任务是在给定的范围内找到平衡序列中涉及的括号对的数量。
**例:**

```
Input : ((())(()
Range : 1 5
Range : 3 8
Output : 2
         2
Explanation :  In range 1 to 5 ((()), 
there are the two pairs. In range 3 to 8 ())
((), there are the two pairs.

Input : )()()))
Range : 1 2
Range : 4 7
Output : 0
         1
Explanation :  In range 1 to 2 )( there 
is no any pair. In range 4 to 7 ())), 
there is the only pair
```

**先决条件:** [段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)
**方法:**
这里，在段树中，对于每个节点，保留一些简单的元素，如整数或集合或向量等。
为每个节点保留三个整数:
1。t =区间内的答案。
2。o =删除括号后剩余的左括号“(”的数量，这些括号属于长度为 t 的间隔中的正确括号序列。c =删除括号后剩余的结束括号')'的数量在这个长度为 t 的间隔中属于正确括号序列的那些。
现在，有了这些变量，使用段树可以很容易地回答查询。
**以下是上述方法的实施:**

## C++

```
// CPP code to find the number of pairs
// involved in balanced parantheses
#include <bits/stdc++.h>
using namespace std;

// Our struct node
struct node {

    // three variables required
    int t, o, c;
};

// Declare array of nodes of very big
// size which acts as segment tree here.
struct node tree_arr[5 * 1000];

// To build a segment tree we pass 1 as
// 'id' 0 as 'l' and l as 'n'.
// Here, we consider query's interval as [x, y)
void build(int id, int l, int r, string s)
{
    /* this base condition is common to
       build any segment tree*/
    // This is the base
    // Only one element left
    if (r - l < 2) {

        // If that element is open bracket
        if (s[l] == '(')
            tree_arr[id].o = 1;

        // If that element is open bracket
        else
            tree_arr[id].c = 1;
        return;
    }

    // Next three lines are common
    // for any segment tree.
    int mid = (l + r) / 2;

    // for left tree
    build(2 * id, l, mid, s);

    // for right tree
    build(2 * id + 1, mid, r, s);

    // Here we take minimum of left tree
    // opening brackets and right tree
    // closing brackets
    int tmp = min(tree_arr[2 * id].o,
                  tree_arr[2 * id + 1].c);

    // we add that to our answer.
    tree_arr[id].t = tree_arr[2 * id].t +
              tree_arr[2 * id + 1].t + tmp;

    // Remove the answer from opening brackets
    tree_arr[id].o = tree_arr[2 * id].o +
               tree_arr[2 * id + 1].o - tmp;

    // Remove the answer from opening brackets
    tree_arr[id].c = tree_arr[2 * id].c +
               tree_arr[2 * id + 1].c - tmp;
}

// This will return the answer for each query.
// Here we consider query's interval as [x, y)
node segment(int x, int y, int id,
             int l, int r, string s)
{
    // If the given interval is out of range
    if (l >= y || x >= r) {
        struct node tem;
        tem.t = 0;
        tem.o = 0;
        tem.c = 0;
        return tem;
    }

    // If the given interval completely lies
    if (x <= l && r <= y)
        return tree_arr[id];

    // Next three lines are common for
    // any segment tree.
    int mid = (l + r) / 2;

    // For left tree
    struct node a =
           segment(x, y, 2 * id, l, mid, s);

    // For right tree
    struct node b =
           segment(x, y, 2 * id + 1, mid, r, s);

    // Same as made in build function
    int temp;
    temp = min(a.o, b.c);
    struct node vis;
    vis.t = a.t + b.t + temp;
    vis.o = a.o + b.o - temp;
    vis.c = a.c + b.c - temp;

    return vis;
}

// Driver code
int main()
{
    string s = "((())(()";
    int n = s.size();

    // range for query
    int a = 3, b = 8;

    build(1, 0, n, s);

    // Here we consider query's interval as [a, b)
    // We subtract 1 from 'a' because indexes start
    // from 0.
    struct node p = segment(a-1, b, 1, 0, n, s);
    cout << p.t << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 code to find the number of pairs
# involved in balanced parantheses

# Our struct node
class node :
    def __init__(self):
        # three variables required
        self.t = 0
        self.o = 0
        self.c = 0

# Declare array of nodes of very big
# size which acts as segment tree here.
tree_arr = [node()]*(5 * 1000)

# To build asegmenttree we pass 1 as
# 'id' 0 as 'l' and l as 'n'.
# Here, we consider query's interval as [x, y)
def build(id, l, r, s):
    global tree_arr

    tree_arr[id] = node()

    # this base condition is common to
    # build any segment tree
    # This is the base
    # Only one element left
    if (r - l < 2) :

        # If that element is open bracket
        if (s[l] == "("):
            tree_arr[id].o = 1

        # If that element is open bracket
        else:
            tree_arr[id].c = 1
        return

    # Next three lines are common
    # for any segment tree.
    mid = int( (l + r) / 2)

    # for left tree
    build(2 * id, l, mid, s)

    # for right tree
    build(2 * id + 1, mid, r, s)

    # Here we take minimum of left tree
    # opening brackets and right tree
    # closing brackets
    tmp = min(tree_arr[2 * id].o,
                tree_arr[2 * id + 1].c)
    # we add that to our answer.
    tree_arr[id].t = tree_arr[2 * id].t + \
                    tree_arr[2 * id + 1].t + tmp

    # Remove the answer from opening brackets
    tree_arr[id].o = tree_arr[2 * id].o + \
                    tree_arr[2 * id + 1].o - tmp

    # Remove the answer from opening brackets
    tree_arr[id].c = tree_arr[2 * id].c + \
                    tree_arr[2 * id + 1].c - tmp

# This will return the answer for each query.
# Here we consider query's interval as [x, y)
def segment(x, y, id, l, r, s):

    global tree_arr

    # If the given interval is out of range
    if (l >= y or x >= r) :
        tem= node()
        tem.t = 0
        tem.o = 0
        tem.c = 0
        return tem

    # If the given interval completely lies
    if (x <= l and r <= y):
        return tree_arr[id]

    # Next three lines are common for
    # any segment tree.
    mid = int((l + r) / 2)

    # For left tree
    a = segment(x, y, 2 * id, l, mid, s)

    # For right tree
    b = segment(x, y, 2 * id + 1, mid, r, s)

    # Same as made in build function
    temp= 0
    temp = min(a.o, b.c)
    vis = node()

    vis.t = a.t + b.t + temp
    vis.o = a.o + b.o - temp
    vis.c = a.c + b.c - temp
    return vis

# Driver code

s = "((())(()"
n = len(s)

# range for query
a = 3
b = 8

build(1, 0, n, s)

# Here we consider query's interval as [a, b)
# We subtract 1 from 'a' because indexes start
# from 0.
p = segment(a-1, b, 1, 0, n, s)
print(p.t )

# This code is contributed by Arnab Kundu
```

**Output:** 

```
2
```