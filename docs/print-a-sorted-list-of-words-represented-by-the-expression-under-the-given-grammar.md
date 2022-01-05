# 打印给定语法下由表达式表示的单词排序列表

> 原文:[https://www . geesforgeks . org/print-一个按给定语法下的表达式表示的单词排序列表/](https://www.geeksforgeeks.org/print-a-sorted-list-of-words-represented-by-the-expression-under-the-given-grammar/)

给定长度为 **n** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **R(x)** ，表示在给定语法下具有一组单词的表达式:

*   对于每个小写字母 **x** ， **R(x) = {x}**
*   对于表达式 **e_1、e_2、…、e_k** 带有 **k≥2** 、 **R({e_1、e_2、…、e _ k })= R(e _ 1)∪R(e _ 2)∪…∪R(e _ k)**。
*   对于表达式 **e_1** 和 **e_2** ， **R(e_1 + e_2) = {a + b for (a，b) in R(e_1) × R(e_2)}** ，其中+表示串联，而×表示笛卡儿积。

任务是找到表达式所代表的单词的排序列表。

**示例:**

> **输入:**“{ { a，z}，a{b，c}，{ab，z } }”
> **输出:**【“a”、“ab”、“ac”、“z”】
> **解释:**每个不同的单词在最终答案中只写一次。
> {a，z}，a{b，c}，{ab，z} → {a，z}，{ab，ac}，{ab，z} → [a，z，ab，ac]
> 
> **输入:**“{ a，b}{c，{d，e } }”
> **输出:**[“AC”、“ad”、“ae”、“bc”、“bd”、“be”]

**方法:**从给定的语法来看，字符串可以表示一组小写单词。让 **R(expr)** 表示表达式所表示的词集。考虑下面的例子来理解这种方法。

*   单个字母代表包含该单词的单个集合。

    > R(“a”)= {“a”}
    > R(“w”)= {“w”}

*   如果遇到由两个或更多表达式组成的逗号分隔列表，则取可能性的并集。

    > R(“{ a，b，c }”= {“a”，“b”，“c”}
    > R(“{ { a，b}，{b，c } }”= {“a”，“b”，“c”}(注意最终集合最多只包含每个单词一次)

*   在连接两个表达式时，取两个单词之间可能的连接集合，其中第一个单词来自第一个表达式，第二个单词来自第二个表达式。

    > R(“{ a，b}{c，d }”)= {“AC”、“ad”、“bc”、“BD”}
    > R(“{ a { b，c}{d，e}f{g，h })= {“abdfg”、“abdfh”、“abefg”、“abefh”、“acdfg”、“acdfh”、“acfg”、“acefg”、“acefh”}

按照以下步骤解决问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，检查以下三个条件:
    1.  如果遇到 **{…}** ，通过[递归调用函数](https://www.geeksforgeeks.org/recursive-functions/)得到 **{…}** 内部的结果，用返回的字符串集做当前字符串集的笛卡儿积。
    2.  如果遇到一个**逗号(，**，将当前的字符串集合推到结果中，并清空当前的字符串。
    3.  如果遇到一个字母，用当前的一组字符串做笛卡尔乘积。
*   最后，[对结果集中的所有字符串进行排序](https://www.geeksforgeeks.org/sort-an-array-of-strings-lexicographically-based-on-prefix/)，只打印唯一的字符串。

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the Cartesian product
// of two set of strings
vector<string> getProduct(vector<string>& lhs,
                          vector<string>& rhs)
{

    // If lhs is empty,
    // return rhs
    if (lhs.empty())
        return rhs;

    // Store the Cartesian product
    // of two set of strings
    vector<string> ret;

    // Iterate over characters of both
    // strings and insert Cartesian product
    for (auto sl : lhs)
        for (auto sr : rhs)
            ret.push_back(sl + sr);

    return ret;
}

// Function to find the sorted list of words
// that the expression represents
vector<string> braceExpansion(string expression)
{

    // Store the sorted list of words
    // that the expression represents
    vector<string> ret;

    // Store the current set of strings
    vector<string> cur;

    // Append Comma
    expression += ', ';

    // Stores the length of expression
    int len = expression.size();

    // Iterate over the characters
    // of the string(expression)
    for (int i = 0; i < len; ++i) {

        // Stores the current character
        char c = expression[i];

        // If { is encountered, find
        // its closing bracket, }
        if (c == '{') {

            // Store the characters inside
            // of these brackets
            string sub;

            // Stores count of unbalanced '{''
            int cnt = 1;

            // Iterate over characters of
            // expression after index i
            while (++i < len) {

                // If current character is '{'
                if (expression[i] == '{') {

                    // Update cnt
                    ++cnt;
                }

                // If current character is '}'
                else if (expression[i] == '}') {

                    // Update cnt
                    --cnt;
                }

                // If cnt is equal to 0
                if (cnt == 0)
                    break;

                // Append current character
                sub += expression[i];
            }

            // Recursively call the function
            // for the string, sub
            vector<string> sub_ret
                = braceExpansion(sub);

            // Store the cartesian product of cur
            // and sub_ret in cur
            cur = getProduct(cur, sub_ret);
        }

        // If current character is Comma
        else if (c == ', ') {

            // Push cur result into ret
            ret.insert(begin(ret),
                       begin(cur), end(cur));

            // Clear the current set
            // of strings
            cur.clear();
        }
        else {

            // Append the current character to tmp
            vector<string> tmp(1, string(1, c));

            // Store the cartesian product of
            // tmp and cur in cur
            cur = getProduct(cur, tmp);
        }
    }

    // Sort the strings present in ret
    // and get only the unique set of strings
    sort(begin(ret), end(ret));

    auto iter = unique(begin(ret), end(ret));

    ret.resize(distance(begin(ret), iter));

    return ret;
}

// Driver Code
int main()
{

    // Given expression, str
    string str = "{a, b}{c, {d, e}}";

    // Store the sorted list of words
    vector<string> res;

    // Function Call
    res = braceExpansion(str);

    // Print the sorted list of words
    for (string x : res) {
        cout << x << " ";
    }

    return 0;
}
```

**Output:**

```
ac ad ae bc bd be

```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*