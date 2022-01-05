# 使用 C++中的无序 _map 检查两个字符串是否是彼此的字谜

> 原文:[https://www . geeksforgeeks . org/check-two-string-是否是彼此的字谜-使用-无序 _map-in-c/](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagrams-of-each-other-using-unordered_map-in-c/)

编写一个函数来检查两个给定的字符串是否是彼此的**字谜**。

字符串的字谜是另一个包含相同字符的字符串，只有字符的顺序可以不同。

> **例如，“abcd”和“dabc”是彼此的字谜。**

![check-whether-two-strings-are-anagram-of-each-other](img/44eca765d93a8501e9332cab7ddb74ba.png)

**方法:** [无序图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)也可以用来查找任意两个给定的字符串是否是字谜。其思想是将第一个字符串的每个字符存储在地图中，以其频率作为值，然后检查地图中第二个字符串的每个字符，如果在地图中找到该字符，则从地图中减少其频率值。如果一个字符的出现频率为 0，将其从映射中删除，最后如果映射为空，这意味着第一个字符串中的所有字符在第二个字符串中出现的次数(每个字符的出现频率)相同。

**实施:**

```
// C++ program to check whether
// two strings are anagrams of
// each other or not, using Hashmap

#include <bits/stdc++.h>
#include <unordered_map>
using namespace std;

// Function to check whether two strings
// are an anagram of each other
bool isanagram(string s1, string s2)
{
    int l1 = s1.length();
    int l2 = s2.length();

    unordered_map<char, int> m;
    if (l1 != l2) {
        return false;
    }
    for (int i = 0; i < l1; i++) {
        m[s1[i]]++;
    }

    for (int i = 0; i < l2; i++) {
        if (m.find(s2[i]) == m.end()) {
            return false;
        }
        else {
            m[s2[i]]--;
            if (m[s2[i]] == 0) {
                m.erase(s2[i]);
            }
        }
    }
    return m.size() == 0;
}

// Test function
void test(string str1, string str2)
{

    cout << "Strings to be checked:\n"
         << str1 << "\n"
         << str2 << "\n";

    if (isanagram(str1, str2)) {
        cout << "The two strings are"
             << "anagram of each other\n";
    }
    else {
        cout << "The two strings are not"
             << " anagram of each other\n";
    }
    cout << endl;
}

// Driver program
int main()
{
    // Get the Strings
    string str1 = "geeksforgeeks";
    string str2 = "forgeeksgeeks";

    // Test the Strings
    test(str1, str2);

    // Get the Strings
    str1 = "geeksforgeeks";
    str2 = "geeks";

    // Test the Strings
    test(str1, str2);
    return 0;
}
```

**Output:**

```
Strings to be checked:
geeksforgeeks
forgeeksgeeks
The two strings areanagram of each other

Strings to be checked:
geeksforgeeks
geeks
The two strings are not anagram of each other

```

**相关文章:**

*   [检查两个字符串是否是彼此的字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)
*   [使用 Java 中的 HashMap](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other-using-hashmap-in-java/) 检查两个字符串是否是彼此的字谜