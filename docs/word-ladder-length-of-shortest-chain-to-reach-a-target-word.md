# 阶梯（到达目标单词的最短链长）

> 原文： [https://www.geeksforgeeks.org/word-ladder-length-of-shortest-chain-to-reach-a-target-word/](https://www.geeksforgeeks.org/word-ladder-length-of-shortest-chain-to-reach-a-target-word/)

给定一本字典，以及两个单词“开始”和“目标”（长度相同）。 查找从“开始”到“目标”的最小链的长度（如果存在），以使链中的相邻单词仅相差一个字符，并且链中的每个单词都是有效单词，即它存在于字典中。 可以假设词典中存在“目标”单词，并且所有词典单词的长度都相同。

**例如**：

```
Input: Dictionary = {POON, PLEE, SAME, POIE, PLEA, PLIE, POIN}
       start = TOON
       target = PLEA
Output: 7
TOON - POON - POIN - POIE - PLIE - PLEE - PLEA

Input: Dictionary = {ABCD, EBAD, EBCD, XYZA}
       Start = ABCV
       End = EBAD
Output: 4
ABCV - ABCD - EBCD - EBAD

```

**<u>解决方案：</u>** 这个想法是使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。

**方法**：

1.  从给定的起始词开始。

2.  将单词推入队列

3.  运行循环，直到队列为空

4.  遍历所有与其相邻（相差一个字符）的单词，并将该单词推入队列（对于 BFS）

5.  继续这样做，直到找到目标单词或遍历所有单词为止。

以下是上述想法的实现。

## C++

```cpp

// C++ program to find length  
// of the shortest chain 
// transformation from source 
// to target 
#include <bits/stdc++.h> 
using namespace std; 

// Returns length of shortest chain  
// to reach 'target' from 'start' 
// using minimum number of adjacent  
// moves.  D is dictionary 
int shortestChainLen( 
string start, string target,  
set<string>& D) 
{ 

    // If the target string is not 
    // present in the dictionary 
    if (D.find(target) == D.end()) 
        return 0; 

    // To store the current chain length 
    // and the length of the words 
    int level = 0, wordlength = start.size(); 

    // Push the starting word into the queue 
    queue<string> Q; 
    Q.push(start); 

    // While the queue is non-empty 
    while (!Q.empty()) { 

        // Increment the chain length 
        ++level; 

        // Current size of the queue 
        int sizeofQ = Q.size(); 

        // Since the queue is being updated while 
        // it is being traversed so only the 
        // elements which were already present 
        // in the queue before the start of this 
        // loop will be traversed for now 
        for (int i = 0; i < sizeofQ; ++i) { 

            // Remove the first word from the queue 
            string word = Q.front(); 
            Q.pop(); 

            // For every character of the word 
            for (int pos = 0; pos < wordlength; ++pos) { 

                // Retain the original character 
                // at the current position 
                char orig_char = word[pos]; 

                // Replace the current character with 
                // every possible lowercase alphabet 
                for (char c = 'a'; c <= 'z'; ++c) { 
                    word[pos] = c; 

                    // If the new word is equal 
                    // to the target word 
                    if (word == target) 
                        return level + 1; 

                    // Remove the word from the set 
                    // if it is found in it 
                    if (D.find(word) == D.end()) 
                        continue; 
                    D.erase(word); 

                    // And push the newly generated word 
                    // which will be a part of the chain 
                    Q.push(word); 
                } 

                // Restore the original character 
                // at the current position 
                word[pos] = orig_char; 
            } 
        } 
    } 

    return 0; 
} 

// Driver program 
int main() 
{ 
    // make dictionary 
    set<string> D; 
    D.insert("poon"); 
    D.insert("plee"); 
    D.insert("same"); 
    D.insert("poie"); 
    D.insert("plie"); 
    D.insert("poin"); 
    D.insert("plea"); 
    string start = "toon"; 
    string target = "plea"; 
    cout << "Length of shortest chain is: "
         << shortestChainLen(start, target, D); 
    return 0; 
} 

```

## Java

```java

// Java program to find length 
// of the shortest chain 
// transformation from source 
// to target 
import java.util.*; 

class GFG 
{ 

// Returns length of shortest chain  
// to reach 'target' from 'start' 
// using minimum number of adjacent moves. 
// D is dictionary 
static int shortestChainLen(String start,  
                            String target,  
                            Set<String> D) 
{ 

    // If the target String is not 
    // present in the dictionary 
    if (!D.contains(target)) 
        return 0; 

    // To store the current chain length 
    // and the length of the words 
    int level = 0, wordlength = start.length(); 

    // Push the starting word into the queue 
    Queue<String> Q = new LinkedList<>(); 
    Q.add(start); 

    // While the queue is non-empty 
    while (!Q.isEmpty()) 
    { 

        // Increment the chain length 
        ++level; 

        // Current size of the queue 
        int sizeofQ = Q.size(); 

        // Since the queue is being updated while 
        // it is being traversed so only the 
        // elements which were already present 
        // in the queue before the start of this 
        // loop will be traversed for now 
        for (int i = 0; i < sizeofQ; ++i)  
        { 

            // Remove the first word from the queue 
            char []word = Q.peek().toCharArray(); 
            Q.remove(); 

            // For every character of the word 
            for (int pos = 0; pos < wordlength; ++pos) 
            { 

                // Retain the original character 
                // at the current position 
                char orig_char = word[pos]; 

                // Replace the current character with 
                // every possible lowercase alphabet 
                for (char c = 'a'; c <= 'z'; ++c) 
                { 
                    word[pos] = c; 

                    // If the new word is equal 
                    // to the target word 
                    if (String.valueOf(word).equals(target)) 
                        return level + 1; 

                    // Remove the word from the set 
                    // if it is found in it 
                    if (!D.contains(String.valueOf(word))) 
                        continue; 
                    D.remove(String.valueOf(word)); 

                    // And push the newly generated word 
                    // which will be a part of the chain 
                    Q.add(String.valueOf(word)); 
                } 

                // Restore the original character 
                // at the current position 
                word[pos] = orig_char; 
            } 
        } 
    } 

    return 0; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // make dictionary 
    Set<String> D = new HashSet<String>(); 
    D.add("poon"); 
    D.add("plee"); 
    D.add("same"); 
    D.add("poie"); 
    D.add("plie"); 
    D.add("poin"); 
    D.add("plea"); 
    String start = "toon"; 
    String target = "plea"; 
    System.out.print("Length of shortest chain is: "
        + shortestChainLen(start, target, D)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# program to find length of the shortest chain 
// transformation from source to target 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// Returns length of shortest chain  
// to reach 'target' from 'start' 
// using minimum number of adjacent moves. 
// D is dictionary 
static int shortestChainLen(String start,  
                            String target,  
                            HashSet<String> D) 
{ 

    // If the target String is not 
    // present in the dictionary 
    if (!D.Contains(target)) 
        return 0; 

    // To store the current chain length 
    // and the length of the words 
    int level = 0, wordlength = start.Length; 

    // Push the starting word into the queue 
    List<String> Q = new List<String>(); 
    Q.Add(start); 

    // While the queue is non-empty 
    while (Q.Count != 0) 
    { 

        // Increment the chain length 
        ++level; 

        // Current size of the queue 
        int sizeofQ = Q.Count; 

        // Since the queue is being updated while 
        // it is being traversed so only the 
        // elements which were already present 
        // in the queue before the start of this 
        // loop will be traversed for now 
        for (int i = 0; i < sizeofQ; ++i)  
        { 

            // Remove the first word from the queue 
            char []word = Q[0].ToCharArray(); 
            Q.RemoveAt(0); 

            // For every character of the word 
            for (int pos = 0; pos < wordlength; ++pos) 
            { 

                // Retain the original character 
                // at the current position 
                char orig_char = word[pos]; 

                // Replace the current character with 
                // every possible lowercase alphabet 
                for (char c = 'a'; c <= 'z'; ++c) 
                { 
                    word[pos] = c; 

                    // If the new word is equal 
                    // to the target word 
                    if (String.Join("", word).Equals(target)) 
                        return level + 1; 

                    // Remove the word from the set 
                    // if it is found in it 
                    if (!D.Contains(String.Join("", word))) 
                        continue; 
                    D.Remove(String.Join("", word)); 

                    // And push the newly generated word 
                    // which will be a part of the chain 
                    Q.Add(String.Join("", word)); 
                } 

                // Restore the original character 
                // at the current position 
                word[pos] = orig_char; 
            } 
        } 
    } 
    return 0; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // make dictionary 
    HashSet<String> D = new HashSet<String>(); 
    D.Add("poon"); 
    D.Add("plee"); 
    D.Add("same"); 
    D.Add("poie"); 
    D.Add("plie"); 
    D.Add("poin"); 
    D.Add("plea"); 
    String start = "toon"; 
    String target = "plea"; 
    Console.Write("Length of shortest chain is: "
        + shortestChainLen(start, target, D)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

输出：

```
Length of shortest chain is: 7

```

**复杂度分析**：

*   **时间复杂度**：O（n²m），其中 m 是字典中最初的条目数，n 是字符串的大小。

*   **辅助空间**：O（m * n），其中 m 是存储在队列中的字符串。

    因此，空间复杂度为 O（m * n）。

**替代实现：（维护中间词和原始词的映射）**：

下面是上述方法的替代实现。

在这里，通过这种方法，我们找到了起始词和给定词典列表中所有词的所有中间词，并维护了中间词的映射和原始词的向量（映射<string vector="">>）。 例如，对于单词“ POON”，中间单词是“ * OON”，“ P * ON”，“ PO * N”，“ POO *”。 然后，我们从起始单词开始执行 BFS 遍历，并将一对起始单词和距离（pair（word，distance））推入队列，直到到达目标单词。 那么，距离就是我们的答案。</string>

## C++

```cpp

// C++ program to find length  
// of the shortest chain 
// transformation from source 
// to target 
#include <bits/stdc++.h> 
using namespace std; 

// Returns length of shortest chain  
// to reach 'target' from 'start' 
// using minimum number of adjacent  
// moves.  D is dictionary 
int shortestChainLen( 
string start, string target,  
set<string>& D) 
{ 

  // Map of intermediate words and  
  // the list of original words 
  map<string, vector<string>> umap; 

  // Find all the intermediate  
  // words for the start word 
  for(int i = 0; i < start.size(); i++) 
  { 
    string str = start.substr(0,i) + "*" +  
                        start.substr(i+1); 
    umap[str].push_back(start); 
  } 

  // Find all the intermediate words for  
  // the words in the given Set 
  for(auto it = D.begin(); it != D.end(); it++) 
  { 
    string word = *it; 
    for(int j = 0; j < word.size(); j++) 
    { 
      string str = word.substr(0,j) + "*" +  
                          word.substr(j+1); 
      umap[str].push_back(word); 
    } 
  } 

  // Perform BFS and push (word, distance) 
  queue<pair<string, int>> q; 

  map<string, int> visited; 

  q.push(make_pair(start,1)); 
  visited[start] = 1; 

  // Traverse until queue is empty 
  while(!q.empty()) 
  { 
    pair<string, int> p = q.front(); 
    q.pop(); 

    string word = p.first; 
    int dist = p.second; 

    // If target word is found 
    if(word == target) 
    { 
      return dist; 
    } 

    // Finding intermediate words for  
    // the word in front of queue 
    for(int i = 0; i < word.size(); i++) 
    { 
      string str = word.substr(0,i) + "*" +  
                           word.substr(i+1); 

      vector<string> vect = umap[str]; 
      for(int j = 0; j < vect.size(); j++) 
      { 
        // If the word is not visited 
        if(visited[vect[j]] == 0) 
        { 
          visited[vect[j]] = 1; 
          q.push(make_pair(vect[j], dist + 1)); 
        } 
      } 
    } 

  } 

    return 0; 
} 

// Driver program 
int main() 
{ 
    // make dictionary 
    set<string> D; 
    D.insert("poon"); 
    D.insert("plee"); 
    D.insert("same"); 
    D.insert("poie"); 
    D.insert("plie"); 
    D.insert("poin"); 
    D.insert("plea"); 
    string start = "toon"; 
    string target = "plea"; 
    cout << "Length of shortest chain is: "
         << shortestChainLen(start, target, D); 
    return 0; 
} 

```

输出：

```
Length of shortest chain is: 7

```

感谢 Gaurav Ahirwar 和 Rajnish Kumar Jha 提供了上述解决方案。

如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

