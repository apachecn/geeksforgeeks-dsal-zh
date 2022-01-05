# 给定一个已排序的外星语言词典，找到字符的顺序

> 原文:[https://www . geesforgeks . org/given-sorted-dictionary-find-preference-characters/](https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/)

给定一个外星语言的排序字典(单词数组)，找到该语言中字符的顺序。

**示例:**

```
Input:  words[] = {"baa", "abcd", "abca", "cab", "cad"}
Output: Order of characters is 'b', 'd', 'a', 'c'
Note that words are sorted and in the given language "baa" 
comes before "abcd", therefore 'b' is before 'a' in output.
Similarly we can find other orders.

Input:  words[] = {"caa", "aaa", "aab"}
Output: Order of characters is 'c', 'a', 'b'
```

**方法 1:**

想法是创建一个字符的图形，然后找到所创建图形的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。以下是详细步骤。
1)创建一个图形 *g* ，其顶点数量等于给定外星语言中字母表的大小。例如，如果字母表的大小是 5，那么单词中可以有 5 个字符。最初图中没有边。
2)对给定排序数组中的每对相邻单词执行以下操作。
…..a)让当前一对单词为*单词 1* 和*单词 2* 。逐一比较两个单词的字符，找出第一个不匹配的字符。
…..b)在 *g* 中创建一条从*字 1* 到*字 2* 的不匹配字符的边。
3)打印上述创建图形的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。

*以上是在 C++中实现的。*

**时间复杂度:**创建图形的第一步需要 O(n + alpha)时间，其中 n 是给定单词的数量，alpha 是给定字母表中的字符数量。第二步也是拓扑排序。请注意，图中将有 alpha 顶点和最多(n-1)条边。拓扑排序的时间复杂度是 O(V+E)，这里是 O(n+α)。所以总的时间复杂度是 O(n+α)+O(n+α)，也就是 O(n+α)。

**练习:**当输入无效时，上述代码不起作用。例如{“ABA”、“bba”、“AAA”}是无效的，因为从前两个词，我们可以推断‘a’应该出现在‘b’之前，但是从最后两个词，我们可以推断‘b’应该出现在‘a’之前，这是不可能的。扩展上述程序以处理无效输入，并将输出生成为“无效”。

**方法 2:【对无效输入数据有效】**

*我们已经在 C#中实现了这种方法。*

<u>算法:</u>

(1)一次比较两个相邻的单词(即单词 1 和单词 2，单词 2 和单词 3，…，单词(开始索引)和单词(开始索引+ 1)

(2)然后，我们对所选的两个单词一次比较一个字符。

(2a)如果两个字符不同，我们在这里停止比较，并得出结论，来自单词(startIndex)的字符在另一个之前。

(2b)如果两个字符相同，我们将继续进行比较，直到(2a)出现，或者如果其中一个单词已经用完。

(3)我们继续以这种方式比较每个单词，直到比较完所有单词。

一旦我们在(2a)中找到一个字符集，我们就将它们传递给“AlienCharacters”类，该类负责字符的整体排序。其思想是保持链表中字符的顺序。为了优化插入链表的时间，使用了一个映射(C# Dictionary)作为索引实体，从而将复杂度降低到 O(1)。这是对以前的算法的改进，以前的算法使用拓扑排序。

<u>边界条件:</u>

1.开始索引必须在范围内

2.当比较两个单词时，如果我们在一个单词上穷尽，即两个单词的长度是不同的。比较，直到任何一个耗尽。

<u>复杂度分析:</u>

为了更好地理解，在下面的代码(C#)中已经提到了方法方面的时间复杂性。

如果“N”是输入的外来词汇/词典中的单词数量，“L”是最大长度单词的长度，“C”是唯一字符的最终数量，

时间复杂度:0(N * 1)

空间复杂性:O(C)

## C++

```
// A C++ program to order of characters in an alien language
#include<bits/stdc++.h>
using namespace std;

// Class to represent a graph
class Graph
{
    int V;    // No. of vertices'

    // Pointer to an array containing adjacency listsList
    list<int> *adj;

    // A function used by topologicalSort
    void topologicalSortUtil(int v, bool visited[], stack<int> &Stack);
public:
    Graph(int V);   // Constructor

    // function to add an edge to graph
    void addEdge(int v, int w);

    // prints a Topological Sort of the complete graph
    void topologicalSort();
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w); // Add w to v’s list.
}

// A recursive function used by topologicalSort
void Graph::topologicalSortUtil(int v, bool visited[], stack<int> &Stack)
{
    // Mark the current node as visited.
    visited[v] = true;

    // Recur for all the vertices adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            topologicalSortUtil(*i, visited, Stack);

    // Push current vertex to stack which stores result
    Stack.push(v);
}

// The function to do Topological Sort. It uses recursive topologicalSortUtil()
void Graph::topologicalSort()
{
    stack<int> Stack;

    // Mark all the vertices as not visited
    bool *visited = new bool[V];
    for (int i = 0; i < V; i++)
        visited[i] = false;

    // Call the recursive helper function to store Topological Sort
    // starting from all vertices one by one
    for (int i = 0; i < V; i++)
        if (visited[i] == false)
            topologicalSortUtil(i, visited, Stack);

    // Print contents of stack
    while (Stack.empty() == false)
    {
        cout << (char) ('a' + Stack.top()) << " ";
        Stack.pop();
    }
}

int min(int x, int y)
{
    return (x < y)? x : y;
}

// This function finds and prints order of character from a sorted
// array of words. n is size of words[].  alpha is set of possible
// alphabets.
// For simplicity, this function is written in a way that only
// first 'alpha' characters can be there in words array.  For
// example if alpha is 7, then words[] should have only 'a', 'b',
// 'c' 'd', 'e', 'f', 'g'
void printOrder(string words[], int n, int alpha)
{
    // Create a graph with 'alpha' edges
    Graph g(alpha);

    // Process all adjacent pairs of words and create a graph
    for (int i = 0; i < n-1; i++)
    {
        // Take the current two words and find the first mismatching
        // character
        string word1 = words[i], word2 = words[i+1];
        for (int j = 0; j < min(word1.length(), word2.length()); j++)
        {
            // If we find a mismatching character, then add an edge
            // from character of word1 to that of word2
            if (word1[j] != word2[j])
            {
                g.addEdge(word1[j]-'a', word2[j]-'a');
                break;
            }
        }
    }

    // Print topological sort of the above created graph
    g.topologicalSort();
}

// Driver program to test above functions
int main()
{
    string words[] = {"caa", "aaa", "aab"};
    printOrder(words, 3, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to order of
// characters in an alien language
import java.util.*;

// Class to represent a graph
class Graph {

    // An array representing the graph as an adjacency list
    private final LinkedList<Integer>[] adjacencyList;

    Graph(int nVertices)
    {
        adjacencyList = new LinkedList[nVertices];
        for (int vertexIndex = 0; vertexIndex < nVertices;
             vertexIndex++) {
            adjacencyList[vertexIndex] = new LinkedList<>();
        }
    }

    // function to add an edge to graph
    void addEdge(int startVertex, int endVertex)
    {
        adjacencyList[startVertex].add(endVertex);
    }

    private int getNoOfVertices()
    {
        return adjacencyList.length;
    }

    // A recursive function used by topologicalSort
    private void topologicalSortUtil(int currentVertex,
                                     boolean[] visited,
                                     Stack<Integer> stack)
    {
        // Mark the current node as visited.
        visited[currentVertex] = true;

        // Recur for all the vertices adjacent to this
        // vertex
        for (int adjacentVertex :
             adjacencyList[currentVertex]) {
            if (!visited[adjacentVertex]) {
                topologicalSortUtil(adjacentVertex, visited,
                                    stack);
            }
        }

        // Push current vertex to stack which stores result
        stack.push(currentVertex);
    }

    // prints a Topological Sort of the complete graph
    void topologicalSort()
    {
        Stack<Integer> stack = new Stack<>();

        // Mark all the vertices as not visited
        boolean[] visited = new boolean[getNoOfVertices()];
        for (int i = 0; i < getNoOfVertices(); i++) {
            visited[i] = false;
        }

        // Call the recursive helper function to store
        // Topological Sort starting from all vertices one
        // by one
        for (int i = 0; i < getNoOfVertices(); i++) {
            if (!visited[i]) {
                topologicalSortUtil(i, visited, stack);
            }
        }

        // Print contents of stack
        while (!stack.isEmpty()) {
            System.out.print((char)('a' + stack.pop())
                             + " ");
        }
    }
}

public class OrderOfCharacters {
    // This function finds and prints order
    // of character from a sorted array of words.
    // alpha is number of possible alphabets
    // starting from 'a'. For simplicity, this
    // function is written in a way that only
    // first 'alpha' characters can be there
    // in words array. For example if alpha
    //  is 7, then words[] should contain words
    // having only 'a', 'b','c' 'd', 'e', 'f', 'g'
    private static void printOrder(String[] words, int n,
                                   int alpha)
    {
        // Create a graph with 'alpha' edges
        Graph graph = new Graph(alpha);

        for (int i = 0; i < n - 1; i++) {
            // Take the current two words and find the first
            // mismatching character
            String word1 = words[i];
            String word2 = words[i + 1];
            for (int j = 0; j < Math.min(word1.length(),
                                         word2.length());
                 j++) {
                // If we find a mismatching character, then
                // add an edge from character of word1 to
                // that of word2
                if (word1.charAt(j) != word2.charAt(j)) {
                    graph.addEdge(word1.charAt(j) - 'a',
                                  word2.charAt(j) - 'a');
                    break;
                }
            }
        }

        // Print topological sort of the above created graph
        graph.topologicalSort();
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        String[] words = { "caa", "aaa", "aab" };
        printOrder(words, 3, 3);
    }
}

// Contributed by Harikrishnan Rajan
```

## C#

```
using System;
using System.Collections.Generic;
using System.Linq;

namespace AlienDictionary
{
    public class DNode
    {
        public string Char;
        public DNode prev = null;
        public DNode next = null;
        public DNode(string character) => Char = character;
    }

    public class AlienCharacters
    {
        public AlienCharacters(int k) => MaxChars = k;

        private int MaxChars;
        private DNode head = null;
        private Dictionary<string, DNode> index = new Dictionary<string, DNode>();

          // As we use Dictionary for indexing, the time complexity for inserting
        // characters in order will take O(1)
        // Time: O(1)
        // Space: O(c), where 'c' is the unique character count.
        public bool UpdateCharacterOrdering(string predChar, string succChar)
        {
            DNode pNode = null, sNode = null;
            bool isSNodeNew = false, isPNodeNew = false;
            if(!index.TryGetValue(predChar, out pNode))
            {
                pNode = new DNode(predChar);
                index[predChar] = pNode;
                isPNodeNew = true;
            }
            if (!index.TryGetValue(succChar, out sNode))
            {
                sNode = new DNode(succChar);
                index[succChar] = sNode;
                isSNodeNew = true;
            }

            // before ordering is formed, validate if both the nodes are already present
            if (!isSNodeNew && !isPNodeNew)
            {
                if (!Validate(predChar, succChar))
                    return false;
            }
            else if ((isPNodeNew && !isSNodeNew) || (isPNodeNew && isSNodeNew))
                InsertNodeBefore(ref pNode, ref sNode);
            else
                InsertNodeAfter(ref pNode, ref sNode);

            if (pNode.prev == null)
                head = pNode;

            return true;
        }

          // Time: O(1)
        private void InsertNodeAfter(ref DNode pNode, ref DNode sNode)
        {
            sNode.next = pNode?.next;
            if (pNode.next != null)
                pNode.next.prev = sNode;

            pNode.next = sNode;
            sNode.prev = pNode;
        }

          // Time: O(1)
        private void InsertNodeBefore(ref DNode pNode, ref DNode sNode)
        {
            // insert pnode before snode
            pNode.prev = sNode?.prev;

            if (sNode.prev != null)
                sNode.prev.next = pNode;
            sNode.prev = pNode;
            pNode.next = sNode;
        }

          // Time: O(1)
        private bool Validate(string predChar, string succChar)
        {
            // this is the first level of validation
            // validate if predChar node actually occurs before succCharNode.
            DNode sNode = index[succChar];

            while(sNode != null)
            {
                if (sNode.Char != predChar)
                    sNode = sNode.prev;
                else
                    return true; // validation successful
            }

            // if we have reached the end and not found the predChar before succChar
            // something is not right!
            return false;
        }

          // Time: O(c), where 'c' is the unique character count.
        public override string ToString()
        {
            string res = "";
            int count = 0;
            DNode currNode = head;

            while(currNode != null)
            {
                res += currNode.Char + " ";
                count++;
                currNode = currNode.next;
            }

            // second level of validation
            if (count != MaxChars) // something went wrong!
                res = "ERROR!!! Input words not enough to find all k unique characters.";

            return res;
        }
    }

    class Program
    {
        static int k = 4;
        static AlienCharacters alienCharacters = new AlienCharacters(k);
        static List<string> vocabulary = new List<string>();

        static void Main(string[] args)
        {
            vocabulary.Add("baa");
            vocabulary.Add("abcd");
            vocabulary.Add("abca");
            vocabulary.Add("cab");
            vocabulary.Add("cad");

            ProcessVocabulary(0);

            Console.WriteLine(alienCharacters.ToString());

            Console.ReadLine();
        }

          // Time: O(vocabulary.Count + max(word.Length))
        static void ProcessVocabulary(int startIndex)
        {
            if (startIndex >= vocabulary.Count - 1)
                return;

            var res = GetPredSuccChar(vocabulary.ElementAt(startIndex), vocabulary.ElementAt(startIndex + 1));
            if (res != null)
            {
                if (!alienCharacters.UpdateCharacterOrdering(res.Item1, res.Item2))
                {
                    Console.WriteLine("ERROR!!! Invalid input data, the words maybe in wrong order");
                    return;
                }
            }

            ProcessVocabulary(startIndex + 1);
        }

          //Time: O(max(str1.Length, str2.Length)
        static Tuple<string, string> GetPredSuccChar(string str1, string str2)
        {
            Tuple<string, string> result = null;

            if (str1.Length == 0 || str2.Length == 0)
                return null; // invalid condition.

            if(str1[0] != str2[0]) // found an ordering
            {
                result = new Tuple<string, string>(str1[0].ToString(), str2[0].ToString());
                return result;
            }

            string s1 = str1.Substring(1, str1.Length - 1);
            string s2 = str2.Substring(1, str2.Length - 1);

            if (s1.Length == 0 || s2.Length == 0)
                return null; // recursion can stop now.

            return GetPredSuccChar(s1, s2);
        }
    }
}

// Contributed by Priyanka Pardesi Ramachander
```

**输出:**

```
c a b
```

本文由**比于什·古普塔(C++)、Harikrishnan Rajan (java)** 、**和 Priyanka Pardesi Ramachander(c#)**投稿。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。