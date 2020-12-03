# 检查给定的顶点度代表图还是树

> 原文： [https://www.geeksforgeeks.org/check-whether-given-degrees-vertices-represent-graph-tree/](https://www.geeksforgeeks.org/check-whether-given-degrees-vertices-represent-graph-tree/)

给定顶点数和每个顶点的阶数，其中顶点数为 1、2、3，... n。 任务是识别它是图还是树。 可以假定该图形已连接。

**示例**：

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

顶点的**度由入射或从其离开的边的数量给出。

只需使用树的属性即可完成–**

1.  树是**连接的**，树没有**循环**，而图形可以有循环。

2.  树没有 **n-1** 边，而图没有这种约束。

3.  假设输入图已连接。 我们至少需要 n-1 个边来连接 n 个节点。

如果我们取所有度的总和，则每个边将被计数两次。 因此，对于具有`n`个顶点和 **n – 1** 边的树，所有度数之和应为 **2 *（n – 1）**。 有关详细信息，请参考[握手引理](https://www.geeksforgeeks.org/handshaking-lemma-and-interesting-tree-properties/)。

因此，基本上我们需要检查所有度的和是否为 2 *（n-1）或否。

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

```cs

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

## 的 PHP

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

本文由 [**Ayush Khanduri**](https://in.linkedin.com/in/ayush-khanduri-b4ab87106) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

