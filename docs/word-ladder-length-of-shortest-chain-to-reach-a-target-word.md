# 单词阶梯(到达目标单词的最短链的长度)

> 原文:[https://www . geesforgeks . org/word-梯形-最短链长-到达目标单词/](https://www.geeksforgeeks.org/word-ladder-length-of-shortest-chain-to-reach-a-target-word/)

给定一个字典，两个词“开始”和“目标”(长度相同)。如果存在，找出从“开始”到“目标”的最小链的长度，使得链中的相邻单词仅相差一个字符，并且链中的每个单词都是有效单词，即它存在于字典中。可以假设“目标”单词存在于词典中，并且所有词典单词的长度都相同。

**示例:**

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

**<u>解:</u>** 思路是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。
**进场:**

1.  从给定的起始词开始。
2.  把这个词推到队列中
3.  运行循环，直到队列为空
4.  遍历与其相邻(相差一个字符)的所有单词，并将该单词推入队列(对于 BFS)
5.  继续这样做，直到我们找到目标词，或者我们已经遍历了所有的词。

以下是上述想法的实现。

## C++

```
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

    if(start == target)
      return 0;

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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

     if(start == target)
      return 0;
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

## 蟒蛇 3

```
# Python3 program to find length of the
# shortest chain transformation from source
# to target
from collections import deque

# Returns length of shortest chain
# to reach 'target' from 'start'
# using minimum number of adjacent
# moves. D is dictionary
def shortestChainLen(start, target, D):

    if start == target:
      return 0
    # If the target is not
    # present in the dictionary
    if target not in D:
        return 0

    # To store the current chain length
    # and the length of the words
    level, wordlength = 0, len(start)

    # Push the starting word into the queue
    Q =  deque()
    Q.append(start)

    # While the queue is non-empty
    while (len(Q) > 0):

        # Increment the chain length
        level += 1

        # Current size of the queue
        sizeofQ = len(Q)

        # Since the queue is being updated while
        # it is being traversed so only the
        # elements which were already present
        # in the queue before the start of this
        # loop will be traversed for now
        for i in range(sizeofQ):

            # Remove the first word from the queue
            word = [j for j in Q.popleft()]
            #Q.pop()

            # For every character of the word
            for pos in range(wordlength):

                # Retain the original character
                # at the current position
                orig_char = word[pos]

                # Replace the current character with
                # every possible lowercase alphabet
                for c in range(ord('a'), ord('z')+1):
                    word[pos] = chr(c)

                    # If the new word is equal
                    # to the target word
                    if ("".join(word) == target):
                        return level + 1

                    # Remove the word from the set
                    # if it is found in it
                    if ("".join(word) not in D):
                        continue

                    del D["".join(word)]

                    # And push the newly generated word
                    # which will be a part of the chain
                    Q.append("".join(word))

                # Restore the original character
                # at the current position
                word[pos] = orig_char

    return 0

# Driver code
if __name__ == '__main__':

    # Make dictionary
    D = {}
    D["poon"] = 1
    D["plee"] = 1
    D["same"] = 1
    D["poie"] = 1
    D["plie"] = 1
    D["poin"] = 1
    D["plea"] = 1
    start = "toon"
    target = "plea"

    print("Length of shortest chain is: ",
    shortestChainLen(start, target, D))

# This code is contributed by mohit kumar 29
```

## C#

```
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

     if(start == target)
       return 0;
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

## java 描述语言

```
<script>
// Javascript program to find length
// of the shortest chain
// transformation from source
// to target

// Returns length of shortest chain
// to reach 'target' from 'start'
// using minimum number of adjacent moves.
// D is dictionary
    function shortestChainLen(start,target,D)
    {
        if(start == target)
      return 0;

    // If the target String is not
    // present in the dictionary
    if (!D.has(target))
        return 0;

    // To store the current chain length
    // and the length of the words
    let level = 0, wordlength = start.length;

    // Push the starting word into the queue
    let Q = [];
    Q.push(start);

    // While the queue is non-empty
    while (Q.length != 0)
    {

        // Increment the chain length
        ++level;

        // Current size of the queue
        let sizeofQ = Q.length;

        // Since the queue is being updated while
        // it is being traversed so only the
        // elements which were already present
        // in the queue before the start of this
        // loop will be traversed for now
        for (let i = 0; i < sizeofQ; ++i)
        {

            // Remove the first word from the queue
            let word = Q[0].split("");
            Q.shift();

            // For every character of the word
            for (let pos = 0; pos < wordlength; ++pos)
            {

                // Retain the original character
                // at the current position
                let orig_char = word[pos];

                // Replace the current character with
                // every possible lowercase alphabet
                for (let c = 'a'.charCodeAt(0); c <= 'z'.charCodeAt(0); ++c)
                {
                    word[pos] = String.fromCharCode(c);

                    // If the new word is equal
                    // to the target word
                    if (word.join("") == target)
                        return level + 1;

                    // Remove the word from the set
                    // if it is found in it
                    if (!D.has(word.join("")))
                        continue;
                    D.delete(word.join(""));

                    // And push the newly generated word
                    // which will be a part of the chain
                    Q.push(word.join(""));
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
    // make dictionary
    let D = new Set();
    D.add("poon");
    D.add("plee");
    D.add("same");
    D.add("poie");
    D.add("plie");
    D.add("poin");
    D.add("plea");
    let start = "toon";
    let target = "plea";
    document.write("Length of shortest chain is: "
        + shortestChainLen(start, target, D));

    // This code is contributed by unknown2108
</script>
```

**Output**

```
Length of shortest chain is: 7
```

**复杂度分析:**

*   **时间复杂度:**O(n ^ m)，其中 m 是原本在字典中的条目数，n 是字符串的大小。

*   **辅助空间:** O(m*n)，其中 m 是存储在队列中的字符串。
    所以空间复杂度是 O(m*n)。

**替代实现:(维护中间词和原词的映射):**

下面是上述方法的替代实现。

这里，在这种方法中，我们找出起始词的所有中间词和给定词典列表中的词，并维护中间词的映射和原始词的向量(映射<string vector="">>)。例如，“POON”一词的中间词是“*OON”、“P*ON”、“PO*N”、“POO*”。然后，我们从起始字开始执行 BFS 遍历，并将一对起始字和距离(对(字，距离))推送到队列，直到到达目标字。那么，距离就是我们的答案。</string>

## C++

```
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

   if(start == target)
      return 0;

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

// Driver code
int main()
{
    // Make dictionary
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

**Output**

```
Length of shortest chain is: 7
```

感谢 Gaurav Ahirwar 和 Rajnish Kumar Jha 的上述解决方案。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。