# 找出离岛数| 组 2（使用不交集）

> 原文： [https://www.geeksforgeeks.org/find-the-number-of-islands-set-2-using-disjoint-set/](https://www.geeksforgeeks.org/find-the-number-of-islands-set-2-using-disjoint-set/)

给定布尔 2D 矩阵，找到孤岛的数量。

一组相连的 1 组成一个岛。 例如，下面的矩阵包含 5 个岛

```
{1, 1, 0, 0, 0},
{0, 1, 0, 0, 1},
{1, 0, 0, 1, 1},
{0, 0, 0, 0, 0},
{1, 0, 1, 0, 1} 
```

2D 矩阵中的一个单元可以连接到 8 个邻居。

这是标准问题的变体：“计算无向图中的已连接组件数”。 我们在下面的第 1 组中讨论了基于 DFS 的解决方案。

[查找孤岛数](https://www.geeksforgeeks.org/find-number-of-islands/)

我们也可以使用这里解释的不相交集数据结构来解决这个问题。 想法是将所有 1 个值视为单独的集合。 遍历矩阵并对所有相邻的 1 个顶点进行并集。 以下是详细步骤。

 **方法**：
1）将结果（孤岛数）初始化为 0
2）遍历 2D 矩阵的每个索引。
3）如果该索引的值为 1，请检查其所有 8 个邻居。 如果邻居也等于 1，则将索引与其邻居合并。
4）现在定义一个大小为 row * column 的数组，以存储所有集合的频率。
5）现在再次遍历矩阵。
6）如果索引处的值为 1，则找到它的集合。
7）如果上述数组中集合的频率为 0，则将结果加 1。

以下是上述步骤的 Java 实现。

## C ++

```

// C++ program to fnd number of islands  
// using Disjoint Set data structure. 
#include <bits/stdc++.h> 
using namespace std; 

// Class to represent 
// Disjoint Set Data structure 
class DisjointUnionSets 
{ 

    vector<int> rank, parent; 
    int n; 

    public: 
    DisjointUnionSets(int n) 
    { 
        rank.resize(n); 
        parent.resize(n); 
        this->n = n; 
        makeSet(); 
    } 

    void makeSet() 
    { 
        // Initially, all elements   
        // are in their own set. 
        for (int i = 0; i < n; i++) 
            parent[i] = i; 
    } 

    // Finds the representative of the set  
    // that x is an element of 
    int find(int x) 
    { 
        if (parent[x] != x) 
        { 
            // if x is not the parent of itself, 
            // then x is not the representative of 
            // its set. 
            // so we recursively call Find on its parent 
            // and move i's node directly under the 
            // representative of this set 
            return find(parent[x]); 
        } 

        return x; 
    } 

    // Unites the set that includes x and the set 
    // that includes y 
    void Union(int x, int y) 
    { 
        // Find the representatives(or the root nodes) 
        // for x an y 
        int xRoot = find(x); 
        int yRoot = find(y); 

        // Elements are in the same set,  
        // no need to unite anything. 
        if (xRoot == yRoot) 
            return; 

        // If x's rank is less than y's rank 
        // Then move x under y so that  
        // depth of tree remains less 
        if (rank[xRoot] < rank[yRoot]) 
            parent[xRoot] = yRoot; 

        // Else if y's rank is less than x's rank 
        // Then move y under x so that depth of tree 
        // remains less 
        else if (rank[yRoot] < rank[xRoot]) 
            parent[yRoot] = xRoot; 

        else // Else if their ranks are the same 
        { 
            // Then move y under x (doesn't matter 
            // which one goes where) 
            parent[yRoot] = xRoot; 

            // And increment the result tree's 
            // rank by 1 
            rank[xRoot] = rank[xRoot] + 1; 
        } 
    } 
}; 

// Returns number of islands in a[][] 
int countIslands(vector<vector<int>>a) 
{ 
    int n = a.size(); 
    int m = a[0].size(); 

    DisjointUnionSets *dus = new DisjointUnionSets(n * m); 

    /* The following loop checks for its neighbours 
    and unites the indexes if both are 1\. */
    for (int j = 0; j < n; j++) 
    { 
        for (int k = 0; k < m; k++) 
        { 
            // If cell is 0, nothing to do 
            if (a[j][k] == 0) 
                continue; 

            // Check all 8 neighbours and do a Union 
            // with neighbour's set if neighbour is 
            // also 1 
            if (j + 1 < n && a[j + 1][k] == 1) 
                dus->Union(j * (m) + k,  
                          (j + 1) * (m) + k); 
            if (j - 1 >= 0 && a[j - 1][k] == 1) 
                dus->Union(j * (m) + k,  
                          (j - 1) * (m) + k); 
            if (k + 1 < m && a[j][k + 1] == 1) 
                dus->Union(j * (m) + k,  
                          (j) * (m) + k + 1); 
            if (k - 1 >= 0 && a[j][k - 1] == 1) 
                dus->Union(j * (m) + k, 
                          (j) * (m) + k - 1); 
            if (j + 1 < n && k + 1 < m &&  
                    a[j + 1][k + 1] == 1) 
                dus->Union(j * (m) + k,  
                          (j + 1) * (m) + k + 1); 
            if (j + 1 < n && k - 1 >= 0 &&  
                    a[j + 1][k - 1] == 1) 
                dus->Union(j * m + k,  
                          (j + 1) * (m) + k - 1); 
            if (j - 1 >= 0 && k + 1 < m &&  
                     a[j - 1][k + 1] == 1) 
                dus->Union(j * m + k,  
                          (j - 1) * m + k + 1); 
            if (j - 1 >= 0 && k - 1 >= 0 &&  
                     a[j - 1][k - 1] == 1) 
                dus->Union(j * m + k,  
                          (j - 1) * m + k - 1); 
        } 
    } 

    // Array to note down frequency of each set 
    int *c = new int[n * m]; 
    int numberOfIslands = 0; 
    for (int j = 0; j < n; j++) 
    { 
        for (int k = 0; k < m; k++) 
        { 
            if (a[j][k] == 1) 
            { 
                int x = dus->find(j * m + k); 

                // If frequency of set is 0, 
                // increment numberOfIslands 
                if (c[x] == 0) 
                { 
                    numberOfIslands++; 
                    c[x]++; 
                } 

                else
                    c[x]++; 
            } 
        } 
    } 
    return numberOfIslands; 
} 

//  Driver Code 
int main(void) 
{ 
    vector<vector<int>>a = {{1, 1, 0, 0, 0}, 
                            {0, 1, 0, 0, 1}, 
                            {1, 0, 0, 1, 1}, 
                            {0, 0, 0, 0, 0}, 
                            {1, 0, 1, 0, 1}}; 
    cout << "Number of Islands is: " 
         << countIslands(a) << endl; 
} 

// This code is contributed by ankush_953 

```

## 爪哇

```

// Java program to fnd number of islands using Disjoint 
// Set data structure. 
import java.io.*; 
import java.util.*; 

public class Main 
{ 
    public static void main(String[] args)throws IOException 
    { 
        int[][] a = new int[][] {{1, 1, 0, 0, 0}, 
                                 {0, 1, 0, 0, 1}, 
                                 {1, 0, 0, 1, 1}, 
                                 {0, 0, 0, 0, 0}, 
                                 {1, 0, 1, 0, 1} 
                                }; 
        System.out.println("Number of Islands is: " + 
                           countIslands(a)); 
     } 

     // Returns number of islands in a[][] 
     static int countIslands(int a[][]) 
     { 
        int n = a.length; 
        int m = a[0].length; 

        DisjointUnionSets dus = new DisjointUnionSets(n*m); 

        /* The following loop checks for its neighbours 
           and unites the indexes  if both are 1\. */
        for (int j=0; j<n; j++) 
        { 
            for (int k=0; k<m; k++) 
            { 
                // If cell is 0, nothing to do 
                if (a[j][k] == 0) 
                    continue; 

                // Check all 8 neighbours and do a union 
                // with neighbour's set if neighbour is  
                // also 1 
                if (j+1 < n && a[j+1][k]==1) 
                    dus.union(j*(m)+k, (j+1)*(m)+k); 
                if (j-1 >= 0 && a[j-1][k]==1) 
                    dus.union(j*(m)+k, (j-1)*(m)+k); 
                if (k+1 < m && a[j][k+1]==1) 
                    dus.union(j*(m)+k, (j)*(m)+k+1); 
                if (k-1 >= 0 && a[j][k-1]==1) 
                    dus.union(j*(m)+k, (j)*(m)+k-1); 
                if (j+1<n && k+1<m && a[j+1][k+1]==1) 
                    dus.union(j*(m)+k, (j+1)*(m)+k+1); 
                if (j+1<n && k-1>=0 && a[j+1][k-1]==1) 
                    dus.union(j*m+k, (j+1)*(m)+k-1); 
                if (j-1>=0 && k+1<m && a[j-1][k+1]==1) 
                    dus.union(j*m+k, (j-1)*m+k+1); 
                if (j-1>=0 && k-1>=0 && a[j-1][k-1]==1) 
                    dus.union(j*m+k, (j-1)*m+k-1); 
            } 
        } 

        // Array to note down frequency of each set 
        int[] c = new int[n*m]; 
        int numberOfIslands = 0; 
        for (int j=0; j<n; j++) 
        { 
            for (int k=0; k<m; k++) 
            { 
                if (a[j][k]==1) 
                { 

                    int x = dus.find(j*m+k); 

                    // If frequency of set is 0,  
                    // increment numberOfIslands 
                    if (c[x]==0) 
                    { 
                        numberOfIslands++; 
                        c[x]++; 
                    } 

                    else
                        c[x]++; 
                } 
            } 
        } 
        return numberOfIslands; 
    } 
} 

// Class to represent Disjoint Set Data structure 
class DisjointUnionSets 
{ 
    int[] rank, parent; 
    int n; 

    public DisjointUnionSets(int n) 
    { 
        rank = new int[n]; 
        parent = new int[n]; 
        this.n = n; 
        makeSet(); 
    } 

    void makeSet() 
    { 
        // Initially, all elements are in their 
        // own set. 
        for (int i=0; i<n; i++) 
            parent[i] = i; 
    } 

    // Finds the representative of the set that x 
    // is an element of 
    int find(int x) 
    { 
        if (parent[x] != x) 
        { 
            // if x is not the parent of itself, 
            // then x is not the representative of 
            // its set. 
            // so we recursively call Find on its parent 
            // and move i's node directly under the 
            // representative of this set 
            return find(parent[x]); 
        } 

        return x; 
    } 

    // Unites the set that includes x and the set 
    // that includes y 
    void union(int x, int y) 
    { 
        // Find the representatives (or the root nodes) 
        // for x an y 
        int xRoot = find(x); 
        int yRoot = find(y); 

        // Elements are in the same set, no need 
        // to unite anything. 
        if (xRoot == yRoot) 
            return; 

        // If x's rank is less than y's rank 
        // Then move x under y  so that depth of tree 
        // remains less 
        if (rank[xRoot] < rank[yRoot]) 
            parent[xRoot] = yRoot; 

        // Else if y's rank is less than x's rank 
        // Then move y under x so that depth of tree 
        // remains less 
        else if(rank[yRoot]<rank[xRoot]) 
            parent[yRoot] = xRoot; 

        else  // Else if their ranks are the same 
        { 
            // Then move y under x (doesn't matter 
            // which one goes where) 
            parent[yRoot] = xRoot; 

            // And increment the result tree's 
            // rank by 1 
            rank[xRoot] = rank[xRoot] + 1; 
        } 
    } 
} 

```

## Python3

```

# Python3 program to find  
# the number of islands using  
# Disjoint Set data structure. 

# Class to represent  
# Disjoint Set Data structure 
class DisjointUnionSets: 
    def __init__(self, n): 
        self.rank = [0] * n 
        self.parent = [0] * n 
        self.n = n 
        self.makeSet() 

    def makeSet(self): 

        # Initially, all elements are in their 
        # own set. 
        for i in range(self.n): 
            self.parent[i] = i 

    # Finds the representative of the set that x 
    # is an element of 
    def find(self, x): 
        if (self.parent[x] != x): 

            # if x is not the parent of itself, 
            # then x is not the representative of 
            # its set. 
            # so we recursively call Find on its parent 
            # and move i's node directly under the 
            # representative of this set 
            return self.find(self.parent[x]) 
        return x 

    # Unites the set that includes x and  
    # the set that includes y 
    def Union(self, x, y): 

        # Find the representatives(or the root nodes) 
        # for x an y 
        xRoot = self.find(x) 
        yRoot = self.find(y) 

        # Elements are in the same set,  
        # no need to unite anything. 
        if xRoot == yRoot: 
            return

        # If x's rank is less than y's rank 
        # Then move x under y so that depth of tree 
        # remains less 
        if self.rank[xRoot] < self.rank[yRoot]: 
            parent[xRoot] = yRoot 

        # Else if y's rank is less than x's rank 
        # Then move y under x so that depth of tree 
        # remains less 
        elif self.rank[yRoot] < self.rank[xRoot]: 
            self.parent[yRoot] = xRoot 

        else: 

            # Else if their ranks are the same 
            # Then move y under x (doesn't matter 
            # which one goes where) 
            self.parent[yRoot] = xRoot 

            # And increment the result tree's 
            # rank by 1 
            self.rank[xRoot] = self.rank[xRoot] + 1

# Returns number of islands in a[][] 
def countIslands(a): 
    n = len(a) 
    m = len(a[0]) 

    dus = DisjointUnionSets(n * m) 

    # The following loop checks for its neighbours 
    # and unites the indexes if both are 1\. 
    for j in range(0, n): 
        for k in range(0, m): 

            # If cell is 0, nothing to do 
            if a[j][k] == 0: 
                continue

            # Check all 8 neighbours and do a Union 
            # with neighbour's set if neighbour is 
            # also 1 
            if j + 1 < n and a[j + 1][k] == 1: 
                dus.Union(j * (m) + k,   
                         (j + 1) * (m) + k) 
            if j - 1 >= 0 and a[j - 1][k] == 1: 
                dus.Union(j * (m) + k,  
                         (j - 1) * (m) + k) 
            if k + 1 < m and a[j][k + 1] == 1: 
                dus.Union(j * (m) + k,  
                        (j) * (m) + k + 1) 
            if k - 1 >= 0 and a[j][k - 1] == 1: 
                dus.Union(j * (m) + k,  
                        (j) * (m) + k - 1) 
            if (j + 1 < n and k + 1 < m and 
                     a[j + 1][k + 1] == 1): 
                dus.Union(j * (m) + k, (j + 1) * 
                              (m) + k + 1) 
            if (j + 1 < n and k - 1 >= 0 and 
                     a[j + 1][k - 1] == 1): 
                dus.Union(j * m + k, (j + 1) * 
                             (m) + k - 1) 
            if (j - 1 >= 0 and k + 1 < m and 
                      a[j - 1][k + 1] == 1): 
                dus.Union(j * m + k, (j - 1) *
                              m + k + 1) 
            if (j - 1 >= 0 and k - 1 >= 0 and 
                      a[j - 1][k - 1] == 1): 
                dus.Union(j * m + k, (j - 1) * 
                              m + k - 1) 

    # Array to note down frequency of each set 
    c = [0] * (n * m) 
    numberOfIslands = 0
    for j in range(n): 
        for k in range(n): 
            if a[j][k] == 1: 
                x = dus.find(j * m + k) 

                # If frequency of set is 0, 
                # increment numberOfIslands 
                if c[x] == 0: 
                    numberOfIslands += 1
                    c[x] += 1
                else: 
                    c[x] += 1
    return numberOfIslands 

# Driver Code 
a = [[1, 1, 0, 0, 0], 
     [0, 1, 0, 0, 1], 
     [1, 0, 0, 1, 1], 
     [0, 0, 0, 0, 0], 
     [1, 0, 1, 0, 1]] 
print("Number of Islands is:", countIslands(a)) 

# This code is contributed by ankush_953 

```

## C＃

```

// C# program to fnd number of islands using Disjoint 
// Set data structure. 
using System; 

class GFG 
{ 
    public static void Main(String[] args) 
    { 
        int[,] a = new int[,] {{1, 1, 0, 0, 0}, 
                                {0, 1, 0, 0, 1}, 
                                {1, 0, 0, 1, 1}, 
                                {0, 0, 0, 0, 0}, 
                                {1, 0, 1, 0, 1} 
                                }; 
        Console.WriteLine("Number of Islands is: " + 
                        countIslands(a)); 
    } 

    // Returns number of islands in[,]a 
    static int countIslands(int[,]a) 
    { 
        int n = a.GetLength(0); 
        int m = a.GetLength(1); 

        DisjointUnionSets dus = new DisjointUnionSets(n * m); 

        /* The following loop checks for its neighbours 
        and unites the indexes if both are 1\. */
        for (int j = 0; j < n; j++) 
        { 
            for (int k = 0; k < m; k++) 
            { 
                // If cell is 0, nothing to do 
                if (a[j, k] == 0) 
                    continue; 

                // Check all 8 neighbours and do a union 
                // with neighbour's set if neighbour is  
                // also 1 
                if (j + 1 < n && a[j + 1, k] == 1) 
                    dus.union(j * (m) + k, (j + 1) * (m) + k); 
                if (j - 1 >= 0 && a[j - 1, k] == 1) 
                    dus.union(j * (m) + k, (j - 1) * (m) + k); 
                if (k + 1 < m && a[j, k + 1] == 1) 
                    dus.union(j * (m) + k, (j) * (m) + k + 1); 
                if (k-1 >= 0 && a[j,k-1]==1) 
                    dus.union(j * (m) + k, (j) * (m) + k - 1); 
                if (j + 1 < n && k + 1 < m && a[j + 1, k + 1] == 1) 
                    dus.union(j * (m) + k, (j + 1) * (m) + k + 1); 
                if (j + 1 < n && k - 1 >= 0 && a[j + 1,k - 1] == 1) 
                    dus.union(j * m + k, (j + 1) * (m) + k - 1); 
                if (j - 1 >= 0 && k + 1 < m && a[j - 1, k + 1] == 1) 
                    dus.union(j * m + k, (j - 1) * m + k + 1); 
                if (j - 1 >= 0 && k - 1 >= 0 && a[j - 1, k - 1] == 1) 
                    dus.union(j * m + k, (j - 1) * m + k - 1); 
            } 
        } 

        // Array to note down frequency of each set 
        int[] c = new int[n*m]; 
        int numberOfIslands = 0; 
        for (int j = 0; j < n; j++) 
        { 
            for (int k = 0; k < m; k++) 
            { 
                if (a[j, k] == 1) 
                { 

                    int x = dus.find(j * m + k); 

                    // If frequency of set is 0,  
                    // increment numberOfIslands 
                    if (c[x] == 0) 
                    { 
                        numberOfIslands++; 
                        c[x]++; 
                    } 

                    else
                        c[x]++; 
                } 
            } 
        } 
        return numberOfIslands; 
    } 
} 

// Class to represent Disjoint Set Data structure 
class DisjointUnionSets 
{ 
    int[] rank, parent; 
    int n; 

    public DisjointUnionSets(int n) 
    { 
        rank = new int[n]; 
        parent = new int[n]; 
        this.n = n; 
        makeSet(); 
    } 

    public void makeSet() 
    { 
        // Initially, all elements are in their 
        // own set. 
        for (int i = 0; i < n; i++) 
            parent[i] = i; 
    } 

    // Finds the representative of the set that x 
    // is an element of 
    public int find(int x) 
    { 
        if (parent[x] != x) 
        { 
            // if x is not the parent of itself, 
            // then x is not the representative of 
            // its set. 
            // so we recursively call Find on its parent 
            // and move i's node directly under the 
            // representative of this set 
            return find(parent[x]); 
        } 

        return x; 
    } 

    // Unites the set that includes x and the set 
    // that includes y 
    public void union(int x, int y) 
    { 
        // Find the representatives (or the root nodes) 
        // for x an y 
        int xRoot = find(x); 
        int yRoot = find(y); 

        // Elements are in the same set, no need 
        // to unite anything. 
        if (xRoot == yRoot) 
            return; 

        // If x's rank is less than y's rank 
        // Then move x under y so that depth of tree 
        // remains less 
        if (rank[xRoot] < rank[yRoot]) 
            parent[xRoot] = yRoot; 

        // Else if y's rank is less than x's rank 
        // Then move y under x so that depth of tree 
        // remains less 
        else if(rank[yRoot] < rank[xRoot]) 
            parent[yRoot] = xRoot; 

        else // Else if their ranks are the same 
        { 
            // Then move y under x (doesn't matter 
            // which one goes where) 
            parent[yRoot] = xRoot; 

            // And increment the result tree's 
            // rank by 1 
            rank[xRoot] = rank[xRoot] + 1; 
        } 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Number of Islands is: 5

```

本文由 **Nikhil Tekwani** 提供。如果您喜欢 GeeksforGeeks 并希望做出贡献，也可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章或将您的文章邮寄到 contribution @ geeksforgeeks .org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

