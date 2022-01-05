# 单词(或字符串)数组中的回文对

> 原文:[https://www . geesforgeks . org/回文-单词或字符串数组对/](https://www.geeksforgeeks.org/palindrome-pair-in-an-array-of-words-or-strings/)

给定一个单词列表，找出这两个单词中是否有任何一个可以连接成回文。
**例:**

```
Input  : list[] = {"geekf", "geeks", "or", 
                            "keeg", "abc", "bc"}
Output : Yes
There is a pair "geekf" and "keeg"

Input : list[] =  {"abc", "xyxcba", "geekst", "or",
                                      "keeg", "bc"}
Output : Yes
There is a pair "abc" and "xyxcba"
```

问于:谷歌采访

**简单方法**:

```
1- Consider each pair one by one.
2- Check if any of the pairs forms a palindrome
   after concatenating them.
3- Return true, if any such pair exists.
4- Else, return false.
```

## C++

```
// C++ program to find if there is a pair that
// can form a palindrome.
#include<bits/stdc++.h>
using namespace std;

// Utility function to check if a string is a
// palindrome
bool isPalindrome(string str)
{
    int len = str.length();

    // compare each character from starting
    // with its corresponding character from last
    for (int i = 0; i < len/2; i++ )
        if (str[i] != str[len-i-1])
            return false;

    return true;
}

// Function to check if a palindrome pair exists
bool checkPalindromePair(vector <string> vect)
{
    // Consider each pair one by one
    for (int i = 0; i< vect.size()-1; i++)
    {
        for (int j = i+1; j< vect.size() ; j++)
        {
            string check_str;

            // concatenate both strings
            check_str = vect[i] + vect[j];

            // check if the concatenated string is
            // palindrome
            if (isPalindrome(check_str))
                return true;

            // check for other combination of the two strings
            check_str = vect[j] + vect[i];
            if (isPalindrome(check_str))
                return true;
        }
    }
    return false;
}

// Driver code
int main()
{
    vector <string> vect = {"geekf", "geeks", "or",
                            "keeg", "abc", "bc"};

    checkPalindromePair(vect)? cout << "Yes" :
                               cout << "No";
    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there is a pair that
// can form a palindrome.
import java.util.Arrays;
import java.util.List;
public class Palin_pair1 {

    // Utility function to check if a string is a
    // palindrome
    static boolean isPalindrome(String str)
    {
        int len = str.length();

        // compare each character from starting
        // with its corresponding character from last
        for (int i = 0; i < len/2; i++ )
            if (str.charAt(i) != str.charAt(len-i-1))
                return false;

        return true;
    }

    // Function to check if a palindrome pair exists
    static boolean checkPalindromePair(List<String> vect)
    {
        // Consider each pair one by one
        for (int i = 0; i< vect.size()-1; i++)
        {
            for (int j = i+1; j< vect.size() ; j++)
            {
                String check_str = "";

                // concatenate both strings
                check_str = check_str + vect.get(i) + vect.get(j);

                // check if the concatenated string is
                // palindrome
                if (isPalindrome(check_str))
                    return true;

                check_str = vect.get(j) + vect.get(i);

                // check if the concatenated string is
                // palindrome
                if (isPalindrome(check_str))
                    return true;
            }
        }
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        List<String> vect = Arrays.asList("geekf", "geeks", "or",
                                "keeg", "abc", "bc");

        if (checkPalindromePair(vect) == true)
            System.out.println("Yes");
        else    
            System.out.println("No");
    }
}
//This code is contributed by Sumit Ghosh

```

## 蟒蛇 3

```
# Python3 program to find if 
# there is a pair that
# can form a palindrome.

# Utility function to check 
# if a string is a palindrome
def isPalindrome(st):

    length = len(st)

    # Compare each character 
    # from starting with its 
    # corresponding character from last
    for i in range(length // 2):
        if (st[i] != st[length - i - 1]):
            return False

    return True

# Function to check if a 
# palindrome pair exists
def checkPalindromePair(vect):

    # Consider each pair one by one
    for i in range(len(vect) - 1):
        for j in range(i + 1, len(vect)):

            # Concatenate both strings
            check_str = vect[i] + vect[j]

            # Check if the concatenated 
            # string is palindrome
            if (isPalindrome(check_str)):
                return True

            # Check for other combination 
            # of the two strings
            check_str = vect[j] + vect[i]
            if (isPalindrome(check_str)):
                return True
    return False

# Driver code
if __name__ == "__main__":

    vect = ["geekf", "geeks", "or",
            "keeg", "abc", "bc"]

    if checkPalindromePair(vect):
        print("Yes")
    else:
        print ("No")

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find if there is a pair that
// can form a palindrome.
using System;
using System.Collections.Generic;

class GFG 
{

    // Utility function to check if 
    // a string is a palindrome
    static Boolean isPalindrome(String str)
    {
        int len = str.Length;

        // compare each character from starting
        // with its corresponding character from last
        for (int i = 0; i < len / 2; i++ )
            if (str[i] != str[len - i - 1])
                return false;

        return true;
    }

    // Function to check if a palindrome pair exists
    static Boolean checkPalindromePair(List<String> vect)
    {
        // Consider each pair one by one
        for (int i = 0; i< vect.Count - 1; i++)
        {
            for (int j = i + 1; j< vect.Count ; j++)
            {
                String check_str = "";

                // concatenate both strings
                check_str = check_str + vect[i] + vect[j];

                // check if the concatenated string is
                // palindrome
                if (isPalindrome(check_str))
                    return true;

                check_str = vect[j] + vect[j];

                // check if the concatenated string is
                // palindrome
                if (isPalindrome(check_str))
                    return true;
            }
        }
        return false;
    }

    // Driver code
    public static void Main(String []args)
    {
        List<String> vect = new List<String>(){"geekf", "geeks", "or",
                                                  "keeg", "abc", "bc"};

        if (checkPalindromePair(vect) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Rajput-Ji

```

## java 描述语言

```
<script>

// Javascript program to find if there 
// is a pair that can form a palindrome.

// Utility function to check if a 
// string is a palindrome
function isPalindrome(str)
{
    let len = str.length;

    // Compare each character from starting
    // with its corresponding character from last
    for(let i = 0; i < len / 2; i++ )
        if (str[i] != str[len - i - 1])
            return false;

    return true;
}

// Function to check if a palindrome pair exists
function checkPalindromePair(vect)
{

    // Consider each pair one by one
    for(let i = 0; i < vect.length - 1; i++)
    {
        for(let j = i + 1; j < vect.length; j++)
        {
            let check_str = "";

            // Concatenate both strings
            check_str = check_str + vect[i] + vect[j];

            // Check if the concatenated string is
            // palindrome
            if (isPalindrome(check_str))
                return true;

            check_str = vect[j] + vect[i];

            // Check if the concatenated string is
            // palindrome
            if (isPalindrome(check_str))
                return true;
        }
    }
    return false;
}

// Driver code
let vect = [ "geekf", "geeks", "or",
             "keeg", "abc", "bc" ]

if (checkPalindromePair(vect) == true)
    document.write("Yes");
else   
    document.write("No");

// This code is contributed by rag2127

</script>

```

**输出:**

```
 Yes
```

**时间复杂度:O(n <sup>2</sup> k)**
这里 n 是列表中的字数，k 是检查回文的最大长度。

**高效方法**
使用 Trie 数据结构可以高效完成。这个想法是保持一个所有单词的反义词的 Trie。

```
1) Create an empty Trie.
2) Do following for every word:-
    a) Insert reverse of current word.
    b) Also store up to which index it is 
       a palindrome.
3) Traverse list of words again and do following 
   for every word.
    a) If it is available in Trie then return true
    b) If it is partially available
         Check the remaining word is palindrome or not 
         If yes then return true that means a pair
         forms a palindrome.
         Note: Position upto which the word is palindrome
               is stored because of these type of cases.
```

## C++

```
// C++ program to check if there is a pair that
// of above method using Trie
#include<bits/stdc++.h>
using namespace std;
#define ARRAY_SIZE(a) sizeof(a)/sizeof(a[0])

// Alphabet size (# of symbols)
#define ALPHABET_SIZE (26)

// Converts key current character into index
// use only 'a' through 'z' and lower case
#define CHAR_TO_INDEX(c) ((int)c - (int)'a')

// Trie node
struct TrieNode
{
    struct TrieNode *children[ALPHABET_SIZE];
    vector<int> pos; // To store palindromic
                     // positions in str
    int id;

    // isLeaf is true if the node represents
    // end of a word
    bool isLeaf;
};

// Returns new Trie node (initialized to NULLs)
struct TrieNode *getNode(void)
{
    struct TrieNode *pNode = new TrieNode;
    pNode->isLeaf = false;
    for (int i = 0; i < ALPHABET_SIZE; i++)
            pNode->children[i] = NULL;

    return pNode;
}

// Utility function to check if a string is a
// palindrome
bool isPalindrome(string str, int i, int len)
{
    // compare each character from starting
    // with its corresponding character from last
    while (i < len)
    {
        if (str[i] != str[len])
            return false;
        i++, len--;
    }

    return true;
}

// If not present, inserts reverse of key into Trie. If 
// the key is prefix of a Trie node, just mark leaf node
void insert(struct TrieNode* root, string key, int id)
{
    struct TrieNode *pCrawl = root;

    // Start traversing word from the last
    for (int level = key.length()-1; level >=0; level--)
    {
        // If it is not available in Trie, then
        // store it
        int index = CHAR_TO_INDEX(key[level]);
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        // If current word is palindrome till this
        // level, store index of current word.
        if (isPalindrome(key, 0, level))
            (pCrawl->pos).push_back(id);

        pCrawl = pCrawl->children[index];
    }
    pCrawl->id = id;
    pCrawl->pos.push_back(id);

    // mark last node as leaf
    pCrawl->isLeaf = true;
}

// Returns true if key presents in Trie, else false
void search(struct TrieNode *root, string key,
            int id, vector<vector<int> > &result)
{
    struct TrieNode *pCrawl = root;
    for (int level = 0; level < key.length(); level++)
    {
        int index = CHAR_TO_INDEX(key[level]);

        // If it is present also check upto which index
        // it is palindrome
        if (pCrawl->id >= 0 && pCrawl->id != id &&
            isPalindrome(key, level, key.size()-1))
            result.push_back({id, pCrawl->id});

        // If not present then return
        if (!pCrawl->children[index])
            return;

        pCrawl = pCrawl->children[index];
    }

    for (int i: pCrawl->pos)
    {
        if (i == id)
            continue;
        result.push_back({id, i});
    }
}

// Function to check if a palindrome pair exists
bool checkPalindromePair(vector <string> vect)
{
    // Construct trie
    struct TrieNode *root = getNode();
    for (int i = 0; i < vect.size(); i++)
        insert(root, vect[i], i);

    // Search for different keys
    vector<vector<int> > result;
    for (int i=0; i<vect.size(); i++)
    {
        search(root, vect[i], i, result);
        if (result.size() > 0)
           return true;
    }

    return false;
}

// Driver code
int main()
{
    vector <string> vect = {"geekf", "geeks", "or",
                            "keeg", "abc", "bc"};

    checkPalindromePair(vect)? cout << "Yes" :
                               cout << "No";
    return 0;
}

```

## Java 语言(一种计算机语言，尤用于创建网站)

```

//Java program to check if there is a pair that
//of above method using Trie
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class Palin_pair2 {

    // Alphabet size (# of symbols)
    static final int ALPHABET_SIZE = 26;

    // Trie node
    static class TrieNode {
        TrieNode[] children = new TrieNode[ALPHABET_SIZE];
        List<Integer> pos; // To store palindromic
                            // positions in str
        int id;

        // isLeaf is true if the node represents
        // end of a word
        boolean isLeaf;

        // constructor
        public TrieNode() {
            isLeaf = false;
            pos = new ArrayList<>();
            for (int i = 0; i < ALPHABET_SIZE; i++)
                children[i] = null;
        }
    }

    // Utility function to check if a string is a
    // palindrome
    static boolean isPalindrome(String str, int i, int len) {
        // compare each character from starting
        // with its corresponding character from last
        while (i < len) {
            if (str.charAt(i) != str.charAt(len))
                return false;

            i++;
            len--;
        }
        return true;
    }

    // If not present, inserts reverse of key into Trie. If
    // the key is prefix of a Trie node, just mark leaf node
    static void insert(TrieNode root, String key, int id) {
        TrieNode pCrawl = root;

        // Start traversing word from the last
        for (int level = key.length() - 1; level >= 0; level--) {
            // If it is not available in Trie, then
            // store it
            int index = key.charAt(level) - 'a';
            if (pCrawl.children[index] == null)
                pCrawl.children[index] = new TrieNode();

            // If current word is palindrome till this
            // level, store index of current word.
            if (isPalindrome(key, 0, level))
                (pCrawl.pos).add(id);

            pCrawl = pCrawl.children[index];
        }
        pCrawl.id = id;
        pCrawl.pos.add(id);

        // mark last node as leaf
        pCrawl.isLeaf = true;
    }

    // list to store result 
    static List<List<Integer>> result;

    // Returns true if key presents in Trie, else false
    static void search(TrieNode root, String key, int id) {
        TrieNode pCrawl = root;
        for (int level = 0; level < key.length(); level++) {
            int index = key.charAt(level) - 'a';

            // If it is present also check upto which index
            // it is palindrome
            if (pCrawl.id >= 0 && pCrawl.id != id
                    && isPalindrome(key, level, key.length() - 1)) {
                List<Integer> l = new ArrayList<>();
                l.add(id);
                l.add(pCrawl.id);
                result.add(l);
            }

            // If not present then return
            if (pCrawl.children[index] == null)
                return;

            pCrawl = pCrawl.children[index];
        }

        for (int i : pCrawl.pos) {
            if (i == id)
                continue;
            List<Integer> l = new ArrayList<>();
            l.add(id);
            l.add(i);
            result.add(l);
        }
    }

    // Function to check if a palindrome pair exists
    static boolean checkPalindromePair(List<String> vect) {

        // Construct trie
        TrieNode root = new TrieNode();
        for (int i = 0; i < vect.size(); i++)
            insert(root, vect.get(i), i);

        // Search for different keys
        result = new ArrayList<>();
        for (int i = 0; i < vect.size(); i++) {
            search(root, vect.get(i), i);

            if (result.size() > 0)
                return true;
        }

        return false;
    }

    // Driver code
    public static void main(String args[]) {
        List<String> vect = Arrays.asList("geekf", "geeks", 
                            "or", "keeg", "abc", "bc");

        if (checkPalindromePair(vect) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
//This code is contributed by Sumit Ghosh

```

## C#

```
// C# program to check if there is 
// a pair that of above method using Trie
using System;
using System.Collections.Generic;

class GFG
{

    // Alphabet size (# of symbols)
    static readonly int ALPHABET_SIZE = 26;

    // Trie node
    class TrieNode
    {
        public TrieNode[] children = new TrieNode[ALPHABET_SIZE];
        public List<int> pos; // To store palindromic
                              // positions in str
        public int id;

        // isLeaf is true if the node 
        // represents end of a word
        public Boolean isLeaf;

        // constructor
        public TrieNode()
        {
            isLeaf = false;
            pos = new List<int>();
            for (int i = 0; i < ALPHABET_SIZE; i++)
                children[i] = null;
        }
    }

    // Utility function to check if 
    // a string is a palindrome
    static Boolean isPalindrome(String str, 
                                int i, int len) 
    {
        // compare each character from starting
        // with its corresponding character from last
        while (i < len) 
        {
            if (str[i] != str[len])
                return false;

            i++;
            len--;
        }
        return true;
    }

    // If not present, inserts reverse of 
    // key into Trie. If the key is prefix of
    // a Trie node, just mark leaf node
    static void insert(TrieNode root, 
                       String key, int id)
    {
        TrieNode pCrawl = root;

        // Start traversing word from the last
        for (int level = key.Length - 1;
                 level >= 0; level--) 
        {
            // If it is not available in Trie, 
            // then store it
            int index = key[level] - 'a';
            if (pCrawl.children[index] == null)
                pCrawl.children[index] = new TrieNode();

            // If current word is palindrome till this
            // level, store index of current word.
            if (isPalindrome(key, 0, level))
                (pCrawl.pos).Add(id);

            pCrawl = pCrawl.children[index];
        }
        pCrawl.id = id;
        pCrawl.pos.Add(id);

        // mark last node as leaf
        pCrawl.isLeaf = true;
    }

    // list to store result 
    static List<List<int>> result;

    // Returns true if key presents 
    // in Trie, else false
    static void search(TrieNode root, 
                       String key, int id) 
    {
        TrieNode pCrawl = root;
        for (int level = 0; 
                 level < key.Length; level++) 
        {
            int index = key[level] - 'a';

            // If it is present also check 
            // upto which index it is palindrome
            if (pCrawl.id >= 0 && pCrawl.id != id && 
                isPalindrome(key, level, key.Length - 1)) 
            {
                List<int> l = new List<int>();
                l.Add(id);
                l.Add(pCrawl.id);
                result.Add(l);
            }

            // If not present then return
            if (pCrawl.children[index] == null)
                return;

            pCrawl = pCrawl.children[index];
        }

        foreach (int i in pCrawl.pos)
        {
            if (i == id)
                continue;
            List<int> l = new List<int>();
            l.Add(id);
            l.Add(i);
            result.Add(l);
        }
    }

    // Function to check if a palindrome pair exists
    static Boolean checkPalindromePair(List<String> vect)
    {

        // Construct trie
        TrieNode root = new TrieNode();
        for (int i = 0; i < vect.Count; i++)
            insert(root, vect[i], i);

        // Search for different keys
        result = new List<List<int>>();
        for (int i = 0; i < vect.Count; i++)
        {
            search(root, vect[i], i);

            if (result.Count > 0)
                return true;
        }
        return false;
    }

    // Driver code
    public static void Main(String []args) 
    {
        List<String> vect = new List<String>(){"geekf", "geeks", 
                                               "or", "keeg", 
                                               "abc", "bc"};

        if (checkPalindromePair(vect) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Rajput-Ji

```

**输出:**

```
Yes
```

时间复杂度:O(nk <sup>2</sup> )

其中 n 是列表中的字数，k 是检查回文的最大长度。
参考:[https://www.careercup.com/question?id=4879869638868992](https://www.careercup.com/question?id=4879869638868992)
本文由 [**萨哈布拉(akku)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。