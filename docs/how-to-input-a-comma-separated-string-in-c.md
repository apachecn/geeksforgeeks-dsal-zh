# 如何在 C++中输入逗号分隔的字符串？

> 原文:[https://www . geesforgeks . org/how-to-input-a-逗号分隔字符串 in-c/](https://www.geeksforgeeks.org/how-to-input-a-comma-separated-string-in-c/)

给定一个用逗号而不是空格分隔的输入字符串，任务是用 C++解析这个输入字符串。
首先，让我们了解一下如果输入字符串是逗号分隔的，会产生什么不同。
**<u>用 C++输入一个空格分隔的字符串</u>**
用 c++输入一个空格分隔的字符串非常容易。这样做的程序是:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string str;

    // Get the string
    getline(cin, str);

    // Print the words
    cout << str;
}
```

**Input:** 

```
1 2 3 4 5 6
```

**输出:**

```
1
2
3
4
5
6
```

**<u>为什么不能用上面的代码进行逗号分隔的输入字符串？</u>**
上面的代码对于空格分隔的输入字符串可以正常工作，但是对于逗号分隔的输入字符串，它不会像预期的那样工作，因为程序会将完整的输入作为字符串中的单个单词。

**Input:** 

```
1, 2, 3, 4, 5, 6
```

**输出:**

```
1, 2, 3, 4, 5, 6
```

**<u>如何输入逗号分隔的字符串？</u>**
现在为了输入逗号分隔的字符串，可以使用以下方法:

1.  在[字符串流](https://www.geeksforgeeks.org/stringstream-c-applications/)中获取要作为输入的字符串
2.  从流中逐个取出字符串的每个字符
3.  检查该字符是否为逗号('，')。
4.  如果是，则忽略该字符。
5.  否则，将该字符插入存储单词的向量中

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to input
// a comma separated string

#include <bits/stdc++.h>
using namespace std;

int main()
{
    // Get the string
    string str = "11,21,31,41,51,61";

    vector<int> v;

    // Get the string to be taken
    // as input in stringstream
    stringstream ss(str);

    // Parse the string
    for (int i; ss >> i;) {
        v.push_back(i);
        if (ss.peek() == ',')
            ss.ignore();
    }

    // Print the words
    for (size_t i = 0; i < v.size(); i++)
        cout << v[i] << endl;
}
```

**Output:** 

```
11
21
31
41
51
61
```