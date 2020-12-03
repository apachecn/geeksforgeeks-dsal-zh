# 打印所有可能的最短链以达到目标词

> 原文： [https://www.geeksforgeeks.org/print-all-possible-shortest-chains-to-reach-a-target-word/](https://www.geeksforgeeks.org/print-all-possible-shortest-chains-to-reach-a-target-word/)

给定两个字符串**开头**和**目标**（长度相同）和字符串 **str []** 列表，任务是打印所有可能的最小序列开头 从**开始从**到**目标**，如果序列中的相邻单词仅相差一个字符，并且序列中的每个单词都出现在给定列表中。

**注意**：可以假设**目标**单词出现在列表中，并且所有单词的长度相同。 如果出现多个序列，请打印所有序列。

**示例**：

> **输入**：str [] = {poon，plee，same，poie，plea，plie，poin}，开始=“卡通”，目标=“ plea”
> **输出**：[[香椿，香椿，poin，poie，pee，恳求]]
> **解释**：香椿→香椿→poin→poie→poie→plee→plea
> 
> **输入**：str [] = {ted，tex，red，tax，tad，den，rex，pee}，start =“ red”，target =“ tax”
> **输出** [[“ red”，“ ted”，“ tad”，“ tax”]，[“ red”，“ ted”，“ tex”，“ tax”]，[“ red”，“ rex”，“ tex” ，“税”]]

**方法**：可以使用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 解决问题。这里的棘手部分是执行路径的 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 而不是单词。 请按照以下步骤解决问题：

1.  初始化变量，例如 **res** ，以存储所有可能的最短路径。

2.  创建一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)将所有访问过的单词存储在当前路径中，当当前路径完成后，擦除所有访问过的单词。

3.  对于每个当前单词，通过将每个字符从“ a”更改为“ z”，找到 **str []** 中可能存在的下一个单词，并找到所有可能的路径。

4.  最后，打印所有可能的路径。

## C++

```cpp

// C++ Program to implememnt 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print all possible shortest 
// sequences starting from start to target. 
void displaypath(vector<vector<string> >& res) 
{ 
    for (int i = 0; i < res.size(); i++) { 
        cout << "[ "; 
        for (int j = 0; j < res[0].size(); j++) { 
            cout << res[i][j] << ", "; 
        } 
        cout << " ]\n"; 
    } 
} 
// Find words differing by a single 
// character with word 
vector<string> addWord( 
    string word, 
    unordered_set<string>& dict) 
{ 
    vector<string> res; 

    // Find next word in dict by changing 
    // each element from 'a' to 'z' 
    for (int i = 0; i < word.size(); i++) { 
        char s = word[i]; 
        for (char c = 'a'; c <= 'z'; c++) { 
            word[i] = c; 
            if (dict.count(word)) 
                res.push_back(word); 
        } 
        word[i] = s; 
    } 
    return res; 
} 

// Function to get all the shortest possible 
// sequences starting from 'start' to 'target' 
vector<vector<string> > findLadders( 
    vector<string>& Dict, 
    string beginWord, 
    string endWord) 
{ 
    // Store all the shortest path. 
    vector<vector<string> > res; 

    // Store visited words in list 
    unordered_set<string> visit; 

    // Queue used to find the shortest path 
    queue<vector<string> > q; 

    // Stores the distinct words from given list 
    unordered_set<string> dict(Dict.begin(), 
                               Dict.end()); 
    q.push({ beginWord }); 

    // Stores whether the shortest 
    // path is found or not 
    bool flag = false; 

    while (!q.empty()) { 
        int size = q.size(); 
        for (int i = 0; i < size; i++) { 

            // Explore the next level 
            vector<string> cur = q.front(); 
            q.pop(); 
            vector<string> newadd; 

            // Find words differing by a 
            // single character 
            newadd = addWord(cur.back(), dict); 

            // Add words to the path. 
            for (int j = 0; j < newadd.size(); j++) { 
                vector<string> newline(cur.begin(), 
                                       cur.end()); 

                newline.push_back(newadd[j]); 

                // Found the target 
                if (newadd[j] == endWord) { 
                    flag = true; 
                    res.push_back(newline); 
                } 

                visit.insert(newadd[j]); 
                q.push(newline); 
            } 
        } 

        // If already reached target 
        if (flag) { 
            break; 
        } 

        // Erase all visited words. 
        for (auto it : visit) { 
            dict.erase(it); 
        } 

        visit.clear(); 
    } 
    return res; 
} 

// Driver Code 
int main() 
{ 
    vector<string> str{ "ted", "tex", "red", 
                        "tax", "tad", "den", 
                        "rex", "pee" }; 
    string beginWord = "red"; 
    string endWord = "tax"; 

    vector<vector<string> > res 
        = findLadders(str, beginWord, endWord); 

    displaypath(res); 
} 

```

**Output:**

```
[ red, ted, tad, tax,  ]
[ red, ted, tex, tax,  ]
[ red, rex, tex, tax,  ]

```

***时间复杂度**：O（N²* M），其中`M`是给定列表中的字符串数，`N`是每个字符串的长度 。*

***辅助空间**：* O（M * N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。