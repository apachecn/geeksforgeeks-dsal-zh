# 根据每条线的给定宽度调整给定文本

> 原文:[https://www . geeksforgeeks . org/基于每行给定宽度的给定文本调整/](https://www.geeksforgeeks.org/justify-the-given-text-based-on-the-given-width-of-each-line/)

给定一个字符串 **str** 和每一行的宽度为 **L** ，任务是对齐该字符串，使得每一行对齐的文本都有长度 **L** ，并有空格(“”)的帮助，最后一行应该左对齐。

**示例:**

> **Input:** str = "GeeksforGeek 是极客们最好的计算机科学门户。”，L = 16
> T3【输出:T5【极客】forgeek _ _ 是
> 最 ______ 优秀的
> 计算机科学
> 门户网站 _______ 面向
> 极客。__________
> 
> **输入:** str =“快棕狐狸跳过懒狗。”，L = 11
> **输出:**
> 那只 ___ 快
> 棕色 _ _ _ 狐狸
> 跳过了
> 那只 _ _ _ _ _ 懒
> 狗。____
> 符号表示一个空格。

**方法:**
每行单词之间的空格数在知道该行的一整套单词之前无法计算。我们将逐行解决这个问题。

1.  将给定的文本拆分成单词
2.  首先选择每一行中可以插入的单词，包括单词之间的空格。为此，中间有一个空格的包含单词的长度总和必须小于或等于 **L** 。
3.  现在计算使每条线的长度 **L** 所需的空格数，并平均分配空格。
4.  对下一组单词重复以上步骤。
5.  对于最后一行，必须在末尾指定空格，因为最后一行必须是**左对齐**。

下面是上述方法的实现:

```
// C++ program to Justify the given Text
// according to the given width of each line

#include "bits/stdc++.h"
using namespace std;

// Function to join the words
// with spaces spread evenly
string JoinALineWithSpace(
    vector<string>& words,
    int start, int end,
    int num_spaces)
{

    // Number of words in current line
    int num_words_curr_line
        = end - start + 1;

    // String to store the justified text
    string line;

    for (int i = start; i < end; i++) {

        line += words[i];
        --num_words_curr_line;

        // Count number of current space needed
        int num_curr_space
            = ceil((double)(num_spaces)
                   / num_words_curr_line);

        // Insert spaces in string line
        line.append(num_curr_space, ' ');

        // Delete the spaces inserted in line
        num_spaces -= num_curr_space;
    }

    // Insert word to string line
    line += words[end];
    line.append(num_spaces, ' ');

    // Return justified text
    return line;
}

// Function that justify the words of
// sentence of length of line L
vector<string> JustifyText(
    vector<string>& words,
    int L)
{

    int curr_line_start = 0;
    int num_words_curr_line = 0;
    int curr_line_length = 0;

    // To store the justified text
    vector<string> result;

    // Traversing the words array
    for (int i = 0; i < words.size(); i++) {

        // curr_line_start is the first word
        // in the current line, and i is
        // used to identify the last word
        ++num_words_curr_line;

        int lookahead_line_length
            = curr_line_length
              + words[i].size()
              + (num_words_curr_line - 1);

        // If by including the words length becomes L,
        // then that set of words is justified
        // and add the justified text to result
        if (lookahead_line_length == L) {

            // Justify the set of words
            string ans
                = JoinALineWithSpace(
                    words,
                    curr_line_start,
                    i,
                    i - curr_line_start);

            // Store the justified text in result
            result.emplace_back(ans);

            // Start the current line
            // with next index
            curr_line_start = i + 1;

            // num of words in the current line
            // and current line length set to 0
            num_words_curr_line = 0;
            curr_line_length = 0;
        }

        // If by including the words such that
        // length of words becomes greater than L,
        // then hat set is justified with
        // one less word and add the
        // justified text to result
        else if (lookahead_line_length > L) {

            // Justify the set of words
            string ans
                = JoinALineWithSpace(
                    words,
                    curr_line_start,
                    i - 1,
                    L - curr_line_length);

            // Store the justified text in result
            result.emplace_back(ans);

            // Current line set to current word
            curr_line_start = i;

            // Number of words set to 1
            num_words_curr_line = 1;

            // Current line length set
            // to current word length
            curr_line_length = words[i].size();
        }

        // If length is less than L then,
        // add the word to current line length
        else {
            curr_line_length
                += words[i].size();
        }
    }

    // Last line is to be left-aligned
    if (num_words_curr_line > 0) {
        string line
            = JoinALineWithSpace(
                words,
                curr_line_start,
                words.size() - 1,
                num_words_curr_line - 1);

        line.append(
            L - curr_line_length
                - (num_words_curr_line - 1),
            ' ');

        // Insert the last line
        // left-aligned to result
        result.emplace_back(line);
    }

    // Return result
    return result;
}

// Function to insert words
// of sentence
vector<string> splitWords(string str)
{

    vector<string> words;
    string a = "";
    for (int i = 0; str[i]; i++) {

        // Add char to string a
        // to get the word
        if (str[i] != ' ') {
            a += str[i];
        }

        // If a space occurs
        // split the words and
        // add it to vector
        else {
            words.push_back(a);
            a = "";
        }
    }

    // Push_back the last word
    // of sentence
    words.push_back(a);

    // Return the vector of
    // words extracted from
    // string
    return words;
}

// Function to print justified text
void printJustifiedText(vector<string>& result)
{
    for (auto& it : result) {
        cout << it << endl;
    }
}

// Function to call the justification
void justifyTheText(string str, int L)
{

    vector<string> words;

    // Inserting words from
    // given string
    words = splitWords(str);

    // Function call to
    // justify the text
    vector<string> result
        = JustifyText(words, L);

    // Print the justified
    // text
    printJustifiedText(result);
}

// Driver Code
int main()
{
    string str
        = "GeeksforGeek is the best"
          " computer science portal"
          " for geeks.";
    int L = 16;

    justifyTheText(str, L);

    return 0;
}
```

**Output:**

```
GeeksforGeek  is
the         best
computer science
portal       for
geeks.

```

**时间复杂度:** O(N)，其中 N =字符串长度