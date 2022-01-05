# 从字符串中删除重复的单词

> 原文:[https://www . geesforgeks . org/remove-replicaterepeated-words-string/](https://www.geeksforgeeks.org/remove-duplicaterepeated-words-string/)

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {
  public static void main(String[] args) {

        System.out.println("Enter The String : ");
        String str = "geeksforgeeks";
        StringBuffer sb = new StringBuffer();
        str.chars().distinct().forEach(c -> sb.append((char) c));
        String DuplicateString = sb.toString();
        System.out.println("String after duplicates removed :"+DuplicateString);
    }
}
```

给定一个字符串，我们必须从字符串中删除所有重复的单词。
示例:

> 输入:str = " Geeks for Geeks A Computer Science portal for Geeks "
> 输出:Geeks for A Computer Science portal
> 解释:这里的“Geeks”和“for”是重复的，因此这些单词从字符串中删除
> 
> 输入:“在 Geeks for Geeks 上发布自己的文章，并与世界分享你的知识”
> 输出:在 GeeksforGeeks 上发布自己的文章，并与世界分享知识
> 解释:这里的“your”是重复的单词，因此单词从字符串中删除

我们创建一个空哈希表。然后在空格周围拆分给定的字符串。对于每个单词，我们首先检查它是否在哈希表中。如果在哈希表中找不到，我们就打印出来存储在哈希表中。
要将给定的字符串拆分成单词，我们在 C++中使用 [stringstream。](https://www.geeksforgeeks.org/stringstream-c-applications/)T3】

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to remove duplicate
// word from string
#include <bits/stdc++.h>
using namespace std;

void removeDupWord(string str)
{
    // Used to split string around spaces.
    istringstream ss(str);

    // To store individual visited words
    unordered_set<string> hsh;

    // Traverse through all words
    do
    {
        string word;
        ss >> word;

        // If current word is not seen before.
        while (hsh.find(word) == hsh.end()) {
            cout << word << " ";
            hsh.insert(word);
        }

    } while (ss);
}

// Driver function
int main()
{
    string str = "Geeks for Geeks A Computer"
                " Science portal for Geeks";
    removeDupWord(str);
    return 0;
}
```

**Output:** 

```
Geeks for A Computer Science portal
```