# 给定天数的最佳阅读列表

> 原文： [https://www.geeksforgeeks.org/optimal-read-list-given-number-days/](https://www.geeksforgeeks.org/optimal-read-list-given-number-days/)

一个人下定决心要在“ k”天内完成这本书，但他永远都不想停下来。 找到最佳的章节分配方式，以使该人员总体上不会阅读过多/多余的页面。

**示例**：

```
Input:  Number of Days to Finish book = 2
        Number of pages in chapters = {10, 5, 5}
Output: Day 1:  Chapter 1
        Day 2:  Chapters 2 and 3

Input:  Number of Days to Finish book = 3
        Number of pages in chapters = {8, 5, 6, 12}
Output: Day 1:  Chapter 1
        Day 2:  Chapters 2 and 3 
        Day 2:  Chapter 4

```

目标是使每天读取的页面与平均页面数之间的差异之和最小。 如果平均页数为非整数，则应四舍五入为最接近的整数。

在上述示例 2 中，平均页数为（8 + 5 + 6 + 12）/ 3 = 31/3，四舍五入为 10。因此，上面显示的输出的平均页数与每天的页数之差为“ abs（8-10）+ abs（5 + 6-10）+ abs（12-10）”，即 5。值 5 是差和之和的最佳值。

考虑上面的示例 2，其中一本书有 4 章，分别有第 8、5、6 和 12 页。用户希望在 3 天内完成。 以上方案的图形表示为：

![BookChapter1](img/66b2c6ada5604408c103ff970ee782bd.png)

在上图中，顶点表示章节，边 e（u，v）表示从'u'到达'v'所要读取的页面数。 添加了接收器节点以表示书的结尾。

首先，计算一天要读取的平均页面数（此处为 31/3，大约为 10）。 新的边权重 e’（u，v）将是平均差| avg – e（u，v）|。 针对上述问题的修改图形为

![BookChapter2](img/526c33a278d84ef2d49d60f0f79332d2.png)

感谢 [Armadillo](https://www.geeksforgeeks.org/amazon-interview-experience-set-170/) 在评论中提出了这个想法。

这个想法是从第 1 章开始，做一个 DFS 来找到边数为“ k”的汇点。 继续将访问的顶点存储在一个名为“ path []”的数组中。 如果到达目标顶点，并且路径总和小于最佳路径，则更新最佳分配 optimistic_path []。 请注意，该图是 DAG，因此在 DFS 期间无需照顾周期。

接下来是相同的 C++实现，邻接矩阵用于表示图。 以下程序主要分为四个阶段。

1.  构造有向无环图。

2.  使用 DFS 查找最佳路径。

3.  打印找到的最佳路径。

## C++

```cpp

// C++ DFS solution to schedule chapters for reading in 
// given days 
# include <iostream> 
# include <cstdlib> 
# include <climits> 
# include <cmath> 
using namespace std; 

// Define total chapters in the book 
// Number of days user can spend on reading 
# define CHAPTERS 4 
# define DAYS 3 
# define NOLINK -1 

// Array to store the final balanced schedule 
int optimal_path[DAYS+1]; 

// Graph - Node chapter+1 is the sink described in the 
//         above graph 
int DAG[CHAPTERS+1][CHAPTERS+1]; 

// Updates the optimal assignment with current assignment 
void updateAssignment(int* path, int path_len); 

// A DFS based recursive function to store the optimal path 
// in path[] of size path_len.  The variable sum stores sum of 
// of all edges on current path.  k is number of days spent so 
// far. 
void assignChapters(int u, int* path, int path_len, int sum, int k) 
{ 
    static int min = INT_MAX; 

    // Ignore the assignment which requires more than required days 
    if (k < 0) 
        return; 

    // Current assignment of chapters to days 
    path[path_len] = u; 
    path_len++; 

    // Update the optimal assignment if necessary 
    if (k == 0 && u == CHAPTERS) 
    { 
        if (sum < min) 
        { 
            updateAssignment(path, path_len); 
            min = sum; 
        } 
    } 

    // DFS - Depth First Search for sink 
    for (int v = u+1; v <= CHAPTERS; v++) 
    { 
        sum += DAG[u][v]; 
        assignChapters(v, path, path_len, sum, k-1); 
        sum -= DAG[u][v]; 
    } 
} 

// This function finds and prints optimal read list.  It first creates a 
// graph, then calls assignChapters(). 
void minAssignment(int pages[]) 
{ 
    // 1) ............CONSTRUCT GRAPH................. 
    // Partial sum array construction S[i] = total pages 
    // till ith chapter 
    int avg_pages = 0, sum = 0, S[CHAPTERS+1], path[DAYS+1]; 
    S[0] = 0; 

    for (int i = 0; i < CHAPTERS; i++) 
    { 
        sum += pages[i]; 
        S[i+1] = sum; 
    } 

    // Average pages to be read in a day 
    avg_pages = round(sum/DAYS); 

    /* DAG construction vertices being chapter name & 
     * Edge weight being |avg_pages - pages in a chapter| 
     * Adjacency matrix representation  */
    for (int i = 0; i <= CHAPTERS; i++) 
    { 
        for (int j = 0; j <= CHAPTERS; j++) 
        { 
            if (j <= i) 
                DAG[i][j] = NOLINK; 
            else
            { 
                sum = abs(avg_pages - (S[j] - S[i])); 
                DAG[i][j] = sum; 
            } 
        } 
    } 

    // 2) ............FIND OPTIMAL PATH................ 
    assignChapters(0, path, 0, 0, DAYS); 

    // 3) ..PRINT OPTIMAL READ LIST USING OPTIMAL PATH.... 
    cout << "Optimal Chapter Assignment :" << endl; 
    int ch; 
    for (int i = 0; i < DAYS; i++) 
    { 
        ch = optimal_path[i]; 
        cout << "Day" << i+1 << ": " << ch << " "; 
        ch++; 
        while ( (i < DAYS-1 && ch < optimal_path[i+1]) || 
                (i == DAYS-1 && ch <= CHAPTERS)) 
        { 
           cout <<  ch << " "; 
           ch++; 
        } 
        cout << endl; 
    } 
} 

// This function updates optimal_path[] 
void updateAssignment(int* path, int path_len) 
{ 
    for (int i = 0; i < path_len; i++) 
        optimal_path[i] = path[i] + 1; 
} 

// Driver program to test the schedule 
int main(void) 
{ 
    int pages[CHAPTERS] = {7, 5, 6, 12}; 

    // Get read list for given days 
    minAssignment(pages); 

    return 0; 
} 

```

## Python

```py

# Python3 DFS solution to schedule chapters  
# for reading in given days 

# A DFS based recursive function to store  
# the optimal path in path[] of size path_len. 
# The variable Sum stores Sum of all edges on  
# current path. k is number of days spent so far.  
def assignChapters(u, path, path_len, Sum, k): 
    global CHAPTERS, DAYS, NOLINK, optical_path, DAG, Min

    # Ignore the assignment which requires 
    # more than required days  
    if (k < 0):  
        return

    # Current assignment of chapters to days  
    path[path_len] = u  
    path_len += 1

    # Update the optimal assignment if necessary  
    if (k == 0 and u == CHAPTERS): 
        if (Sum < Min): 
            updateAssignment(path, path_len)  
            Min = Sum

    # DFS - Depth First Search for sink 
    for v in range(u + 1, CHAPTERS + 1): 
        Sum += DAG[u][v]  
        assignChapters(v, path, path_len, Sum, k - 1)  
        Sum -= DAG[u][v] 

# This function finds and prints  
# optimal read list. It first creates a  
# graph, then calls assignChapters().  
def MinAssignment(pages): 
    global CHAPTERS, DAYS, NOLINK, optical_path, DAG, MIN

    # 1) ............CONSTRUCT GRAPH.................  
    # Partial Sum array construction S[i] = total pages  
    # till ith chapter  
    avg_pages = 0
    Sum = 0 
    S = [None] * (CHAPTERS + 1) 
    path = [None] * (DAYS + 1)  
    S[0] = 0

    for i in range(CHAPTERS): 
        Sum += pages[i]  
        S[i + 1] = Sum

    # Average pages to be read in a day  
    avg_pages = round(Sum/DAYS)  

    # DAG construction vertices being chapter name &  
    # Edge weight being |avg_pages - pages in a chapter|  
    # Adjacency matrix representation 
    for i in range(CHAPTERS + 1): 
        for j in range(CHAPTERS + 1): 
            if (j <= i): 
                DAG[i][j] = NOLINK  
            else: 
                Sum = abs(avg_pages - (S[j] - S[i]))  
                DAG[i][j] = Sum

    # 2) ............FIND OPTIMAL PATH................  
    assignChapters(0, path, 0, 0, DAYS)  

    # 3) ..PROPTIMAL READ LIST USING OPTIMAL PATH....  
    print("Optimal Chapter Assignment :")  
    ch = None
    for i in range(DAYS): 
        ch = optimal_path[i]  
        print("Day", i + 1, ": ", ch, end = " ")  
        ch += 1
        while ((i < DAYS - 1 and ch < optimal_path[i + 1]) or 
               (i == DAYS - 1 and ch <= CHAPTERS)): 
            print(ch, end = " ")  
            ch += 1
        print() 

# This function updates optimal_path[]  
def updateAssignment(path, path_len): 
    for i in range(path_len): 
        optimal_path[i] = path[i] + 1

# Driver Code 

# Define total chapters in the book  
# Number of days user can spend on reading  
CHAPTERS = 4
DAYS = 3
NOLINK = -1

# Array to store the final balanced schedule  
optimal_path = [None] * (DAYS + 1) 

# Graph - Node chapter+1 is the sink  
#          described in the above graph  
DAG = [[None] * (CHAPTERS + 1)  
       for i in range(CHAPTERS + 1)]  

Min = 999999999999
pages = [7, 5, 6, 12]  

# Get read list for given days  
MinAssignment(pages) 

# This code is contributed by PranchalK 

```

**输出**：

```

Optimal Chapter Assignment :
Day1: 1
Day2: 2 3
Day3: 4
```

本文由 **Balaji S** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

