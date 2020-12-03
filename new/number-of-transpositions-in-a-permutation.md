# 排列中的换位数

> 原文： [https://www.geeksforgeeks.org/number-of-transpositions-in-a-permutation/](https://www.geeksforgeeks.org/number-of-transpositions-in-a-permutation/)

**排列**排列是元素的排列。 n 个元素的排列可以由数字 1，2，…n 的排列以某种顺序表示。 例如。 5 1 4 2 3

**循环符号**排列可以表示为排列循环的组成。 置换周期是置换中彼此交换位置的一组元素。

例如

> P = {5，1，4，2，3}：
> 此处，5 转到 1，1 转到 2，依此类推（根据它们的索引位置）：
> 5-> 1
> 1-> 2
> 2-> 4
> 4-> 3
> 3-> 5
> 因此，它可以表示为一个周期：（5， 1，2，4，3）。
> 
> 现在考虑置换：{5，1，4，3，2}。 这里
> 5-> 1
> 1-> 2
> 2-> 5 关闭 1 个周期。
> 
> 另一个周期是
> 4-> 3
> 3-> 4
> 在周期表示法中，它将表示为（5，1，2）（4，3）。

**换位**

现在，所有循环都可以分解为 2 个循环（换位）的组合。 置换中的换位数目很重要，因为它给出了从标识排列中获得此特定排列所需的 2 个元素交换的最少数目：1、2、3，…n。 该 2 个周期的数量的奇偶性表示排列是偶数还是奇数。

例如

> 周期（5、1、2、4、3）可以写为（5、3）（5、4）（5、2）（5、1）。 4 个换位（偶数）。
> 同样，
> （5，1，2）->（5，2）（5，1）
> （5，1，2）（4，3）->（5 ，2）（5，1）（4，3）。 3 个换位（奇数）。
> 从示例中可以清楚地看出，一个循环的**换位数=循环的长度–1。**

**问题**

给定 n 个数的排列 P <sub>1</sub> ，P <sub>2</sub> ，P <sub>3</sub> ，…P <sub>n [</sub> 。 计算其中的换位数量。

示例：

```
Input: 5 1 4 3 2
Output: 3

```

**方法**：排列可以容易地表示为有向图，其中连接的组件数给出了循环数。 并且（每个分量的大小– 1）给出了该循环的转座数。

**示例排列**：{5，1，4，3，2}->（5，1，2）（4，3）

![Untitled drawing(3)](img/be0c4e35c2b7f3d2930cecae1e3f554f.png)

下面是上述方法的实现。

## C++

```cpp

// CPP Program to find the number of 
// transpositions in a permutation 
#include <bits/stdc++.h> 
using namespace std; 

#define N 1000001 

int visited[N]; 

// This array stores which element goes to which position 
int goesTo[N]; 

// For eg. in { 5, 1, 4, 3, 2 } 
// goesTo[1] = 2 
// goesTo[2] = 5 
// goesTo[3] = 4 
// goesTo[4] = 3 
// goesTo[5] = 1 

// This function returns the size of a component cycle 
int dfs(int i) 
{ 
    // If it is already visited 
    if (visited[i] == 1) 
        return 0; 

    visited[i] = 1; 
    int x = dfs(goesTo[i]); 
    return (x + 1); 
} 

// This functio returns the number 
// of transpositions in the permutation 
int noOfTranspositions(int P[], int n) 
{ 
    // Initializing visited[] array 
    for (int i = 1; i <= n; i++) 
        visited[i] = 0; 

    // building the goesTo[] array 
    for (int i = 0; i < n; i++) 
        goesTo[P[i]] = i + 1; 

    int transpositions = 0; 

    for (int i = 1; i <= n; i++) { 
        if (visited[i] == 0) { 
            int ans = dfs(i); 
            transpositions += ans - 1; 
        } 
    } 
    return transpositions; 
} 

// Driver Code 
int main() 
{ 
    int permutation[] = { 5, 1, 4, 3, 2 }; 
    int n = sizeof(permutation) / sizeof(permutation[0]); 

    cout << noOfTranspositions(permutation, n); 
    return 0; 
} 

```