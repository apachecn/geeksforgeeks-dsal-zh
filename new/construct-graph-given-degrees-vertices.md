# 根据所有顶点的给定度构建图

> 原文： [https://www.geeksforgeeks.org/construct-graph-given-degrees-vertices/](https://www.geeksforgeeks.org/construct-graph-given-degrees-vertices/)

这是一个 C ++程序，用于为给定的度数序列生成图，该算法为给定的度数序列生成无向图，它不包括自边缘和多边。

**示例**：

```
Input : degrees[] = {2, 2, 1, 1}
Output :  (0)  (1)  (2)  (3)
    (0)    0    1    1    0                              
    (1)    1    0    0    1                   
    (2)    1    0    0    0                       
    (3)    0    1    0    0     
Explanation : We are given that there
are four vertices with degree of vertex
0 as 2, degree of vertex 1 as 2, degree
of vertex 2 as 1 and degree of vertex 3
as 1\. Following is graph that follows
given conditions.                   
    (0)----------(1)
     |            | 
     |            | 
     |            |
    (2)          (3) 

```

**方法**：
1-输入顶点数及其对应度数的输入。
2-声明邻接矩阵 mat [] []以存储图形。
3-要创建图形，请创建第一个循环以连接每个顶点“ i”。
4-秒嵌套循环，用于将顶点“ i”连接到旁边的每个有效顶点“ j”。
5-如果顶点“ i”和“ j”的度大于零，请连接它们。
6-打印邻接矩阵。

根据以上说明，以下是实现：

## C++

```cpp

// C++ program to generate a graph for a 
// given fixed degrees 
#include <bits/stdc++.h> 
using namespace std; 

// A function to print the adjacency matrix. 
void printMat(int degseq[], int n) 
{ 
    // n is number of vertices 
    int mat[n][n]; 
    memset(mat, 0, sizeof(mat)); 

    for (int i = 0; i < n; i++) { 
        for (int j = i + 1; j < n; j++) { 

            // For each pair of vertex decrement 
            // the degree of both vertex. 
            if (degseq[i] > 0 && degseq[j] > 0) { 
                degseq[i]--; 
                degseq[j]--; 
                mat[i][j] = 1; 
                mat[j][i] = 1; 
            } 
        } 
    } 

    // Print the result in specified format 
    cout << "\n"
         << setw(3) << "     "; 
    for (int i = 0; i < n; i++) 
        cout << setw(3) << "(" << i << ")"; 
    cout << "\n\n"; 
    for (int i = 0; i < n; i++) { 
        cout << setw(4) << "(" << i << ")"; 
        for (int j = 0; j < n; j++) 
            cout << setw(5) << mat[i][j]; 
        cout << "\n"; 
    } 
} 

// driver program to test above function 
int main() 
{ 
    int degseq[] = { 2, 2, 1, 1, 1 }; 
    int n = sizeof(degseq) / sizeof(degseq[0]); 
    printMat(degseq, n); 
    return 0; 
} 

```

## Java

```java

// Java program to generate a graph for a 
// given fixed degrees 
import java.util.*; 

class GFG 
{ 

// A function to print the adjacency matrix. 
static void printMat(int degseq[], int n) 
{ 
    // n is number of vertices 
    int [][]mat = new int[n][n]; 

    for (int i = 0; i < n; i++)  
    { 
        for (int j = i + 1; j < n; j++) 
        { 

            // For each pair of vertex decrement 
            // the degree of both vertex. 
            if (degseq[i] > 0 && degseq[j] > 0)  
            { 
                degseq[i]--; 
                degseq[j]--; 
                mat[i][j] = 1; 
                mat[j][i] = 1; 
            } 
        } 
    } 

    // Print the result in specified format 
    System.out.print("\n" + setw(3) + "     "); 

    for (int i = 0; i < n; i++) 
        System.out.print(setw(3) + "(" + i + ")"); 
    System.out.print("\n\n"); 
    for (int i = 0; i < n; i++) 
    { 
        System.out.print(setw(4) + "(" + i + ")"); 

        for (int j = 0; j < n; j++) 
            System.out.print(setw(5) + mat[i][j]); 
        System.out.print("\n"); 
    } 
} 

static String setw(int n) 
{ 
    String space = ""; 
    while(n-- > 0) 
        space += " "; 
    return space; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int degseq[] = { 2, 2, 1, 1, 1 }; 
    int n = degseq.length; 
    printMat(degseq, n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```

# Python3 program to generate a graph  
# for a given fixed degrees  

# A function to print the adjacency matrix.  
def printMat(degseq, n): 

    # n is number of vertices  
    mat = [[0] * n for i in range(n)] 

    for i in range(n): 
        for j in range(i + 1, n): 

            # For each pair of vertex decrement  
            # the degree of both vertex.  
            if (degseq[i] > 0 and degseq[j] > 0): 
                degseq[i] -= 1
                degseq[j] -= 1
                mat[i][j] = 1
                mat[j][i] = 1

    # Print the result in specified form 
    print("      ", end = " ") 
    for i in range(n): 
        print(" ", "(", i, ")", end = "")  
    print() 
    print() 
    for i in range(n): 
        print(" ", "(", i, ")", end = "") 
        for j in range(n): 
            print("     ", mat[i][j], end = "")  
        print() 

# Driver Code 
if __name__ == '__main__':  
    degseq = [2, 2, 1, 1, 1]  
    n = len(degseq) 
    printMat(degseq, n) 

# This code is contributed by PranchalK 

```

## C#

```cs

// C# program to generate a graph for a 
// given fixed degrees 
using System; 

class GFG 
{ 

// A function to print the adjacency matrix. 
static void printMat(int []degseq, int n) 
{ 
    // n is number of vertices 
    int [,]mat = new int[n, n]; 

    for (int i = 0; i < n; i++)  
    { 
        for (int j = i + 1; j < n; j++) 
        { 

            // For each pair of vertex decrement 
            // the degree of both vertex. 
            if (degseq[i] > 0 && degseq[j] > 0)  
            { 
                degseq[i]--; 
                degseq[j]--; 
                mat[i, j] = 1; 
                mat[j, i] = 1; 
            } 
        } 
    } 

    // Print the result in specified format 
    Console.Write("\n" + setw(3) + "     "); 

    for (int i = 0; i < n; i++) 
        Console.Write(setw(3) + "(" + i + ")"); 
    Console.Write("\n\n"); 
    for (int i = 0; i < n; i++) 
    { 
        Console.Write(setw(4) + "(" + i + ")"); 

        for (int j = 0; j < n; j++) 
            Console.Write(setw(5) + mat[i, j]); 
        Console.Write("\n"); 
    } 
} 

static String setw(int n) 
{ 
    String space = ""; 
    while(n-- > 0) 
        space += " "; 
    return space; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int []degseq = { 2, 2, 1, 1, 1 }; 
    int n = degseq.Length; 
    printMat(degseq, n); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
        (0)  (1)  (2)  (3)  (4)

   (0)    0    1    1    0    0
   (1)    1    0    0    1    0
   (2)    1    0    0    0    0
   (3)    0    1    0    0    0
   (4)    0    0    0    0    0

```

**时间复杂度**：O（v * v）。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。