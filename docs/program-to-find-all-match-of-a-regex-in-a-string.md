# 在字符串中查找正则表达式所有匹配的程序

> 原文:[https://www . geesforgeks . org/program-to-find-all-match-of-a-regex-in-a-string/](https://www.geeksforgeeks.org/program-to-find-all-match-of-a-regex-in-a-string/)

**先决条件:**[c++中的 smatch | Regex(正则表达式)](https://www.geeksforgeeks.org/smatch-regex-regular-expressions-in-c/)

给定一个正则表达式，任务是在一个字符串中找到所有的正则表达式匹配。

*   **Without using iterator:**

    ```
    // C++ program to find all the matches
    #include <bits/stdc++.h>
    using namespace std;
    int main()
    {
        string subject("My GeeksforGeeks is my " 
                        "GeeksforGeeks none of your GeeksforGeeks");

        // Template instantiations for
        // extracting the matching pattern.
        smatch match;
        regex r("GeeksforGeeks");
        int i = 1;
        while (regex_search(subject, match, r)) {
            cout << "\nMatched string is " << match.str(0) << endl
                 << "and it is found at position " 
                 << match.position(0)<<endl; 
            i++;

            // suffix to find the rest of the string.
            subject = match.suffix().str();
        }
        return 0;
    }
    ```

    **Output:**

    ```
    Matched string is GeeksforGeeks
    and it is found at position 3

    Matched string is GeeksforGeeks
    and it is found at position 7

    Matched string is GeeksforGeeks
    and it is found at position 14

    ```

    **注意:**上面的代码运行得很好，但问题是输入字符串会丢失。

*   **使用迭代器:**
    可以通过调用带有三个参数的构造函数来构造对象:指示搜索开始位置的字符串迭代器、指示搜索结束位置的字符串迭代器和 regex 对象。使用默认构造函数构造另一个迭代器对象，以获得序列结束迭代器。

    ```
    #include <bits/stdc++.h>
    using namespace std;
    int main()
    {
        string subject("geeksforgeeksabcdefghg"
                       "eeksforgeeksabcdgeeksforgeeks");

        // regex object.
        regex re("geeks(for)geeks");

        // finding all the match.
        for (sregex_iterator it = sregex_iterator(subject.begin(), subject.end(), re);
             it != sregex_iterator(); it++) {
            smatch match;
            match = *it;
            cout << "\nMatched  string is = " << match.str(0)
                 << "\nand it is found at position "
                 << match.position(0) << endl;
            cout << "Capture " << match.str(1)
                 << " at position " << match.position(1) << endl;
        }
        return 0;
    }
    ```

    **输出:**

    ```
    Matched  string is = geeksforgeeks
    and it is found at position 0
    Capture for at position 5

    Matched  string is = geeksforgeeks
    and it is found at position 21
    Capture for at position 26

    Matched  string is = geeksforgeeks
    and it is found at position 38
    Capture for at position 43

    ```