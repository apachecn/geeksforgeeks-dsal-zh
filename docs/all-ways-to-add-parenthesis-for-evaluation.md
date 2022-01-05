# 评估时添加括号的所有方式

> 原文:[https://www . geesforgeks . org/all-way-to-add-括号-for-evaluation/](https://www.geeksforgeeks.org/all-ways-to-add-parenthesis-for-evaluation/)

给定一个字符串，该字符串仅表示由数字和二进制运算符+、–和*组成的表达式。我们需要用所有可能的方式给表达式加上圆括号，并返回所有计算出的值。

```
Input : expr = “3-2-1”
Output : {0, 2}
((3-2)-1) = 0 
(3-(2-1)) = 2

Input : expr = "5*4-3*2"
Output : {-10, 10, 14, 10, 34}
(5*(4-(3*2))) = -10
(5*((4-3)*2)) = 10
((5*4)-(3*2)) = 14
((5*(4-3))*2) = 10
(((5*4)-3)*2) = 34

```

我们可以通过给表达式的所有可能的有效子串加上括号，然后对它们进行求值来解决这个问题，但是正如我们所看到的，这将涉及到解决许多重复的子问题，为了节省我们自己，我们可以遵循动态编程方法。
我们将每个子串的结果存储在一个映射中，如果递归中的字符串已经被求解，我们将从映射中返回结果，而不是再次求解。
下面的代码在字符串中运行一个循环，如果在任何时刻，字符是运算符，那么我们从那里划分输入，递归求解每个部分，然后以所有可能的方式组合结果。
参见 c_str()函数的用法，这个函数把 C++字符串转换成 C char 数组，这个函数用在下面的代码中是因为 atoi()函数需要一个字符数组作为参数而不是字符串。它将字符数组转换为数字。

```
//  C++ program to output all possible values of
// an expression by parenthesizing it.
#include <bits/stdc++.h>
using namespace std;

//  method checks, character is operator or not
bool isOperator(char op)
{
    return (op == '+' || op == '-' || op == '*');
}

//  Utility recursive method to get all possible
// result of input string
vector<int> possibleResultUtil(string input,
            map< string, vector<int> > memo)
{
    //  If already calculated, then return from memo
    if (memo.find(input) != memo.end())
        return memo[input];

    vector<int> res;
    for (int i = 0; i < input.size(); i++)
    {
        if (isOperator(input[i]))
        {
            // If character is operator then split and
            // calculate recursively
            vector<int> resPre =
              possibleResultUtil(input.substr(0, i), memo);
            vector<int> resSuf =
              possibleResultUtil(input.substr(i + 1), memo);

            //  Combine all possible combination
            for (int j = 0; j < resPre.size(); j++)
            {
                for (int k = 0; k < resSuf.size(); k++)
                {
                    if (input[i] == '+')
                        res.push_back(resPre[j] + resSuf[k]);
                    else if (input[i] == '-')
                        res.push_back(resPre[j] - resSuf[k]);
                    else if (input[i] == '*')
                        res.push_back(resPre[j] * resSuf[k]);
                }
            }
        }
    }

    // if input contains only number then save that 
    // into res vector
    if (res.size() == 0)
        res.push_back(atoi(input.c_str()));

    // Store in memo so that input string is not 
    // processed repeatedly
    memo[input] = res;
    return res;
}

//  method to return all possible output 
// from input expression
vector<int> possibleResult(string input)
{
    map< string, vector<int> > memo;
    return possibleResultUtil(input, memo);
}

//  Driver code to test above methods
int main()
{
    string input = "5*4-3*2";
    vector<int> res = possibleResult(input);

    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
    return 0;
}
```

输出:

```
-10 10 14 10 34 

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。