# std::regex_match，std::regex_replace() | Regex(正则表达式)在 C++中

> 原文:[https://www . geeksforgeeks . org/regex-正则表达式 in-c/](https://www.geeksforgeeks.org/regex-regular-expression-in-c/)

Regex 是“**正则表达式**的简称，在编程语言和许多不同的库中经常以这种方式使用。它在 C++11 以后的编译器中得到支持。
**正则表达式中使用的函数模板**
**正则表达式匹配给定字符串时，该函数返回真，否则返回假。** 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate working of regex_match()
#include <iostream>
#include <regex>

using namespace std;
int main()
{
    string a = "GeeksForGeeks";

    // Here b is an object of regex (regular expression)
    regex b("(Geek)(.*)"); // Geek followed by any character

    // regex_match function matches string a against regex b
    if ( regex_match(a, b) )
        cout << "String 'a' matches regular expression 'b' \n";

    // regex_match function for matching a range in string
    // against regex b
    if ( regex_match(a.begin(), a.end(), b) )
        cout << "String 'a' matches with regular expression "
                "'b' in the range from 0 to string end\n";

    return 0;
}
```

输出:

```
String 'a' matches regular expression 'b' 
String 'a' matches with regular expression 'b' in the range from 0 to string end
```

**regex _ search()**–该函数用于搜索与正则表达式
匹配的模式

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate working of regex_search()
#include <iostream>
#include <regex>
#include<string.h>
using namespace std;

int main()
{
    // Target sequence
    string s = "I am looking for GeeksForGeeks "
               "articles";

    // An object of regex for pattern to be searched
    regex r("Geek[a-zA-Z]+");

    // flag type for determining the matching behavior
    // here it is for matches on 'string' objects
    smatch m;

    // regex_search() for searching the regex pattern
    // 'r' in the string 's'. 'm' is flag for determining
    // matching behavior.
    regex_search(s, m, r);

    // for each loop
    for (auto x : m)
        cout << x << " ";

    return 0;
}
```

输出:

```
GeeksForGeeks
```

**regex_replace()** 这个函数用于用字符串替换与正则表达式匹配的模式。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate working of regex_replace()
#include <iostream>
#include <string>
#include <regex>
#include <iterator>
using namespace std;

int main()
{
    string s = "I am looking for GeeksForGeek \n";

    // matches words beginning by "Geek"
    regex r("Geek[a-zA-z]+");

    // regex_replace() for replacing the match with 'geek'
    cout << std::regex_replace(s, r, "geek");

    string result;

    // regex_replace( ) for replacing the match with 'geek'
    regex_replace(back_inserter(result), s.begin(), s.end(),
                  r,  "geek");

    cout << result;

    return 0;
}
```

输出:

```
I am looking for geek 
I am looking for geek
```

因此，Regex 操作使用以下参数:-

*   目标序列(主题)–要匹配的字符串。
*   正则表达式(模式)–目标序列的正则表达式。
*   匹配数组–关于匹配的信息存储在特殊的 match_result 数组中。
*   替换字符串–这些字符串用于替换匹配项。

本文由**阿比纳夫·蒂瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。