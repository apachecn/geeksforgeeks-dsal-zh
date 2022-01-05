# 改变给定字符串的性别

> 原文:[https://www.geeksforgeeks.org/change-gender-given-string/](https://www.geeksforgeeks.org/change-gender-given-string/)

更改字符串的性别，即切换输入字符串中所有特定性别的单词。
示例:

```
Input:  “she is my sister” 
Output:  “he is my brother”.
There are two gender-specific words in this
sentence:“she” and “sister”. After toggling
gender specific words to their respective 
counterparts - “he” and “brother” :
Gender specific words of the string are now 
changed.

```

**算法:**

*   维护一个散列图，该图将所有“女性”单词映射到“男性”单词，并将所有“男性”单词映射到“女性”单词。
*   然后对于字符串中的每个单词，我们检查这是否是一个特定性别的单词。如果是的话，我们就用它的对应词来交换这个词。否则我们不交换这个词。
*   所有的单词被连接在一个新的字符串中，这个字符串在最后被打印出来，是我们需要的字符串。

```
// A C++ Program to change the gender of a string
#include<bits/stdc++.h>
using namespace std;

// A Function that returns the new string with gender
// changed
string changeGender(string str)
{
    // A Dictionary to store the mapping of genders
    // The user can add his words too.
    unordered_multimap <string, string> dictionary =
    {
      {"batman", "batwoman"}, {"batwoman", "batman"},
      {"boy", "girl"}, {"girl", "boy"},
      {"boyfriend", "girlfriend"}, {"girlfriend", "boyfriend"},
      {"father", "mother"}, {"mother", "father"},
      {"husband", "wife"}, {"wife", "husband"},
      {"he", "she"}, {"she", "he"},
      {"his", "her"}, {"her", "his"},
      {"male", "female"}, {"female", "male"},
      {"man", "woman"}, {"woman", "man"},
      {"Mr", "Ms"}, {"Mr", "Ms"},
      {"sir", "madam"}, {"madam", "sir"},
      {"son", "daughter"}, {"daughter", "son"},
      {"uncle", "aunt"}, {"aunt", "uncle"},
    };

    str = str + ' '; // Append a space at the end

    int n = str.length();

    // 'temp' string will hold the intermediate words
    // and 'ans' string will be our result
    string temp = "", ans = "";

    for (int i=0; i<=n-1; i++)
    {
        if (str[i] != ' ')
            temp.push_back(str[i]);
        else
        {
            // If this is a 'male' or a 'female' word then
            // swap this with its counterpart
            if (dictionary.find(temp) != dictionary.end())
                temp = dictionary.find(temp)->second;

            ans = ans + temp + ' ';
            temp.clear();
        }
    }

    return(ans);
}

// Driver Program to test above functions
int main()
{
    string str = "she is going to watch movie with"
                " her boyfriend";

    cout << changeGender(str);

    return (0);
}
```

**时间复杂度:** O(N^2)，其中 n 是字符串的长度，因为字符串的‘+’/‘append’运算符可能需要 O(N)个时间，并且假设在字典中查找需要 O(1)个最坏情况的时间。

**辅助空间:**除了将所有单词映射到对应单词的字典，我们为新字符串声明 O(N)空间，其中 N 是输入字符串的长度。

**改进范围:**

*   我们可以在字典中添加更多的单词和它们的对应词，以提高程序的准确性。例如，我们可以在字典中添加–“演员、女演员”、“上帝、女神”。
*   还可以导入所有女性和男性单词的文本文件。
*   该程序可以修改为不区分大小写。

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。