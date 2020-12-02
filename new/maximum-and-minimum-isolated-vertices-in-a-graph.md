# 图形

中的最大和最小孤立顶点

> 原文： [https://www.geeksforgeeks.org/maximum-and-minimum-isolated-vertices-in-a-graph/](https://www.geeksforgeeks.org/maximum-and-minimum-isolated-vertices-in-a-graph/)

给定图形的“ n”个顶点和“ m”个边。 找到图形中可能的孤立顶点的最小数量和最大数量。
**范例：**

```
Input : 4 2
Output : Minimum 0
         Maximum 1

1--2 3--4 <---Minimum -  No isolated vertex
1--2   <--- Maximum - 1 Isolated vertex i.e. 4
   |
   3

Input : 5 2
Output : Minimum 1
         Maximum 2

1--2 3--4 5  <-- Minimum - 1 isolated vertex i.e. 5
1--2   4  5  <-- Maximum - 2 isolated vertex i.e. 4 and 5
   |
   3

```

1.  对于最少数量的孤立顶点，我们仅通过一条边连接两个顶点。 每个顶点应仅连接到另一个顶点，并且每个顶点应具有一个度
    。因此，如果边的数量为'm'，并且如果'n'个顶点< = 2 *'m'个边，则存在 没有孤立的顶点，并且如果此条件为假，则存在 n-2 * m 个孤立的顶点。
2.  为了获得最大数量的孤立顶点，我们创建一个多边形，使每个顶点都连接到其他顶点，并且每个顶点与其他每个顶点都有一个对角线。 因此，从 n 个多边形的一个顶点到另一顶点的对角线的数量为 n *（n-3）/ 2，并且连接相邻顶点的边的数量为 n。 因此，边缘的总数为 n *（n-1）/ 2。

下面是上述方法的实现。

## C ++

```

// CPP program to find maximum/minimum number 
// of isolated vertices. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find out the minimum and  
// maximum number of isolated vertices 
void find(int n, int m) 
{ 
    // Condition to find out minimum number  
    // of isolated vertices 
    if (n <= 2 * m) 
        cout << "Minimum " << 0 << endl; 
    else
        cout << "Minimum " << n - 2 * m << endl; 

    // To find out maximum number of isolated  
    // vertices 
    // Loop to find out value of number of  
    // vertices that are connected 
    int i; 
    for (i = 1; i <= n; i++) { 
        if (i * (i - 1) / 2 >= m) 
            break; 
    } 
    cout << "Maximum " << n - i; 
} 

// Driver Function 
int main() 
{ 
    // Number of vertices 
    int n = 4; 

    // Number of edges 
    int m = 2; 

    // Calling the function to maximum and  
    // minimum number of isolated vertices 
    find(n, m); 
    return 0; 
} 

```