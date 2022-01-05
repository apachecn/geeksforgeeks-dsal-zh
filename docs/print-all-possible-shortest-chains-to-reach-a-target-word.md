# 打印所有可能的最短链到达目标单词

> 原文:[https://www . geeksforgeeks . org/print-所有可能的最短链到达目标单词/](https://www.geeksforgeeks.org/print-all-possible-shortest-chains-to-reach-a-target-word/)

给定两个字符串 **start** 和 **target** (两者长度相同)和一个字符串列表**str【】**，任务是打印从 **start** 到 **target** 的所有可能的最小序列(如果存在)，使得序列中的相邻单词仅相差一个字符，并且序列中的每个单词都出现在给定的列表中。

**注意:**可以假设列表中存在**目标**字，所有字的长度都相同。如果出现多个序列，打印所有序列。

**示例:**

> **输入:** str[] = {poon，plee，same，plee，Input，辩白，plie，poin}，start =“toon”，target =“辩白”
> **输出:** [[toon，poon，poin，apoi，plee，辩白]]
> **解释:**香椿→poon→poin→poi→plee→辩白
> 
> **输入:** str[] = { ted，tex，red，tax，tad，den，rex，pee}，start =“red”，target =“tax”
> **输出**[“red”，“ted”，“tad”，“tax”]，[“red”，“ted”，“tex”，“tax”]，[“red”，“rex”，“tex”，“tax”]

**方法:**使用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 可以解决问题。这里棘手的部分是做 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 的路径，而不是文字。按照以下步骤解决问题:

1.  初始化一个变量，比如 **res** ，来存储所有可能的最短路径。
2.  创建一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储当前路径中所有访问过的单词，一旦当前路径完成，擦除所有访问过的单词。
3.  对于每个当前单词，通过将每个字符从“a”更改为“z”来查找**str【】**中可能出现的下一个单词，并查找所有可能的路径。
4.  最后，打印所有可能的路径。

## C++

```
// C++ Program to implement
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

## 蟒蛇 3

```
# Python Program to implement
# the above approach
from collections import deque
from typing import Deque, List, Set

# Function to print all possible shortest
# sequences starting from start to target.
def displaypath(res: List[List[str]]):
    for i in res:
        print("[ ", end="")
        for j in i:
            print(j, end=", ")
        print("]")

# Find words differing by a single
# character with word
def addWord(word: str, Dict: Set):
    res: List[str] = []
    wrd = list(word)

    # Find next word in dict by changing
    # each element from 'a' to 'z'
    for i in range(len(wrd)):
        s = wrd[i]
        c = 'a'
        while c <= 'z':
            wrd[i] = c
            if ''.join(wrd) in Dict:
                res.append(''.join(wrd))
            c = chr(ord(c) + 1)
        wrd[i] = s
    return res

# Function to get all the shortest possible
# sequences starting from 'start' to 'target'
def findLadders(Dictt: List[str], beginWord: str, endWord: str):

    # Store all the shortest path.
    res: List[List[str]] = []

    # Store visited words in list
    visit = set()

    # Queue used to find the shortest path
    q: Deque[List[str]] = deque()

    # Stores the distinct words from given list
    Dict = set()
    for i in Dictt:
        Dict.add(i)
    q.append([beginWord])

    # Stores whether the shortest
    # path is found or not
    flag = False
    while q:
        size = len(q)
        for i in range(size):

            # Explore the next level
            cur = q[0]
            q.popleft()
            newadd = []

            # Find words differing by a
            # single character
            newadd = addWord(cur[-1], Dict)

            # Add words to the path.
            for j in range(len(newadd)):
                newline = cur.copy()
                newline.append(newadd[j])

                # Found the target
                if (newadd[j] == endWord):
                    flag = True
                    res.append(newline)

                visit.add(newadd[j])
                q.append(newline)

        # If already reached target
        if (flag):
            break

        # Erase all visited words.
        for it in visit:
            Dict.remove(it)
        visit.clear()
    return res

# Driver Code
if __name__ == "__main__":

    string = ["ted", "tex", "red", "tax", "tad", "den", "rex", "pee"]
    beginWord = "red"
    endWord = "tax"

    res = findLadders(string, beginWord, endWord)

    displaypath(res)

# This code is contributed by sanjeev2552
```

**Output:** 

```
[ red, ted, tad, tax,  ]
[ red, ted, tex, tax,  ]
[ red, rex, tex, tax,  ]
```

***时间复杂度:** O(N *M)，其中 **M** 为给定列表中的字符串个数， **N** 为每个字符串的长度。*

***辅助空间:** O(M*N)*