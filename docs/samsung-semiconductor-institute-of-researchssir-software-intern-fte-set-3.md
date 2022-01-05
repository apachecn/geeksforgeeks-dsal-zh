# 三星半导体研究院(SSIR 软件)实习生/FTE | Set-3

> 原文:[https://www . geesforgeks . org/Samsung-semiconductor-institute-research ssir-software-intern-fte-set-3/](https://www.geeksforgeeks.org/samsung-semiconductor-institute-of-researchssir-software-intern-fte-set-3/)

我们得到了 m*n 矩阵，它可以有一个 0 到 7 之间的数。每个数字代表一个形状如下的管道:

![Pipes](img/bd2c309899392ab2dc25a1ea3fc5f5b4.png)

如果两个管道的端点相连，则认为它们是相连的。

> 示例:
> 如果矩阵如下:
> 0040
> 1360
> 5000
> 管道 1 和 3{1 向右打开。连接了 3 个向左打开的按钮。其他连接的管道是 3 和 6(3 向右开口。6 向左打开)。
> 4 和 6 没有连接，因为 6 没有打开到顶部，4 没有打开到底部。
> 1 和 5 也没有连接，因为即使 1 向底部开放，5 也没有向顶部开放。

给定这个矩阵、起始点(X，Y)和探测工具“L”的长度，找出可以到达多少个管道{矩阵元素}。
注意:探针工具:是测量工具，如果可以达到 6 根管子，但是探针工具的长度是 4 根。如果可以到达 3 个管道，但探测工具的长度为 4，则答案为 4。答案将是 3。

> 示例:
> 起始指数:(1，0)
> 探针长度:4
> 矩阵:
> 0040
> 1360
> 5000
> 通过探针连接的管道- (1，0)—>(1，1)—>(1，2)
> Ans- 3
> 起始指数:(0，0)
> 探针长度:4
> 矩阵:
> 0040
> 1360【T11

**解决的关键步骤:**
找到可以从一个起点访问的相邻管道元素{保持检查的详尽列表以确定如上定义的相邻标准}。
找到一种方法，通过元素进行处理，找到下一组可以访问的元素。{遍历图表}。应该注意的是，我们希望到达距离小于“1”的从起始节点可到达的所有节点。重点不是到达很多节点，而是从起点(X，Y)以较少的移动到达它们。

**递归:**
我们将所有节点标记为未访问，访问节点计数为 0。如果在递归过程中处理了标记为未访问的节点，则将访问节点计数增加 1，并将其标记为已访问。
我们从访问 start 节点(X，Y)开始，然后递归地访问它的所有连接的邻居(基于上面定义的连接标准的检查)，直到递归深度为“L”。

**缺点:**
在高连接矩阵的情况下(几乎所有的管道都连接在一起，并且存在多种到达管道的方式)，我们多次到达一个节点并对其进行多次处理，这可能会导致高运行时间。我们可以通过检查我们是否再次处理一个节点来优化它，前提是我们已经达到了一个较低的递归级别。
这不是 DFS 解决方案，因为我们重新处理节点，即使已经被访问过，因为新的访问可能会将节点的访问深度更新到更低的级别，并且在该节点之后会达到更大的深度。

**广度优先搜索:**
我们将所有节点标记为未访问，访问节点计数为 0。如果在处理过程中处理了标记为未访问的节点，则将访问节点计数增加 1。
我们首先将开始节点(X，Y)推入深度为 1 的队列，然后开始处理该队列，直到它为空。
在每次迭代中，取出队列的一个成员，并分析其相连的邻居。如果邻居未被访问，并且当前元素的深度不大于 1，则连接的元素被放入队列，标记为已访问，并且已访问的节点数增加 1。
当 BFS 执行节点的层级顺序遍历时，不可能在更小的距离内到达被访问节点。所以，以前方法的缺点是不存在的。这是这个问题的最优解。

**简单编码解决方案中可能的简化:**
由于有 7 种类型的管道，我们将不得不放置多个 if 条件，导致难以调试的嵌套 if 语句。可以通过将 7 个值转换为基于方向的数据来简化它。例如，每个值可以被转换成具有 4 个布尔变量的结构，每个方向一个。或者，每个数字可以被映射到一个 4 比特的数字，其中每个比特代表一个方向。输入减少后，检查将变得更简单，复杂性也更低。

## C++

```
#include <bits/stdc++.h>
using namespace std;
#define Max 1000
#define row_size 3
#define col_size 4

int x = 1, y = 0; // starting index(x, y),
int l = 4; // length of probe tool

// input matrix containing the pipes
int mt[row_size][col_size] = { { 0, 0, 4, 0 },
                               { 1, 3, 6, 0 },
                               { 5, 0, 0, 0 } };

// visited matrix checks for cells already visited
int vi[row_size][col_size];

// calculates the depth of connection for each cell
int depth[row_size][col_size];

int f = 0;
int r = 0;

// queue for BFS
struct node {
    int x;
    int y;
    int d;
};
node q[Max];
void push(int a, int b, int d) // push function
{
    node temp;
    temp.x = a;
    temp.y = b;
    temp.d = d;
    q[r++] = temp;
    vi[a][b] = 1;
}
node pop() // pop function
{
    node temp;
    temp.x = q[f].x;
    temp.y = q[f].y;
    temp.d = q[f].d;
    f++;
    return temp;
}

// It can be simplified by converting the 7
// values into direction based data. For e.g.
// each value can be transformed into a structure
// with 4 Boolean variables, one for each direction.
// Alternatively, each number can be mapped to a 4
// bit number where each bit represents a direction.
bool s1(int i, int j) // conversion to final direction
{
    if (i >= 0 && i < row_size && j >= 0 &&
        j < col_size && vi[i][j] == 0 && (mt[i][j] == 1 ||
        mt[i][j] == 3 || mt[i][j] == 6 || mt[i][j] == 7))
        return true;
    else
        return false;
}

bool s2(int i, int j) // conversion to final direction
{
    if (i >= 0 && i < row_size && j >= 0 && j < col_size &&
        vi[i][j] == 0 && (mt[i][j] == 1 || mt[i][j] == 2 ||
        mt[i][j] == 4 || mt[i][j] == 7))
        return true;
    else
        return false;
}
bool s3(int i, int j) // conversion to final direction
{
    if (i >= 0 && i < row_size && j >= 0 && j < col_size &&
        vi[i][j] == 0 && (mt[i][j] == 1 || mt[i][j] == 3 ||
        mt[i][j] == 4 || mt[i][j] == 5))
        return true;
    else
        return false;
}
bool s4(int i, int j) // conversion to final direction
{
    if (i >= 0 && i < row_size && j >= 0 && j < col_size &&
       vi[i][j] == 0 && (mt[i][j] == 1 || mt[i][j] == 2 ||
       mt[i][j] == 6 || mt[i][j] == 5))
        return true;
    else
        return false;
}

// search for connection
// We start by pushing the start node (X, Y) into a queue
// with depth 1  and then start processing the queue till
// it is empty.
void bfs(int x, int y, int d)
{
    push(x, y, d);
    while (r > f) {
        node temp = pop();
        int i = temp.x;
        int j = temp.y;
        int c = temp.d;
        depth[i][j] = c;

        if (mt[i][j] == 1 || mt[i][j] == 3 ||
            mt[i][j] == 4 || mt[i][j] == 5) {
            if (s1(i, j + 1))
                push(i, j + 1, c + 1);
        }
        if (mt[i][j] == 1 || mt[i][j] == 2 ||
            mt[i][j] == 6 || mt[i][j] == 5) {
            if (s2(i + 1, j))
                push(i + 1, j, c + 1);
        }
        if (mt[i][j] == 1 || mt[i][j] == 3 ||
            mt[i][j] == 7 || mt[i][j] == 6) {
            if (s3(i, j - 1))
                push(i, j - 1, c + 1);
        }
        if (mt[i][j] == 1 || mt[i][j] == 2 ||
            mt[i][j] == 4 || mt[i][j] == 7) {
            if (s4(i - 1, j))
                push(i - 1, j, c + 1);
        }
    }
}
int main() // main function
{

    f = 0;
    r = 0;
    // matrix
    for (int i = 0; i < row_size; i++) {
        for (int j = 0; j < col_size; j++) {

            // visited matrix for BFS set to
            // unvisited for every cell
            vi[i][j] = 0;

            // depth set to max initial value
            depth[i][j] = Max;
        }
    }

    if (mt[x][y] != 0) // condition for BFS
        bfs(x, y, 1);

    int nc = 0;
    for (int i = 0; i < row_size; i++) {
        for (int j = 0; j < col_size; j++) {
            if (depth[i][j] <= l) {
                cout << "(" << i << ", " << j << ")";
                nc++;
            }
        }
    }
    cout << " " << nc << "\n";
}
```

## 蟒蛇 3

```
Max=1000
row_size=3
col_size=4

x = 1; y = 0 # starting index(x, y),
l = 4 # length of probe tool

# input matrix containing the pipes
mt = [[ 0, 0, 4, 0 ,],
                               [ 1, 3, 6, 0],
                               [ 5, 0, 0, 0],]

# visited matrix checks for cells already visited
vi=[[False for _ in range(col_size)]for _ in range(row_size)]

# calculates the depth of connection for each cell
depth=[[0 for _ in range(col_size)] for _ in range(row_size)]

f = 0
r = 0

# queue for BFS
class node:
    def __init__(self,x,y,d):
        self.x=x
        self.y=y
        self.d=d

q=[None for _ in range(Max)]
def push(a, b, d): # push function
    global r
    temp=node(a,b,d)
    q[r] = temp
    r+=1
    vi[a][b] = 1

def pop(): # pop function
    global f
    temp=node(q[f].x,q[f].y,q[f].d)
    f+=1
    return temp

# It can be simplified by converting the 7
# values into direction based data. For e.g.
# each value can be transformed into a structure
# with 4 Boolean variables, one for each direction.
# Alternatively, each number can be mapped to a 4
# bit number where each bit represents a direction.
def s1(i, j): # conversion to final direction
    if (i >= 0 and i < row_size and j >= 0 and
        j < col_size and vi[i][j] == 0 and (mt[i][j] == 1 or
        mt[i][j] == 3 or mt[i][j] == 6 or mt[i][j] == 7)):
        return True
    else:
        return False

def s2(i, j): # conversion to final direction

    if (i >= 0 and i < row_size and j >= 0 and j < col_size and
        vi[i][j] == 0 and (mt[i][j] == 1 or mt[i][j] == 2 or
        mt[i][j] == 4 or mt[i][j] == 7)):
        return True
    else:
        return False

def s3(i, j): # conversion to final direction
    if (i >= 0 and i < row_size and j >= 0 and j < col_size and
        vi[i][j] == 0 and (mt[i][j] == 1 or mt[i][j] == 3 or
        mt[i][j] == 4 or mt[i][j] == 5)):
        return True
    else:
        return False

def s4(i, j): # conversion to final direction

    if (i >= 0 and i < row_size and j >= 0 and j < col_size and
       vi[i][j] == 0 and (mt[i][j] == 1 or mt[i][j] == 2 or
       mt[i][j] == 6 or mt[i][j] == 5)):
        return True
    else:
        return False

# search for connection
# We start by pushing the start node (X, Y) into a queue
# with depth 1  and then start processing the queue till
# it is empty.
def bfs(x, y, d):
    push(x, y, d)
    while (r > f) :
        temp = pop()
        i = temp.x
        j = temp.y
        c = temp.d
        depth[i][j] = c

        if (mt[i][j] == 1 or mt[i][j] == 3 or
            mt[i][j] == 4 or mt[i][j] == 5) :
            if (s1(i, j + 1)):
                push(i, j + 1, c + 1)

        if (mt[i][j] == 1 or mt[i][j] == 2 or
            mt[i][j] == 6 or mt[i][j] == 5) :
            if (s2(i + 1, j)):
                push(i + 1, j, c + 1)

        if (mt[i][j] == 1 or mt[i][j] == 3 or
            mt[i][j] == 7 or mt[i][j] == 6) :
            if (s3(i, j - 1)):
                push(i, j - 1, c + 1)

        if (mt[i][j] == 1 or mt[i][j] == 2 or
            mt[i][j] == 4 or mt[i][j] == 7) :
            if (s4(i - 1, j)):
                push(i - 1, j, c + 1)

if __name__=='__main__': # main function

    f = 0
    r = 0
    # matrix
    for i in range(row_size) :
        for j in range(col_size) :

            # visited matrix for BFS set to
            # unvisited for every cell
            vi[i][j] = 0

            # depth set to max initial value
            depth[i][j] = Max

    if (mt[x][y] != 0): # condition for BFS
        bfs(x, y, 1)

    nc = 0
    for i in range(row_size) :
        for j in range(col_size) :
            if (depth[i][j] <= l) :
                print("({}, {})".format(i,j),end='')
                nc+=1

    print(" ",nc)
```

**Output:** 

```
(1, 0)(1, 1)(1, 2) 3
```

**时间复杂度:** O(N * M)其中 N 为总行数，M 为总列数
T3】辅助空间: O(N * M)