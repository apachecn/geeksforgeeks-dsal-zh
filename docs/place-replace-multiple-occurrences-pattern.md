# 原位替换一个模式的多次出现

> 原文:[https://www . geeksforgeeks . org/place-replace-多次出现-pattern/](https://www.geeksforgeeks.org/place-replace-multiple-occurrences-pattern/)

给定一个字符串和一个模式，用字符“X”替换模式的多次出现。转换应该到位，并且解决方案应该用单个“X”替换一个模式的多个连续(且不重叠)出现。

```
String – GeeksForGeeks
Pattern – Geeks
Output: XforX

String – GeeksGeeks
Pattern – Geeks
Output: X

String – aaaa
Pattern – aa
Output: X

String – aaaaa
Pattern – aa
Output: Xa
```

这个想法是保持两个索引 I 和 j 用于就地替换。索引 I 总是指向输出字符串中的下一个字符。索引 j 遍历字符串并搜索一个或多个模式匹配。如果找到匹配，我们将字符‘X’放在索引 I 处，并将索引 I 增加 1，将索引 j 增加模式长度。如果我们发现模式多次连续出现，索引 I 只增加一次。如果没有找到模式，我们将索引 j 处的当前字符复制到索引 I，并将 I 和 j 都增加 1。由于模式长度总是大于等于 1，替换长度只有 1 个字符，我们永远不会覆盖未处理的字符，即 j >= i 是不变的。

## C++

```
// C++ program to in-place replace multiple
// occurrences of a pattern by character ‘X’
#include <bits/stdc++.h>
using namespace std;

// returns true if pattern is prefix of str
bool compare(char* str, char* pattern)
{
    for (int i = 0; pattern[i]; i++)
        if (str[i] != pattern[i])
            return false;
    return true;
}

// Function to in-place replace multiple
// occurrences of a pattern by character ‘X’
void replacePattern(char* str, char* pattern)
{
    // If pattern is null or empty string,
    // nothing needs to be done
    if (pattern == NULL)
        return;

    int len = strlen(pattern);
    if (len == 0)
        return;

    int i = 0, j = 0;
    int count;

    // for each character
    while (str[j]) {
        count = 0;

        // compare str[j..j+len] with pattern
        while (compare(str + j, pattern)) {
            // increment j by length of pattern
            j = j + len;
            count++;
        }

        // If single or multiple occurrences of pattern
        // is found, replace it by character 'X'
        if (count > 0)
            str[i++] = 'X';

        // copy character at current position j
        // to position i and increment i and j
        if (str[j])
            str[i++] = str[j++];
    }

    // add a null character to terminate string
    str[i] = '\0';
}

// Driver code
int main()
{
    char str[] = "GeeksforGeeks";
    char pattern[] = "Geeks";

    replacePattern(str, pattern);
    cout << str;

    return 0;
}
```

**Output:** 

```
XforX
```

上述算法的时间复杂度为 O(n*m)，其中 n 为字符串长度，m 为模式长度。
**使用 STL 实现**

```
The idea of this implementation is to use the STL in-built functions 
to search for pattern string in main string and then erasing it 
from the main string
```

## C++

```
// C++ program to in-place replace multiple
// occurrences of a pattern by character ‘X’
#include <bits/stdc++.h>
using namespace std;

// Function to in-place replace multiple
// occurrences of a pattern by character ‘X’
void replacePattern(string str, string pattern)
{

    // making an iterator for string str
    string::iterator it = str.begin();
    // run this loop until iterator reaches end of string
    while (it != str.end()) {
        // searching the first index in string str where
        // the first occurrence of string pattern occurs
        it = search(str.begin(), str.end(), pattern.begin(), pattern.end());
        // checking if iterator is not pointing to end of the
        // string str
        if (it != str.end()) {
            // erasing the full pattern string from that iterator
            // position in string str
            str.erase(it, it + pattern.size());
            // inserting 'X' at that iterator position
            str.insert(it, 'X');
        }
    }

    // this loop removes consecutive 'X' in string s
    // Example: GeeksGeeksforGeeks was changed to 'XXforX'
    // running this loop will change it to 'XforX'
    for (int i = 0; i < str.size() - 1; i++) {
        if (str[i] == 'X' && str[i + 1] == 'X') {
            // removing 'X' at position i in string str
            str.erase(str.begin() + i);
            i--; // i-- because one character was deleted
            // so repositioning i
        }
    }
    cout << str;
}

// Driver code
int main()
{
    string str = "GeeksforGeeks";
    string pattern = "Geeks";

    replacePattern(str, pattern);

    return 0;
}
```

**Output:** 

```
XforX
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息