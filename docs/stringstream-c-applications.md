# c++中的 stringstream 及其应用

> 原文:[https://www.geeksforgeeks.org/stringstream-c-applications/](https://www.geeksforgeeks.org/stringstream-c-applications/)

stringstream 将一个字符串对象与一个流相关联，允许您像读取流一样读取该字符串(如 cin)。

基本方法是–

> clear() —清除流
> str() —获取并设置流中存在内容的 string 对象。
> 运算符< < —向 stringstream 对象添加一个字符串。
> 操作符> > —从 stringstream 对象中读取一些内容，

stringstream 类在解析输入时非常有用。

**应用:**

1.  **Count number of words in a string**

    ```
    Examples:
    Input : Asipu Pawan Kumar
    Output : 3

    Input : Geeks For Geeks Ide
    Output : 4
    ```

    ```
    // CPP program to count words in a string
    // using stringstream.
    #include <bits/stdc++.h>
    using namespace std;

    int countWords(string str)
    {
        // breaking input into word using string stream
        stringstream s(str); // Used for breaking words
        string word; // to store individual words

        int count = 0;
        while (s >> word)
            count++;
        return count;
    }

    // Driver code
    int main()
    {
        string s = "geeks for geeks geeks "
                   "contribution placements";
        cout << " Number of words are: " << countWords(s);
        return 0;
    }
    ```

    输出:

    ```
      Number of words are: 6
    ```

2.  **Print frequencies of individual words in a string**

    ```
    Input : Geeks For Geeks Quiz Geeks Quiz Practice Practice
    Output : For -> 1
             Geeks -> 3
             Practice -> 2
             Quiz -> 2

    Input : Word String Frequency String
    Output : Frequency -> 1
             String -> 2
             Word -> 1 

    ```

    ```
    // CPP program to demonstrate use of stringstream
    // to count frequencies of words.
    #include <bits/stdc++.h>
    using namespace std;

    void printFrequency(string st)
    {
        // each word it mapped to it's frequency
        map<string, int> FW;
        stringstream ss(st); // Used for breaking words
        string Word; // To store individual words

        while (ss >> Word)
            FW[Word]++;

        map<string, int>::iterator m;
        for (m = FW.begin(); m != FW.end(); m++)
            cout << m->first << " -> "
                 << m->second << "\n";
    }

    // Driver code
    int main()
    {
        string s = "Geeks For Geeks Ide";
        printFrequency(s);
        return 0;
    }
    ```

    输出:

    ```
    For -> 1
    Geeks -> 2
    Ide -> 1

    ```

3.  [使用 Stringstream 删除字符串中的空格](https://www.geeksforgeeks.org/removing-spaces-string-using-stringstream/)
4.  [在 C/C++中将字符串转换为数字](https://www.geeksforgeeks.org/converting-strings-numbers-cc/)

本文由 **ASIPU PAWAN KUMAR** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。