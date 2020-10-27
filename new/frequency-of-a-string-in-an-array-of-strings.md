# 字符串数组中字符串的频率

您会得到一个字符串集合和一个查询列表。 对于每个查询，都有一个字符串。 我们需要打印给定字符串在字符串集合中出现的次数。
**范例：**

```
Input : arr[] = {wer, wer, tyu, oio, tyu}
        q[] =   {wer, tyu, uio}
Output : 2 2 0
Explanation : 
q[0] appears two times in arr[], q1[] appears

```

#### **方法 1（简单）**

这个想法很简单，对于每个查询字符串，我们都将其与数组中给出的所有字符串进行比较。 如果查询字符串匹配，我们将增加计数。

## C++

```cpp

// C++ program to find number of times a 
// string appears in an array.
#include<bits/stdc++.h>
using namespace std;

// Returns count of occurrences of s in arr[] 
int search(string arr[], string s, int n)
{
    int counter = 0;

    for(int j = 0; j < n; j++)

        // Checking if string given in query
        // is present in the given string. 
        // If present, increase times
        if (s == arr[j])
            counter++;

   return counter;
}

void answerQueries(string arr[], string q[], 
                   int n, int m)
{
    for(int i = 0; i < m; i++)
        cout << search(arr, q[i], n) << " ";
}    

// Driver Code
int main()
{
    string arr[] = { "aba", "baba", 
                     "aba", "xzxb" };
    string q[]   = { "aba", "xzxb", "ab" };

    int n = sizeof(arr) / sizeof(arr[0]);
    int m = sizeof(q) / sizeof(q[0]);

    answerQueries(arr, q, n, m);
}

// This code is contributed by rutvik_56

```

## Java

```java

// Java program to find number of times a string
// appears in an array.
class SubString
{
    /* Returns count of occurrences of s in arr[] */
    static int search(String[]arr, String s)
    {
            int counter = 0;
            for (int j = 0; j < arr.length; j++)

                /* checking if string given in query is
                  present in the given string. If present,
                  increase times*/
                if (s.equals(arr[j]))
                    counter++;

           return counter;
    }

    static void answerQueries(String[] arr, String q[])
    {
        for (int i=0;i<q.length; i++)
            System.out.print(search(arr, q[i]) + " ");
    }

    /* driver code*/
    public static void main(String[] args) {

        String[] arr = {"aba","baba","aba","xzxb"};
        String[] q   = {"aba","xzxb","ab"};
        answerQueries(arr, q);
    }
}

```

## Python3

```py

# Python3 program to find number of 
# times a string appears in an array.

# Returns count of occurrences of s in arr[] 
def search(arr, s):
    counter = 0
    for j in range(len(arr)):

        # checking if string given in query 
        # is present in the given string.  
        # If present, increase times
        if (s == (arr[j])):
            counter += 1

    return counter

def answerQueries(arr, q):
    for i in range(len(q)):
        print(search(arr, q[i]), 
                     end = " ")

# Driver code
if __name__ == '__main__':
    arr = ["aba", "baba", "aba", "xzxb"]
    q = ["aba", "xzxb", "ab"]
    answerQueries(arr, q)

# This code is contributed 
# by PrinciRaj19992

```

## C#

```cs

// C# program to find number of 
// times a string appears in an array.
using System;

class SubString
{
    /* Returns count of occurrences of s in arr[] */
    static int search(String[]arr, String s)
    {
            int counter = 0;
            for (int j = 0; j < arr.Length; j++)

                /* checking if string given in query is
                present in the given string. If present,
                increase times*/
                if (s.Equals(arr[j]))
                    counter++;

        return counter;
    }

    static void answerQueries(String []arr, String []q)
    {
        for (int i = 0; i < q.Length; i++)
            Console.Write(search(arr, q[i]) + " ");
    }

    // Driver code
    public static void Main() 
    {
        String []arr = {"aba","baba","aba","xzxb"};
        String []q = {"aba","xzxb","ab"};
        answerQueries(arr, q);
    }
}

//This code is contributed by nitin mittal

```

## PHP

```php

<?php
# Php program to find number of 
# times a string appears in an array.

# Returns count of occurrences of s in arr[] 
function search($arr, $s)
{
    $counter = 0;
    for ($j=0; $j<count($arr); $j++)
    {
        # checking if string given in query 
        # is present in the given string. 
        # If present, increase times
        if ($s == ($arr[$j]))
            $counter += 1;
    }
    return $counter;
}
function answerQueries($arr, $q)
{
    for ($i=0; $i<count($q); $i++)
    {
        echo(search($arr, $q[$i]));
        echo (" ");
    }
}

# Driver code

$arr = array("aba", "baba", "aba", "xzxb");
$q = array("aba", "xzxb", "ab");
answerQueries($arr, $q);

# This code is contributed 
# by Shivi_Aggarwal
?>

```

**输出：**

```
2 1 0 

```

#### **方法 2（使用 Trie）**

[Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 一种有效的数据结构，用于增强和检索类似字符串的数据。 搜索复杂度是最佳的密钥长度。
在此解决方案中，我们将字符串集合插入到 Trie 数据结构中，以便将它们存储在其中。 一件重要的事情是，我们要统计叶节点中的出现次数。 然后，在 Trie 中搜索给定的查询字符串，并检查 Trie 中是否存在该字符串。

## CPP

```

// C++ program to count number of times
// a string appears in an array of strings
#include<iostream>
using namespace std;

const int MAX_CHAR = 26;

struct Trie
{
    // To store number of times
    // a string is present. It is
    // 0 is string is not present
    int cnt;

    Trie *node[MAX_CHAR];
    Trie()
    {
        for(int i=0; i<MAX_CHAR; i++)
            node[i] = NULL;
        cnt = 0;
    }
};

/* function to insert a string into the Trie*/
Trie *insert(Trie *root,string s)
{
    Trie *temp = root;
    int n = s.size();
    for(int i=0; i<n; i++)
    {
        /*calculation ascii value*/
        int index = s[i]-'a';

        /* If the given node is not already
          present in the Trie than create
          the new node*/
        if (!root->node[index])
            root->node[index] = new Trie();

        root = root->node[index];
    }
    root->cnt++;
    return temp;
}

/* Returns count of occurrences of s in Trie*/
int search(Trie *root, string s)
{
    int n = s.size();
    for (int i=0; i<n; i++)
    {
        int index = s[i]-'a';
        if (!root->node[index])
            return 0;
        root = root->node[index];
    }
    return root->cnt;
}

void answerQueries(string arr[], int n, string q[],
                                           int m)
{
    Trie *root = new Trie();

    /* inserting in Trie */
    for (int i=0; i<n; i++)
        root = insert(root,arr[i]);

    /* searching the strings in Trie */
    for (int i=0; i<m; i++)
        cout << search(root, q[i]) << " ";

}

/* Driver code */
int main()
{
    string arr[] = {"aba","baba","aba","xzxb"};
    int n = sizeof(arr)/sizeof(arr[0]);

    string q[] = {"aba","xzxb","ab"};
    int m = sizeof(q)/sizeof(q[0]);

    answerQueries(arr, n, q, m);

    return 0;
}

```

**输出：**

```
2
1
0

```

#### **方法 3（哈希）**

我们可以使用[哈希图](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)并将所有给定的字符串插入其中。 对于每个查询字符串，我们只需要在哈希图中进行查找即可。
请参考[字典的数据结构](https://www.geeksforgeeks.org/data-structure-dictionary-spell-checker/)，以比较基于哈希和基于 Trie 的解决方案。
本文由 **Pranav** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，您还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想共享有关上述主题的更多信息，请发表评论。

