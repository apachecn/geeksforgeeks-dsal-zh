# 给定天数的最佳阅读列表

> 原文:[https://www . geesforgeks . org/optimal-read-list-给定天数/](https://www.geeksforgeeks.org/optimal-read-list-given-number-days/)

一个人决心在“k”天内完成这本书，但他从来不想在中间停下一章。找到章节的最佳分配，这样这个人总体上不会读太多额外/较少的页面。

**示例:**

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

目标是最小化每天读取的页数和平均页数之间的差异总和。如果平均页数是非整数，则应该四舍五入到最接近的整数。

在上面的例子 2 中，平均页数是(8 + 5 + 6 + 12)/3 = 31/3，四舍五入到 10。因此，对于上面显示的输出，每天的平均页数和页数之差是“ABS(8-10)+ABS(5+6-10)+ABS(12-10)”，即 5。值 5 是差值总和的最佳值。

考虑上面的例子 2，其中一本书有 4 章，第 8、5、6 和 12 页。用户希望在 3 天内完成。上述场景的图形表示是，

![BookChapter1](img/66b2c6ada5604408c103ff970ee782bd.png)

在上图中，顶点代表章节，边 e(u，v)代表要从“u”读到“v”的页数。增加了下沉节点来象征书的结尾。

首先，计算一天的平均阅读页数(这里 31/3 大致是 10)。新的边权重 e '(u，v)将是平均差值| avg–e(u，v)|。上述问题的修正图是，

![BookChapter2](img/526c33a278d84ef2d49d60f0f79332d2.png)

感谢犰狳在评论中提出这个想法。

这个想法是从第 1 章开始，做一个 DFS 来寻找边数为“k”的 sink。继续将访问过的顶点存储在一个数组中，比如“路径[]”。如果我们到达目的顶点，并且路径和小于最优路径，则更新最优分配 optimal_path[]。注意，该图是 DAG，因此在 DFS 期间不需要考虑周期。
下面，是 C++实现的同款，邻接矩阵用来表示图。以下程序主要有 4 个阶段。
1)构造一个有向无环图。
2)利用 DFS 寻找最优路径。
3)打印找到的最优路径。

## C++

```
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

## 蟒蛇 3

```
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

**输出:**

```

Optimal Chapter Assignment :
Day1: 1
Day2: 2 3
Day3: 4
```

本文由**巴拉吉 S** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。