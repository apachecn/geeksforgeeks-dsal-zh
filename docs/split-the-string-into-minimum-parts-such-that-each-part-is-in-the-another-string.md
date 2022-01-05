# 将绳子分成最小的部分，使每个部分都在另一根绳子中

> 原文:[https://www . geeksforgeeks . org/将字符串拆分为最小部分，这样每个部分都在另一个字符串中/](https://www.geeksforgeeks.org/split-the-string-into-minimum-parts-such-that-each-part-is-in-the-another-string/)

给定两个字符串 **A** 和 **B** ，任务是将字符串 A 拆分成最小数量的子字符串，使得每个子字符串都在字符串 B 中

**注意:**如果没有办法拆分字符串，那么打印-1

**示例:**

> **输入:**A =“abcdab”，B =“dabc”
> **输出:** 2
> **解释:**
> 也存在于 B 中的 A 的两个子串是–
> {“ABC”、“dab”}
> 
> **输入:** A = "abcde "，B = "edcb"
> **输出:** -1
> **解释:**
> 无法将字符串 A 拆分为子字符串
> 使得每个字符串也存在于 B 中

**进场:**

*   构造一个 b 的每个子串的 [trie](https://www.geeksforgeeks.org/trie-insert-and-search/)
*   之后，我们将使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)找到最小的部分数来断开字符串 A，使得每个部分都是 b 的子串。

动态规划中的递归关系；

> dp[i] =将字符串 A 分解为前缀的最小零件数。

```
dp[0] = 0
for i in {0, S1.length}
    for j in {i, S1.length}
        if(S1[i, ... j] is found in trie
            dp[j] = min(dp[j], dp[i] + 1);
        else
            break;

dp[S1.length] is the
minimum number of parts.
```

下面是上述方法的实现:

## C++

```
// C++ implementation to split the
// string into minimum number of
// parts such that each part is also
// present in the another string

#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9 + 9;

// Node of Trie
struct TrieNode {
    TrieNode* child[26] = { NULL };
};

// Function to insert a node in the
// Trie Data Structure
void insert(int idx, string& s,
            TrieNode* root)
{
    TrieNode* temp = root;
    for (int i = idx; i < s.length(); i++) {

        // Inserting every character from idx
        // till end to string into trie
        if (temp->child[s[i] - 'a'] == NULL)

            // if there is no edge corresponding
            // to the ith character,
            // then make a new node
            temp->child[s[i] - 'a'] = new TrieNode;

        temp = temp->child[s[i] - 'a'];
    }
}

// Function to find the minimum
// number of parts such that each
// part is present into another string
int minCuts(string S1, string S2)
{
    int n1 = S1.length();
    int n2 = S2.length();

    // Making a new trie
    TrieNode* root = new TrieNode;

    for (int i = 0; i < n2; i++) {

        // Inserting every substring
        // of S2 in trie
        insert(i, S2, root);
    }

    // Creating dp array and
    // init it with infinity
    vector<int> dp(n1 + 1, INF);

    // Base Case
    dp[0] = 0;
    for (int i = 0; i < n1; i++) {

        // Starting the cut from ith character
        // taking temporary node pointer
        // for checking whether the substring
        // [i, j) is present in trie of not
        TrieNode* temp = root;
        for (int j = i + 1; j <= n1; j++) {
            if (temp->child[S1[j - 1] - 'a'] == NULL)

                // if the jth character is not in trie
                // we'll break
                break;

            // Updating the the ending of
            // jth character with dp[i] + 1
            dp[j] = min(dp[j], dp[i] + 1);

            // Descending the trie pointer
            temp = temp->child[S1[j - 1] - 'a'];
        }
    }

    // Answer not possible
    if (dp[n1] >= INF)
        return -1;
    else
        return dp[n1];
}

// Driver Code
int main()
{
    string S1 = "abcdab";
    string S2 = "dabc";

    cout << minCuts(S1, S2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to split the
// String into minimum number of
// parts such that each part is also
// present in the another String
import java.util.*;

class GFG{

static int INF = (int)(1e9 + 9);

// Node of Trie
static class TrieNode
{
    TrieNode []child = new TrieNode[26];
};

// Function to insert a node in the
// Trie Data Structure
static void insert(int idx, String s,
                   TrieNode root)
{
    TrieNode temp = root;
    for(int i = idx; i < s.length(); i++)
    {

        // Inserting every character from idx
        // till end to String into trie
        if (temp.child[s.charAt(i) - 'a'] == null)

            // If there is no edge corresponding
            // to the ith character,
            // then make a new node
            temp.child[s.charAt(i) - 'a'] = new TrieNode();

        temp = temp.child[s.charAt(i) - 'a'];
    }
}

// Function to find the minimum
// number of parts such that each
// part is present into another String
static int minCuts(String S1, String S2)
{
    int n1 = S1.length();
    int n2 = S2.length();

    // Making a new trie
    TrieNode root = new TrieNode();

    for(int i = 0; i < n2; i++)
    {

        // Inserting every subString
        // of S2 in trie
        insert(i, S2, root);
    }

    // Creating dp array and
    // init it with infinity
    int []dp = new int[n1 + 1];
    Arrays.fill(dp, INF);

    // Base Case
    dp[0] = 0;

    for(int i = 0; i < n1; i++)
    {

        // Starting the cut from ith character
        // taking temporary node pointer
        // for checking whether the subString
        // [i, j) is present in trie of not
        TrieNode temp = root;
        for(int j = i + 1; j <= n1; j++)
        {
            if (temp.child[S1.charAt(j - 1) - 'a'] == null)

                // If the jth character is not in trie
                // we'll break
                break;

            // Updating the the ending of
            // jth character with dp[i] + 1
            dp[j] = Math.min(dp[j], dp[i] + 1);

            // Descending the trie pointer
            temp = temp.child[S1.charAt(j - 1) - 'a'];
        }
    }

    // Answer not possible
    if (dp[n1] >= INF)
        return -1;
    else
        return dp[n1];
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "abcdab";
    String S2 = "dabc";

    System.out.print(minCuts(S1, S2));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to split the
# string into minimum number of
# parts such that each part is also
# present in the another string
INF = 1e9 + 9

# Node of Trie
class TrieNode():
    def __init__(self):

        self.child = [None] * 26

# Function to insert a node in the
# Trie Data Structure
def insert(idx, s, root):

    temp = root

    for i in range(idx, len(s)):

        # Inserting every character from idx
        # till end to string into trie
        if temp.child[ord(s[i]) -
                      ord('a')] == None:

            # If there is no edge corresponding
            # to the ith character,
            # then make a new node
            temp.child[ord(s[i]) -
                       ord('a')] = TrieNode()

        temp = temp.child[ord(s[i]) - ord('a')]

# Function to find the minimum
# number of parts such that each
# part is present into another string
def minCuts(S1, S2):

    n1 = len(S1)
    n2 = len(S2)

    # Making a new trie
    root = TrieNode()

    for i in range(n2):

        # Inserting every substring
        # of S2 in trie
        insert(i, S2, root)

    # Creating dp array and
    # init it with infinity
    dp = [INF] * (n1 + 1)

    # Base Case
    dp[0] = 0

    for i in range(n1):

        # Starting the cut from ith character
        # taking temporary node pointer
        # for checking whether the substring
        # [i, j) is present in trie of not
        temp = root
        for j in range(i + 1, n1 + 1):
            if temp.child[ord(S1[j - 1]) -
                          ord('a')] == None:

                # If the jth character is not
                # in trie we'll break
                break

            # Updating the the ending of
            # jth character with dp[i] + 1
            dp[j] = min(dp[j], dp[i] + 1)

            # Descending the trie pointer
            temp = temp.child[ord(S1[j - 1]) -
                              ord('a')]

    # Answer not possible
    if dp[n1] >= INF:
        return -1
    else:
        return dp[n1]

# Driver Code
S1 = "abcdab"
S2 = "dabc"

print(minCuts(S1, S2))

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to split the
// String into minimum number of
// parts such that each part is also
// present in the another String
using System;
class GFG{

static int INF = (int)(1e9 + 9);

// Node of Trie
class TrieNode
{
    public TrieNode []child =
                    new TrieNode[26];
};

// Function to insert a node in the
// Trie Data Structure
static void insert(int idx, String s,
                   TrieNode root)
{
    TrieNode temp = root;
    for(int i = idx; i < s.Length; i++)
    {       
        // Inserting every character from idx
        // till end to String into trie
        if (temp.child[s[i] - 'a'] == null)

            // If there is no edge corresponding
            // to the ith character,
            // then make a new node
            temp.child[s[i] - 'a'] =
                       new TrieNode();

        temp = temp.child[s[i] - 'a'];
    }
}

// Function to find the minimum
// number of parts such that each
// part is present into another String
static int minCuts(String S1, String S2)
{
    int n1 = S1.Length;
    int n2 = S2.Length;

    // Making a new trie
    TrieNode root = new TrieNode();

    for(int i = 0; i < n2; i++)
    {       
        // Inserting every subString
        // of S2 in trie
        insert(i, S2, root);
    }

    // Creating dp array and
    // init it with infinity
    int []dp = new int[n1 + 1];
    for(int i = 0; i <= n1; i++)
        dp[i] = INF;

    // Base Case
    dp[0] = 0;

    for(int i = 0; i < n1; i++)
    {       
        // Starting the cut from ith character
        // taking temporary node pointer
        // for checking whether the subString
        // [i, j) is present in trie of not
        TrieNode temp = root;
        for(int j = i + 1; j <= n1; j++)
        {
            if (temp.child[S1[j-1] - 'a'] == null)

                // If the jth character is not in trie
                // we'll break
                break;

            // Updating the the ending of
            // jth character with dp[i] + 1
            dp[j] = Math.Min(dp[j], dp[i] + 1);

            // Descending the trie pointer
            temp = temp.child[S1[j - 1] - 'a'];
        }
    }

    // Answer not possible
    if (dp[n1] >= INF)
        return -1;
    else
        return dp[n1];
}

// Driver Code
public static void Main(String[] args)
{
    String S1 = "abcdab";
    String S2 = "dabc";
    Console.Write(minCuts(S1, S2));
}
}
// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // Javascript implementation to split the
    // String into minimum number of
    // parts such that each part is also
    // present in the another String

    let INF = (1e9 + 9);

    // Node of Trie
    class Node
    {
        constructor()
        {

        }
    }

    function TrieNode()
    {
        let temp = new Node();
        temp.child = new Node(26);
        for(let i = 0; i < 26; i++)
        {
            temp.child[i] = null;
        }
        return temp;
    }

    // Function to insert a node in the
    // Trie Data Structure
    function insert(idx, s, root)
    {
        let temp = root;
        for(let i = idx; i < s.length; i++)
        {

            // Inserting every character from idx
            // till end to String into trie
            if (temp.child[s[i].charCodeAt() - 'a'.charCodeAt()] == null)

                // If there is no edge corresponding
                // to the ith character,
                // then make a new node
                temp.child[s[i].charCodeAt() - 'a'.charCodeAt()] = new TrieNode();

            temp = temp.child[s[i].charCodeAt() - 'a'.charCodeAt()];
        }
    }

    // Function to find the minimum
    // number of parts such that each
    // part is present into another String
    function minCuts(S1, S2)
    {
        let n1 = S1.length;
        let n2 = S2.length;

        // Making a new trie
        let root = new TrieNode();

        for(let i = 0; i < n2; i++)
        {

            // Inserting every subString
            // of S2 in trie
            insert(i, S2, root);
        }

        // Creating dp array and
        // init it with infinity
        let dp = new Array(n1 + 1);
        dp.fill(INF);

        // Base Case
        dp[0] = 0;

        for(let i = 0; i < n1; i++)
        {

            // Starting the cut from ith character
            // taking temporary node pointer
            // for checking whether the subString
            // [i, j) is present in trie of not
            let temp = root;
            for(let j = i + 1; j <= n1; j++)
            {
                if (temp.child[S1[j - 1].charCodeAt() - 'a'.charCodeAt()] == null)

                    // If the jth character is not in trie
                    // we'll break
                    break;

                // Updating the the ending of
                // jth character with dp[i] + 1
                dp[j] = Math.min(dp[j], dp[i] + 1);

                // Descending the trie pointer
                temp = temp.child[S1[j - 1].charCodeAt() - 'a'.charCodeAt()];
            }
        }

        // Answer not possible
        if (dp[n1] >= INF)
            return -1;
        else
            return dp[n1];
    }

    let S1 = "abcdab";
    let S2 = "dabc";

    document.write(minCuts(S1, S2));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
2
```

**时间复杂度:**

![O(N^2)       ](img/cbc843e652e8df587895072cfdf0b8e1.png "Rendered by QuickLaTeX.com")

**空间复杂度:**

![O(N^2)       ](img/cbc843e652e8df587895072cfdf0b8e1.png "Rendered by QuickLaTeX.com")