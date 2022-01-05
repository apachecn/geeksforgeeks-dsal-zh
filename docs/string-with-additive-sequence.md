# 添加序列的字符串

> 原文:[https://www . geesforgeks . org/带加法序列的字符串/](https://www.geeksforgeeks.org/string-with-additive-sequence/)

给定一个字符串，任务是找出它是否包含加法序列。如果一个字符串的数字可以组成一个数字序列，其中每个数字都是前两个数字的加法，则该字符串包含一个加法序列。一个有效的字符串应该包含至少三个数字来组成一个加法序列。
示例:

```
Input : s = “235813”
Output : true
2 + 3 = 5, 3 + 5 = 8, 5 + 8 = 13

Input : s = “199100199”
Output : true
1 + 99 = 100, 99 + 100 = 199

Input : s = “12345678”
Output : false
```

这个问题是可以递归解决的，注意，相加值中的位数不能小于其任何操作数中的位数，这就是为什么我们将循环直到第一个数字的(字符串长度)/ 2 和第二个数字的(字符串长度–第一个数字的长度)/2，以忽略无效结果。
接下来要注意的是，第一个和第二个数字不能以 0 开头，这是通过 isValid 方法在下面的代码中检入的。当我们递归调用时，我们检查第一个和第二个数字的和是否正好等于字符串的其余部分。如果是，则直接返回结果，否则检查求和字符串是否是字符串剩余部分的前缀，如果是，则在从字符串剩余部分中移除求和字符串后，用第二个数字、求和字符串和字符串剩余部分递归调用，如果求和字符串不是字符串剩余部分的前缀，则没有可用的解决方案。
下面是 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to check whether a string
// makes an additive sequence or not
#include <bits/stdc++.h>
using namespace std;

// Checks whether num is valid or not, by
// checking first character and size
bool isValid(string num)
{
    if (num.size() > 1 && num[0] == '0')
        return false;
    return true;
}

// returns int value at pos string, if pos is
// out of bound then returns 0
int val(string a, int pos)
{
    if (pos >= a.length())
        return 0;

    //  converting character to integer
    return (a[pos] - '0');
}

// add two number in string form and return
// result as a string
string addString(string a, string b)
{
    string sum = "";
    int i = a.length() - 1;
    int j = b.length() - 1;
    int carry = 0;

    //  loop until both string get processed
    while (i >= 0 || j >= 0)
    {
        int t = val(a, i) + val(b, j) + carry;
        sum += (t % 10 + '0');
        carry = t / 10;
        i--;    j--;
    }
    if (carry)
        sum += (carry + '0');
    reverse(sum.begin(), sum.end());
    return sum;
}

//  Recursive method to check c = a + b
bool checkAddition(list<string>& res, string a,
                             string b, string c)
{
    //  both first and second number should be valid
    if (!isValid(a) || !isValid(b))
        return false;
    string sum = addString(a, b);

    //  if sum is same as c then direct return
    if (sum == c)
    {
        res.push_back(sum);
        return true;
    }

    /*  if sum size is greater than c, then no
        possible sequence further OR if c is not
        prefix of sum string, then no possible
        sequence further  */
    if (c.size() <= sum.size() ||
        sum != c.substr(0, sum.size()))
        return false;
    else
    {
        res.push_back(sum);

        //  next recursive call will have b as first
        //  number, sum as second number and string
        //  c as third number after removing prefix
        //  sum string from c
        return checkAddition(res, b, sum,
                             c.substr(sum.size()));
    }
}

//  Method returns additive sequence from string as
// a list
list<string> additiveSequence(string num)
{
    list<string> res;
    int l = num.length();

    // loop until l/2 only, because if first
    // number is larger,then no possible sequence
    // later
    for (int i = 1; i <= l/2; i++)
    {
        for (int j = 1; j <= (l - i)/2; j++)
        {
            if (checkAddition(res, num.substr(0, i),
                              num.substr(i, j),
                              num.substr(i + j)))
            {
                // adding first and second number at
                // front of result list
                res.push_front(num.substr(i, j));
                res.push_front(num.substr(0, i));
                return res;
            }
        }
    }

    // If code execution reaches here, then string
    // doesn't have any additive sequence
    res.clear();
    return res;
}

//  Method to print result list
void printResult(list<string> res)
{
    for (auto it = res.begin(); it != res.end(); it++)
        cout << *it << " ";
    cout << endl;
}

//  Driver code to test above methods
int main()
{
    string num = "235813";
    list<string> res = additiveSequence(num);
    printResult(res);

    num = "199100199";
    res = additiveSequence(num);
    printResult(res);
    return 0;
}
```

输出:

```
2 3 5 8 13 
1 99 100 199 
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。