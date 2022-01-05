# 最长公共目录路径程序

> 原文:[https://www . geesforgeks . org/program-long-common-directory-path/](https://www.geeksforgeeks.org/program-longest-common-directory-path/)

给定 n 个目录路径，我们需要编写一个程序来寻找最长的公共目录路径。
示例:

```
Input : 3
"/home/User/Desktop/gfg/test"
"/home/User/Desktop/gfg/file"
"/home/User/Desktop/geeks/folders"

Output : Longest Common Path is /home/User/Desktop!

Input : 4
"/home/User/Desktop/gfg/test",
"/home/User/Desktop/gfg/file",
"/home/User/Desktop/gfg/folders",
"/home/User/Desktop/gfg/folders"

Output : Longest Common Path is /home/User/Desktop/gfg!
```

在函数 **LongestCommonPath()** 中，使用了两个主要变量，分别是**“common characters”**用于存储常用字符的长度，**“common string”**用于存储最长的路径字符串，这样我们就得到了最长的公共路径。
根据输入路径中出现的公共路径的长度，公共字符变量会在每次迭代中更新。
最后，迭代后得到公共路径串的长度。然后，我们通过子串直到分隔符**/**得到我们的公共路径，好像*我们不这样做，那么我们得到路径中最长的公共字符串，这不应该是我们的结果*。
以下是上述办法的实施情况。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program for longest common path
#include <bits/stdc++.h>
using namespace std;

string LongestCommonPath(const vector<string>& input_directory,
                                                char separator)
{
    vector<string>::const_iterator iter;

    // stores the length of common characters
    // and initialized with the length of
    // first string .
    int CommonCharacters = input_directory[0].length();

    // stores the common string and initialized
    // with the first string .
    string CommonString = input_directory[0];

    for (iter = input_directory.begin() + 1;
        iter != input_directory.end(); iter++) {

        // finding the two pointers through the mismatch()
        // function which is 'mismatch at first string' and
        //  'mismatch at the other string '
        pair<string::const_iterator, string::const_iterator> p =
                                mismatch(CommonString.begin(),
                                    CommonString.end(), iter->begin());

        // As the first mismatch string pointer points to the mismatch
        // present in the "CommonString" so "( p.first-CommonString.begin())"
        // determines the common characters in each iteration .
        if ((p.first - CommonString.begin()) < CommonCharacters) {

            // If the expression is smaller than commonCharacters
            // then we will update the commonCharacters because
            // this states that common path is smaller than the
            // string commonCharacters we have evaluated till .
            CommonCharacters = p.first - CommonString.begin();
        }

        // Updating CommonString variable
        // so that in this maximum length
        // string is stored .
        if (*iter > CommonString)
            CommonString = *iter;
    }

    // In 'found' variable we store the index of '/' in
    // the length of common characters in CommonString
    int found;

    for (int i = CommonCharacters; i >= 0; --i) {
        if (CommonString[i] == '/') {
            found = i;
            break;
        }
    }

    // The substring from index 0 to index of
    // separator is the longest common substring
    return CommonString.substr(0, found);
}

int main()
{
    int n = 4;

    string input_directory[4] = {
        "/home/User/Desktop/gfg/test",
        "/home/User/Desktop/gfg/file",
        "/home/User/Desktop/gfg/folders",
        "/home/User/Desktop/gfg/folders"
    };

    vector<string> input(input_directory,
                        input_directory + n);
    cout << "Longest Common Path is "
        << LongestCommonPath(input, '/') << "!\n";

    return 0;
}
```

**Output:** 

```
Longest Common Path is /home/User/Desktop/gfg!
```

参考文献:
[罗塞塔代码](https://rosettacode.org/wiki/Find_common_directory_path)