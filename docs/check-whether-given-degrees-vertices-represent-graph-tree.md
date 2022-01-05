# 检查给定的顶点度数是代表图形还是树

> 原文:[https://www . geesforgeks . org/check-是否-给定-度-顶点-表示-图-树/](https://www.geeksforgeeks.org/check-whether-given-degrees-vertices-represent-graph-tree/)

给定顶点数和每个顶点的度，其中顶点数是 1，2，3，…n。任务是识别它是图还是树。可以假设图是连通的。

**示例:**

```
Input : 5
        2 3 1 1 1
Output : Tree
Explanation : The input array indicates that 
              vertex one has degree 2, vertex
              two has degree 3, vertices 3, 4 
              and 5 have degree 1\.  
            1
           / \
          2   3
         / \
        4   5

Input : 3
        2 2 2
Output : Graph      
            1
           / \
          2 - 3

```

顶点的**度由入射或出射的边数给出。
这可以简单地利用树木的特性来完成，比如–**

1.  树是**连接的**，没有**循环**，而图可以有循环。
2.  树正好有 **n-1** 条边，而图没有这样的约束。
3.  给出了输入图是连通的。我们需要至少 n-1 条边来连接 n 个节点。

如果我们取所有度数的总和，每条边将被计算两次。因此，对于具有 **n** 个顶点和**n–1**条边的树，所有度数的总和应为**2 *(n–1)**。详见[握手引理](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)。

所以基本上我们需要检查所有度数的总和是 2*(n-1)还是不是。

## C++

```
// C++ program to check whether input degree
// sequence is graph or tree
#include<bits/stdc++.h>
using namespace std;

// Function returns true for tree
// false for graph
bool check(int degree[], int n)
{
    // Find sum of all degrees
    int deg_sum = 0;
    for (int i = 0; i < n; i++)
        deg_sum += degree[i];

    // Graph is tree if sum is equal to 2(n-1)
    return (2*(n-1) == deg_sum);
}

// Driver program to test above function
int main()
{
    int n = 5;
    int degree[] = {2, 3, 1, 1, 1};

    if (check(degree, n))
        cout << "Tree";
    else
        cout << "Graph";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether input degree 
// sequence is graph or tree 
class GFG 
{

    // Function returns true for tree 
    // false for graph 
    static boolean check(int degree[], int n)
    {
        // Find sum of all degrees 
        int deg_sum = 0;
        for (int i = 0; i < n; i++) 
        {
            deg_sum += degree[i];
        }

        // Graph is tree if sum is equal to 2(n-1) 
        return (2 * (n - 1) == deg_sum);
    }

    // Driver code 
    public static void main(String[] args)
    {
        int n = 5;
        int degree[] = {2, 3, 1, 1, 1};

        if (check(degree, n))
        {
            System.out.println("Tree");
        } 
        else 
        {
            System.out.println("Graph");
        }
    }
} 

// This code has been contributed 
// by 29AjayKumar
```

## 计算机编程语言

```
# Python program to check whether input degree
# sequence is graph or tree
def check(degree, n):

    # Find sum of all degrees
    deg_sum = sum(degree)

    # It is tree if sum is equal to 2(n-1)
    if (2*(n-1) == deg_sum):
        return True
    else:
        return False

#main
n = 5
degree = [2, 3, 1, 1, 1];
if (check(degree, n)):
    print "Tree"
else:
    print "Graph"
```

## C#

```
// C# program to check whether input 
// degree sequence is graph or tree 
using System;

class GFG 
{

    // Function returns true for tree 
    // false for graph 
    static bool check(int[] degree, int n)
    {
        // Find sum of all degrees 
        int deg_sum = 0;
        for (int i = 0; i < n; i++) 
        {
            deg_sum += degree[i];
        }

        // Graph is tree if sum is 
        // equal to 2(n-1) 
        return (2 * (n - 1) == deg_sum);
    }

    // Driver code 
    public static void Main()
    {
        int n = 5;
        int[] degree = {2, 3, 1, 1, 1};

        if (check(degree, n))
        {
            Console.WriteLine("Tree");
        } 
        else
        {
            Console.WriteLine("Graph");
        }
    }
} 

// This code has been contributed 
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether input 
// degree sequence is graph or tree

// Function returns true for tree
// false for graph
function check(&$degree, $n)
{
    // Find sum of all degrees
    $deg_sum = 0;
    for ($i = 0; $i < $n; $i++)
        $deg_sum += $degree[$i];

    // Graph is tree if sum is 
    // equal to 2(n-1)
    return (2 * ($n - 1) == $deg_sum);
}

// Driver Code
$n = 5;
$degree = array(2, 3, 1, 1, 1);

if (check($degree, $n))
    echo "Tree";
else
    echo "Graph";

// This code is contributed by 
// Shivi_Aggarwal
?>
```

**Output:**

```
Tree

```

本文由 **[阿育什·坎德里](https://in.linkedin.com/in/ayush-khanduri-b4ab87106)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。