# 无限二叉树中两个节点之间的最短距离

> 原文:[https://www . geesforgeks . org/无限二叉树中两个节点之间的最短距离/](https://www.geeksforgeeks.org/shortest-distance-between-two-nodes-in-an-infinite-binary-tree/)

假设您有一个无限长的二叉树，其模式如下:

```

               1
            /      \
           2        3
         /  \      / \
        4    5    6   7
      /  \  / \  / \ / \
     .  .  .  . .  .  .  .
```

给定两个值为 x 和 y 的节点，任务是找出两个节点之间最短路径的长度。

**示例:**

```
Input:  x = 2, y = 3
Output: 2

Input: x = 4, y = 6
Output: 4
```

一种简单的方法是将两个节点的所有祖先存储在两个数据结构中([向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)、[数组](https://www.geeksforgeeks.org/array-data-structure/)等)..)并对 vector1 中的第一个元素(let index i)执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，检查它是否存在于 vector2 中。如果有，返回 vector2 中元素的索引(让 x)。答案是这样的

> 距离= v1 . size()–1–I+v2 . size()–1–x

下面是上述方法的实现。

## C++

```
// C++ program to find distance
// between two nodes
// in a infinite binary tree
#include <bits/stdc++.h>
using namespace std;

// to stores ancestors of first given node
vector<int> v1;
// to stores ancestors of first given node
vector<int> v2;

// normal binary search to find the element
int BinarySearch(int x)
{
    int low = 0;
    int high = v2.size() - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        if (v2[mid] == x)
            return mid;
        else if (v2[mid] > x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// function to make ancestors of first node
void MakeAncestorNode1(int x)
{
    v1.clear();
    while (x) {
        v1.push_back(x);
        x /= 2;
    }
    reverse(v1.begin(), v1.end());
}

// function to make ancestors of second node
void MakeAncestorNode2(int x)
{
    v2.clear();
    while (x) {
        v2.push_back(x);
        x /= 2;
    }
    reverse(v2.begin(), v2.end());
}

// function to find distance between two nodes
int Distance()
{
    for (int i = v1.size() - 1; i >= 0; i--) {
        int x = BinarySearch(v1[i]);
        if (x != -1) {
            return v1.size() - 1 - i + v2.size() - 1 - x;
        }
    }
}

// Driver code
int main()
{
    int node1 = 2, node2 = 3;

    // find ancestors
    MakeAncestorNode1(node1);
    MakeAncestorNode2(node2);

    cout << "Distance between " << node1 <<
    " and " << node2 << " is : " << Distance();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find distance
// between two nodes
// in a infinite binary tree
import java.util.*;
class GFG
{

// to stores ancestors of first given node
static Vector<Integer> v1 = new Vector<Integer>();

// to stores ancestors of first given node
static Vector<Integer> v2 = new Vector<Integer>();

// normal binary search to find the element
static int BinarySearch(int x)
{
    int low = 0;
    int high = v2.size() - 1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (v2.get(mid) == x)
            return mid;
        else if (v2.get(mid) > x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// function to make ancestors of first node
static void MakeAncestorNode1(int x)
{
    v1.clear();
    while (x > 0)
    {
        v1.add(x);
        x /= 2;
    }
    Collections.reverse(v1);
}

// function to make ancestors of second node
static void MakeAncestorNode2(int x)
{
    v2.clear();
    while (x > 0)
    {
        v2.add(x);
        x /= 2;
    }
    Collections.reverse(v2);
}

// function to find distance between two nodes
static int Distance()
{
    for (int i = v1.size() - 1; i >= 0; i--)
    {
        int x = BinarySearch(v1.get(i));
        if (x != -1)
        {
            return v1.size() - 1 - i +
                   v2.size() - 1 - x;
        }
    }
    return Integer.MAX_VALUE;
}

// Driver code
public static void main(String[] args)
{
    int node1 = 2, node2 = 3;

    // find ancestors
    MakeAncestorNode1(node1);
    MakeAncestorNode2(node2);

    System.out.print("Distance between " + node1 +
                      " and " + node2 + " is : " +
                                      Distance());
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the distance between
# two nodes in an infinite binary tree

# normal binary search to find the element
def BinarySearch(x):

    low = 0
    high = len(v2) - 1

    while low <= high:
        mid = (low + high) // 2

        if v2[mid] == x:
            return mid
        elif v2[mid] > x:
            high = mid - 1
        else:
            low = mid + 1

    return -1

# Function to make ancestors of first node
def MakeAncestorNode1(x):

    v1.clear()
    while x:
        v1.append(x)
        x //= 2

    v1.reverse()

# Function to make ancestors of second node
def MakeAncestorNode2(x):

    v2.clear()
    while x:
        v2.append(x)
        x //= 2

    v2.reverse()

# Function to find distance between two nodes
def Distance():

    for i in range(len(v1) - 1, -1, -1):
        x = BinarySearch(v1[i])

        if x != -1:
            return (len(v1) - 1 - i +
                    len(v2) - 1 - x)

# Driver code
if __name__ == "__main__":

    node1, node2 = 2, 3
    v1, v2 = [], []

    # Find ancestors
    MakeAncestorNode1(node1)
    MakeAncestorNode2(node2)

    print("Distance between", node1,
          "and", node2, "is :", Distance())

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find distance
// between two nodes
// in a infinite binary tree
using System;
using System.Collections.Generic;

class GFG
{

// to stores ancestors of first given node
static List<int> v1 = new List<int>();

// to stores ancestors of first given node
static List<int> v2 = new List<int>();

// normal binary search to find the element
static int BinarySearch(int x)
{
    int low = 0;
    int high = v2.Count - 1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (v2[mid] == x)
            return mid;
        else if (v2[mid] > x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// function to make ancestors of first node
static void MakeAncestorNode1(int x)
{
    v1.Clear();
    while (x > 0)
    {
        v1.Add(x);
        x /= 2;
    }
    v1.Reverse();
}

// function to make ancestors of second node
static void MakeAncestorNode2(int x)
{
    v2.Clear();
    while (x > 0)
    {
        v2.Add(x);
        x /= 2;
    }
    v2.Reverse();
}

// function to find distance between two nodes
static int Distance()
{
    for (int i = v1.Count - 1; i >= 0; i--)
    {
        int x = BinarySearch(v1[i]);
        if (x != -1)
        {
            return v1.Count - 1 - i +
                v2.Count - 1 - x;
        }
    }
    return int.MaxValue;
}

// Driver code
public static void Main(String[] args)
{
    int node1 = 2, node2 = 3;

    // find ancestors
    MakeAncestorNode1(node1);
    MakeAncestorNode2(node2);

    Console.Write("Distance between " + node1 +
                   " and " + node2 + " is : " +
                                   Distance());
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to find distance
// between two nodes
// in a infinite binary tree

// to stores ancestors of first given node
let v1 = [];

// to stores ancestors of first given node
let v2 = [];

// normal binary search to find the element
function BinarySearch(x)
{
    let low = 0;
       let high = v2.length - 1;

    while (low <= high)
    {
        let mid = Math.floor((low + high) / 2);

        if (v2[mid] == x)
            return mid;
        else if (v2[mid] > x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return -1;
}

// function to make ancestors of first node
function MakeAncestorNode1(x)
{
    v1=[];
    while (x > 0)
    {
        v1.push(x);
        x = Math.floor(x/2);
    }
    v1.reverse();
}

// function to make ancestors of second node
function MakeAncestorNode2(x)
{
    v2=[];
    while (x > 0)
    {
        v2.push(x);
        x = Math.floor(x/2);
    }
    v2.reverse();
}

// function to find distance between two nodes
function Distance()
{
    for (let i = v1.length - 1; i >= 0; i--)
    {
        let x = BinarySearch(v1[i]);
        if (x != -1)
        {
            return v1.length - 1 - i +
                   v2.length - 1 - x;
        }
    }
    return Number.MAX_VALUE;
}

// Driver code
let node1 = 2, node2 = 3;

// find ancestors
MakeAncestorNode1(node1);
MakeAncestorNode2(node2);

document.write("Distance between " + node1 +
                 " and " + node2 + " is : " +
                 Distance());

// This code is contributed by patel2127
</script>
```

**Output:** 

```
Distance between 2 and 3 is : 2
```

***时间复杂度:** O(log(max(x，y)) * log(max(x，y)))*
***辅助空间:** O(log(max(x，y)))*

一种有效的方法是利用给定的 2*x 和 2*x+1 的性质。继续将两个节点中较大的一个除以 2。如果大的变成小的，那就把另一个分开。在某个阶段，这两个值将是相同的，统计一下除法的次数，这就是答案。

下面是上述方法的实现。

## C++

```
// C++ program to find the distance
// between two nodes in an infinite
// binary tree
#include <bits/stdc++.h>
using namespace std;

// function to find the distance
// between two nodes in an infinite
// binary tree
int Distance(int x, int y)
{
    // swap the smaller
    if (x < y) {
        swap(x, y);
    }
    int c = 0;

    // divide till x!=y
    while (x != y) {

        // keep a count
        ++c;

        // perform division
        if (x > y)
            x = x >> 1;

        // when the smaller
        // becomes the greater
        if (y > x) {
            y = y >> 1;
            ++c;
        }
    }
    return c;
}

// Driver code
int main()
{
    int x = 4, y = 6;
    cout << Distance(x, y);

 return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the distance
// between two nodes in an infinite
// binary tree
class GFG
{

// function to find the distance
// between two nodes in an infinite
// binary tree
static int Distance(int x, int y)
{
    // swap the smaller
    if (x < y)
    {
        int temp = x;
        x = y;
        y = temp;
    }
    int c = 0;

    // divide till x!=y
    while (x != y)
    {

        // keep a count
        ++c;

        // perform division
        if (x > y)
            x = x >> 1;

        // when the smaller
        // becomes the greater
        if (y > x)
        {
            y = y >> 1;
            ++c;
        }
    }
    return c;
}

// Driver code
public static void main(String[] args)
{
    int x = 4, y = 6;
    System.out.println(Distance(x, y));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the distance between
# two nodes in an infinite binary tree

# Function to find the distance between
# two nodes in an infinite binary tree
def Distance(x, y):

    # Swap the smaller
    if x < y:
        x, y = y, x

    c = 0

    # divide till x != y
    while x != y:

        # keep a count
        c += 1

        # perform division
        if x > y:
            x = x >> 1

        # when the smaller becomes
        # the greater
        if y > x:
            y = y >> 1
            c += 1

    return c

# Driver code
if __name__ == "__main__":

    x, y = 4, 6
    print(Distance(x, y))

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program to find the distance
// between two nodes in an infinite
// binary tree
using System;

class GFG
{

// function to find the distance
// between two nodes in an infinite
// binary tree
static int Distance(int x, int y)
{
    // swap the smaller
    if (x < y)
    {
        int temp = x;
        x = y;
        y = temp;
    }
    int c = 0;

    // divide till x!=y
    while (x != y)
    {

        // keep a count
        ++c;

        // perform division
        if (x > y)
            x = x >> 1;

        // when the smaller
        // becomes the greater
        if (y > x)
        {
            y = y >> 1;
            ++c;
        }
    }
    return c;
}

// Driver code
public static void Main(String[] args)
{
    int x = 4, y = 6;
    Console.WriteLine(Distance(x, y));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the distance
// between two nodes in an infinite
// binary tree

// Function to find the distance
// between two nodes in an infinite
// binary tree
function Distance(x, y)
{

    // Swap the smaller
    if (x < y)
    {
        let temp = x;
        x = y;
        y = temp;
    }
    let c = 0;

    // Divide till x!=y
    while (x != y)
    {

        // Keep a count
        ++c;

        // Perform division
        if (x > y)
            x = x >> 1;

        // When the smaller
        // becomes the greater
        if (y > x)
        {
            y = y >> 1;
            ++c;
        }
    }
    return c;
}

// Driver code
let x = 4, y = 6;

document.write(Distance(x, y));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log(max(x，y))*
***辅助空间:** O(1)*
高效的方法已经由 [Striver 提出。](https://auth.geeksforgeeks.org/user/Striver/articles)

**另一种方法:**

主要思路是使用公式 Level(n)+Level(m)–2 * LCA(n，m)。因此，使用对数基数 2 可以很容易地计算出级别，通过将较大的数字除以 2，直到 n 和 m 相等，就可以计算出生命周期评价。

下面是上述方法的实现:

## C++

```
// C++ program to find the distance
// between two nodes in an infinite
// binary tree
#include <bits/stdc++.h>
using namespace std;

int LCA(int n,int m)
{
    // swap to keep n smallest

    if (n > m) {
        swap(n, m);
    }

    // a,b is level of n and m
    int a = log2(n);
    int b = log2(m);

    // divide until n!=m
    while (n != m)
    {
        if (n < m)
            m = m >> 1;

        if (n > m)
            n = n >> 1;
    }

    // now n==m which is the LCA of n ,m

    int v = log2(n);

    return  a + b - 2 * v;
}

// Driver Code
int main()
{
    int n = 2, m = 6;

     // Function call
    cout << LCA(n,m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the distance
// between two nodes in an infinite
// binary tree
import java.util.*;
class GFG{

static int LCA(int n,int m)
{
    // swap to keep n smallest

    if (n > m) {
        int temp = n;
        n = m;
        m = temp;
    }

    // a,b is level of n and m
    int a = (int)(Math.log(n) / Math.log(2));
    int b = (int)(Math.log(m) / Math.log(2));
    // divide until n!=m
    while (n != m)
    {
        if (n < m)
            m = m >> 1;

        if (n > m)
            n = n >> 1;
    }

    // now n==m which is the LCA of n ,m

    int v = (int)(Math.log(n) / Math.log(2));
    return  a + b - 2 * v;
}

// Driver Code
public static void main(String[] args)
{
    int n = 2, m = 6;

     // Function call
    System.out.print(LCA(n,m) +"\n");
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# python program to find the distance
# between two nodes in an infinite
# binary tree
import math
def LCA(n, m):

    # swap to keep n smallest
    if (n > m):
        n, m = m, n

    # a,b is level of n and m
    a = int(math.log2(n))
    b = int(math.log2(m))

    # divide until n!=m
    while (n != m):
        if (n < m):
            m = m >> 1
        if (n > m):
            n = n >> 1

    # now n==m which is the LCA of n ,m
    v = int(math.log2(n))
    return a + b - 2 * v

n = 2
m = 6

# Function call
print(LCA(n,m))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to find the distance
// between two nodes in an infinite
// binary tree
using System;
class GFG{

static int LCA(int n,int m)
{
    // swap to keep n smallest
    if (n > m) {
        int temp = n;
        n = m;
        m = temp;
    }

    // a,b is level of n and m
    int a = (int)(Math.Log(n) / Math.Log(2));
    int b = (int)(Math.Log(m) / Math.Log(2));

    // divide until n!=m
    while (n != m)
    {
        if (n < m)
            m = m >> 1;

        if (n > m)
            n = n >> 1;
    }

    // now n==m which is the LCA of n ,m

    int v = (int)(Math.Log(n) / Math.Log(2));
    return  a + b - 2 * v;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 2, m = 6;

     // Function call
    Console.Write(LCA(n,m) +"\n");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program to find the distance
// between two nodes in an infinite
// binary tree
function LCA(n, m)
{

    // Swap to keep n smallest
    if (n > m)
    {
        let temp = n;
        n = m;
        m = temp;
    }

    // a,b is level of n and m
    let a = Math.log2(n);
    let b = Math.log2(m);

    // Divide until n!=m
    while (n != m)
    {
        if (n < m)
            m = m >> 1;

        if (n > m)
            n = n >> 1;
    }

    // Now n==m which is the LCA of n ,m
    let v = Math.log2(n);

    return a + b - 2 * v;
}

// Driver Code
let n = 2, m = 6;

// Function call
document.write(LCA(n, m));

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
3
```

***时间复杂度:** O(log(max(x，y))*
***辅助空间:** O(1)*