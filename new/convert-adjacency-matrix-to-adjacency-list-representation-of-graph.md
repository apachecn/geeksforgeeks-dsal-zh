# 将邻接矩阵转换为图

的邻接列表表示

> 原文： [https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/](https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/)

**先决条件：** [图及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)
给定图的[邻接矩阵表示。 任务是将给定的邻接矩阵转换为邻接列表表示形式。
**范例：**](https://www.geeksforgeeks.org/graph-and-its-representations/)

> **输入：** arr [] [] = [[0，0，1]，[0，0，1]，[1，1，0]]
> **输出：** 相邻列表为：
> 0-> 2
> 1-> 2
> 2-> 0-> 1
> 
> **输入：** arr [] [] = [[0，1，0，0，1]，[1，0，1，1，1]，[0，1，0，1，0] ，[0，1，1，0，1]，[1，1，0，1，0]]
> **输出：**邻接表是：
> 0-> 1 -> 4
> 1-> 0-> 2-> 3-> 4
> 2-> 1-> 3
> 3-> 1-> 2-> 4
> 4-> 0-> 1-> 3

**邻接矩阵**：邻接矩阵是大小为 V x V 的 2D 数组，其中 V 是图形中的顶点数。 假设 2D 数组为 adj [] []，则槽 adj [i] [j] = 1 表示从顶点 i 到顶点 j 有一条边。

**邻接列表：**使用列表数组。 数组的大小等于顶点数。 令数组为 array []。 条目数组[i]表示与第 i 个顶点相邻的顶点的列表。

将邻接矩阵转换为邻接表。 创建一个列表数组并遍历邻接矩阵。 如果矩阵“ **mat [i] [j] = 1** ”中的任何单元格**（i，j）**，则表示从 **i 到 j** ，因此将 **j** 插入列表列表中**第 i** 个位置的列表中。

下面是上述方法的实现：

## C ++

```

#include<bits/stdc++.h> 
using namespace std; 

// CPP program to convert Adjacency matrix 
// representation to Adjacency List 

// converts from adjacency matrix to adjacency list 
vector<vector<int>> convert( vector<vector<int>> a) 
{ 
    vector<vector<int>> adjList(a.size()); 
    for (int i = 0; i < a.size(); i++) 
    { 

        for (int j = 0; j < a[i].size(); j++) 
        { 
            if (a[i][j] == 1) 
            { 
                adjList[i].push_back(j); 
            } 
        } 
    } 
    return adjList; 
} 

// Driver code 
int main() 
{ 
    vector<vector<int>> a; 
    vector<int> p({0, 0, 1}); 
    vector<int> q({0, 0, 1}); 
    vector<int> r({1, 1, 0}); // adjacency matrix 
    a.push_back(p); 
    a.push_back(q); 
    a.push_back(r); 
    vector<vector<int>> AdjList = convert(a); 
    cout<<"Adjacency List:"<<endl; 

    // print the adjacency list 
    for (int i = 0; i < AdjList.size(); i++) 
    { 
        cout << i; 
        for(int j = 0; j < AdjList[i].size(); j++) 
        { 
            if(j == AdjList[i].size() - 1) 
            { 
                cout << " -> " << AdjList[i][j] << endl; 
                break; 
            } 
            else
                cout << " -> " << AdjList[i][j]; 
        } 
    } 
} 

// This code is contributed by Surendra_Gangwar 

```

## 爪哇

```

// Java program to convert adjacency 
// matrix representation to 
// adjacency list 
import java.util.*; 

public class GFG { 

    // Function to convert adjacency 
    // list to adjacency matrix 
    static ArrayList<ArrayList<Integer>> convert(int[][] a) 
    { 
        // no of vertices 
        int l = a[0].length; 
        ArrayList<ArrayList<Integer>> adjListArray  
        = new ArrayList<ArrayList<Integer>>(l); 

        // Create a new list for each 
        // vertex such that adjacent 
        // nodes can be stored 
        for (int i = 0; i < l; i++) { 
            adjListArray.add(new ArrayList<Integer>()); 
        } 

        int i, j; 
        for (i = 0; i < a[0].length; i++) { 
            for (j = 0; j < a.length; j++) { 
                if (a[i][j] == 1) { 
                    adjListArray.get(i).add(j); 
                } 
            } 
        } 

        return adjListArray; 
    } 

    // Function to print the adjacency list 
    static void printArrayList(ArrayList<ArrayList<Integer>>  
                                                adjListArray) 
    { 
        // Print the adjacency list 
        for (int v = 0; v < adjListArray.size(); v++) { 
            System.out.print(v); 
            for (Integer u : adjListArray.get(v)) { 
                System.out.print(" -> " + u); 
            } 
            System.out.println(); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Given Adjacency Matrix 
        int[][] a = { { 0, 0, 1 }, 
                    { 0, 0, 1 }, 
                    { 1, 1, 0 } }; 

        // function to convert adjacency 
        // list to adjacency matrix 
        ArrayList<ArrayList<Integer>> adjListArray = convert(a); 
        System.out.println("Adjacency List: "); 

        printArrayList(adjListArray); 
    } 
} 

```

## 蟒蛇

```

# Python program to convert Adjacency matrix 
# representation to Adjacency List 

from collections import defaultdict 
# converts from adjacency matrix to adjacency list 
def convert(a): 
    adjList = defaultdict(list) 
    for i in range(len(a)): 
        for j in range(len(a[i])): 
                       if a[i][j]== 1: 
                           adjList[i].append(j) 
    return adjList 

# driver code 
a =[[0, 0, 1], [0, 0, 1], [1, 1, 0]] # adjacency matrix 
AdjList = convert(a) 
print("Adjacency List:") 
# print the adjacency list 
for i in AdjList: 
    print(i, end ="") 
    for j in AdjList[i]: 
        print(" -> {}".format(j), end ="") 
    print() 

# This code is contributed by Muskan Kalra. 

```

## C＃

```

// C# program to convert adjacency 
// matrix representation to 
// adjacency list 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    // Function to convert adjacency 
    // list to adjacency matrix 
    static List<List<int>> convert(int[,] a) 
    { 
        // no of vertices 
        int l = a.GetLength(0); 
        List<List<int>> adjListArray = new List<List<int>>(l); 
        int i, j; 

        // Create a new list for each 
        // vertex such that adjacent 
        // nodes can be stored 
        for (i = 0; i < l; i++)  
        { 
            adjListArray.Add(new List<int>()); 
        } 

        for (i = 0; i < a.GetLength(0); i++)  
        { 
            for (j = 0; j < a.GetLength(1); j++) 
            { 
                if (a[i,j] == 1)  
                { 
                    adjListArray[i].Add(j); 
                } 
            } 
        } 

        return adjListArray; 
    } 

    // Function to print the adjacency list 
    static void printList(List<List<int>> adjListArray)  
    { 

        // Print the adjacency list 
        for (int v = 0; v < adjListArray.Count; v++)  
        { 
            Console.Write(v); 
            foreach (int u in adjListArray[v]) 
            { 
                Console.Write(" -> " + u); 
            } 
            Console.WriteLine(); 
        } 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 

        // Given Adjacency Matrix 
        int[,] a = { { 0, 0, 1 }, { 0, 0, 1 }, { 1, 1, 0 } }; 

        // function to convert adjacency 
        // list to adjacency matrix 
        List<List<int>> adjListArray = convert(a); 
        Console.WriteLine("Adjacency List: "); 

        printList(adjListArray); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Adjacency List:
0 -> 2
1 -> 2
2 -> 0 -> 1

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。