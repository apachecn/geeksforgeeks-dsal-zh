# 在无向图和连接图

中长度为 n 的循环

> 原文： [https://www.geeksforgeeks.org/cycles-of-length-n-in-an-undirected-and-connected-graph/](https://www.geeksforgeeks.org/cycles-of-length-n-in-an-undirected-and-connected-graph/)

给定一个无向图和连通图，并给定一个数字 n，请计算该图中长度为 n 的循环总数。 长度为 n 的循环仅表示该循环包含 n 个顶点和 n 条边。 而且我们必须计算所有存在的此类循环。
**范例**：

```
Input :  n = 4

Output : Total cycles = 3
Explanation : Following 3 unique cycles 
   0 -> 1 -> 2 -> 3 -> 0
   0 -> 1 -> 4 -> 3 -> 0
   1 -> 2 -> 3 -> 4 -> 1
Note* : There are more cycles but
these 3 are unique as 0 -> 3 -> 2 -> 1
-> 0 and 0 -> 1 -> 2 -> 3 -> 0 are 
same cycles and hence will be counted as 1.

```

为了解决该问题，可以有效地使用 [DFS（深度优先搜索）](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。 使用 DFS，我们可以找到特定来源（或起点）的每个长度（n-1）的可能路径。 然后我们检查该路径是否以其开始的顶点结束，如果是，则将其计为长度为 n 的周期。 注意，我们在寻找长度为（n-1）的路径，因为第 n 个<sup>边</sup>将是循环的闭合边。

只能使用`V`–（`n`–`1`）个顶点（其中 V 是顶点总数）来搜索每个长度（n-1）的可能路径。 ）。
对于上面的示例，长度为 4 的所有循环只能使用 5-（4-1）= 2 个顶点进行搜索。 这背后的原因很简单，因为我们使用这 2 个顶点（包括其余 3 个顶点）搜索长度（n-1）= 3 的所有可能路径。 因此，这 2 个顶点也涵盖了其余 3 个顶点的周期，因此仅使用 3 个顶点我们就无法形成长度为 4 的周期。

还有一点要注意的是，每个顶点为其形成的每个循环找到 2 个重复的循环。 对于上述示例，第 0 个<sup>顶点找到两个重复周期，即 **0-> 3-> 2-> 1-> 0** 和 **0- > 1-> 2-> 3-> 0** 。 因此总计数必须除以 2，因为每个循环都被计数两次。</sup>

## C ++

```

// CPP Program to count cycles of length n 
// in a given graph. 
#include <bits/stdc++.h> 
using namespace std; 

// Number of vertices 
const int V = 5; 

void DFS(bool graph[][V], bool marked[], int n, 
               int vert, int start, int &count) 
{ 
    // mark the vertex vert as visited 
    marked[vert] = true; 

    // if the path of length (n-1) is found 
    if (n == 0) { 

        // mark vert as un-visited to make 
        // it usable again. 
        marked[vert] = false; 

        // Check if vertex vert can end with 
        // vertex start 
        if (graph[vert][start]) 
        { 
            count++; 
            return; 
        } else
            return; 
    } 

    // For searching every possible path of 
    // length (n-1) 
    for (int i = 0; i < V; i++) 
        if (!marked[i] && graph[vert][i]) 

            // DFS for searching path by decreasing 
            // length by 1 
            DFS(graph, marked, n-1, i, start, count); 

    // marking vert as unvisited to make it 
    // usable again. 
    marked[vert] = false; 
} 

// Counts cycles of length N in an undirected 
// and connected graph. 
int countCycles(bool graph[][V], int n) 
{ 
    // all vertex are marked un-visited initially. 
    bool marked[V]; 
    memset(marked, 0, sizeof(marked)); 

    // Searching for cycle by using v-n+1 vertices 
    int count = 0; 
    for (int i = 0; i < V - (n - 1); i++) { 
        DFS(graph, marked, n-1, i, i, count); 

        // ith vertex is marked as visited and 
        // will not be visited again. 
        marked[i] = true; 
    } 

    return count/2; 
} 

int main() 
{ 
    bool graph[][V] = {{0, 1, 0, 1, 0}, 
                      {1, 0, 1, 0, 1}, 
                      {0, 1, 0, 1, 0}, 
                      {1, 0, 1, 0, 1}, 
                      {0, 1, 0, 1, 0}}; 
    int n = 4; 
    cout << "Total cycles of length " << n << " are "
         << countCycles(graph, n); 
    return 0; 
} 

```

## 爪哇

```

// Java program to calculate cycles of 
// length n in a given graph 
public class Main { 

    // Number of vertices 
    public static final int V = 5; 
    static int count = 0; 

    static void DFS(int graph[][], boolean marked[], 
                    int n, int vert, int start) { 

        // mark the vertex vert as visited 
        marked[vert] = true; 

        // if the path of length (n-1) is found 
        if (n == 0) { 

            // mark vert as un-visited to  
            // make it usable again 
            marked[vert] = false; 

            // Check if vertex vert end  
            // with vertex start 
            if (graph[vert][start] == 1) { 
                count++; 
                return; 
            } else
                return; 
        } 

        // For searching every possible  
        // path of length (n-1) 
        for (int i = 0; i < V; i++) 
            if (!marked[i] && graph[vert][i] == 1) 

                // DFS for searching path by 
                // decreasing length by 1 
                DFS(graph, marked, n-1, i, start); 

        // marking vert as unvisited to make it 
        // usable again 
        marked[vert] = false; 
    } 

    // Count cycles of length N in an  
    // undirected and connected graph. 
    static int countCycles(int graph[][], int n) { 

        // all vertex are marked un-visited 
        // initially. 
        boolean marked[] = new boolean[V]; 

        // Searching for cycle by using  
        // v-n+1 vertices 
        for (int i = 0; i < V - (n - 1); i++) { 
            DFS(graph, marked, n-1, i, i); 

            // ith vertex is marked as visited 
            // and will not be visited again 
            marked[i] = true; 
        } 

        return count / 2;  
    } 

    // driver code 
    public static void main(String[] args) { 
        int graph[][] = {{0, 1, 0, 1, 0}, 
                        {1, 0, 1, 0, 1}, 
                        {0, 1, 0, 1, 0}, 
                        {1, 0, 1, 0, 1}, 
                        {0, 1, 0, 1, 0}}; 

        int n = 4; 

        System.out.println("Total cycles of length "+ 
                          n + " are "+  
                          countCycles(graph, n)); 
    } 
} 

// This code is contributed by nuclode 

```

## Python3

```

# Python Program to count 
# cycles of length n 
# in a given graph. 

# Number of vertices 
V = 5

def DFS(graph, marked, n, vert, start, count): 

    # mark the vertex vert as visited 
    marked[vert] = True

    # if the path of length (n-1) is found 
    if n == 0:  

        # mark vert as un-visited to make 
        # it usable again. 
        marked[vert] = False

        # Check if vertex vert can end with 
        # vertex start 
        if graph[vert][start] == 1: 
            count = count + 1
            return count 
        else: 
            return count 

    # For searching every possible path of 
    # length (n-1) 
    for i in range(V): 
        if marked[i] == False and graph[vert][i] == 1: 

            # DFS for searching path by decreasing 
            # length by 1 
            count = DFS(graph, marked, n-1, i, start, count) 

    # marking vert as unvisited to make it 
    # usable again. 
    marked[vert] = False
    return count 

# Counts cycles of length 
# N in an undirected 
# and connected graph. 
def countCycles( graph, n): 

    # all vertex are marked un-visited initially. 
    marked = [False] * V  

    # Searching for cycle by using v-n+1 vertices 
    count = 0
    for i in range(V-(n-1)): 
        count = DFS(graph, marked, n-1, i, i, count) 

        # ith vertex is marked as visited and 
        # will not be visited again. 
        marked[i] = True

    return int(count/2) 

# main : 
graph = [[0, 1, 0, 1, 0], 
         [1 ,0 ,1 ,0, 1], 
         [0, 1, 0, 1, 0], 
         [1, 0, 1, 0, 1], 
         [0, 1, 0, 1, 0]] 

n = 4
print("Total cycles of length ",n," are ",countCycles(graph, n)) 

# this code is contributed by Shivani Ghughtyal 

```

## C＃

```

// C# program to calculate cycles of 
// length n in a given graph 
using System; 

class GFG  
{ 

    // Number of vertices 
    public static int V = 5; 
    static int count = 0; 

    static void DFS(int [,]graph, bool []marked, 
                    int n, int vert, int start)  
    { 

        // mark the vertex vert as visited 
        marked[vert] = true; 

        // if the path of length (n-1) is found 
        if (n == 0)  
        { 

            // mark vert as un-visited to  
            // make it usable again 
            marked[vert] = false; 

            // Check if vertex vert end  
            // with vertex start 
            if (graph[vert, start] == 1) 
            { 
                count++; 
                return; 
            }  
            else
                return; 
        } 

        // For searching every possible  
        // path of length (n-1) 
        for (int i = 0; i < V; i++) 
            if (!marked[i] && graph[vert, i] == 1) 

                // DFS for searching path by 
                // decreasing length by 1 
                DFS(graph, marked, n - 1, i, start); 

        // marking vert as unvisited to make it 
        // usable again 
        marked[vert] = false; 
    } 

    // Count cycles of length N in an  
    // undirected and connected graph. 
    static int countCycles(int [,]graph, int n)  
    { 

        // all vertex are marked un-visited 
        // initially. 
        bool []marked = new bool[V]; 

        // Searching for cycle by using  
        // v-n+1 vertices 
        for (int i = 0; i < V - (n - 1); i++)  
        { 
            DFS(graph, marked, n - 1, i, i); 

            // ith vertex is marked as visited 
            // and will not be visited again 
            marked[i] = true; 
        } 

        return count / 2;  
    } 

    // Driver code 
    public static void Main() 
    { 
        int [,]graph = {{0, 1, 0, 1, 0}, 
                        {1, 0, 1, 0, 1}, 
                        {0, 1, 0, 1, 0}, 
                        {1, 0, 1, 0, 1}, 
                        {0, 1, 0, 1, 0}}; 

        int n = 4; 

        Console.WriteLine("Total cycles of length "+ 
                        n + " are "+  
                        countCycles(graph, n)); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Total cycles of length 4 are 3

```

本文由 [**Shubham Rana**](https://auth.geeksforgeeks.org/profile.php?user=shubham_rana_77&list=practice) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

