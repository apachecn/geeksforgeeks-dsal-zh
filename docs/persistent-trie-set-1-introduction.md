# 持久 Trie |第 1 集(简介)

> 原文:[https://www . geesforgeks . org/persistent-trie-set-1-introduction/](https://www.geeksforgeeks.org/persistent-trie-set-1-introduction/)

**先决条件:**

1.  排序
2.  [数据结构的持久性](https://www.geeksforgeeks.org/persistent-data-structures/)

Trie 是一种方便的数据结构，在执行多个字符串查找时经常用到。在这篇文章中，我们将在这个数据结构中引入持久性的概念。坚持仅仅意味着保留改变。但是很明显，保留更改会导致额外的内存消耗，从而影响时间复杂度。

我们的目标是在 trie 中应用持久性，并确保它不会超过标准的 Trie 搜索，即**O(key _ length)**。我们还将分析持久性导致的超过 Trie 标准空间复杂性的额外空间复杂性。

让我们从版本的角度来考虑，也就是说，对于我们的 Trie 中的每个更改/插入，我们都会创建一个新版本。
我们将考虑我们的初始版本为版本-0。现在，当我们在 trie 中进行任何插入时，我们将为它创建一个新版本，并以类似的方式跟踪所有版本的记录。

但是每次为每个版本创建整个 trie 会使内存加倍，并严重影响空间复杂度。所以，这个想法对于大量版本来说很容易耗尽内存。

让我们利用这样一个事实:对于 trie 中的每个新插入，将访问/修改确切的 **X** (length_of_key)节点。所以，我们的新版本将只包含这些 **X** 新节点，其余三个节点将与上一版本相同。因此，很明显，对于每个新版本，我们只需要创建这些 **X** 新节点，而其余的 trie 节点可以从以前的版本中共享。

考虑下图以获得更好的可视化效果:

![](img/26023ac9ed9e8c435e4b029da192fd82.png)

**现在，问题来了:如何跟踪所有版本？**
我们只需要跟踪所有版本的第一个根节点，这将用于跟踪不同版本中所有新创建的节点，因为根节点为我们提供了特定版本的入口点。为此，我们可以为所有版本维护一个指向 trie 根节点的指针数组。

> *我们来考虑一下下面的场景，看看如何使用 Persistent Trie 来解决！*
> 给定一个字符串数组，我们需要确定一个字符串是否存在于数组中的某个
> 范围【l，r】内。举个例子，假设数组是字典中第 1 页的单词列表
> (I 是数组的索引)
> 我们需要确定给定的单词 X 是否存在于页面范围[l，r]中？

**以下是上述问题的实现:-**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Distinct numbers of chars in key
const int sz = 26;

// Persistent Trie node structure
struct PersistentTrie {

    // Stores all children nodes, where ith children denotes
    // ith alphabetical character
    vector<PersistentTrie*> children;

    // Marks the ending of the key
    bool keyEnd = false;

    // Constructor 1
    PersistentTrie(bool keyEnd = false)
    {
        this->keyEnd = keyEnd;
    }

    // Constructor 2
    PersistentTrie(vector<PersistentTrie*>& children, bool keyEnd = false)
    {
        this->children = children;
        this->keyEnd = keyEnd;
    }

    // detects existence of key in trie
    bool findKey(string& key, int len);

    // Inserts key into trie
    // returns new node after insertion
    PersistentTrie* insert(string& key, int len);
};

// Dummy PersistentTrie node
PersistentTrie* dummy;

// Initialize dummy for easy implementation
void init()
{
    dummy = new PersistentTrie(true);

    // All children of dummy as dummy
    vector<PersistentTrie*> children(sz, dummy);
    dummy->children = children;
}

// Inserts key into current trie
// returns newly created trie node after insertion
PersistentTrie* PersistentTrie::insert(string& key, int len)
{

    // If reached the end of key string
    if (len == key.length()) {

        // Create new trie node with current trie node
        // marked as keyEnd
        return new PersistentTrie((*this).children, true);
    }

    // Fetch current child nodes
    vector<PersistentTrie*> new_version_PersistentTrie = (*this).children;

    // Insert at key[len] child and
    // update the new child node
    PersistentTrie* tmpNode = new_version_PersistentTrie[key[len] - 'a'];
    new_version_PersistentTrie[key[len] - 'a'] = tmpNode->insert(key, len + 1);

    // Return a new node with modified key[len] child node
    return new PersistentTrie(new_version_PersistentTrie);
}

// Returns the presence of key in current trie
bool PersistentTrie::findKey(string& key, int len)
{
    // If reached end of key
    if (key.length() == len)

        // Return if this is a keyEnd in trie
        return this->keyEnd;

    // If we cannot find key[len] child in trie
    // we say key doesn't exist in the trie
    if (this->children[key[len] - 'a'] == dummy)
        return false;

    // Recursively search the rest of
    // key length in children[key] trie
    return this->children[key[len] - 'a']->findKey(key, len + 1);
}

// dfs traversal over the current trie
// prints all the keys present in the current trie
void printAllKeysInTrie(PersistentTrie* root, string& s)
{
    int flag = 0;
    for (int i = 0; i < sz; i++) {
        if (root->children[i] != dummy) {
            flag = 1;
            s.push_back('a' + i);
            printAllKeysInTrie(root->children[i], s);
            s.pop_back();
        }
    }
    if (flag == 0 and s.length() > 0)
        cout << s << endl;
}

// Driver code
int main(int argc, char const* argv[])
{

    // Initialize the PersistentTrie
    init();

    // Input keys
    vector<string> keys({ "goku", "gohan", "goten", "gogeta" });

    // Cache to store trie entry roots after each insertion
    PersistentTrie* root[keys.size()];

    // Marking first root as dummy
    root[0] = dummy;

    // Inserting all keys
    for (int i = 1; i <= keys.size(); i++) {

        // Caching new root for ith version of trie
        root[i] = root[i - 1]->insert(keys[i - 1], 0);
    }

    int idx = 3;
    cout << "All keys in trie after version - " << idx << endl;
    string key = "";
    printAllKeysInTrie(root[idx], key);

    string queryString = "goku";
    int l = 2, r = 3;
    cout << "range : "
         << "[" << l << ", " << r << "]" << endl;
    if (root[r]->findKey(queryString, 0) and !root[l - 1]->findKey(queryString, 0))
        cout << queryString << " - exists in above range" << endl;
    else
        cout << queryString << " - does not exist in above range" << endl;

    queryString = "goten";
    l = 2, r = 4;
    cout << "range : "
         << "[" << l << ", " << r << "]" << endl;
    if (root[r]->findKey(queryString, 0) and !root[l - 1]->findKey(queryString, 0))
        cout << queryString << " - exists in above range" << endl;
    else
        cout << queryString << " - does not exist in above range" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

// Persistent Trie node structure
class PersistentTrie
{

    // Stores all children nodes, where
    // ith children denotes ith
    // alphabetical character
    PersistentTrie[] children;

    // Marks the ending of the key
    boolean keyEnd = false;

    // Constructor 1
    PersistentTrie(boolean keyEnd)
    {
        this.keyEnd = keyEnd;
    }

    // Constructor 2
    PersistentTrie(PersistentTrie[] children,
                   boolean keyEnd)
    {
        this.children = children;
        this.keyEnd = keyEnd;
    }

    // Detects existence of key in trie
    boolean findKey(String key, int len,
                    PersistentTrie dummy)
    {

        // If reached end of key
        if (key.length() == len)

            // Return if this is a keyEnd in trie
            return this.keyEnd;

        // If we cannot find key[len] child in trie
        // we say key doesn't exist in the trie
        if (this.children[key.charAt(len) - 'a'] == dummy)
            return false;

        // Recursively search the rest of
        // key length in children[key] trie
        return this.children[key.charAt(len) - 'a'].findKey(
            key, len + 1, dummy);
    }

    // Inserts key into trie
    // returns new node after insertion
    PersistentTrie insert(String key, int len)
    {

        // If reached the end of key string
        if (len == key.length())
        {

            // Create new trie node with current trie node
            // marked as keyEnd
            return new PersistentTrie(this.children.clone(),
                                      true);
        }

        // Fetch current child nodes
        PersistentTrie[] new_version_PersistentTrie
            = this.children.clone();

        // Insert at key[len] child and
        // update the new child node
        PersistentTrie tmpNode
            = new_version_PersistentTrie[key.charAt(len)
                                         - 'a'];
        new_version_PersistentTrie[key.charAt(len) - 'a']
            = tmpNode.insert(key, len + 1);

        // Return a new node with modified key[len] child
        // node
        return new PersistentTrie(
            new_version_PersistentTrie, false);
    }
}

class GFG{

static final int sz = 26;

// Dummy PersistentTrie node
static PersistentTrie dummy;

// Initialize dummy for easy implementation
static void init()
{
    dummy = new PersistentTrie(false);

    // All children of dummy as dummy
    PersistentTrie[] children = new PersistentTrie[sz];
    for(int i = 0; i < sz; i++)
        children[i] = dummy;

    dummy.children = children;
}

// dfs traversal over the current trie
// prints all the keys present in the current trie
static void printAllKeysInTrie(PersistentTrie root,
                               String s)
{
    int flag = 0;
    for(int i = 0; i < sz; i++)
    {
        if (root.children[i] != dummy)
        {
            flag = 1;
            printAllKeysInTrie(root.children[i],
                               s + ((char)('a' + i)));
        }
        if (root.children[i].keyEnd)
            System.out.println(s + (char)('a' + i));
    }
}

// Driver code
public static void main(String[] args)
{

    // Initialize the PersistentTrie
    init();

    // Input keys
    List<String> keys = Arrays.asList(new String[]{
        "goku", "gohan", "goten", "gogeta" });

    // Cache to store trie entry roots after each
    // insertion
    PersistentTrie[] root
        = new PersistentTrie[keys.size() + 1];

    // Marking first root as dummy
    root[0] = dummy;

    // Inserting all keys
    for(int i = 1; i <= keys.size(); i++)
    {

        // Caching new root for ith version of trie
        root[i]
            = root[i - 1].insert(keys.get(i - 1), 0);
    }

    int idx = 3;
    System.out.println("All keys in trie " +
                       "after version - " + idx);
    String key = "";

    printAllKeysInTrie(root[3], key);

    String queryString = "goku";

    int l = 2, r = 3;
    System.out.println("range : " + "[" + l +
                       ", " + r + "]");

    if (root[r].findKey(queryString, 0, dummy) &&
       !root[l - 1].findKey(queryString, 0, dummy))
        System.out.println(queryString +
                           " - exists in above range");
    else
        System.out.println(queryString +
                           " - does not exist in " +
                           "above range");

    queryString = "goten";
    l = 2;
    r = 4;
    System.out.println("range : " + "[" + l +
                       ", " + r + "]");

    if (root[r].findKey(queryString, 0, dummy) &&
       !root[l - 1].findKey(queryString, 0, dummy))
        System.out.println(queryString +
                           " - exists in above range");
    else
        System.out.println(queryString +
                           " - does not exist in above range");
}
}

// This code is contributed by jithin
```

**Output:** 

```
All keys in trie after version - 3
gohan
goku
goten
range : [2, 3]
goku - does not exist in above range
range : [2, 4]
goten - exists in above range
```

**时间复杂度:**如上所述，我们将在插入时访问 trie 中所有的 **X** (密钥长度)个节点；因此，我们将访问 X 个状态，并且在每个状态下，我们将通过为新创建的 trie 节点使用当前版本来喜欢上一版本的 sz 子节点，从而完成 **O(sz)** 数量的工作。因此，插入的时间复杂度变为**0(密钥长度* sz)** 。但是搜索在要搜索的关键字的长度上仍然是线性的，因此，搜索关键字的时间复杂度仍然是**0(关键字的长度)**，就像标准的 trie 一样。
**空间复杂性:**显然，数据结构的持久性伴随着空间的交易，我们将消耗更多的内存来维护 trie 的不同版本。现在，让我们想象一下最坏的情况——对于插入，我们正在创建 **O(length_of_key)** 节点，每个新创建的节点将占用 **O(sz)** 的空间来存储其子节点。因此，插入上述实现的空间复杂度是**0(密钥长度* sz)。**