# 根据给定的规则

对队列进行给定的查询

> 原文:[https://www . geesforgeks . org/根据给定规则在队列中执行给定查询/](https://www.geeksforgeeks.org/perform-given-queries-on-queue-according-to-the-given-rules/)

给定由第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)和{E，X}类型的查询 **Query[][]** 组成的[队列](https://www.geeksforgeeks.org/queue-data-structure/)，任务是根据以下规则对给定队列执行给定查询:

*   如果 **E** 的值为 **1** ，则[从队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)中弹出前元素。
*   如果 **E** 的值为 **2** ，则从队列中删除值 **X** (如果存在)。
*   如果 **E** 的值是 **3** ，那么找到 **X** 在队列中的位置，如果存在的话。否则，打印**-1”**。

**示例:**

> **输入:** N = 5，查询[][] = {{1，0}，{3，3}，{2，2}}
> **输出:** 2
> **解释:**
> 最初队列看起来像{1，2，3，4，5 }。以下是根据给定的查询执行的操作:
> 第一个查询 E = 1，X = 0 - > 1 弹出，将队列改为{ 2，3，4，5 }。
> 第二次查询 E = 3，X = 3 - >打印 3 的位置。
> 第三个查询 E = 2，X = 2 - > 2 从队列中删除，变为队列{ 3，4，5 }。
> 
> **输入:** N = 5，查询[][] = {{1，0}，{3，1}}
> **输出:** -1

**逼近:**给定的问题可以用[贪婪逼近](https://www.geeksforgeeks.org/greedy-algorithms/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决。按照以下步骤解决给定的问题。

*   初始化一个变量，比如说**将 1** 计数为 **0** 来计算事件 **E1** 的发生次数。
*   当查询类型为 **E1** 时，将**计数 1** 的值增加 **1** 。
*   维护一个[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)，存储在执行查询操作时删除的元素。
*   对于**的查询，键入 3** 执行以下步骤:
    *   初始化一个变量，说**位置**存储 **X** 的初始位置。
    *   在集合中找到 **X** 的值，检查 **X** 是否已经被移除，如果[T5】X 存在于集合](https://www.geeksforgeeks.org/set-find-function-in-c-stl/)中，则打印 **-1** 。否则，找到 **X** 的位置。
    *   用迭代器遍历集合，说**它**，如果**它的值> X** ，那么[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，将位置降低 **1** 。
    *   打印存储在位置变量中的 **X** 的最终位置。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to perform all the queries
// operations on the given queue
void solve(int n, int m, int** queries)
{
    // Stores the count query of type 1
    int countE1 = 0;
    set<int> removed;

    for (int i = 0; i < m; i++) {

        // Event E1: increase countE1
        if (queries[i][0] == 1)
            ++countE1;

        // Event E2: add the X in set
        else if (queries[i][0] == 2)
            removed.insert(queries[i][1]);

        // Event E3: Find position of X
        else {

            // Initial position is
            // (position - countE1)
            int position = queries[i][1]
                           - countE1;

            // If X is already removed or
            // popped out
            if (removed.find(queries[i][1])
                    != removed.end()
                || position <= 0)
                cout << "-1\n";

            // Finding the position of
            // X in queue
            else {

                // Traverse set to decrease
                // position of X for all the
                // number removed in front
                for (int it : removed) {

                    if (it > queries[i][1])
                        break;

                    position--;
                }

                // Print the position of X
                cout << position << "\n";
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 5, Q = 3;
    int** queries = new int*[Q];
    for (int i = 0; i < Q; i++) {
        queries[i] = new int[2];
    }

    queries[0][0] = 1;
    queries[0][1] = 0;
    queries[1][0] = 3;
    queries[1][1] = 3;
    queries[2][0] = 2;
    queries[2][1] = 2;

    solve(N, Q, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to perform all the queries
// operations on the given queue
static void solve(int n, int m, int [][]queries)
{

    // Stores the count query of type 1
    int countE1 = 0;
    HashSet<Integer> removed = new HashSet<Integer>();

    for (int i = 0; i < m; i++) {

        // Event E1: increase countE1
        if (queries[i][0] == 1)
            ++countE1;

        // Event E2: add the X in set
        else if (queries[i][0] == 2)
            removed.add(queries[i][1]);

        // Event E3: Find position of X
        else {

            // Initial position is
            // (position - countE1)
            int position = queries[i][1]
                           - countE1;

            // If X is already removed or
            // popped out
            if (removed.contains(queries[i][1])
                || position <= 0)
                System.out.print("-1\n");

            // Finding the position of
            // X in queue
            else {

                // Traverse set to decrease
                // position of X for all the
                // number removed in front
                for (int it : removed) {

                    if (it > queries[i][1])
                        break;

                    position--;
                }

                // Print the position of X
                System.out.print(position+ "\n");
            }
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, Q = 3;
    int [][]queries = new int[Q][2];

    queries[0][0] = 1;
    queries[0][1] = 0;
    queries[1][0] = 3;
    queries[1][1] = 3;
    queries[2][0] = 2;
    queries[2][1] = 2;

    solve(N, Q, queries);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python program for the above approach

# Function to perform all the queries
# operations on the given queue

def solve(n, m, queries):

        # Stores the count query of type 1
    countE1 = 0
    removed = set()

    for i in range(0, m):

                # Event E1: increase countE1
        if (queries[i][0] == 1):
            countE1 += 1

            # Event E2: add the X in set
        elif(queries[i][0] == 2):
            removed.add(queries[i][1])

            # Event E3: Find position of X
        else:

                        # Initial position is
                        # (position - countE1)
            position = queries[i][1] - countE1

            # If X is already removed or
            # popped out

            if (queries[i][1] in removed or position <= 0):
                print("-1")

                # Finding the position of
                # X in queue
            else:

                                # Traverse set to decrease
                                # position of X for all the
                                # number removed in front
                for it in removed:
                    if (it > queries[i][1]):
                        break

                    position -= 1

                    # Print the position of X
                print(position)

# Driver Code
if __name__ == "__main__":

    N = 5
    Q = 3
    queries = [[0 for _ in range(2)] for _ in range(Q)]
    queries[0][0] = 1
    queries[0][1] = 0
    queries[1][0] = 3
    queries[1][1] = 3
    queries[2][0] = 2
    queries[2][1] = 2

    solve(N, Q, queries)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

public class GFG {

// Function to perform all the queries
// operations on the given queue
static void solve(int n, int m, int [,]queries)
{

    // Stores the count query of type 1
    int countE1 = 0;
    HashSet<int> removed = new HashSet<int>();

    for (int i = 0; i < m; i++) {

        // Event E1: increase countE1
        if (queries[i, 0] == 1)
            ++countE1;

        // Event E2: add the X in set
        else if (queries[i, 0] == 2)
            removed.Add(queries[i, 1]);

        // Event E3: Find position of X
        else {

            // Initial position is
            // (position - countE1)
            int position = queries[i, 1]
                           - countE1;

            // If X is already removed or
            // popped out
            if (removed.Contains(queries[i, 1])
                || position <= 0)
                Console.WriteLine("-1\n");

            // Finding the position of
            // X in queue
            else {

                // Traverse set to decrease
                // position of X for all the
                // number removed in front
                foreach (int it in removed) {

                    if (it > queries[i, 1])
                        break;

                    position--;
                }

                // Print the position of X
                Console.WriteLine(position+ "\n");
            }
        }
    }
}

// Driver Code
public static void Main (string[] args) {

    int N = 5, Q = 3;
    int [,]queries = new int[Q, 2];

    queries[0, 0] = 1;
    queries[0, 1] = 0;
    queries[1, 0] = 3;
    queries[1, 1] = 3;
    queries[2, 0] = 2;
    queries[2, 1] = 2;

    solve(N, Q, queries);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to perform all the queries
        // operations on the given queue
        function solve(n, m, queries)
        {

            // Stores the count query of type 1
            let countE1 = 0;
            let removed = new Set();

            for (let i = 0; i < m; i++) {

                // Event E1: increase countE1
                if (queries[i][0] == 1)
                    ++countE1;

                // Event E2: add the X in set
                else if (queries[i][0] == 2)
                    removed.add(queries[i][1]);

                // Event E3: Find position of X
                else {

                    // Initial position is
                    // (position - countE1)
                    let position = queries[i][1]
                        - countE1;

                    // If X is already removed or
                    // popped out
                    if (removed.has(queries[i][1])
                        != false
                        || position <= 0)
                        document.write("-1" + "<br>");

                    // Finding the position of
                    // X in queue
                    else {

                        // Traverse set to decrease
                        // position of X for all the
                        // number removed in front
                        for (let it of removed) {

                            if (it > queries[i][1])
                                break;

                            position--;
                        }

                        // Print the position of X
                        document.write(position + "<br>");
                    }
                }
            }
        }

        // Driver Code

        let N = 5, Q = 3;
        let queries = new Array(Q);
        for (let i = 0; i < Q; i++) {
            queries[i] = new Array(2);
        }

        queries[0][0] = 1;
        queries[0][1] = 0;
        queries[1][0] = 3;
        queries[1][1] = 3;
        queries[2][0] = 2;
        queries[2][1] = 2;

        solve(N, Q, queries);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:***

*   ***查询类型 1:**0(1)*
*   ***对于类型 2 的查询:**0(对数 N)*
*   ***对于类型 3 的查询:** O(N <sup>2</sup> log N)*

***辅助空间:** O(N)*