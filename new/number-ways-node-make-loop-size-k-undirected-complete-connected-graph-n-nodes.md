# 从特定节点

开始的大小为 k 的循环数

> 原文： [https://www.geeksforgeeks.org/number-ways-node-make-loop-size-k-undirected-complete-connected-graph-n-nodes/](https://www.geeksforgeeks.org/number-ways-node-make-loop-size-k-undirected-complete-connected-graph-n-nodes/)

给定两个正整数 **n，k** 。 考虑完整连接图中 n 个节点的无向​​完整连接图。 任务是计算可以从任何节点开始并通过访问 K 个节点返回该节点的方式的数目。

例子：

```
Input : n = 3, k = 3
Output : 2

Input : n = 4, k = 2
Output : 3

```

令 **f（n，k）**为一个函数，该函数返回可以从任意节点开始并通过访问 K 个节点返回该节点的方式数。

如果我们从一个节点开始和结束，那么对于中间节点，我们将有 K – 1 个选择，因为我们已经在开始时选择了一个节点。 对于每个中间选择，您都有 n – 1 个选项。 因此，这将产生（n – 1） <sup>k – 1</sup> ，但随后我们必须删除所有导致较小循环的选择，因此我们减去 **f（n，k –1）**。

因此，递归关系变为：

f（n，k）=（n – 1） <sup>k – 1</sup> – f（n，k – 1），基本情况为 f（n，2 ）= n –1。

展开时，

f（n，k）=（n – 1） <sup>k – 1</sup> –（n – 1） <sup>k – 2</sup> +（n – 1） <sup>k – 3</sup> …..（n – 1）（例如 eqn 1）

将 f（n，k）除以（n – 1），

f（n，k）/（n – 1）=（n – 1） <sup>k – 2</sup> –（n – 1） <sup>k – 3</sup> +（n – 1） <sup>k – 4</sup> ….. 1（等式 2）

在加上等式 1 和等式 2 时，

f（n，k）+ f（n，k）/（n – 1）=（n – 1） <sup>k – 1</sup> +（-1） <sup>k</sup>

f（n，k）*（（n -1）+1）/（n – 1）=（n – 1） <sup>k – 1</sup> +（- 1） <sup>k</sup>

![ f(n, k) =  \frac{(n-1)^{k} + (-1)^{k}(n-1)}{n}](img/7fa00fe326bc96fadcf528fcab986e48.png "Rendered by QuickLaTeX.com")

以下是此方法的实现：

## C++

```cpp

// C++ Program to find number of cycles of length 
// k in a graph with n nodes. 
#include <bits/stdc++.h> 
using namespace std; 

// Return the Number of ways from a 
// node to make a loop of size K in undirected 
// complete connected graph of N nodes 
int numOfways(int n, int k) 
{ 
    int p = 1; 

    if (k % 2) 
        p = -1; 

    return (pow(n - 1, k) + p * (n - 1)) / n; 
} 

// Driven Program 
int main() 
{ 
    int n = 4, k = 2; 
    cout << numOfways(n, k) << endl; 
    return 0; 
} 

```

## Java

```java

// Java Program to find number of 
// cycles of length k in a graph 
// with n nodes. 
public class GFG { 

    // Return the Number of ways 
    // from a node to make a loop 
    // of size K in undirected 
    // complete connected graph of 
    // N nodes 
    static int numOfways(int n, int k) 
    { 
        int p = 1; 

        if (k % 2 != 0) 
            p = -1; 

        return (int)(Math.pow(n - 1, k) 
                    + p * (n - 1)) / n; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int n = 4, k = 2; 

        System.out.println(numOfways(n, k)); 
    } 
} 

// This code is contributed by Sam007\. 

```

## Python

```py

# python Program to find number of  
# cycles of length k in a graph  
# with n nodes. 

# Return the Number of ways from a 
# node to make a loop of size K in 
# undirected complete connected  
# graph of N nodes 
def numOfways(n,k): 

    p = 1

    if (k % 2): 
        p = -1

    return (pow(n - 1, k) +
                   p * (n - 1)) / n 

# Driver code 
n = 4
k = 2
print (numOfways(n, k)) 

# This code is contributed by Sam007\. 

```

## C#

```cs

// C# Program to find number of cycles 
// of length k in a graph with n nodes. 
using System; 

class GFG { 

    // Return the Number of ways from 
    // a node to make a loop of size 
    // K in undirected complete  
    // connected graph of N nodes 
    static int numOfways(int n, int k) 
    { 
        int p = 1; 

        if (k % 2 != 0) 
            p = -1; 

        return (int)(Math.Pow(n - 1, k) 
                     + p * (n - 1)) / n; 
    } 

    // Driver code 
    static void Main() 
    { 
        int n = 4, k = 2; 

        Console.Write( numOfways(n, k) ); 
    } 
} 

// This code is contributed by Sam007\. 

```

## 的 PHP

```

<?php 
// PHP Program to find number 
// of cycles of length 
// k in a graph with n nodes. 

// Return the Number of ways from a 
// node to make a loop of size K  
// in undirected complete connected 
// graph of N nodes 
function numOfways( $n, $k) 
{ 
$p = 1; 

if ($k % 2) 
    $p = -1; 

return (pow($n - 1, $k) +  
        $p * ($n - 1)) / $n; 
} 

    // Driver Code 
    $n = 4; 
    $k = 2; 
    echo numOfways($n, $k); 

// This code is contributed by vt_m.  
?> 

```

**Output:**

```
3

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。