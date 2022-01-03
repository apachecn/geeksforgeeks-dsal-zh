# 所有顶点的度数总和为 L 的树的数量

> 原文： [https://www.geeksforgeeks.org/number-of-trees-whose-sum-of-degrees-of-all-the-vertices-is-l/](https://www.geeksforgeeks.org/number-of-trees-whose-sum-of-degrees-of-all-the-vertices-is-l/)

给定一个整数`L`，它是某棵树的所有顶点的度数之和。 任务是找到所有这些不同的树（标记为树）的计数。 如果两棵树至少具有一个不同的边，则它们是不同的。

**示例**：

> **输入**：L = 2
> **输出**：1
> 
> **输入**：L = 6
> **输出**：16

**简单解决方案**：一个简单的解决方案是找到树的节点数目，该树的所有顶点的度之和为`L`。 此类树中的节点数为 **n =（L / 2 + 1）**，如[此](https://www.geeksforgeeks.org/sum-of-degrees-of-all-nodes-of-a-undirected-graph/)文章中所述。

现在的解决方案是形成所有可以使用 n 个节点形成的标记树。 这种方法非常复杂，并且对于较大的 n 值，无法使用此过程找出树木的数量。

**有效解决方案**：一种有效的解决方案是使用 [Cayley 公式](https://en.wikipedia.org/wiki/Cayley%27s_formula)查找节点数，该公式指出存在 **n <sup>（n – 2）</sup>** 带有 n 个标记顶点的树。 因此，现在代码的时间复杂度降低到 **`O(N)`**，可以使用模幂将其进一步降低到 **O（logn）**。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 
#define ll long long int 

// Iterative Function to calculate (x^y) in O(log y) 
ll power(int x, ll y) 
{ 

    // Initialize result 
    ll res = 1; 

    while (y > 0) { 

        // If y is odd, multiply x with result 
        if (y & 1) 
            res = (res * x); 

        // y must be even now 
        // y = y / 2 
        y = y >> 1; 
        x = (x * x); 
    } 
    return res; 
} 

// Function to return the count  
// of required trees 
ll solve(int L) 
{ 
    // number of nodes 
    int n = L / 2 + 1; 

    ll ans = power(n, n - 2); 

    // Return the result 
    return ans; 
} 

// Driver code 
int main() 
{ 
    int L = 6; 

    cout << solve(L); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.io.*; 

class GFG 
{ 

// Iterative Function to calculate (x^y) in O(log y) 
static long power(int x, long y) 
{ 

    // Initialize result 
    long res = 1; 

    while (y > 0) 
    { 

        // If y is odd, multiply x with result 
        if (y==1) 
            res = (res * x); 

        // y must be even now 
        // y = y / 2 
        y = y >> 1; 
        x = (x * x); 
    } 
    return res; 
} 

// Function to return the count  
// of required trees 
static long solve(int L) 
{ 
    // number of nodes 
    int n = L / 2 + 1; 

    long ans = power(n, n - 2); 

    // Return the result 
    return ans; 
} 

// Driver code 
public static void main (String[] args) 
{ 

    int L = 6; 
    System.out.println (solve(L)); 
} 
} 

// This code is contributed by ajit.  

```

## Python

```py

# Python implementation of the approach 

# Iterative Function to calculate (x^y) in O(log y) 
def power(x, y): 

    # Initialize result 
    res = 1; 

    while (y > 0): 

        # If y is odd, multiply x with result 
        if (y %2== 1): 
            res = (res * x); 

        # y must be even now 
        #y = y / 2 
        y = int(y) >> 1; 
        x = (x * x); 
    return res; 

# Function to return the count  
# of required trees 
def solve(L): 

    # number of nodes 
    n = L / 2 + 1; 

    ans = power(n, n - 2); 

    # Return the result 
    return int(ans); 

L = 6; 
print(solve(L)); 

# This code has been contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// Iterative Function to calculate (x^y) in O(log y) 
static long power(int x, long y) 
{ 

    // Initialize result 
    long res = 1; 

    while (y > 0) 
    { 

        // If y is odd, multiply x with result 
        if (y == 1) 
            res = (res * x); 

        // y must be even now 
        // y = y / 2 
        y = y >> 1; 
        x = (x * x); 
    } 
    return res; 
} 

// Function to return the count  
// of required trees 
static long solve(int L) 
{ 
    // number of nodes 
    int n = L / 2 + 1; 

    long ans = power(n, n - 2); 

    // Return the result 
    return ans; 
} 

// Driver code 
static public void Main () 
{ 
    int L = 6; 
    Console.WriteLine(solve(L)); 
} 
} 

// This code is contributed by Tushil.  

```

**Output:**

```
16

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。