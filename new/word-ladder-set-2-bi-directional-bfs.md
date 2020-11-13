# 文字阶梯 – 系列 2（双向 BFS）

> 原文：[https://www.geeksforgeeks.org/word-ladder-set-2-bi-directional-bfs/](https://www.geeksforgeeks.org/word-ladder-set-2-bi-directional-bfs/)

给定一个字典，并且两个单词`start`和`target`（两者长度相同）。 查找从`start`到`target`的最小链的长度（如果存在），使得链中的相邻单词仅相差一个字符，并且链中的每个单词都是有效单词，即， 它存在于字典中。 可以假设在字典中存在`target`词，并且所有字典词的长度均相等。

**示例**：

> **输入**：`Dictionary = {POON, PLEE, SAME, POIE, PLEA, PLIE, POIN}`
>
> `start = "TOON"`
>
> `target = PLEA""`
>
> **输出**：7
>
> `TOON -> POON –> POIN –> POIE –> PLIE –> PLEE –> PLEA`

**方法**：可以使用标准 [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 方法（如[在此处](https://www.geeksforgeeks.org/word-ladder-length-of-shortest-chain-to-reach-a-target-word/)讨论的方法）解决，但可以通过使用双向 BFS 来提高其性能。

双向 BFS 不会降低解决方案的时间复杂度，但是在许多情况下，它无疑可以优化性能。 这种方法还可以用于许多其他最短寻路问题中，在这些问题中，我们可以获得有关源节点和目标节点的足够信息。 双向 BFS 涉及的基本思想是从路径的两端开始搜索。

因此，需要维护两个队列和两个访问数组来跟踪两条路径。 因此，只要源队列中存在一个节点（例如`A`）遇到目标队列中存在的一个节点（例如`B`），我们就可以通过将`A`到源的距离与`B`到目标的距离减一（一个节点是公共的）相加来计算答案。 这样，与标准 BFS 方法相比，我们可以在一半时间内计算出答案。 此方法也称为中间相遇 BFS 方法。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure for queue 
struct node { 
    string word; 
    int len; 
}; 

// Function that returns true if a and b 
// differ in only a single character 
bool isAdj(string a, string b) 
{ 
    int count = 0; 
    for (int i = 0; i < a.length(); i++) { 
        if (a[i] != b[i]) 
            count++; 
    } 
    if (count == 1) 
        return true; 
    return false; 
} 

// Function to return the length of the shortest 
// chain from 'beginWord' to 'endWord' 
int ladderLength(string beginWord, string endWord, 
                 vector<string>& wordList) 
{ 

    /* q1 is used to traverse the graph from beginWord  
        and q2 is used to traverse the graph from endWord. 
        vis1 and vis2 are used to keep track of the  
        visited states from respective directions */
    queue<node> q1; 
    queue<node> q2; 
    unordered_map<string, int> vis1; 
    unordered_map<string, int> vis2; 

    node start = { beginWord, 1 }; 
    node end = { endWord, 1 }; 

    vis1[beginWord] = 1; 
    q1.push(start); 
    vis2[endWord] = 1; 
    q2.push(end); 

    while (!q1.empty() && !q2.empty()) { 

        // Fetch the current node 
        // from the source queue 
        node curr1 = q1.front(); 
        q1.pop(); 

        // Fetch the current node from 
        // the destination queue 
        node curr2 = q2.front(); 
        q2.pop(); 

        // Check all the neighbors of curr1 
        for (auto it = wordList.begin(); it != wordList.end(); it++) { 

            // If any one of them is adjacent to curr1 
            // and is not present in vis1 
            // then push it in the queue 
            if (isAdj(curr1.word, *it) && vis1.count(*it) == false) { 

                node temp = { *it, curr1.len + 1 }; 
                q1.push(temp); 
                vis1[*it] = curr1.len + 1; 

                // If temp is the destination node 
                // then return the answer 
                if (temp.word == endWord) { 
                    return temp.len; 
                } 

                // If temp is present in vis2 i.e. distance from 
                // temp and the destination is already calculated 
                if (vis2.count(temp.word)) { 
                    return temp.len + vis2[temp.word] - 1; 
                } 
            } 
        } 

        // Check all the neighbors of curr2 
        for (auto it = wordList.begin(); it != wordList.end(); it++) { 

            // If any one of them is adjacent to curr2 
            // and is not present in vis1 then push it in the queue. 
            if (isAdj(curr2.word, *it) && vis2.count(*it) == false) { 

                node temp = { *it, curr2.len + 1 }; 
                q2.push(temp); 
                vis2[*it] = curr2.len + 1; 

                // If temp is the destination node 
                // then return the answer 
                if (temp.word == beginWord) { 
                    return temp.len; 
                } 

                // If temp is present in vis1 i.e. distance from 
                // temp and the source is already calculated 
                if (vis1.count(temp.word)) { 
                    return temp.len + vis1[temp.word] - 1; 
                } 
            } 
        } 
    } 
    return 0; 
} 

// Driver code 
int main() 
{ 

    vector<string> wordList; 
    wordList.push_back("poon"); 
    wordList.push_back("plee"); 
    wordList.push_back("same"); 
    wordList.push_back("poie"); 
    wordList.push_back("plie"); 
    wordList.push_back("poin"); 
    wordList.push_back("plea"); 

    string start = "toon"; 
    string target = "plea"; 

    cout << ladderLength(start, target, wordList); 

    return 0; 
} 

```

## Java

```java

import java.util.*; 
public class GFG 
{ 
public static class node 
{ 
    String word; 
    int len; 
    public node(String word, int len) 
    { 
        this.word = word; 
        this.len = len; 
    } 
} 

public static boolean isAdj(String a, String b)  
{  
    int count = 0;  
    for (int i = 0; i < a.length(); i++)  
    {  
        if (a.charAt(i) != b.charAt(i))  
            count++;  
    }  
    if (count == 1)  
        return true;  
    return false;  
}  

// Function to return the length of the shortest  
// chain from 'beginWord' to 'endWord'  
public static int ladderLength(String beginWord, String endWord,  
                               ArrayList<String> wordList)  
{  

    /* q1 is used to traverse the graph from beginWord  
        and q2 is used to traverse the graph from endWord.  
        vis1 and vis2 are used to keep track of the  
        visited states from respective directions */
    Queue<node> q1 = new LinkedList<>();  
    Queue<node> q2 = new LinkedList<>();  
    HashMap<String, Integer> vis1 = new HashMap<>();  
    HashMap<String, Integer> vis2 = new HashMap<>();  

    node start = new node(beginWord, 1);  
    node end = new node(endWord, 1);  

    vis1.put(beginWord, 1);  
    q1.add(start);  
    vis2.put(endWord, 1);  
    q2.add(end);  

    while (q1.size() > 0 && q2.size() > 0)  
    {  

        // Fetch the current node  
        // from the source queue  
        node curr1 = q1.remove();  

        // Fetch the current node from  
        // the destination queue  
        node curr2 = q2.remove();  

        // Check all the neighbors of curr1  
        for (int i = 0; i < wordList.size(); i++)  
        {  

            // If any one of them is adjacent to curr1  
            // and is not present in vis1  
            // then push it in the queue  
            if (isAdj(curr1.word,wordList.get(i)) &&  
                vis1.containsKey(wordList.get(i)) == false) 
            {  

                node temp = new node(wordList.get(i), 
                                      curr1.len + 1);  
                q1.add(temp);  
                vis1.put(wordList.get(i), curr1.len + 1);  

                // If temp is the destination node  
                // then return the answer  
                if (temp.word.equals(endWord))  
                {  
                    return temp.len;  
                }  

                // If temp is present in vis2 i.e. distance from  
                // temp and the destination is already calculated  
                if (vis2.containsKey(temp.word))  
                {  
                    return temp.len + vis2.get(temp.word) - 1;  
                }  
            }  
        }  

        // Check all the neighbors of curr2  
        for (int i = 0; i < wordList.size(); i++)  
        {  

            // If any one of them is adjacent to curr2  
            // and is not present in vis1 then push it in the queue.  
            if (isAdj(curr2.word,wordList.get(i)) &&  
                vis2.containsKey(wordList.get(i)) == false)  
            {  

                node temp = new node(wordList.get(i),  
                                     curr2.len + 1 );  
                q2.add(temp);  
                vis2.put(wordList.get(i), curr2.len + 1);  

                // If temp is the destination node  
                // then return the answer  
                if (temp.word.equals(beginWord)) 
                {  
                    return temp.len;  
                }  

                // If temp is present in vis1 i.e. distance from  
                // temp and the source is already calculated  
                if (vis1.containsKey(temp.word)) 
                {  
                    return temp.len + vis1.get(temp.word) - 1;  
                }  
            }  
        }  
    }  
    return 0;  
}  

// Driver code  
public static void main(String args[])  
{  
    ArrayList<String> wordList = new ArrayList<>();  
    wordList.add("poon");  
    wordList.add("plee");  
    wordList.add("same");  
    wordList.add("poie");  
    wordList.add("plie");  
    wordList.add("poin");  
    wordList.add("plea");  

    String start = "toon";  
    String target = "plea";  

    System.out.println(ladderLength(start, target, wordList));  
}  
} 

// This code is contributed by Sambhav Jain 

```

## C#

```cs

// C# implementation of the approach     
using System; 
using System.Collections.Generic; 

class GFG 
{ 

class node 
{ 
    public String word; 
    public int len; 
    public node(String word, int len) 
    { 
        this.word = word; 
        this.len = len; 
    } 
} 

public static bool isAdj(String a, String b)  
{  
    int count = 0;  
    for (int i = 0; i < a.Length; i++)  
    {  
        if (a[i] != b[i])  
            count++;  
    }  
    if (count == 1)  
        return true;  
    return false;  
}  

// Function to return the length of the shortest  
// chain from 'beginWord' to 'endWord'  
public static int ladderLength(String beginWord, String endWord,  
                            List<String> wordList)  
{  

    /* q1 is used to traverse the graph from beginWord  
        and q2 is used to traverse the graph from endWord.  
        vis1 and vis2 are used to keep track of the  
        visited states from respective directions */
    Queue<node> q1 = new Queue<node>();  
    Queue<node> q2 = new Queue<node>();  
    Dictionary<String, int> vis1 = new Dictionary<String, int>();  
    Dictionary<String, int> vis2 = new Dictionary<String, int>();  

    node start = new node(beginWord, 1);  
    node end = new node(endWord, 1);  

    vis1.Add(beginWord, 1);  
    q1.Enqueue(start);  
    vis2.Add(endWord, 1);  
    q2.Enqueue(end);  

    while (q1.Count > 0 && q2.Count > 0)  
    {  

        // Fetch the current node  
        // from the source queue  
        node curr1 = q1.Dequeue();  

        // Fetch the current node from  
        // the destination queue  
        node curr2 = q2.Dequeue();  

        // Check all the neighbors of curr1  
        for (int i = 0; i < wordList.Count; i++)  
        {  

            // If any one of them is adjacent to curr1  
            // and is not present in vis1  
            // then push it in the queue  
            if (isAdj(curr1.word,wordList[i]) &&  
                vis1.ContainsKey(wordList[i]) == false) 
            {  

                node temp = new node(wordList[i], 
                                    curr1.len + 1);  
                q1.Enqueue(temp);  
                vis1.Add(wordList[i], curr1.len + 1);  

                // If temp is the destination node  
                // then return the answer  
                if (temp.word.Equals(endWord))  
                {  
                    return temp.len;  
                }  

                // If temp is present in vis2 i.e. distance from  
                // temp and the destination is already calculated  
                if (vis2.ContainsKey(temp.word))  
                {  
                    return temp.len + vis2[temp.word] - 1;  
                }  
            }  
        }  

        // Check all the neighbors of curr2  
        for (int i = 0; i < wordList.Count; i++)  
        {  

            // If any one of them is adjacent to curr2  
            // and is not present in vis1 then push it in the queue.  
            if (isAdj(curr2.word,wordList[i]) &&  
                vis2.ContainsKey(wordList[i]) == false)  
            {  

                node temp = new node(wordList[i],  
                                    curr2.len + 1 );  
                q2.Enqueue(temp);  
                vis2.Add(wordList[i], curr2.len + 1);  

                // If temp is the destination node  
                // then return the answer  
                if (temp.word.Equals(beginWord)) 
                {  
                    return temp.len;  
                }  

                // If temp is present in vis1 i.e. distance from  
                // temp and the source is already calculated  
                if (vis1.ContainsKey(temp.word)) 
                {  
                    return temp.len + vis1[temp.word] - 1;  
                }  
            }  
        }  
    }  
    return 0;  
}  

// Driver code  
public static void Main(String []args)  
{  
    List<String> wordList = new List<String>();  
    wordList.Add("poon");  
    wordList.Add("plee");  
    wordList.Add("same");  
    wordList.Add("poie");  
    wordList.Add("plie");  
    wordList.Add("poin");  
    wordList.Add("plea");  

    String start = "toon";  
    String target = "plea";  

    Console.WriteLine(ladderLength(start, target, wordList));  
}  
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
7

```



* * *

* * *



