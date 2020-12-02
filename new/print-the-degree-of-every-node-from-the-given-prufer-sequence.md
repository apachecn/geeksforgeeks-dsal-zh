# 打印给定 Prufer 序列

中每个节点的度数

> 原文： [https://www.geeksforgeeks.org/print-the-degree-of-every-node-from-the-given-prufer-sequence/](https://www.geeksforgeeks.org/print-the-degree-of-every-node-from-the-given-prufer-sequence/)

给定 [Prufer 序列](https://www.geeksforgeeks.org/prufer-code-tree-creation/)，任务是查找由 Prufer 序列构成的树的所有节点的度数。

**示例：**

```
Input: arr[] = {4, 1, 3, 4} 
Output: 2 1 2 3 1 1

The tree is:
2----4----3----1----5
     |
     6 

Input: arr[] = {1, 2, 2} 
Output: 2 3 1 1 1

```

**简单方法**是使用 Prufer 序列创建树，然后找到所有节点的度数。

**高效方法：**创建一个**度[]** 数组，其大小比穿刺针序列的长度大 2 个，因为穿刺针序列的长度为 **N – 2** **N** 是节点数。 首先，用 **1** 填充度数组。 对 Prufer 序列进行迭代，并增加度表中每个元素的频率。 该方法之所以有效，是因为 Prufer 序列中节点的频率比树中的度数小 1。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print the degrees of every 
// node in the tree made by 
// the given Prufer sequence 
void printDegree(int prufer[], int n) 
{ 
    int node = n + 2; 

    // Hash-table to mark the 
    // degree of every node 
    int degree[n + 2 + 1]; 

    // Initially let all the degrees be 1 
    for (int i = 1; i <= node; i++) 
        degree[i] = 1; 

    // Increase the count of the degree 
    for (int i = 0; i < n; i++) 
        degree[prufer[i]]++; 

    // Print the degree of every node 
    for (int i = 1; i <= node; i++) { 
        cout << degree[i] << " "; 
    } 
} 

// Driver code 
int main() 
{ 
    int a[] = { 4, 1, 3, 4 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    printDegree(a, n); 

    return 0; 
} 

```

## 爪哇

```

// Java implementation of the approach 
import java.util.*; 

class GFG  
{ 

    // Function to print the degrees of every 
    // node in the tree made by 
    // the given Prufer sequence 
    static void printDegree(int prufer[], int n)  
    { 
        int node = n + 2; 

        // Hash-table to mark the 
        // degree of every node 
        int[] degree = new int[n + 2 + 1]; 

        // Initially let all the degrees be 1 
        for (int i = 1; i <= node; i++) 
        { 
            degree[i] = 1; 
        } 

        // Increase the count of the degree 
        for (int i = 0; i < n; i++)  
        { 
            degree[prufer[i]]++; 
        } 

        // Print the degree of every node 
        for (int i = 1; i <= node; i++)  
        { 
            System.out.print(degree[i] + " "); 
        } 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        int a[] = {4, 1, 3, 4}; 
        int n = a.length; 
        printDegree(a, n); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

## Python3

```

# Python3 implementation of the approach  

# Function to print the degrees of  
# every node in the tree made by  
# the given Prufer sequence  
def printDegree(prufer, n):  

    node = n + 2 

    # Hash-table to mark the  
    # degree of every node  
    degree = [1] * (n + 2 + 1)  

    # Increase the count of the degree  
    for i in range(0, n):  
        degree[prufer[i]] += 1 

    # Print the degree of every node  
    for i in range(1, node+1):   
        print(degree[i], end = " ")  

# Driver code  
if __name__ == "__main__": 

    a = [4, 1, 3, 4]  
    n = len(a)  
    printDegree(a, n)  

# This code is contributed by Rituraj Jain 

```

## C＃

```

// C# implementation of the approach 
using System; 

class GFG  
{ 

// Function to print the degrees of every 
// node in the tree made by 
// the given Prufer sequence 
static void printDegree(int []prufer, int n)  
{ 
    int node = n + 2; 

    // Hash-table to mark the 
    // degree of every node 
    int[] degree = new int[n + 2 + 1]; 

    // Initially let all the degrees be 1 
    for (int i = 1; i <= node; i++) 
    { 
        degree[i] = 1; 
    } 

    // Increase the count of the degree 
    for (int i = 0; i < n; i++)  
    { 
        degree[prufer[i]]++; 
    } 

    // Print the degree of every node 
    for (int i = 1; i <= node; i++)  
    { 
        Console.Write(degree[i] + " "); 
    } 
} 

// Driver code 
public static void Main(String[] args)  
{ 
    int []a = {4, 1, 3, 4}; 
    int n = a.Length; 
    printDegree(a, n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
2 1 2 3 1 1

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。