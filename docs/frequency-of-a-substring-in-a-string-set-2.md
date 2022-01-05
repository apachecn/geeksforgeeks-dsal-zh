# 字符串中子字符串的频率|集合 2

> 原文:[https://www . geeksforgeeks . org/字符串集中子字符串的频率-2/](https://www.geeksforgeeks.org/frequency-of-a-substring-in-a-string-set-2/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**和长度为 **M** 的子字符串**模式**，任务是在给定字符串中找到作为子字符串的模式出现的[频率。如果**模式**出现在字符串**字符串**中，则打印“**是**”及其出现次数。否则，打印**“否”**。](https://www.geeksforgeeks.org/frequency-substring-string/)

**示例:**

> **输入:** str = "geeksforgeeks "，pattern = "geeks"
> **输出:** 2
> **解释:**
> 字符串“geeksforgeeks”中字符串“geeks”的出现在索引 0 和索引 8 处。
> 因此，计数为 2。
> 
> **输入:**输出: 0

**天真的做法:**参考[之前的帖子](https://www.geeksforgeeks.org/frequency-substring-string/)最简单的解决问题的方法。
***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*

**使用 [KMP 算法的方法:](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)** 参考本文[之前的帖子](https://www.geeksforgeeks.org/frequency-substring-string/)使用 [KMP 算法](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/)解决问题。
***时间复杂度:** O(N + M)*
***辅助空间:** O(M)*

**使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)的方法:**按照以下步骤解决问题:

*   使用[正则表达式()函数](https://www.geeksforgeeks.org/regex-regular-expression-in-c/)形成字符串**模式**的正则表达式。
*   使用功能 [smatch()](https://www.geeksforgeeks.org/smatch-regex-regular-expressions-in-c/) 创建一个 smatch **M** 。
*   使用函数 [regex_match()](https://www.geeksforgeeks.org/regex-regular-expression-in-c/) 检查字符串**字符串**中字符串**模式**是否存在，如下所示:

> regex_search(str，m，c)
> 其中，
> str 是给定的字符串，
> m 是 smatch，
> c 是字符串模式的正则表达式。

*   在上述步骤中，如果函数 **regex_match()** 返回 **True** ，则打印**“是”**，找到字符串**模式**的出现。否则，打印**“否”**。
*   创建一个变量**number of matts**[数据类型](https://www.geeksforgeeks.org/c-data-types/) **ptrdiff_t** 来存储出现次数。
*   使用函数 [**找到**匹配数**regex _ iterator()**](https://www.geeksforgeeks.org/regex_iterator-function-in-c-stl/)函数如下:

> ptrdiff _ t**number of matts**= STD::distance(sregex_iterator(s . begin()，S.end()，c)，sregex _ iterator())

*   打印上述步骤中出现的次数作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the frequency of
// substring in the given string S
void find_frequency(string S,
                    string pattern)
{
    // Create a regular expression
    // of the string pattern
    regex c(pattern);

    // Determines the matching behavior
    smatch m;

    // Use member function on 'm'
    // regex_search to check if
    // string X is present in S or not
    if (regex_search(S, m, c) == true) {
        cout << "Yes"
             << "\n";
    }
    else {
        cout << "No";
    }

    // Count the number of matches
    ptrdiff_t numberOfMatches
        = std::distance(
            sregex_iterator(S.begin(),
                            S.end(), c),
            sregex_iterator());

    // Print the coun of occurrence
    cout << "Frequency of string "
         << pattern << " is "
         << numberOfMatches;
}
// Driver code
int32_t main()
{
    // Given string str and pattern
    string str = "geeksforgeeks";
    string pattern = "geeks";

    // Function Call
    find_frequency(str, pattern);

    return 0;
}
```

**Output:**

```
Yes
Frequency of string geeks is 2

```

***时间复杂度:** O(N + M)*
***辅助空间:** O(M)*