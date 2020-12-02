# 二进制值图

中连接组件的八进制等效项

> 原文： [https://www.geeksforgeeks.org/octal-equivalents-of-connected-components-in-binary-valued-graph/](https://www.geeksforgeeks.org/octal-equivalents-of-connected-components-in-binary-valued-graph/)

给定**二进制值** [无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，并带有`V`顶点和`E`边，任务是找到**八进制等效项** 图中所有已连接组件的]。 可以将二进制值图视为仅将二进制数**（0 或 1）**作为顶点值。

**示例**：

> **输入**：E = 4，V = 7
> 
> ![](img/fb50e4ce31778dd68a347b016976fde7.png)
> 
> **输出**：
> 链= 0 1 八进制等效值= 1
> 链= 0 0 0 八进制等效值= 0
> 链= 1 1 八进制等效值= 3
> **说明**：
> 在第一个连接的组件的情况下，二进制链为[0，1]
> 因此，二进制字符串=“ 01”且二进制数= 01
> 因此，八进制等效项为 1
> 
> **输入**：E = 6，V = 10
> 
> ![](img/83927206790a724c02078daf19b731bf.png)
> 
> **输出**：
> 链= 1 [八进制等效值] 1
> 链= 0 0 1 0 八进制等效值= 2
> 链= 1 1 0 八进制等效值= 6
> 链= 1 0 八进制等效值= 2

**方法**：的想法是使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来跟踪无向图中的已连接组件，如本文的[中所述。 对于每个连接的组件，将显示二进制字符串，并根据二进制值（如](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)[本文](https://www.geeksforgeeks.org/convert-binary-number-octal/)中所述）计算等效的八进制值并进行打印。

下面是上述方法的实现：

## C ++

```

// C++ implementation to find
// octal equivalents of
// all connected components

#include <bits/stdc++.h>

using namespace std;

// Function to traverse the undirected
// graph using the Depth first traversal
void depthFirst(int v, vector<int> graph[],
                vector<bool>& visited,
                vector<int>& storeChain)
{
    // Marking the visited
    // vertex as true
    visited[v] = true;

    // Store the connected chain
    storeChain.push_back(v);

    for (auto i : graph[v]) {
        if (visited[i] == false) {

            // Recursive call to
            // the DFS algorithm
            depthFirst(i, graph,
                       visited, storeChain);
        }
    }
}

// Function to create map between binary
// number and its equivalent octal value
void createMap(unordered_map<string, char>* um)
{
    (*um)["000"] = '0';
    (*um)["001"] = '1';
    (*um)["010"] = '2';
    (*um)["011"] = '3';
    (*um)["100"] = '4';
    (*um)["101"] = '5';
    (*um)["110"] = '6';
    (*um)["111"] = '7';
}

// Function to return octal
// equivalent of each connected
// component
string Octal(string bin)
{
    int l = bin.size();
    int t = bin.find_first_of('.');

    // length of string before '.'
    int len_left = t != -1 ? t : l;

    // add min 0's in the beginning to make
    // left substring length divisible by 3
    for (int i = 1;
         i <= (3 - len_left % 3) % 3;
         i++)
        bin = '0' + bin;

    // if decimal point exists
    if (t != -1) {
        // length of string after '.'
        int len_right = l - len_left - 1;

        // add min 0's in the end to make right
        // substring length divisible by 3
        for (int i = 1;
             i <= (3 - len_right % 3) % 3;
             i++)
            bin = bin + '0';
    }

    // create map between binary and its
    // equivalent octal code
    unordered_map<string, char> bin_oct_map;
    createMap(&bin_oct_map);

    int i = 0;
    string octal = "";

    while (1) {

        // one by one extract from left,
        // substring of size 3 and
        // add its octal code
        octal += bin_oct_map[bin.substr(i, 3)];
        i += 3;
        if (i == bin.size())
            break;

        // if '.' is encountered
        // add it to result
        if (bin.at(i) == '.') {
            octal += '.';
            i++;
        }
    }

    // required octal number
    return octal;
}

// Function to find the octal equivalents
// of all connected components
void octalValue(
    vector<int> graph[], int vertices,
    vector<int> values)
{
    // Initializing boolean array
    // to mark visited vertices
    vector<bool> visited(1001, false);

    // Following loop invokes DFS algorithm
    for (int i = 1; i <= vertices; i++) {
        if (visited[i] == false) {

            // Variable to hold
            // temporary length
            int sizeChain;

            // Container to store each chain
            vector<int> storeChain;

            // DFS algorithm
            depthFirst(i, graph,
                       visited, storeChain);

            // Variable to hold each chain size
            sizeChain = storeChain.size();

            // Container to store values
            // of vertices of individual chains
            int chainValues[sizeChain + 1];

            // Storing the values of each chain
            for (int i = 0; i < sizeChain; i++) {

                int temp
                    = values[storeChain[i] - 1];
                chainValues[i] = temp;
            }

            // Printing binary chain
            cout << "Chain = ";
            for (int i = 0; i < sizeChain; i++) {
                cout << chainValues[i] << " ";
            }
            cout << "\t";

            // Converting the array with vertex
            // values to a binary string
            // using string stream
            stringstream ss;
            ss << chainValues[0];
            string s = ss.str();

            for (int i = 1; i < sizeChain; i++) {
                stringstream ss1;
                ss1 << chainValues[i];
                string s1 = ss1.str();
                s.append(s1);
            }

            // Printing the octal values
            cout << "Octal equivalent = ";
            cout << Octal(s) << endl;
        }
    }
}

// Driver code to test above function
int main()
{
    // Initializing graph in the
    // form of adjacency list
    vector<int> graph[1001];

    // Defining the number
    // of edges and vertices
    int E, V;
    E = 4;
    V = 7;

    // Assigning the values for each
    // vertex of the undirected graph
    vector<int> values;
    values.push_back(0);
    values.push_back(1);
    values.push_back(0);
    values.push_back(0);
    values.push_back(0);
    values.push_back(1);
    values.push_back(1);

    // Constructing the undirected graph
    graph[1].push_back(2);
    graph[2].push_back(1);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[4].push_back(5);
    graph[5].push_back(4);
    graph[6].push_back(7);
    graph[7].push_back(6);

    octalValue(graph, V, values);
    return 0;
}

```

## 爪哇

```

// Java implementation to find 
// octal equivalents of all 
// connected components 
import java.io.*;
import java.util.*;

class GFG{

// Function to traverse the undirected
// graph using the Depth first traversal
static void depthFirst(int v,
                       List<List<Integer>> graph,
                       boolean[] visited,
                       List<Integer> storeChain)
{

    // Marking the visited
    // vertex as true
    visited[v] = true;

    // Store the connected chain
    storeChain.add(v);

    for(int i : graph.get(v)) 
    {
        if (visited[i] == false)
        {

            // Recursive call to
            // the DFS algorithm
            depthFirst(i, graph, visited,
                       storeChain);
        }
    }
}

// Function to create map between binary
// number and its equivalent hexadecimal
static void createMap(Map<String, Character> um)
{
    um.put("000", '0');
    um.put("001", '1');
    um.put("010", '2');
    um.put("011", '3');
    um.put("100", '4');
    um.put("101", '5');
    um.put("110", '6');
    um.put("111", '7');
}

// Function to return octal
// equivalent of each connected
// component
static String octal(String bin)
{
    int l = bin.length();
    int t = bin.indexOf('.');

    // Length of string before '.'
    int len_left = t != -1 ? t : l;

    // Add min 0's in the beginning to make
    // left substring length divisible by 3
    for(int i = 1; 
            i <= (3 - len_left % 3) % 3; 
            i++)
        bin = '0' + bin;

    // If decimal point exists
    if (t != -1)
    {

        // Length of string after '.'
        int len_right = l - len_left - 1;

        // Add min 0's in the end to make right
        // substring length divisible by 3
        for(int i = 1; 
                i <= (3 - len_right % 3) % 3;
                i++)
            bin = bin + '0';
    }

    // Create map between binary and its
    // equivalent octal code
    Map<String,
        Character> bin_oct_map = new HashMap<String,
                                             Character>();
    createMap(bin_oct_map);

    int i = 0;
    String octal = "";

    while (true)
    {

        // One by one extract from left,
        // substring of size 3 and
        // add its octal code
        octal += bin_oct_map.get(
            bin.substring(i, i + 3));

        i += 3;
        if (i == bin.length())
            break;

        // If '.' is encountered
        // add it to result
        if (bin.charAt(i) == '.')
        {
            octal += '.';
            i++;
        }
    }

    // Required octal number
    return octal;
}

// Function to find the octal equivalents
// of all connected components
static void octalValue(List<List<Integer>> graph,
                       int vertices,
                       List<Integer> values)
{

    // Initializing boolean array
    // to mark visited vertices
    boolean[] visited = new boolean[1001];

    // Following loop invokes DFS algorithm
    for(int i = 1; i <= vertices; i++)
    {
        if (visited[i] == false) 
        {

            // Variable to hold
            // temporary length
            int sizeChain;

            // Container to store each chain
            List<Integer> storeChain = new ArrayList<Integer>();

            // DFS algorithm
            depthFirst(i, graph, visited, storeChain);

            // Variable to hold each chain size
            sizeChain = storeChain.size();

            // Container to store values
            // of vertices of individual chains
            int[] chainValues = new int[sizeChain + 1];

            // Storing the values of each chain
            for(int j = 0; j < sizeChain; j++)
            {
                int temp = values.get(
                    storeChain.get(j) - 1);
                chainValues[j] = temp;
            }

            // Printing binary chain
            System.out.print("Chain = ");

            for(int j = 0; j < sizeChain; j++) 
            {
                System.out.print(chainValues[j] + " ");
            }

            System.out.print("\t");

            // Converting the array with vertex
            // values to a binary string
            String s = "";
            for(int j = 0; j < sizeChain; j++) 
            {
                String s1 = String.valueOf(
                    chainValues[j]);
                s += s1;
            }

            // Printing the octal values
            System.out.println("Octal equivalent = " +
                                octal(s));
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Initializing graph in the
    // form of adjacency list
    @SuppressWarnings("unchecked")
    List<List<Integer>> graph = new ArrayList();

    for(int i = 0; i < 1001; i++)
        graph.add(new ArrayList<Integer>());

    // Defining the number
    // of edges and vertices
    int E = 4, V = 7;

    // Assigning the values for each
    // vertex of the undirected graph
    List<Integer> values = new ArrayList<Integer>();
    values.add(0);
    values.add(1);
    values.add(0);
    values.add(0);
    values.add(0);
    values.add(1);
    values.add(1);

    // Constructing the undirected graph
    graph.get(1).add(2);
    graph.get(2).add(1);
    graph.get(3).add(4);
    graph.get(4).add(3);
    graph.get(4).add(5);
    graph.get(5).add(4);
    graph.get(6).add(7);
    graph.get(7).add(6);

    octalValue(graph, V, values);
}
}

// This code is contributed by jithin

```

**Output:** 

```
Chain = 0 1     Octal equivalent = 1
Chain = 0 0 0     Octal equivalent = 0
Chain = 1 1     Octal equivalent = 3

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。