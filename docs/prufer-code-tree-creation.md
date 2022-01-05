# 将代码保存到树创建中

> 原文:[https://www.geeksforgeeks.org/prufer-code-tree-creation/](https://www.geeksforgeeks.org/prufer-code-tree-creation/)

**什么是普鲁弗码？**
给定一棵树(表示为图，而不是根树)，该树有 n 个标签节点，标签从 1 到 n，一个普鲁弗代码唯一地识别该树。序列有 n-2 个值。
**如何获取树的普鲁弗码？**

1.  将 Prufer 代码初始化为空。
2.  从最低标签的一片叶子开始，比如 x。找到连接它和树的其余部分的顶点，比如 y。从树中移除 x，并将 y 添加到 Prufer 代码中
3.  重复上面的步骤 2，直到我们剩下两个节点。

```
A tree with labels from 1 to n.
             5 
           /   \      
          1     4 
        /  \
       2    3

PruferCode = {}
The lowest label leaf is 2, we remove it from tree
and add the other vertex (connecting it to the tree)
to Prufer code
Tree now becomes
             5 
           /   \      
          1     4
           \
            3
Prufer Code becomes = {1}

The lowest label leaf is 3, we remove it from tree
and add the other vertex (connecting it to the tree)
to Prufer code
Tree now becomes
             5 
           /   \      
          1     4
Prufer Code becomes = {1, 1}

The lowest label leaf is 1, we remove it from tree
and add the other vertex (connecting it to the tree)
to Prufer code
Tree now becomes
             5 
              \      
               4     
Prufer Code becomes = {1, 1, 5}

We have only two nodes left now, so we stop.
```

**如何从给定的普鲁弗码构造树？**

```
Input : (4, 1, 3, 4)
Output : Edges of following tree
         2----4----3----1----5
              |
              6

Input : (1, 3, 5)
Output : Edges of following tree
         2----1----3----5----4
```

假设给定普鲁弗码的长度为 m，其思想是创建一个 m+2 个顶点的空图。我们从序列中移除第一个元素。假设当前序列的第一个元素是 x，然后我们找到在给定序列中不存在且尚未添加到树中的最小值。让这个值为 y。我们添加一条从 x 到 y 的边，重复这个步骤。
用上面第一个例子来理解构造树的算法:

```
Input : (4, 1, 3, 4)

Step 1: First we create an empty graph of 6 vertices 
        and get 4 from the sequence. 
Step 2: Out of 1 to 6, the least vertex not in 
        Prufer sequence is 2\. 
Step 3: We form an edge between 2 and 4\. 
             2----4    1    3    5      6
Step 4: Next in the sequence is 1 and corresponding 
        vertex with least degree is 5 (as 2 has been 
        considered). 
             2----4    1----5    3    6
Step 5: Next in the sequence is 3 and corresponding 
        vertex with least degree is 1 
        (as 1 is now not part of remaining Prufer sequence) 
             2----4    3----1----5    6
Step 6: Next in the sequence is 4 and corresponding vertex
        with least degree is 3 (as 3 has not been considered 
        as is not present further in sequence)
             2----4----3----1----5    6
Step 7: Finally two vertices are left out from 1 to 6 (4
         and 6) so we join them.
             2----4----3----1----5
                  |
                  6
This is the required tree on 6 vertices.
```

下面是实现。

## C++

```
// C++ program to construct tree from given Prufer Code
#include <bits/stdc++.h>
using namespace std;

// Prints edges of tree represented by give Prufer code
void printTreeEdges(int prufer[], int m)
{
    int vertices = m + 2;
    int vertex_set[vertices];

    // Initialize the array of vertices
    for (int i = 0; i < vertices; i++)
        vertex_set[i] = 0;

    // Number of occurrences of vertex in code
    for (int i = 0; i < vertices - 2; i++)
        vertex_set[prufer[i] - 1] += 1;

    cout << "\nThe edge set E(G) is :\n";

    // Find the smallest label not present in
    // prufer[].
    int j = 0;
    for (int i = 0; i < vertices - 2; i++) {
        for (j = 0; j < vertices; j++) {
            // If j+1 is not present in prufer set
            if (vertex_set[j] == 0) {
                // Remove from Prufer set and print
                // pair.
                vertex_set[j] = -1;
                cout << "(" << (j + 1) << ", "
                     << prufer[i] << ")  ";

                vertex_set[prufer[i] - 1]--;

                break;
            }
        }
    }

    j = 0;
    // For the last element
    for (int i = 0; i < vertices; i++) {
        if (vertex_set[i] == 0 && j == 0) {
            cout << "(" << (i + 1) << ", ";
            j++;
        }
        else if (vertex_set[i] == 0 && j == 1)
            cout << (i + 1) << ")\n";
    }
}

// Driver code
int main()
{
    int prufer[] = { 4, 1, 3, 4 };
    int n = sizeof(prufer) / sizeof(prufer[0]);
    printTreeEdges(prufer, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct tree from given Prufer Code
class GFG {

    // Prints edges of tree represented by give Prufer code
    static void printTreeEdges(int prufer[], int m)
    {
        int vertices = m + 2;
        int vertex_set[] = new int[vertices];

        // Initialize the array of vertices
        for (int i = 0; i < vertices; i++)
            vertex_set[i] = 0;

        // Number of occurrences of vertex in code
        for (int i = 0; i < vertices - 2; i++)
            vertex_set[prufer[i] - 1] += 1;

        System.out.print("\nThe edge set E(G) is :\n");

        // Find the smallest label not present in
        // prufer[].
        int j = 0;
        for (int i = 0; i < vertices - 2; i++) {
            for (j = 0; j < vertices; j++) {
                // If j+1 is not present in prufer set
                if (vertex_set[j] == 0) {
                    // Remove from Prufer set and print
                    // pair.
                    vertex_set[j] = -1;
                    System.out.print("(" + (j + 1) + ", "
                                     + prufer[i] + ") ");

                    vertex_set[prufer[i] - 1]--;

                    break;
                }
            }
        }

        j = 0;
        // For the last element
        for (int i = 0; i < vertices; i++) {
            if (vertex_set[i] == 0 && j == 0) {
                System.out.print("(" + (i + 1) + ", ");
                j++;
            }
            else if (vertex_set[i] == 0 && j == 1)
                System.out.print((i + 1) + ")\n");
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int prufer[] = { 4, 1, 3, 4 };
        int n = prufer.length;
        printTreeEdges(prufer, n);
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to construct
# tree from given Prufer Code

# Prints edges of tree represented
# by give Prufer code
def printTreeEdges(prufer, m):

    vertices = m + 2

    # Initialize the array of vertices
    vertex_set = [0] * vertices

    # Number of occurrences of vertex in code
    for i in range(vertices - 2):
        vertex_set[prufer[i] - 1] += 1

    print("The edge set E(G) is :")

    # Find the smallest label not present in
    # prufer.
    j = 0
    for i in range(vertices - 2):
        for j in range(vertices):

            # If j+1 is not present in prufer set
            if (vertex_set[j] == 0):

                # Remove from Prufer set and print
                # pair.
                vertex_set[j] = -1
                print("(" , (j + 1),", ",prufer[i],") ",sep = "",end = "")
                vertex_set[prufer[i] - 1] -= 1
                break

    j = 0

    # For the last element
    for i in range(vertices):
        if (vertex_set[i] == 0 and j == 0):
            print("(", (i + 1),", ", sep="", end="")
            j += 1
        elif (vertex_set[i] == 0 and j == 1):
            print((i + 1),")")

# Driver code
prufer = [4, 1, 3, 4]
n = len(prufer)
printTreeEdges(prufer, n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to construct tree from given Prufer Code
using System;

class GFG {

    // Prints edges of tree represented by give Prufer code
    static void printTreeEdges(int[] prufer, int m)
    {
        int vertices = m + 2;
        int[] vertex_set = new int[vertices];

        // Initialize the array of vertices
        for (int i = 0; i < vertices; i++)
            vertex_set[i] = 0;

        // Number of occurrences of vertex in code
        for (int i = 0; i < vertices - 2; i++)
            vertex_set[prufer[i] - 1] += 1;

        Console.Write("\nThe edge set E(G) is :\n");

        // Find the smallest label not present in
        // prufer[].
        int j = 0;
        for (int i = 0; i < vertices - 2; i++) {
            for (j = 0; j < vertices; j++) {
                // If j+1 is not present in prufer set
                if (vertex_set[j] == 0) {
                    // Remove from Prufer set and print
                    // pair.
                    vertex_set[j] = -1;
                    Console.Write("(" + (j + 1) + ", "
                                  + prufer[i] + ") ");

                    vertex_set[prufer[i] - 1]--;

                    break;
                }
            }
        }

        j = 0;
        // For the last element
        for (int i = 0; i < vertices; i++) {
            if (vertex_set[i] == 0 && j == 0) {
                Console.Write("(" + (i + 1) + ", ");
                j++;
            }
            else if (vertex_set[i] == 0 && j == 1)
                Console.Write((i + 1) + ")\n");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] prufer = { 4, 1, 3, 4 };
        int n = prufer.Length;
        printTreeEdges(prufer, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to construct tree from given Prufer Code

// Prints edges of tree represented by give Prufer code   
function printTreeEdges(prufer,m)
{
    let vertices = m + 2;
        let vertex_set = new Array(vertices);

        // Initialize the array of vertices
        for (let i = 0; i < vertices; i++)
            vertex_set[i] = 0;

        // Number of occurrences of vertex in code
        for (let i = 0; i < vertices - 2; i++)
            vertex_set[prufer[i] - 1] += 1;

        document.write("<br>The edge set E(G) is :<br>");

        // Find the smallest label not present in
        // prufer[].
        let j = 0;
        for (let i = 0; i < vertices - 2; i++) {
            for (j = 0; j < vertices; j++) {
                // If j+1 is not present in prufer set
                if (vertex_set[j] == 0) {
                    // Remove from Prufer set and print
                    // pair.
                    vertex_set[j] = -1;
                    document.write("(" + (j + 1) + ", "
                                     + prufer[i] + ") ");

                    vertex_set[prufer[i] - 1]--;

                    break;
                }
            }
        }

        j = 0;
        // For the last element
        for (let i = 0; i < vertices; i++) {
            if (vertex_set[i] == 0 && j == 0) {
                document.write("(" + (i + 1) + ", ");
                j++;
            }
            else if (vertex_set[i] == 0 && j == 1)
                document.write((i + 1) + ")\n");
        }
}

// Driver code
let prufer=[4, 1, 3, 4];
let n = prufer.length;
printTreeEdges(prufer, n);

// This code is contributed by rag2127

</script>
```

**输出:**

```
The edge set E(G) is :
(2, 4) (5, 1) (1, 3) (3, 4) (4, 6)
```

本文由**尼克尔·夏尔马**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。