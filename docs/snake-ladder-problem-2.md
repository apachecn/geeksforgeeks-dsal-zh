# 蛇梯问题

> 原文:[https://www.geeksforgeeks.org/snake-ladder-problem-2/](https://www.geeksforgeeks.org/snake-ladder-problem-2/)

给定一条蛇和梯子板，找到到达目的地或从源或第一个单元到达最后一个单元所需的最小掷骰子次数。基本上，玩家可以完全控制掷骰子的结果，并想知道到达最后一个单元所需的最小投掷次数。
如果玩家到达梯子底部的一个小室，玩家必须爬上那个梯子，如果到达的小室是蛇的嘴，则必须不掷骰子就下到蛇的尾巴。

![snakesandladders](img/445afdffbac8968eb6da613e690774b0.png)

例如，考虑所示的板，从单元 1 到达单元 30 所需的最小掷骰子次数是 3。
步骤如下:
a)先掷两个骰子到达 3 号格，然后阶梯到达 22
b)然后掷 6 到达 28。
c)最后通过 2 达到 30。
也可以有其他解决方案，如(2，2，6)，(2，4，4)，(2，3，5)..等等。

其思想是将给定的蛇和阶梯板视为顶点数等于板中单元数的有向图。这个问题简化为寻找图中的最短路径。如果接下来的 6 个顶点没有蛇或梯子，那么图的每个顶点都有一条到接下来的 6 个顶点的边。如果接下来的六个顶点中的任何一个有一条蛇或梯子，那么从当前顶点开始的边将到达梯子的顶部或蛇的尾部。由于所有边的权重相等，我们可以利用图的[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)高效地找到最短路径。
以下是上述想法的实施情况。输入由两件事表示，第一是“N”，它是给定板中的单元数，第二是大小为 N 的数组“move[0…N-1]”。如果 I 中没有蛇和梯子，则条目 move[i]为-1，否则 move[i]包含 I 中蛇或梯子的目标单元索引

## C++

```
// C++ program to find minimum number of dice throws required to
// reach last cell from first cell of a given snake and ladder
// board
#include<iostream>
#include <queue>
using namespace std;

// An entry in queue used in BFS
struct queueEntry
{
    int v;     // Vertex number
    int dist;  // Distance of this vertex from source
};

// This function returns minimum number of dice throws required to
// Reach last cell from 0'th cell in a snake and ladder game.
// move[] is an array of size N where N is no. of cells on board
// If there is no snake or ladder from cell i, then move[i] is -1
// Otherwise move[i] contains cell to which snake or ladder at i
// takes to.
int getMinDiceThrows(int move[], int N)
{
    // The graph has N vertices. Mark all the vertices as
    // not visited
    bool *visited = new bool[N];
    for (int i = 0; i < N; i++)
        visited[i] = false;

    // Create a queue for BFS
    queue<queueEntry> q;

    // Mark the node 0 as visited and enqueue it.
    visited[0] = true;
    queueEntry s = {0, 0};  // distance of 0't vertex is also 0
    q.push(s);  // Enqueue 0'th vertex

    // Do a BFS starting from vertex at index 0
    queueEntry qe;  // A queue entry (qe)
    while (!q.empty())
    {
        qe = q.front();
        int v = qe.v; // vertex no. of queue entry

        // If front vertex is the destination vertex,
        // we are done
        if (v == N-1)
            break;

        // Otherwise dequeue the front vertex and enqueue
        // its adjacent vertices (or cell numbers reachable
        // through a dice throw)
        q.pop();
        for (int j=v+1; j<=(v+6) && j<N; ++j)
        {
            // If this cell is already visited, then ignore
            if (!visited[j])
            {
                // Otherwise calculate its distance and mark it
                // as visited
                queueEntry a;
                a.dist = (qe.dist + 1);
                visited[j] = true;

                // Check if there a snake or ladder at 'j'
                // then tail of snake or top of ladder
                // become the adjacent of 'i'
                if (move[j] != -1)
                    a.v = move[j];
                else
                    a.v = j;
                q.push(a);
            }
        }
    }

    // We reach here when 'qe' has last vertex
    // return the distance of vertex in 'qe'
    return qe.dist;
}

// Driver program to test methods of graph class
int main()
{
    // Let us construct the board given in above diagram
    int N = 30;
    int moves[N];
    for (int i = 0; i<N; i++)
        moves[i] = -1;

    // Ladders
    moves[2] = 21;
    moves[4] = 7;
    moves[10] = 25;
    moves[19] = 28;

    // Snakes
    moves[26] = 0;
    moves[20] = 8;
    moves[16] = 3;
    moves[18] = 6;

    cout << "Min Dice throws required is " << getMinDiceThrows(moves, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of dice
// throws required to reach last cell from first
// cell of a given snake and ladder board

import java.util.LinkedList;
import java.util.Queue;

public class SnakesLadder
{
    // An entry in queue used in BFS
    static class qentry
    {
        int v;// Vertex number
        int dist;// Distance of this vertex from source
    }

    // This function returns minimum number of dice
    // throws required to Reach last cell from 0'th cell
    // in a snake and ladder game. move[] is an array of
    // size N where N is no. of cells on board If there
    // is no snake or ladder from cell i, then move[i]
    // is -1 Otherwise move[i] contains cell to which
    // snake or ladder at i takes to.
    static int getMinDiceThrows(int move[], int n)
    {
        int visited[] = new int[n];
        Queue<qentry> q = new LinkedList<>();
        qentry qe = new qentry();
        qe.v = 0;
        qe.dist = 0;

        // Mark the node 0 as visited and enqueue it.
        visited[0] = 1;
        q.add(qe);

        // Do a BFS starting from vertex at index 0
        while (!q.isEmpty())
        {
            qe = q.remove();
            int v = qe.v;

            // If front vertex is the destination
            // vertex, we are done
            if (v == n - 1)
                break;

            // Otherwise dequeue the front vertex and
            // enqueue its adjacent vertices (or cell
            // numbers reachable through a dice throw)
            for (int j = v + 1; j <= (v + 6) && j < n; ++j)
            {
                // If this cell is already visited, then ignore
                if (visited[j] == 0)
                {
                    // Otherwise calculate its distance and
                    // mark it as visited
                    qentry a = new qentry();
                    a.dist = (qe.dist + 1);
                    visited[j] = 1;

                    // Check if there a snake or ladder at 'j'
                    // then tail of snake or top of ladder
                    // become the adjacent of 'i'
                    if (move[j] != -1)
                        a.v = move[j];
                    else
                        a.v = j;
                    q.add(a);
                }
            }
        }

        // We reach here when 'qe' has last vertex
        // return the distance of vertex in 'qe'
        return qe.dist;
    }

    public static void main(String[] args)
    {
        // Let us construct the board given in above diagram
        int N = 30;
        int moves[] = new int[N];
        for (int i = 0; i < N; i++)
            moves[i] = -1;

        // Ladders
        moves[2] = 21;
        moves[4] = 7;
        moves[10] = 25;
        moves[19] = 28;

        // Snakes
        moves[26] = 0;
        moves[20] = 8;
        moves[16] = 3;
        moves[18] = 6;

        System.out.println("Min Dice throws required is " +
                          getMinDiceThrows(moves, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of dice throws required to reach last
# cell from first cell of a given
# snake and ladder board

# An entry in queue used in BFS
class QueueEntry(object):
    def __init__(self, v = 0, dist = 0):
        self.v = v
        self.dist = dist

'''This function returns minimum number of
dice throws required to. Reach last cell
from 0'th cell in a snake and ladder game.
move[] is an array of size N where N is
no. of cells on board. If there is no
snake or ladder from cell i, then move[i]
is -1\. Otherwise move[i] contains cell to
which snake or ladder at i takes to.'''
def getMinDiceThrows(move, N):

    # The graph has N vertices. Mark all
    # the vertices as not visited
    visited = [False] * N

    # Create a queue for BFS
    queue = []

    # Mark the node 0 as visited and enqueue it
    visited[0] = True

    # Distance of 0't vertex is also 0
    # Enqueue 0'th vertex
    queue.append(QueueEntry(0, 0))

    # Do a BFS starting from vertex at index 0
    qe = QueueEntry() # A queue entry (qe)
    while queue:
        qe = queue.pop(0)
        v = qe.v # Vertex no. of queue entry

        # If front vertex is the destination
        # vertex, we are done
        if v == N - 1:
            break

        # Otherwise dequeue the front vertex
        # and enqueue its adjacent vertices
        # (or cell numbers reachable through
        # a dice throw)
        j = v + 1
        while j <= v + 6 and j < N:

            # If this cell is already visited,
            # then ignore
            if visited[j] is False:

                # Otherwise calculate its
                # distance and mark it
                # as visited
                a = QueueEntry()
                a.dist = qe.dist + 1
                visited[j] = True

                # Check if there a snake or ladder
                # at 'j' then tail of snake or top
                # of ladder become the adjacent of 'i'
                a.v = move[j] if move[j] != -1 else j

                queue.append(a)

            j += 1

    # We reach here when 'qe' has last vertex
    # return the distance of vertex in 'qe
    return qe.dist

# driver code
N = 30
moves = [-1] * N

# Ladders
moves[2] = 21
moves[4] = 7
moves[10] = 25
moves[19] = 28

# Snakes
moves[26] = 0
moves[20] = 8
moves[16] = 3
moves[18] = 6

print("Min Dice throws required is {0}".
       format(getMinDiceThrows(moves, N)))

# This code is contributed by Ajitesh Pathak
```

## C#

```
// C# program to find minimum
// number of dice throws required
// to reach last cell from first
// cell of a given snake and ladder board
using System;
using System.Collections.Generic;

public class SnakesLadder
{
    // An entry in queue used in BFS
    public class qentry
    {
        public int v;// Vertex number
        public int dist;// Distance of this vertex from source
    }

    // This function returns minimum number of dice
    // throws required to Reach last cell from 0'th cell
    // in a snake and ladder game. move[] is an array of
    // size N where N is no. of cells on board If there
    // is no snake or ladder from cell i, then move[i]
    // is -1 Otherwise move[i] contains cell to which
    // snake or ladder at i takes to.
    static int getMinDiceThrows(int []move, int n)
    {
        int []visited = new int[n];
        Queue<qentry> q = new Queue<qentry>();
        qentry qe = new qentry();
        qe.v = 0;
        qe.dist = 0;

        // Mark the node 0 as visited and enqueue it.
        visited[0] = 1;
        q.Enqueue(qe);

        // Do a BFS starting from vertex at index 0
        while (q.Count != 0)
        {
            qe = q.Dequeue();
            int v = qe.v;

            // If front vertex is the destination
            // vertex, we are done
            if (v == n - 1)
                break;

            // Otherwise dequeue the front vertex and
            // enqueue its adjacent vertices (or cell
            // numbers reachable through a dice throw)
            for (int j = v + 1; j <= (v + 6) && j < n; ++j)
            {
                // If this cell is already visited, then ignore
                if (visited[j] == 0)
                {
                    // Otherwise calculate its distance and
                    // mark it as visited
                    qentry a = new qentry();
                    a.dist = (qe.dist + 1);
                    visited[j] = 1;

                    // Check if there a snake or ladder at 'j'
                    // then tail of snake or top of ladder
                    // become the adjacent of 'i'
                    if (move[j] != -1)
                        a.v = move[j];
                    else
                        a.v = j;
                    q.Enqueue(a);
                }
            }
        }

        // We reach here when 'qe' has last vertex
        // return the distance of vertex in 'qe'
        return qe.dist;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Let us construct the board
        // given in above diagram
        int N = 30;
        int []moves = new int[N];
        for (int i = 0; i < N; i++)
            moves[i] = -1;

        // Ladders
        moves[2] = 21;
        moves[4] = 7;
        moves[10] = 25;
        moves[19] = 28;

        // Snakes
        moves[26] = 0;
        moves[20] = 8;
        moves[16] = 3;
        moves[18] = 6;

        Console.WriteLine("Min Dice throws required is " +
                        getMinDiceThrows(moves, N));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find minimum number of dice
// throws required to reach last cell from first
// cell of a given snake and ladder board

class qentry
{
    constructor()
    {
        this.v = 0;
        this.dist = 0;
    }
}

// This function returns minimum number of dice
    // throws required to Reach last cell from 0'th cell
    // in a snake and ladder game. move[] is an array of
    // size N where N is no. of cells on board If there
    // is no snake or ladder from cell i, then move[i]
    // is -1 Otherwise move[i] contains cell to which
    // snake or ladder at i takes to.
function getMinDiceThrows(move,n)
{
    let visited = new Array(n);
    for(let i = 0; i < n; i++)
        visited[i] = false;
        let q = [];
        let qe = new qentry();
        qe.v = 0;
        qe.dist = 0;

        // Mark the node 0 as visited and enqueue it.
        visited[0] = 1;
        q.push(qe);

        // Do a BFS starting from vertex at index 0
        while (q.length != 0)
        {
            qe = q.shift();
            let v = qe.v;

            // If front vertex is the destination
            // vertex, we are done
            if (v == n - 1)
                break;

            // Otherwise dequeue the front vertex and
            // enqueue its adjacent vertices (or cell
            // numbers reachable through a dice throw)
            for (let j = v + 1; j <= (v + 6) && j < n; ++j)
            {
                // If this cell is already visited, then ignore
                if (visited[j] == 0)
                {
                    // Otherwise calculate its distance and
                    // mark it as visited
                    let a = new qentry();
                    a.dist = (qe.dist + 1);
                    visited[j] = 1;

                    // Check if there a snake or ladder at 'j'
                    // then tail of snake or top of ladder
                    // become the adjacent of 'i'
                    if (move[j] != -1)
                        a.v = move[j];
                    else
                        a.v = j;
                    q.push(a);
                }
            }
        }

        // We reach here when 'qe' has last vertex
        // return the distance of vertex in 'qe'
        return qe.dist;
}

// Let us construct the board given in above diagram
let N = 30;
let moves = new Array(N);
for (let i = 0; i < N; i++)
    moves[i] = -1;

// Ladders
moves[2] = 21;
moves[4] = 7;
moves[10] = 25;
moves[19] = 28;

// Snakes
moves[26] = 0;
moves[20] = 8;
moves[16] = 3;
moves[18] = 6;

document.write("Min Dice throws required is " +
                   getMinDiceThrows(moves, N));

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Min Dice throws required is 3
```

上述解决方案的时间复杂度为 0(N)，因为每个单元仅从队列中添加和移除一次。典型的入队或出列操作需要 0(1)个时间。

本文由**西达尔特**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。