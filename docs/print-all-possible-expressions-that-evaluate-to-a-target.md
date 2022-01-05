# 打印评估目标的所有可能表达式

> 原文:[https://www . geeksforgeeks . org/print-所有可能的表达式-评估目标/](https://www.geeksforgeeks.org/print-all-possible-expressions-that-evaluate-to-a-target/)

给定一个只包含 0 到 9 的数字和一个整数值的字符串，**目标为**。在给定的数字串中，使用二进制运算符+、–和*找出有多少表达式可以评估为**目标**。

```
Input : "123",  Target : 6
Output : {“1+2+3”, “1*2*3”}

Input : “125”, Target : 7
Output : {“1*2+5”, “12-5”}
```

这个问题可以通过将所有可能的二进制运算符放在中间到数字之间并对它们进行评估，然后检查它们是否评估为目标来解决。

*   在编写递归代码时，我们需要保留这些变量作为递归方法的参数——结果向量、输入字符串、当前表达式字符串、目标值、处理输入的位置、当前评估值和评估中的最后一个值。
*   由于乘法运算，最后一个值被保留在递归中，在做乘法时，我们需要最后一个值来进行正确的计算。

为了更好地理解，请参见下面的示例–

```
Input is 125, suppose we have reached till 1+2 now,
Input = “125”, current expression = “1+2”, 
position = 2, current val = 3, last = 2

Now when we go for multiplication, we need last 
value for evaluation as follows:

current val = current val - last + last * current val

First we subtract last and then add last * current 
val for evaluation, new last is last * current val.
current val = 3 – 2 + 2*5 = 11
last = 2*5 = 10 
```

在下面的代码中需要注意的另一件事是，我们忽略了所有从 0 开始的数字，在循环中强加了一个条件作为第一个条件，这样我们就不会处理像 03，05 这样的数字。
参见 c_str()函数的用法，这个函数将 C++字符串转换成 C char 数组，这个函数用在下面的代码中是因为 atoi()函数需要一个字符数组作为参数而不是字符串。它将字符数组转换为数字。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find all possible expression which
// evaluate to target
#include <bits/stdc++.h>
using namespace std;

// Utility recursive method to generate all possible
// expressions
void getExprUtil(vector<string>& res, string curExp,
                 string input, int target, int pos,
                 int curVal, int last)
{
    // true if whole input is processed with some
    // operators
    if (pos == input.length())
    {
        // if current value is equal to target
        //then only add to final solution
        // if question is : all possible o/p then just
        //push_back without condition
        if (curVal == target)
            res.push_back(curExp);
        return;
    }

    // loop to put operator at all positions
    for (int i = pos; i < input.length(); i++)
    {
        // ignoring case which start with 0 as they
        // are useless for evaluation
        if (i != pos && input[pos] == '0')
            break;

        // take part of input from pos to i
        string part = input.substr(pos, i + 1 - pos);

        // take numeric value of part
        int cur = atoi(part.c_str());

        // if pos is 0 then just send numeric value
        // for next recursion
        if (pos == 0)
            getExprUtil(res, curExp + part, input,
                     target, i + 1, cur, cur);

        // try all given binary operator for evaluation
        else
        {
            getExprUtil(res, curExp + "+" + part, input,
                     target, i + 1, curVal + cur, cur);
            getExprUtil(res, curExp + "-" + part, input,
                     target, i + 1, curVal - cur, -cur);
            getExprUtil(res, curExp + "*" + part, input,
                     target, i + 1, curVal - last + last * cur,
                     last * cur);
        }
    }
}

// Below method returns all possible expression
// evaluating to target
vector<string> getExprs(string input, int target)
{
    vector<string> res;
    getExprUtil(res, "", input, target, 0, 0, 0);
    return res;
}

// method to print result
void printResult(vector<string> res)
{
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
    cout << endl;
}

// Driver code to test above methods
int main()
{
    string input = "123";
    int target = 6;
    vector<string> res = getExprs(input, target);
    printResult(res);

    input = "125";
    target = 7;
    res = getExprs(input, target);
    printResult(res);
    return 0;
}
```

## 蟒蛇 3

```
# C++ program to find all possible expression which
# evaluate to target

# Utility recursive method to generate all possible
# expressions
def getExprUtil(res, curExp, _input, target, pos, curVal, last):
    # true if whole input is processed with some
    # operators
    if (pos == len(_input)):
        # if current value is equal to target
        #then only add to final solution
        # if question is : all possible o/p then just
        #push_back without condition
        if (curVal == target):
            res.append(curExp)
        return

    # loop to put operator at all positions
    for i in range(pos,len(_input)):
        # ignoring case which start with 0 as they
        # are useless for evaluation
        if (i != pos and _input[pos] == '0'):
            break

        # take part of input from pos to i
        part = _input[pos: i + 1].strip()

        # take numeric value of part
        cur = int(part)

        # if pos is 0 then just send numeric value
        # for next recursion
        if (pos == 0):
            getExprUtil(res, curExp + part, _input,
                     target, i + 1, cur, cur)

        # try all given binary operator for evaluation
        else:
            getExprUtil(res, curExp + "+" + part, _input,
                     target, i + 1, curVal + cur, cur)
            getExprUtil(res, curExp + "-" + part, _input,
                     target, i + 1, curVal - cur, -cur)
            getExprUtil(res, curExp + "*" + part, _input,
                     target, i + 1, curVal - last + last * cur,
                     last * cur)

# Below method returns all possible expression
# evaluating to target
def getExprs(_input, target):
    res=[]
    getExprUtil(res, "", _input, target, 0, 0, 0)
    return res

# method to print result
def printResult(res):
    for i in range(len(res)):
        print(res[i],end=" ")
    print()

# Driver code to test above methods
if __name__ == '__main__':
    _input = "123"
    target = 6
    res = getExprs(_input, target)
    printResult(res)

    _input = "125"
    target = 7
    res = getExprs(_input, target)
    printResult(res)
```

输出:

```
1+2+3 1*2*3 
1*2+5 12-5
```

**时间复杂度:** O( ![4 ^ N ](img/1e436e0c1e9689234ac92a9413a2d842.png "Rendered by QuickLaTeX.com") )
**辅助空间:** O(N)
本文由 [**Utkarsh Trivedi**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。