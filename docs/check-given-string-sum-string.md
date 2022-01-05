# 检查给定的字符串是否为和字符串

> 原文:[https://www . geesforgeks . org/check-given-string-sum-string/](https://www.geeksforgeeks.org/check-given-string-sum-string/)

给定一个数字串，确定它是否是一个“和串”。如果最右边的子串可以写成它前面两个子串的和，并且它前面的子串递归为真，那么这个串被称为和串。

示例:

```
“12243660” is a sum string. 
Explanation : 24 + 36 = 60, 12 + 24 = 36

“1111112223” is a sum string. 
Explanation: 111+112 = 223, 1+111 = 112 

“2368” is not a sum string

```

一般来说，如果一个字符串满足以下属性，它就被称为和字符串:

```
sub-string(i, x) + sub-string(x+1, j) 
 = sub-string(j+1, l)
and 
sub-string(x+1, j)+sub-string(j+1, l) 
 = sub-string(l+1, m) 
and so on till end. 
```

从例子中，我们可以看到我们的决定取决于前两个选择的数字。
所以我们为给定的字符串选择所有可能的前两个数字。那么对于每一个选择的两个数字，我们检查它是否是和串？所以方法很简单。我们使用两个循环使用两个子字符串 s1 和 s2 生成所有可能的前两个数字。然后我们检查是否有可能使号码 s3 = (s1 + s2)。如果我们可以生成 s3，那么我们递归地检查 s2 + s3，以此类推。

```
// C++ program to check if a given string
// is sum-string or not
#include <bits/stdc++.h>
using namespace std;

// this is function for finding sum of two
// numbers as string
string string_sum(string str1, string str2)
{
    if (str1.size() < str2.size())
       swap(str1, str2);

    int m = str1.size();
    int n = str2.size();
    string ans = "";

    // sum the str2 with str1
    int carry = 0;
    for (int i = 0; i < n; i++) {

        // Sum of current digits
        int ds = ((str1[m - 1 - i] - '0') +
                  (str2[n - 1 - i] - '0') +
                  carry) % 10;

        carry = ((str1[m - 1 - i] - '0') +
                 (str2[n - 1 - i] - '0') +
                 carry) / 10;

        ans = char(ds + '0') + ans;
    }

    for (int i = n; i < m; i++) {
        int ds = (str1[m - 1 - i] - '0' +
                  carry) % 10;
        carry = (str1[m - 1 - i] - '0' +
                 carry) / 10;
        ans = char(ds + '0') + ans;
    }

    if (carry)
        ans = char(carry + '0') + ans;
    return ans;
}

// Returns true of two substrings of ginven
// lengths of str[beg..] can cause a positive
// result.
bool checkSumStrUtil(string str, int beg,
                     int len1, int len2)
{

    // Finding two substrings of given lengths
    // and their sum
    string s1 = str.substr(beg, len1);
    string s2 = str.substr(beg + len1, len2);
    string s3 = string_sum(s1, s2);

    int s3_len = s3.size();

    // if number of digits s3 is greater then
    // the available string size
    if (s3_len > str.size() - len1 - len2 - beg)
        return false;

    // we got s3 as next number in main string
    if (s3 == str.substr(beg + len1 + len2, s3_len)) {

        // if we reach at the end of the string
        if (beg + len1 + len2 + s3_len == str.size())
            return true;

        // otherwise call recursively for n2, s3
        return checkSumStrUtil(str, beg + len1, len2,
                                              s3_len);
    }

    // we do not get s3 in main string
    return false;
}

// Returns true if str is sum string, else false.
bool isSumStr(string str)
{
    int n = str.size();

    // choosing first two numbers and checking
    // whether it is sum-string or not.
    for (int i = 1; i < n; i++)
        for (int j = 1; i + j < n; j++)
            if (checkSumStrUtil(str, 0, i, j))
                return true;

    return false;
}

// Driver code
int main()
{
    cout << isSumStr("1212243660") << endl;
    cout << isSumStr("123456787");
    return 0;
}
```

输出:

```
1
0

```

本文由**杰伊·普拉卡什·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。