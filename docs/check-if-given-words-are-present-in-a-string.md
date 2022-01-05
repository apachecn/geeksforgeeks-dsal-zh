# 检查字符串中是否存在给定的单词

> 原文:[https://www . geesforgeks . org/check-if-given-words-in-a-string/](https://www.geeksforgeeks.org/check-if-given-words-are-present-in-a-string/)

给定一个大字符串和一组小字符串，所有这些字符串的长度都小于大字符串。任务是创建一个布尔数组，其中每个布尔表示小字符串数组中该索引处的小字符串是否包含在大字符串中。

**注意:**说明不能使用语言内置的字符串匹配方法。

**示例:**

> **输入:** bigString =“这是一个大字符串”，small string =[“这”、“哟”、“是”、“一个”、“更大”、“字符串”、“kappa”]
> **输出:**【真、假、真、真、假、真、假】
> 
> **输入:** bigString =“玛丽每周都会去购物中心。”，small strings =[“to”、“Mary”、“centers”、“shop”、“shopping”、“string”、“kappa”]
> **输出:**【真、真、假、真、假、假】

**方法:天真的方法**
解决这个问题的一个简单方法是迭代所有的小字符串，通过迭代大字符串的字符并通过几个循环将它们与给定的小字符串的字符进行比较来检查它们中的每一个是否包含在大字符串中。

以下是上述方法的实现:

## C++

```
// Find the small string at that index in the array of
// small strings is contained in the big string
#include <bits/stdc++.h>
using namespace std;
bool isInBigString(string bigString, string smallString);
bool isInBigStringHelper(string bigString, string smallString, int startIdx);

// Function to the multiStringSearch
vector<bool> multiStringSearch(string bigString,
                          vector<string> smallStrings)
{
    vector<bool> solution;

    // iterate in the smallString
    for (string smallString : smallStrings) {

        // calling the isInBigString Function
        solution.push_back(isInBigString(bigString, smallString));
    }
    return solution;
}

// Function to the bigString
bool isInBigString(string bigString, string smallString)
{
    // iterate in the bigString
    for (int i = 0; i < bigString.length(); i++) {

        // Check if length of smallString + i is greater than
        // the length of bigString
        if (i + smallString.length() > bigString.length()) {
            break;
        }

        // call the function isInBigStringHelper
        if (isInBigStringHelper(bigString, smallString, i)) {
            return true;
        }
    }
    return false;
}

// Helper Function to the Finding bigString
bool isInBigStringHelper(string bigString, string smallString, int startIdx)
{
    // Initialize leftBigIdx and rightBigIdx and leftSmallIdx variables
    int leftBigIdx = startIdx;
    int rightBigIdx = startIdx + smallString.length() - 1;
    int leftSmallIdx = 0;
    int rightSmallIdx = smallString.length() - 1;

    // Iterate until leftBigIdx variable reaches less 
    // than or equal to rightBigIdx
    while (leftBigIdx <= rightBigIdx) {

        // Check if bigString[leftBigIdx] is not equal
        // to smallString[leftSmallIdx] or Check if 
        // bigString[rightBigIdx] is not equal to 
        // smallString[rightSmallIdx] than return false
        // otherwise increment leftBigIdx and leftSmallIdx
        // decrement rightBigIdx and rightSmallIdx
        if (bigString[leftBigIdx] != smallString[leftSmallIdx] || 
            bigString[rightBigIdx] != smallString[rightSmallIdx]) {
            return false;
        }

        leftBigIdx++;
        rightBigIdx--;
        leftSmallIdx++;
        rightSmallIdx--;
    }

    return true;
}

// Driver code
int main(int argc, char* argv[])
{
    // initialize string
    string str = "this is a big string";

    // initialize vector string

    vector<string> substr = { "this", "yo", "is", "a", 
                        "bigger", "string", "kappa" };

    // Function call
    vector<bool> ans = multiStringSearch(str, substr);

    // Print answers
    for (int i = 0; i < ans.size(); i++) {

        // Check if ans[i] is equal to 1
        // then Print true otherwise print false
        if (ans[i] == 1) {
            cout << "true"
                 << " ";
        }
        else {
            cout << "false"
                 << " ";
        }
    }
    return 0;
}
```

## 蟒蛇 3

```
# Find the small string at that index in the array of
# small strings is contained in the big string

# Helper Function to the Finding bigString
def isInBigStringHelper(bigString,smallString,startIdx):

    # Initialize leftBigIdx and rightBigIdx and leftSmallIdx variables
    leftBigIdx = startIdx
    rightBigIdx = startIdx + len(smallString) - 1
    leftSmallIdx = 0
    rightSmallIdx = len(smallString) - 1

    # Iterate until leftBigIdx variable reaches less 
    # than or equal to rightBigIdx
    while (leftBigIdx <= rightBigIdx):

        # Check if bigString[leftBigIdx] is not equal
        # to smallString[leftSmallIdx] or Check if 
        # bigString[rightBigIdx] is not equal to 
        # smallString[rightSmallIdx] than return false
        # otherwise increment leftBigIdx and leftSmallIdx
        # decrement rightBigIdx and rightSmallIdx
        if (bigString[leftBigIdx] != smallString[leftSmallIdx] or 
            bigString[rightBigIdx] != smallString[rightSmallIdx]):
            return False

        leftBigIdx += 1
        rightBigIdx -= 1
        leftSmallIdx += 1
        rightSmallIdx -= 1
    return True

# Function to the bigString
def isInBigString(bigString, smallString):

    # iterate in the bigString
    for i in range(len(bigString)):

        # Check if length of smallString + i is greater than
        # the length of bigString
        if (i + len(smallString) > len(bigString)):
            break

        # call the function isInBigStringHelper
        if (isInBigStringHelper(bigString, smallString, i)):
            return True
    return False

# Function to the multiStringSearch
def multiStringSearch(bigString, smallStrings):
    solution = []

    # iterate in the smallString
    for smallString in smallStrings:
        # calling the isInBigString Function
        solution.append(isInBigString(bigString, smallString))
    return solution

# Driver code
if __name__ == '__main__':
    # initialize string
    str1 = "this is a big string"

    # initialize vector string

    substr = ["this", "yo", "is", "a","bigger", "string", "kappa"]

    # Function call
    ans = multiStringSearch(str1, substr)

    # Print answers
    for i in range(len(ans)):
        # Check if ans[i] is equal to 1
        # then Print true otherwise print false
        if (ans[i] == 1):
            print("true",end = " ")
        else:
            print("false",end = " ")

# This code is contributed by Bhupendra_Singh
```

**输出:**

```
true false true true false true false

```

**时间复杂度:** O(b * n * s)，其中 b 为大串的长度，n 为小串的个数，s 为最长小串的长度。

**辅助空间:** O(n)

**方法:使用后缀 Trie**
构建一个包含所有大字符串后缀的[后缀-trie](https://www.geeksforgeeks.org/pattern-searching-using-suffix-tree/) 数据结构。然后，遍历所有的小字符串，检查它们是否包含在您创建的数据结构中。

下面是上述方法的实现:

```
// Find the small string at that index in the array of
// small strings is contained in the big string
#include <bits/stdc++.h>
using namespace std;
// Blueprint of the TrieNode
class TrieNode {
public:

    // Declaring children to be of <char, TrieNode> type
    // key will be of char type and mapped value will
    // be of TrieNode type
    unordered_map<char, TrieNode*> children;
};

// Blueprint of the ModifiedSuffixTrie
class ModifiedSuffixTrie {
public:
    TrieNode* root;
    ModifiedSuffixTrie(string str)
    {
        this->root = new TrieNode();

        // Function call 
        this->populateModifiedSuffixTrieFrom(str); 
    }

    void populateModifiedSuffixTrieFrom(string str)
    {
        // iterate in the length of String
        for (int i = 0; i < str.length(); i++) {

            // Function call 
            this->insertSubstringStartingAt(i, str); 
        }
    }

    void insertSubstringStartingAt(int i, string str)
    {
        TrieNode* node = this->root;

        // iterate in the length of String
        for (int j = i; j < str.length(); j++) {

            // initialize char as a letter
            // put the value of str[j] in letter
            char letter = str[j];

            // Check if letter is is equal to endnode or not
            if (node->children.find(letter) == node->children.end()) {
                TrieNode* newNode = new TrieNode();
                node->children.insert({ letter, newNode });
            }
            node = node->children[letter];
        }
    }

    bool contains(string str)
    {
        TrieNode* node = this->root;

        // iterate in the String
        for (char letter : str) {

            // Check if letter is is equal to endnode or not
            if (node->children.find(letter) == node->children.end()) {
                return false;
            }
            node = node->children[letter];
        }
        return true;
    }
};

// Function to the multiStringSearch
vector<bool> multiStringSearch(string bigString, vector<string> smallStrings)
{
    ModifiedSuffixTrie modifiedSuffixTrie(bigString);
    vector<bool> solution;

    // iterate in the smallString
    for (string smallString : smallStrings) {
        solution.push_back(modifiedSuffixTrie.contains(smallString));
    }
    return solution;
}

// Driver code
int main(int argc, char* argv[])
{
    // initialize string
    string str = "this is a big string";

    // initialize vector string
    vector<string> substr = { "this", "yo", "is", "a", 
                        "bigger", "string", "kappa" };

    // Function call
    vector<bool> ans = multiStringSearch(str, substr);

    // Print answers
    for (int i = 0; i < ans.size(); i++) {

        // Check if ans[i] is equal to 1
        // then Print true otherwise print false
        if (ans[i] == 1) {
            cout << "true"
                 << " ";
        }
        else {
            cout << "false"
                 << " ";
        }
    }
    return 0;
}
```

**输出:**

```
true false true true false true false

```

**时间复杂度:** O(b*b + n * s)，其中 b 为大串的长度，n 为小串的个数，s 为最长小串的长度。
**辅助空间:** O(b*2 + n)

**方法:使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/)**
尝试构建一个包含所有小字符串的 Trie。然后，遍历大字符串的字符，检查大字符串的任何部分是否是包含在您创建的 trie 中的字符串。

下面是上述方法的实现:

```
// Find the small string at that index in the array of
// small strings is contained in the big string
#include <bits/stdc++.h>
using namespace std;

// Blueprint of the TrieNode
class TrieNode {
public:

    // Declaring children to be of <char, TrieNode> type
    // key will be of char type and mapped value will
    // be of TrieNode type
    unordered_map<char, TrieNode*> children;
    string word;
};

// Blueprint of the Trie
class Trie {
public:
    TrieNode* root;
    char endSymbol;
    Trie()
    {
        this->root = new TrieNode();
        this->endSymbol = '*';
    }

    // function to insert string
    void insert(string str)
    {
        TrieNode* current = this->root;

        // iterate in the length of String
        for (int i = 0; i < str.length(); i++) {

            // initialize char as a letter
            // put the value of str[i] in letter
            char letter = str[i];

            // Check if letter is is equal to endnode or not
            if (current->children.find(letter) == current->children.end()) {
                TrieNode* newNode = new TrieNode();
                current->children.insert({ letter, newNode });
            }
            current = current->children[letter];
        }
        current->children.insert({ this->endSymbol, NULL });
        current->word = str;
    }
};

// define a findSmallStringsIn function
void findSmallStringsIn(string str, int startIdx, Trie* trie, 
                   unordered_map<string, bool>* containedStrings);

// Function to the multiStringSearch
vector<bool> multiStringSearch(string bigString, vector<string> smallStrings)
{
    Trie* trie = new Trie();

    // iterate in the smallString
    for (string smallString : smallStrings) {
        trie->insert(smallString);
    }

    // Declaring containedStrings to be of <string, bool> type
    // key will be of string type and mapped value will
    // be of boolean type
    unordered_map<string, bool> containedStrings;

    // iterate in the bigString
    for (int i = 0; i < bigString.length(); i++) {
        findSmallStringsIn(bigString, i, trie, &containedStrings);
    }

    vector<bool> solution;

    // iterate in the smallString
    for (string smallString : smallStrings) {
        solution.push_back(containedStrings.find(smallString) 
                                   != containedStrings.end());
    }
    return solution;
}

// Function to findSmallStringsIn
void findSmallStringsIn(string str, int startIdx, 
    Trie* trie, unordered_map<string, bool>* containedStrings)
{
    TrieNode* currentNode = trie->root;

    // iterate the length of the string
    for (int i = startIdx; i < str.length(); i++) {

        // Check if letter is is equal to endnode or not
        if (currentNode->children.find(str[i]) ==
                          currentNode->children.end()) {
            break;
        }
        currentNode = currentNode->children[str[i]];

        if (currentNode->children.find(trie->endSymbol) != 
                             currentNode->children.end()) {
            containedStrings->insert({ currentNode->word, true });
        }
    }
}

// Driver code
int main(int argc, char* argv[])
{
    // initialize string
    string str = "this is a big string";

    // initialize vector string
    vector<string> substr = { "this", "yo", "is", "a",
                         "bigger", "string", "kappa" };

    // Function call
    vector<bool> ans = multiStringSearch(str, substr);

    // Print answers
    for (int i = 0; i < ans.size(); i++) {

        // Check if ans[i] is equal to 1
        // then Print true otherwise print false
        if (ans[i] == 1) {
            cout << "true"
                 << " ";
        }
        else {
            cout << "false"
                 << " ";
        }
    }
    return 0;
}
```

**输出:**

```
true false true true false true false

```

**时间复杂度:** O(n*s + b * s)，其中 b 为大串的长度，n 为小串的个数，s 为最长小串的长度。
**辅助空间:**奥(ns)