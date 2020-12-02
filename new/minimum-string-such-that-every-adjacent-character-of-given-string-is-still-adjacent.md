# 最小字符串，以使给定字符串的每个相邻字符仍相邻

> 原文： [https://www.geeksforgeeks.org/minimum-string-such-that-every-adjacent-character-of-given-string-is-still-adjacent/](https://www.geeksforgeeks.org/minimum-string-such-that-every-adjacent-character-of-given-string-is-still-adjacent/)

给定字符串 **S** ，任务是找到最小长度的字符串，以使字符串的每个相邻字符在最小长度的字符串中保持相邻。

**示例：**

> **输入：** S =“ acabpba”
> **输出：** pbac
> **说明：**
> 可以将给定的字符串转换为
> 中的每个相邻字符都保持相邻。
> 
> **输入：** S =“ abcdea”
> **输出：**不可能
> **说明：**
> 找不到这样的字符串。

**方法：**想法是准备一个[图](https://www.geeksforgeeks.org/graph-and-its-representations/)类似的结构，其中图的每个相邻节点表示字符串的相邻字符。 在两种情况下，无法使用这种类型的字符串–

*   一个字符包含三个或更多相邻字符。
*   如果两个字符不只有一个相邻字符，则长度为 1 的字符串除外。

如果满足上述条件的字符串为真，则只需[用](https://www.geeksforgeeks.org/algorithms-gq/graph-traversals-gq/)[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历图，则遍历的路径将是最小长度的字符串。 DFS 的源顶点将是只有一个相邻字符的任何一个字符。

下面是上述方法的实现：

## C ++

```

// C++ implementation to find the 
// minimum length string such that 
// adjacent characters of the string 
// remains adjacent in the string 

#include <bits/stdc++.h> 
using namespace std; 

class graph { 
    int arr[26][2]; 
    vector<int> alpha; 
    vector<int> answer; 

public: 
    // Constructor for the graph 
    graph() 
    { 
        // Initialize the matrix by -1 
        for (int i = 0; i < 26; i++) { 
            for (int j = 0; j < 2; j++) 
                arr[i][j] = -1; 
        } 

        // Initialize the alphabet array 
        alpha = vector<int>(26); 
    } 

    // Function to do Depth first 
    // search Traversal 
    void dfs(int v) 
    { 
        // Pushing current character 
        answer.push_back(v); 

        alpha[v] = 1; 

        for (int i = 0; i < 2; i++) { 
            if (alpha[arr[v][i]] == 1 
                || arr[v][i] == -1) 
                continue; 

            dfs(arr[v][i]); 
        } 
    } 

    // Function to find the minimum 
    // length string 
    void minString(string str) 
    { 
        // Condition if given string 
        // length is 1 
        if (str.length() == 1) { 
            cout << str << "\n"; 
            return; 
        } 

        bool flag = true; 

        // Loop to find the adjacency 
        // list of the given string 
        for (int i = 0; i < str.length() - 1; 
             i++) { 
            int j = str[i] - 'a'; 
            int k = str[i + 1] - 'a'; 

            // Condition if character 
            // already present 
            if (arr[j][0] == k 
                || arr[j][1] == k) { 
            } 
            else if (arr[j][0] == -1) 
                arr[j][0] = k; 
            else if (arr[j][1] == -1) 
                arr[j][1] = k; 

            // Condition if a character 
            // have more than two different 
            // adjacent characters 
            else { 
                flag = false; 
                break; 
            } 

            if (arr[k][0] == j 
                || arr[k][1] == j) { 
            } 
            else if (arr[k][0] == -1) 
                arr[k][0] = j; 
            else if (arr[k][1] == -1) 
                arr[k][1] = j; 

            // Condition if a character 
            // have more than two different 
            // adjacent characters 
            else { 
                flag = false; 
                break; 
            } 
        } 

        // Variable to check string contain 
        // two end characters or not 
        bool contain_ends = false; 

        int count = 0; 
        int index; 

        for (int i = 0; i < 26; i++) { 

            // Condition if a character has 
            // only one type of adjacent 
            // character 
            if ((arr[i][0] == -1 
                 && arr[i][1] != -1) 
                || (arr[i][1] == -1 
                    && arr[i][0] != -1)) { 
                count++; 
                index = i; 
            } 

            // Condition if the given string 
            // has exactly two characters 
            // having only one type of adjacent 
            // character 
            if (count == 2) 
                contain_ends = true; 

            if (count == 3) 
                contain_ends = false; 
        } 

        if (contain_ends == false
            || flag == false) { 
            cout << "Impossible"
                 << "\n"; 
            return; 
        } 

        // Depth first Search Traversal 
        // on one of the possible end 
        // character of the string 
        dfs(index); 

        // Loop to print the answer 
        for (int i = 0; i < answer.size(); 
             i++) { 
            char ch = answer[i] + 'a'; 
            cout << ch; 
        } 
    } 
}; 

// Driver Code 
int main() 
{ 
    string s = "abcdea"; 

    graph g; 
    g.minString(s); 

    return 0; 
} 

```

**Output:**

```
pbac

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。