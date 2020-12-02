# 在联系人列表中查找相同的联系人

> 原文： [https://www.geeksforgeeks.org/find-same-contacts-in-a-list-of-contacts/](https://www.geeksforgeeks.org/find-same-contacts-in-a-list-of-contacts/)

给定一个包含用户名，电子邮件和电话号码的联系人列表（顺序不限）。 识别相同的联系人（即，同一个人有多个联系人），并将相同的联系人一起输出。

注意：
1）联系人可以以任何顺序存储其三个字段，即电话号码可以出现在用户名之前，或者用户名可以出现在电话号码之前。
2）如果两个联系人具有相同的用户名或电子邮件或电话号码，则它们是相同的。

**示例**：

```
Input: contact[] = 
     { {"Gaurav", "gaurav@gmail.com", "gaurav@gfgQA.com"},
       { "Lucky", "lucky@gmail.com", "+1234567"},
       { "gaurav123", "+5412312", "gaurav123@skype.com"}.
       { "gaurav1993", "+5412312", "gaurav@gfgQA.com"}
     }
Output:
   0 2 3
   1 
contact[2] is same as contact[3] because they both have same
contact number.
contact[0] is same as contact[3] because they both have same
e-mail address.
Therefore, contact[0] and contact[2] are also same.

```

**我们强烈建议您最小化浏览器，然后自己尝试。**
输入基本上是一个结构数组。 一个结构包含三个字段，以便任何字段都可以表示有关联系人的任何详细信息。
这个想法是首先使用给定的数组创建联系人图。 在图中，如果两个顶点都具有相同的用户名，相同的电子邮件或相同的电话号码，则它们在顶点 i 与顶点 j 之间会有一条边。 一旦构建了图，任务就减少到在无向图中找到[连接的组件。 我们可以通过从每个未访问的顶点开始执行](http://geeksquiz.com/connected-components-in-an-undirected-graph/) [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 或 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 来找到连接的组件。 在下面的代码中，使用了 DFS。
以下是此想法的实现。

## C++

```cpp

// A C++ program to find same contacts in a list of contacts
#include<bits/stdc++.h>
using namespace std;

// Structure for storing contact details.
struct contact
{
    string field1, field2, field3;
};

// A utility function to fill entries in adjacency matrix
// representation of graph
void buildGraph(contact arr[], int n, int *mat[])
{
    // Initialize the adjacency matrix
    for (int i=0; i<n; i++)
       for (int j=0; j<n; j++)
           mat[i][j] = 0;

    // Traverse through all contacts
    for (int i = 0; i < n; i++) {

        // Add mat from i to j and vice versa, if possible.
        // Since length of each contact field is at max some
        // constant. (say 30) so body execution of this for
        // loop takes constant time.
        for (int j = i+1; j < n; j++)
            if (arr[i].field1 == arr[j].field1 ||
                arr[i].field1 == arr[j].field2 ||
                arr[i].field1 == arr[j].field3 ||
                arr[i].field2 == arr[j].field1 ||
                arr[i].field2 == arr[j].field2 ||
                arr[i].field2 == arr[j].field3 ||
                arr[i].field3 == arr[j].field1 ||
                arr[i].field3 == arr[j].field2 ||
                arr[i].field3 == arr[j].field3)
            {
                mat[i][j] = 1;
                mat[j][i] = 1;
                break;
            }
    }
}

// A recuesive function to perform DFS with vertex i as source
void DFSvisit(int i, int *mat[], bool visited[], vector<int>& sol, int n)
{
    visited[i] = true;
    sol.push_back(i);

    for (int j = 0; j < n; j++)
        if (mat[i][j] && !visited[j])
            DFSvisit(j, mat, visited, sol, n);
}

// Finds similar contacrs in an array of contacts
void findSameContacts(contact arr[], int n)
{
    // vector for storing the solution
    vector<int> sol;

    // Declare 2D adjaceny matrix for mats
    int **mat = new int*[n];

    for (int i = 0; i < n; i++)
        mat[i] = new int[n];

    // visited array to keep track of visited nodes
    bool visited[n];
    memset(visited, 0, sizeof(visited));

    // Fill adjacency matrix
    buildGraph(arr, n, mat);

    // Since, we made a graph with contacts as nodes with fields as links.
    // two nodes are linked if they represent the same person.
    // so, total number of connected components and nodes in each component
    // will be our answer.
    for (int i = 0; i < n; i++)
    {
        if (!visited[i])
        {
            DFSvisit(i, mat, visited, sol, n);

            // Add delimeter to separate nodes of one component from other.
            sol.push_back(-1);
        }
    }

    // Print the solution
    for (int i = 0; i < sol.size(); i++)
        if (sol[i] == -1) cout << endl;
        else cout << sol[i] << " ";
}

// Drive Code
int main()
{
    contact arr[] = {{"Gaurav", "gaurav@gmail.com", "gaurav@gfgQA.com"},
                     {"Lucky", "lucky@gmail.com", "+1234567"},
                     {"gaurav123", "+5412312", "gaurav123@skype.com"},
                     {"gaurav1993", "+5412312", "gaurav@gfgQA.com"},
                     {"raja", "+2231210", "raja@gfg.com"},
                     {"bahubali", "+878312", "raja"}
                    };

    int n = sizeof arr / sizeof arr[0];
    findSameContacts(arr, n);
    return 0;
}

```

## Python

```py

# A Python3 program to find same contacts
# in a list of contacts 

# Structure for storing contact details. 
class contact:
    def __init__(self, field1, 
                       field2, field3):
        self.field1 = field1
        self.field2 = field2
        self.field3 = field3

# A utility function to fill entries in 
# adjacency matrix representation of graph 
def buildGraph(arr, n, mat):

    # Initialize the adjacency matrix
    for i in range(n):
        for j in range(n):
            mat[i][j] = 0

    # Traverse through all contacts 
    for i in range(n):

        # Add mat from i to j and vice versa, 
        # if possible. Since length of each 
        # contact field is at max some constant.
        # (say 30) so body execution of this for 
        # loop takes constant time.
        for j in range(i + 1, n):
            if (arr[i].field1 == arr[j].field1 or
                arr[i].field1 == arr[j].field2 or
                arr[i].field1 == arr[j].field3 or
                arr[i].field2 == arr[j].field1 or
                arr[i].field2 == arr[j].field2 or
                arr[i].field2 == arr[j].field3 or
                arr[i].field3 == arr[j].field1 or
                arr[i].field3 == arr[j].field2 or
                arr[i].field3 == arr[j].field3):
                mat[i][j] = 1
                mat[j][i] = 1
                break

# A recuesive function to perform DFS 
# with vertex i as source 
def DFSvisit(i, mat, visited, sol, n):
    visited[i] = True
    sol.append(i) 

    for j in range(n):
        if (mat[i][j] and not visited[j]):
            DFSvisit(j, mat, visited, sol, n)

# Finds similar contacrs in an
# array of contacts 
def findSameContacts(arr, n):

    # vector for storing the solution 
    sol = []

    # Declare 2D adjaceny matrix for mats 
    mat = [[None] * n for i in range(n)] 

    # visited array to keep track
    # of visited nodes 
    visited = [0] * n

    # Fill adjacency matrix 
    buildGraph(arr, n, mat) 

    # Since, we made a graph with contacts  
    # as nodes with fields as links. Two 
    # nodes are linked if they represent
    # the same person. So, total number of 
    # connected components and nodes in each
    # component will be our answer.
    for i in range(n):
        if (not visited[i]):
            DFSvisit(i, mat, visited, sol, n) 

            # Add delimeter to separate nodes
            # of one component from other. 
            sol.append(-1)

    # Print the solution
    for i in range(len(sol)):
        if (sol[i] == -1):
            print()
        else:
            print(sol[i], end = " ")

# Driver Code 
if __name__ == '__main__': 
    arr = [contact("Gaurav", "gaurav@gmail.com", "gaurav@gfgQA.com"), 
           contact("Lucky", "lucky@gmail.com", "+1234567"), 
           contact("gaurav123", "+5412312", "gaurav123@skype.com"), 
           contact("gaurav1993", "+5412312", "gaurav@gfgQA.com"), 
           contact("raja", "+2231210", "raja@gfg.com"),
           contact("bahubali", "+878312", "raja")]

    n = len(arr) 
    findSameContacts(arr, n)

# This code is contributed by PranchalK

```

**输出**：

```
0 3 2
1
4 5

```

**时间复杂度**：O（n <sup>2</sup> ）其中，n 是触点数。
感谢 [Gaurav Ahirwar](http://qa.geeksforgeeks.org/user/Mr.Lazy) 提供了上述解决方案。

**另一种方法：（使用联合查找）**

该问题也可以通过 [Union Find](https://www.geeksforgeeks.org/union-find/) 解决。 在这里，我们统一了至少有一个共同联系人的所有人员。 我们需要隔离所有具有共同联系的索引。 为此，我们可以维护每个联系人的索引图数组，并统一对应于它们的所有索引。 联合查找后，我们得到了不相交的集合，它们是不同的人。

## CPP14

```

// CPP14 program to find common contacts.
#include <bits/stdc++.h>
using namespace std;

// The class DSU will implement the Union Find
class DSU {

    vector<int> parent, size;

public:
    // In the constructor, we assign the each index as its
    // own parent and size as the number of contacts
    // available for that index

    DSU(vector<vector<string> >& contacts)
    {
        for (int i = 0; i < contacts.size(); i++) {

            parent.push_back(i);

            size.push_back(contacts[i].size());
        }
    }

    // Finds the set in which the element belongs. Path
    // compression is used to optimise time complexity
    int findSet(int v)
    {

        if (v == parent[v])
            return v;

        return parent[v] = findSet(parent[v]);
    }

    // Unifies the sets a and b where, the element belonging
    // to the smaller set is merged to the one belonging to
    // the smaller set
    void unionSet(int a, int b, vector<string>& person1,
                  vector<string>& person2)
    {

        if (size[a] > size[b]) {
            parent[b] = a;
            size[a] += size[b];
            for (auto contact : person2)
                person1.push_back(contact);
        }
        else {

            parent[a] = b;
            size[b] += size[a];
            for (auto contact : person1)
                person2.push_back(contact);
        }
    }
};

// Driver Code
int main()
{
    vector<vector<string> > contacts = {
        { "Gaurav", "gaurav@gmail.com",
          "gaurav@gfgQA.com" },
        { "Lucky", "lucky@gmail.com", "+1234567" },
        { "gaurav123", "+5412312", "gaurav123@skype.com" },
        { "gaurav1993", "+5412312", "gaurav@gfgQA.com" },
        { "raja", "+2231210", "raja@gfg.com" },
        { "bahubali", "+878312", "raja" }
    };

    // Initializing the object of DSU class
    DSU dsu(contacts);

    // Will contain the mapping of a contact to all the
    // indices it is present within
    unordered_map<string, vector<int> > contactToIndex;

    for (int index = 0; index < contacts.size(); index++) {

        for (auto contact : contacts[index])
            contactToIndex[contact].push_back(index);
    }

    // Unifies the sets of each contact if they are not
    // present in the same set
    for (auto contact : contactToIndex) {

        vector<int> indices = contact.second;

        for (int i = 0; i < indices.size() - 1; i++) {

            int set1 = dsu.findSet(indices[i]),
                set2 = dsu.findSet(indices[i + 1]);

            if (set1 != set2)
                dsu.unionSet(set1, set2, contacts[set1],
                             contacts[set2]);
        }
    }

    // Contains a map of all the distinct sets available
    // after union find has been completed
    unordered_map<int, vector<int> > unifiedSet;

    // All parents are mapped to the elemets in the set
    for (int i = 0; i < contacts.size(); i++) {

        unifiedSet[dsu.findSet(i)].push_back(i);
    }

    // Printing out elements from distict sets
    for (auto eachSet : unifiedSet) {

        for (auto element : eachSet.second)
            cout << element << " ";

        cout << endl;
    }

    return 0;
}

```

输出：

```
4 5 
0 2 3 
1 

```

**时间复杂度**：O（N *α（N）），其中 N 是接触数，α是[阿克曼逆函数](https://en.wikipedia.org/wiki/Ackermann_function)
**空间复杂度**：上）

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

