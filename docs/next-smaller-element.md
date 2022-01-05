# 下一个较小的元素

> 原文:[https://www.geeksforgeeks.org/next-smaller-element/](https://www.geeksforgeeks.org/next-smaller-element/)

给定一个数组，为每个元素打印下一个较小的元素。元素 x 的 NSE 是数组中 x 右侧的第一个较小的元素。不存在较小元素的元素(右侧)，将 NSE 视为-1。
示例:
**a)** 对于任何数组，最右边的元素总是将 NSE 设为-1。
**b)** 对于按递增顺序排序的数组，所有元素的 NSE 都为-1。
**c)** 对于输入数组**【4、8、5、2、25}** ，每个元素的 NSE 如下。

```
Element         NSE
   4      -->    2
   8      -->    5
   5      -->    2
   2      -->   -1
   25     -->   -1
```

**d)** 对于输入数组**【13，7，6，12}，**每个元素的下一个较小元素如下。

```
  Element        NSE
   13      -->    7
   7       -->    6
   6       -->   -1
   12      -->   -1
```

**方法 1(简单)**
使用两个循环:外循环逐个拾取所有元素。内环为外环拾取的元素寻找第一个较小的元素。如果找到一个较小的元素，则该元素被打印为下一个，否则，打印-1。
感谢萨钦提供以下代码。

**时间复杂度** : ![O(N^2)    ](img/ae2c5eb0d06189f7aa4d6d8423e5898f.png "Rendered by QuickLaTeX.com")。最坏的情况发生在所有元素按降序排列的时候。

## C++

```
// Simple C++ program to print
// next smaller elements in a given array
#include "bits/stdc++.h"
using namespace std;

/* prints element and NSE pair
for all elements of arr[] of size n */
void printNSE(int arr[], int n)
{
    int next, i, j;
    for (i = 0; i < n; i++)
    {
        next = -1;
        for (j = i + 1; j < n; j++)
        {
            if (arr[i] > arr[j])
            {
                next = arr[j];
                break;
            }
        }
        cout << arr[i] << " -- "
             << next << endl;
    }
}

// Driver Code
int main()
{
    int arr[]= {11, 13, 21, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    printNSE(arr, n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// Simple C program to print next smaller elements
// in a given array
#include<stdio.h>

/* prints element and NSE pair for all elements of
arr[] of size n */
void printNSE(int arr[], int n)
{
    int next, i, j;
    for (i=0; i<n; i++)
    {
        next = -1;
        for (j = i+1; j<n; j++)
        {
            if (arr[i] > arr[j])
            {
                next = arr[j];
                break;
            }
        }
        printf("%d -- %d\n", arr[i], next);
    }
}

int main()
{
    int arr[]= {11, 13, 21, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    printNSE(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to print next
// smaller elements in a given array

class Main {
    /* prints element and NSE pair for
     all elements of arr[] of size n */
    static void printNSE(int arr[], int n)
    {
        int next, i, j;
        for (i = 0; i < n; i++) {
            next = -1;
            for (j = i + 1; j < n; j++) {
                if (arr[i] > arr[j]) {
                    next = arr[j];
                    break;
                }
            }
            System.out.println(arr[i] + " -- " + next);
        }
    }

    public static void main(String args[])
    {
        int arr[] = { 11, 13, 21, 3 };
        int n = arr.length;
        printNSE(arr, n);
    }
}
```

## 计算机编程语言

```
# Function to print element and NSE pair for all elements of list
def printNSE(arr):

    for i in range(0, len(arr), 1):

        next = -1
        for j in range(i + 1, len(arr), 1):
            if arr[i] > arr[j]:
                next = arr[j]
                break

        print(str(arr[i]) + " -- " + str(next))

# Driver program to test above function
arr = [11, 13, 21, 3]
printNSE(arr)

# This code is contributed by Sunny Karira
```

## C#

```
// Simple C# program to print next
// smaller elements in a given array
using System;

class GFG {

    /* prints element and NSE pair for
    all elements of arr[] of size n */
    static void printNSE(int[] arr, int n)
    {
        int next, i, j;
        for (i = 0; i < n; i++) {
            next = -1;
            for (j = i + 1; j < n; j++) {
                if (arr[i] > arr[j]) {
                    next = arr[j];
                    break;
                }
            }
            Console.WriteLine(arr[i] + " -- " + next);
        }
    }

    // driver code
    public static void Main()
    {
        int[] arr = { 11, 13, 21, 3 };
        int n = arr.Length;

        printNSE(arr, n);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to print next
// smaller elements in a given array

/* prints element and NSE pair for
   all elements of arr[] of size n */
function printNSE($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        $next = -1;
        for ($j = $i + 1; $j < $n; $j++)
        {
            if ($arr[$i] > $arr[$j])
            {
                $next = $arr[$j];
                break;
            }
        }
        echo $arr[$i]." -- ". $next."\n";

    }
}

    // Driver Code
    $arr= array(11, 13, 21, 3);
    $n = count($arr);
    printNSE($arr, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Simple Javascript program to print
// next smaller elements in a given array

/* prints element and NSE pair
for all elements of arr[] of size n */
function printNSE(arr, n)
{
    var next, i, j;
    for (i = 0; i < n; i++)
    {
        next = -1;
        for (j = i + 1; j < n; j++)
        {
            if (arr[i] > arr[j])
            {
                next = arr[j];
                break;
            }
        }
        document.write( arr[i] + " -- "
             + next+"<br>" );
    }
}

// Driver Code
var arr= [11, 13, 21, 3];  
var n = arr.length;
printNSE(arr, n);

</script>
```

**Output**

```
11 -- 3
13 -- 3
21 -- 3
3 -- -1

```

**方法 2(使用段树和二分搜索法)**

这个方法也很简单，如果你知道段树和二分搜索法。让我们考虑一个数组![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")，假设![a_{i}  ](img/0d551e4a3072e72d4b194e43c4fb06b6.png "Rendered by QuickLaTeX.com")的神经元特异性烯醇化酶是![a_{j}  ](img/9cb1bc94db8be584f0d37dbce4e92088.png "Rendered by QuickLaTeX.com")，我们只需要在![i + 1  ](img/ecc593da4fe5ef52cda504c3421f0264.png "Rendered by QuickLaTeX.com")到![n - 1  ](img/5f8bf755ae0a9fb350a96a4260a281d3.png "Rendered by QuickLaTeX.com")的范围内为![j  ](img/6366ae6e5f22e9dc0560b6369584e22c.png "Rendered by QuickLaTeX.com")到二分搜索法。![j  ](img/6366ae6e5f22e9dc0560b6369584e22c.png "Rendered by QuickLaTeX.com")将是第一个索引![k  ](img/6dce11affafcfd36e54cc73b709157c6.png "Rendered by QuickLaTeX.com")，这样从索引![i + 1  ](img/ecc593da4fe5ef52cda504c3421f0264.png "Rendered by QuickLaTeX.com")到![k  ](img/6dce11affafcfd36e54cc73b709157c6.png "Rendered by QuickLaTeX.com") ( ![\forall k\in [i+1, n - 1]  ](img/fd30ec6b41974984f7cd11f1fe9b180c.png "Rendered by QuickLaTeX.com"))的元素范围最小值小于![a_{i}  ](img/0d551e4a3072e72d4b194e43c4fb06b6.png "Rendered by QuickLaTeX.com")。

**时间复杂度:** ![O(N(log(N))^2)  ](img/2fd8ee719fbf0bdb54386e289c6c616e.png "Rendered by QuickLaTeX.com")。对于每个![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")数组元素，我们做一个二分搜索法，包括![ log(N)  ](img/62829b148efa588308cc3914918e9d0d.png "Rendered by QuickLaTeX.com")步骤，每个步骤花费![log(N)   ](img/17c4d349fba4da743fa042f967489e70.png "Rendered by QuickLaTeX.com")操作【范围最小查询】。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Program to find next smaller element for all elements in
// an array, using segment tree and binary search

// --------Segment Tree Starts Here-----------------

vector<int> seg_tree;

// combine function for combining two nodes of the tree, in
// this case we need to take min of two
int combine(int a, int b) { return min(a, b); }

// build function, builds seg_tree based on vector parameter
// arr
void build(vector<int>& arr, int node, int tl, int tr)
{
    // if current range consists only of one element, then
    // node should be this element
    if (tl == tr) {
        seg_tree[node] = arr[tl];
    }
    else {
        // divide the build operations into two parts
        int tm = (tr - tl) / 2 + tl;

        build(arr, 2 * node, tl, tm);
        build(arr, 2 * node + 1, tm + 1, tr);

        // combine the results from two parts, and store it
        // into current node
        seg_tree[node] = combine(seg_tree[2 * node],
                                 seg_tree[2 * node + 1]);
    }
}

// query function, returns minimum in the range [l, r]
int query(int node, int tl, int tr, int l, int r)
{
    // if range is invalid, then return infinity
    if (l > r) {
        return INT32_MAX;
    }

    // if range completely aligns with a segment tree node,
    // then value of this node should be returned
    if (l == tl && r == tr) {
        return seg_tree[node];
    }

    // else divide the query into two parts
    int tm = (tr - tl) / 2 + tl;

    int q1 = query(2 * node, tl, tm, l, min(r, tm));
    int q2 = query(2 * node + 1, tm + 1, tr, max(l, tm + 1),
                   r);

    // and combine the results from the two parts and return
    // it
    return combine(q1, q2);
}

// --------Segment Tree Ends Here-----------------

void printNSE(vector<int> arr, int n)
{
    seg_tree = vector<int>(4 * n);

    // build segment tree initially
    build(arr, 1, 0, n - 1);

    int q, l, r, mid, ans;
    for (int i = 0; i < n; i++) {
        // binary search for ans in range [i + 1, n - 1],
        // initially ans is -1 representing there is no NSE
        // for this element
        l = i + 1;
        r = n - 1;
        ans = -1;

        while (l <= r) {
            mid = (r - l) / 2 + l;
            // q is the minimum element in range [l, mid]
            q = query(1, 0, n - 1, l, mid);

            // if the minimum element in range [l, mid] is
            // less than arr[i], then mid can be answer, we
            // mark it, and look for a better answer in left
            // half. Else if q is greater than arr[i], mid
            // can't be an answer, we should search in right
            // half

            if (q < arr[i]) {
                ans = arr[mid];
                r = mid - 1;
            }
            else {
                l = mid + 1;
            }
        }

        // print NSE for arr[i]
        cout << arr[i] << " ---> " << ans << "\n";
    }
}

// Driver program to test above functions
int main()
{
    vector<int> arr = { 11, 13, 21, 3 };
    printNSE(arr, 4);
    return 0;
}
```

**Output**

```
11 ---> 3
13 ---> 3
21 ---> 3
3 ---> -1

```

**方法 3(使用线段树和坐标压缩)**

在这种方法中，我们在压缩数组元素的索引上构建一个段树:

1.  沿着这条线，我们将构建一个数组![aux   ](img/4c9b44bd6c3c58043706c0ef75950d71.png "Rendered by QuickLaTeX.com")-使得![aux[i]  ](img/e071ceda99f8686399d4ccca24749caf.png "Rendered by QuickLaTeX.com")是输入数组中![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")出现的最小索引。
2.  很容易看出，我们需要压缩输入数组来构建这个数组![aux  ](img/24bb277c1fd20ef8aa3a306b39aa3e0d.png "Rendered by QuickLaTeX.com")，因为如果![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")超过![10^7  ](img/9d7fc484f7030383ff6bb72f51ee86f8.png "Rendered by QuickLaTeX.com")(在线裁判的内存限制)，我们很可能会出现分割错误。
3.  为了压缩，我们对输入数组进行排序，然后对于数组中的每个新值，如果可能的话，我们将其映射到相应的较小值。使用这些映射值生成一个与输入数组顺序相同的![compressed  ](img/9bae4940ebb3b94397eaa97b6381781a.png "Rendered by QuickLaTeX.com")数组。
4.  现在我们已经完成了压缩，我们可以从查询部分开始:
    *   假设在上一步中，我们将数组压缩为![ctr  ](img/a3037ed6a0747ce6ce11654cb77e0f9b.png "Rendered by QuickLaTeX.com")个不同的值。最初设置![aux[i] =  -1 \forall i \in [0, ctr)  ](img/eb0079a678a6ac230430bf77812c3f2a.png "Rendered by QuickLaTeX.com")，这表示到目前为止，任何索引都没有处理任何值。
    *   以相反的顺序遍历压缩数组，这意味着在过去，我们只处理右侧的元素。
        *   对于![compressed[i]  ](img/ae7415420e2937e0c98e1538921e9e1e.png "Rendered by QuickLaTeX.com")，使用段树查询(并存储在![ans[i]  ](img/5bbcf70ef8fd6c557dded29db32c103f.png "Rendered by QuickLaTeX.com")中)值的最小索引![[0, compressed[i])  ](img/c4d0e66d5a62a9e1aa042b9869153b81.png "Rendered by QuickLaTeX.com")，这一定是![compressed[i]  ](img/ae7415420e2937e0c98e1538921e9e1e.png "Rendered by QuickLaTeX.com")的 NSE！
        *   将![compressed[i]  ](img/ae7415420e2937e0c98e1538921e9e1e.png "Rendered by QuickLaTeX.com")的索引更新为![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")。
5.  我们存储了所有数组元素的 NSEs 索引，我们可以轻松地打印 NSEs 本身，如代码所示。

**注意:**在实现中我们使用 *INT32_MAX* 而不是-1，因为存储 *INT32_MAX* 不会影响我们的最小段树，并且仍然服务于识别未处理值的目的。

**时间复杂度** : ![O(Nlog(N))  ](img/11800cd73564bc1f3de848efdee4308e.png "Rendered by QuickLaTeX.com")

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Program to find next smaller element for all elements in
// an array, using segment tree and coordinate compression

// --------Segment Tree Starts Here-----------------

vector<int> seg_tree;

// combine function for combining two nodes of the tree, in
// this case we need to take min of two
int combine(int a, int b) { return min(a, b); }

// build function, builds seg_tree based on vector parameter
// arr
void build(vector<int>& arr, int node, int tl, int tr)
{
    // if current range consists only of one element, then
    // node should be this element
    if (tl == tr) {
        seg_tree[node] = arr[tl];
    }
    else {
        // divide the build operations into two parts
        int tm = (tr - tl) / 2 + tl;

        build(arr, 2 * node, tl, tm);
        build(arr, 2 * node + 1, tm + 1, tr);

        // combine the results from two parts, and store it
        // into current node
        seg_tree[node] = combine(seg_tree[2 * node],
                                 seg_tree[2 * node + 1]);
    }
}

// update function, used to make a point update, update
// arr[pos] to new_val and make required changes to segtree
void update(int node, int tl, int tr, int pos, int new_val)
{
    // if current range only contains one point, this must
    // be arr[pos], update the corresponding node to new_val
    if (tl == tr) {
        seg_tree[node] = new_val;
    }
    else {
        // else divide the range into two parts
        int tm = (tr - tl) / 2 + tl;

        // if pos lies in first half, update this half, else
        // update second half
        if (pos <= tm) {
            update(2 * node, tl, tm, pos, new_val);
        }
        else {
            update(2 * node + 1, tm + 1, tr, pos, new_val);
        }

        // combine results from both halfs
        seg_tree[node] = combine(seg_tree[2 * node],
                                 seg_tree[2 * node + 1]);
    }
}

// query function, returns minimum in the range [l, r]
int query(int node, int tl, int tr, int l, int r)
{
    // if range is invalid, then return infinity
    if (l > r) {
        return INT32_MAX;
    }

    // if range completely aligns with a segment tree node,
    // then value of this node should be returned
    if (l == tl && r == tr) {
        return seg_tree[node];
    }

    // else divide the query into two parts
    int tm = (tr - tl) / 2 + tl;

    int q1 = query(2 * node, tl, tm, l, min(r, tm));
    int q2 = query(2 * node + 1, tm + 1, tr, max(l, tm + 1),
                   r);

    // and combine the results from the two parts and return
    // it
    return combine(q1, q2);
}

// --------Segment Tree Ends Here-----------------

void printNSE(vector<int> original, int n)
{
    vector<int> sorted(n);
    map<int, int> encode;

    // -------Coordinate Compression Starts Here ------

    // created a temporary sorted array out of original
    for (int i = 0; i < n; i++) {
        sorted[i] = original[i];
    }
    sort(sorted.begin(), sorted.end());

    // encode each value to a new value in sorted array
    int ctr = 0;
    for (int i = 0; i < n; i++) {
        if (encode.count(sorted[i]) == 0) {
            encode[sorted[i]] = ctr++;
        }
    }

    // use encode to compress original array
    vector<int> compressed(n);
    for (int i = 0; i < n; i++) {
        compressed[i] = encode[original[i]];
    }

    // -------Coordinate Compression Ends Here ------

    // Create an aux array of size ctr, and build a segtree
    // based on this array

    vector<int> aux(ctr, INT32_MAX);
    seg_tree = vector<int>(4 * ctr);

    build(aux, 1, 0, ctr - 1);

    // For each compressed[i], query for index of NSE and
    // update segment tree

    vector<int> ans(n);
    for (int i = n - 1; i >= 0; i--) {
        ans[i] = query(1, 0, ctr - 1, 0, compressed[i] - 1);
        update(1, 0, ctr - 1, compressed[i], i);
    }

    // Print -1 if NSE doesn't exist, otherwise print NSE
    // itself

    for (int i = 0; i < n; i++) {
        cout << original[i] << " ---> ";
        if (ans[i] == INT32_MAX) {
            cout << -1;
        }
        else {
            cout << original[ans[i]];
        }
        cout << "\n";
    }
}

// Driver program to test above functions
int main()
{
    vector<int> arr = { 11, 13, 21, 3 };
    printNSE(arr, 4);
    return 0;
}
```

**Output**

```
11 ---> 3
13 ---> 3
21 ---> 3
3 ---> -1

```

**方法 4(使用叠加)**
这个问题类似于[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。这里，我们在堆栈中以递增的顺序维护项目(而不是在下一个更大的元素问题中递减)。

1.  将第一个元素推入堆栈。
2.  一个接一个地拾取剩余的元素，并按照以下步骤循环。
    *   将当前元素标记为*下一个*。
    *   如果栈不为空，则比较*下一个*与栈顶。如果下一个的*比顶部小，那么下一个*的*就是顶部的 NSE。当顶部大于下一个*时，继续从堆栈中弹出。*下一步*成为所有此类弹出元素的神经元特异性烯醇化酶
    *   将下一个推入堆栈
3.  步骤 2 中的循环结束后，从堆栈中弹出所有元素，并打印-1 作为它们的下一个元素。

**注意:**为了达到同样的顺序，我们使用了一堆对，其中第一个元素是值，第二个元素是数组元素的索引。

**时间复杂度:** ![O(N)   ](img/23f09f991be3459af525bfd21659fc83.png "Rendered by QuickLaTeX.com")

## C++

```
// A Stack based C++ program to find next
// smaller element for all array elements
#include <bits/stdc++.h>
using namespace std;

// prints NSE for elements of array arr[] of size n

void printNSE(int arr[], int n)
{
    stack<pair<int, int> > s;
    vector<int> ans(n);

    // iterate for rest of the elements
    for (int i = 0; i < n; i++) {
        int next = arr[i];

        // if stack is empty then this element can't be NSE
        // for any other element, so just push it to stack
        // so that we can find NSE for it, and continue
        if (s.empty()) {
            s.push({ next, i });
            continue;
        }

        // while stack is not empty and the top element is
        // greater than next
        //  a) NSE for top is next, use top's index to
        //    maintain original order
        //  b) pop the top element from stack

        while (!s.empty() && s.top().first > next) {
            ans[s.top().second] = next;
            s.pop();
        }

        // push next to stack so that we can find NSE for it

        s.push({ next, i });
    }

    // After iterating over the loop, the remaining elements
    // in stack do not have any NSE, so set -1 for them

    while (!s.empty()) {
        ans[s.top().second] = -1;
        s.pop();
    }

    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ---> " << ans[i] << endl;
    }
}

// Driver program to test above functions
int main()
{
    int arr[] = { 11, 13, 21, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printNSE(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Stack based Java program to find next
// smaller element for all array elements
// in same order as input.
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {
    /* prints element and NSE pair for all
    elements of arr[] of size n */
    public static void printNSE(int arr[], int n)
    {
        Stack<Integer> s = new Stack<Integer>();
        HashMap<Integer, Integer> mp
            = new HashMap<Integer, Integer>();

        /* push the first element to stack */
        s.push(arr[0]);

        // iterate for rest of the elements
        for (int i = 1; i < n; i++) {

            if (s.empty()) {
                s.push(arr[i]);
                continue;
            }

            /* if stack is not empty, then
    pop an element from stack.
    If the popped element is greater
    than next, then
    a) print the pair
    b) keep popping while elements are
    greater and stack is not empty */

            while (s.empty() == false
                   && s.peek() > arr[i]) {
                mp.put(s.peek(), arr[i]);
                s.pop();
            }

            /* push next to stack so that we can find
            next smaller for it */
            s.push(arr[i]);
        }

        /* After iterating over the loop, the remaining
        elements in stack do not have the next smaller
        element, so print -1 for them */
        while (s.empty() == false) {
            mp.put(s.peek(), -1);
            s.pop();
        }

        for (int i = 0; i < n; i++)
            System.out.println(arr[i] + " ---> "
                               + mp.get(arr[i]));
    }

    /* Driver program to test above functions */
    public static void main(String[] args)
    {
        int arr[] = { 11, 13, 21, 3 };
        int n = arr.length;
        printNSE(arr, n);
    }
}
```

## 蟒蛇 3

```
# A Stack based Python3 program to find next
# smaller element for all array elements
# in same order as input.using System;

""" prints element and NSE pair for all
elements of arr[] of size n """

def printNSE(arr, n):
    s = []
    mp = {}

    # push the first element to stack
    s.append(arr[0])

    # iterate for rest of the elements
    for i in range(1, n):
        if (len(s) == 0):
            s.append(arr[i])
            continue

        """ if stack is not empty, then
        pop an element from stack.
        If the popped element is greater
        than next, then
        a) print the pair
        b) keep popping while elements are
        greater and stack is not empty """
        while (len(s) != 0 and s[-1] > arr[i]):
            mp[s[-1]] = arr[i]
            s.pop()

        """ push next to stack so that we can find
        next smaller for it """
        s.append(arr[i])

    """ After iterating over the loop, the remaining
    elements in stack do not have the next smaller
    element, so print -1 for them """
    while (len(s) != 0):
        mp[s[-1]] = -1
        s.pop()

    for i in range(n):
        print(arr[i], "--->", mp[arr[i]])

arr = [11, 13, 21, 3]
n = len(arr)
printNSE(arr, n)

# This code is contributed by decode2207.
```

## C#

```
// A Stack based C# program to find next
// smaller element for all array elements
// in same order as input.using System;
using System;
using System.Collections.Generic;

class GFG {
    /* prints element and NSE pair for all
    elements of arr[] of size n */
    public static void printNSE(int[] arr, int n)
    {
        Stack<int> s = new Stack<int>();
        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        /* push the first element to stack */
        s.Push(arr[0]);

        // iterate for rest of the elements
        for (int i = 1; i < n; i++) {
            if (s.Count == 0) {
                s.Push(arr[i]);
                continue;
            }
            /* if stack is not empty, then
            pop an element from stack.
            If the popped element is greater
            than next, then
            a) print the pair
            b) keep popping while elements are
            greater and stack is not empty */
            while (s.Count != 0 && s.Peek() > arr[i]) {
                mp.Add(s.Peek(), arr[i]);
                s.Pop();
            }

            /* push next to stack so that we can find
            next smaller for it */
            s.Push(arr[i]);
        }

        /* After iterating over the loop, the remaining
        elements in stack do not have the next smaller
        element, so print -1 for them */
        while (s.Count != 0) {
            mp.Add(s.Peek(), -1);
            s.Pop();
        }

        for (int i = 0; i < n; i++)
            Console.WriteLine(arr[i] + " ---> "
                              + mp[arr[i]]);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 11, 13, 21, 3 };
        int n = arr.Length;
        printNSE(arr, n);
    }
}
// This code is contributed by
// 29AjayKumar
```

## java 描述语言

```
<script>
    // A Stack based Javascript program to find next
    // smaller element for all array elements
    // in same order as input.

    /* prints element and NSE pair for all
    elements of arr[] of size n */
    function printNSE(arr, n)
    {
        let s = [];
        let mp = new Map();

        /* push the first element to stack */
        s.push(arr[0]);

        // iterate for rest of the elements
        for (let i = 1; i < n; i++)
        {
            if (s.length==0)
            {
                s.push(arr[i]);
                continue;
            }
            /* if stack is not empty, then
            pop an element from stack.
            If the popped element is greater
            than next, then
            a) print the pair
            b) keep popping while elements are
            greater and stack is not empty */
            while (s.length != 0 && s[s.length - 1] > arr[i])
            {
                mp[s[s.length - 1]] = arr[i];
                s.pop();
            }

            /* push next to stack so that we can find
            next smaller for it */
            s.push(arr[i]);
        }

        /* After iterating over the loop, the remaining
        elements in stack do not have the next smaller
        element, so print -1 for them */
        while (s.length != 0)
        {
            mp[s[s.length - 1]] = -1;
            s.pop();
        }

        for (let i = 0; i < n; i++)
            document.write(arr[i] + " ---> " + mp[arr[i]] + "</br>");
    }

    let arr = [11, 13, 21, 3];
    let n = arr.length;
    printNSE(arr, n);

    // This code is contributed by divyesh072019.
</script>
```

**Output**

```
11 ---> 3
13 ---> 3
21 ---> 3
3 ---> -1

```