# 删除无效括号

> 原文:[https://www.geeksforgeeks.org/remove-invalid-parentheses/](https://www.geeksforgeeks.org/remove-invalid-parentheses/)

将给出一个表达式，该表达式可以包含左括号和右括号以及可选的一些字符，字符串中不会有其他运算符。我们需要删除最少数量的括号来使输入字符串有效。如果可能有多个有效输出，删除相同数量的括号，然后打印所有这样的输出。
**例:**

```
Input  : str = “()())()” -
Output : ()()() (())()
There are two possible solutions
"()()()" and "(())()"

Input  : str = (v)())()
Output : (v)()()  (v())()
```

由于我们需要生成所有可能的输出，我们将通过移除一个左括号或右括号来回溯所有状态，并检查它们是否有效(如果无效)，然后将移除的括号添加回来并转到下一个状态。我们将使用 BFS 在各州之间移动，使用 BFS 将确保移除最少数量的括号，因为我们逐级遍历各州，每个级别对应于一个额外的括号移除。除此之外，BFS 不涉及递归，因此也节省了传递参数的开销。
下面的代码有一个方法 isValidString 来检查字符串的有效性，它计算每个索引处的左括号和右括号，忽略非括号字符。如果在任何时刻右括号的计数变得大于开，那么我们返回 false，否则我们继续更新计数变量。

## C++

```
/*  C/C++ program to remove invalid parenthesis */
#include <bits/stdc++.h>
using namespace std;

//  method checks if character is parenthesis(open
// or closed)
bool isParenthesis(char c)
{
    return ((c == '(') || (c == ')'));
}

//  method returns true if string contains valid
// parenthesis
bool isValidString(string str)
{
    int cnt = 0;
    for (int i = 0; i < str.length(); i++)
    {
        if (str[i] == '(')
            cnt++;
        else if (str[i] == ')')
            cnt--;
        if (cnt < 0)
            return false;
    }
    return (cnt == 0);
}

//  method to remove invalid parenthesis
void removeInvalidParenthesis(string str)
{
    if (str.empty())
        return ;

    //  visit set to ignore already visited string
    set<string> visit;

    //  queue to maintain BFS
    queue<string> q;
    string temp;
    bool level;

    //  pushing given string as starting node into queue
    q.push(str);
    visit.insert(str);
    while (!q.empty())
    {
        str = q.front();  q.pop();
        if (isValidString(str))
        {
            cout << str << endl;

            // If answer is found, make level true
            // so that valid string of only that level
            // are processed.
            level = true;
        }
        if (level)
            continue;
        for (int i = 0; i < str.length(); i++)
        {
            if (!isParenthesis(str[i]))
                continue;

            // Removing parenthesis from str and
            // pushing into queue,if not visited already
            temp = str.substr(0, i) + str.substr(i + 1);
            if (visit.find(temp) == visit.end())
            {
                q.push(temp);
                visit.insert(temp);
            }
        }
    }
}

//  Driver code to check above methods
int main()
{
    string expression = "()())()";
    removeInvalidParenthesis(expression);

    expression = "()v)";
    removeInvalidParenthesis(expression);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove invalid parenthesis
import java.util.*;

class GFG
{

// method checks if character is parenthesis(open
// or closed)
static boolean isParenthesis(char c)
{
    return ((c == '(') || (c == ')'));
}

// method returns true if string contains valid
// parenthesis
static boolean isValidString(String str)
{
    int cnt = 0;
    for (int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == '(')
            cnt++;
        else if (str.charAt(i) == ')')
            cnt--;
        if (cnt < 0)
            return false;
    }
    return (cnt == 0);
}

// method to remove invalid parenthesis
static void removeInvalidParenthesis(String str)
{
    if (str.isEmpty())
        return;

    // visit set to ignore already visited string
    HashSet<String> visit = new HashSet<String>();

    // queue to maintain BFS
    Queue<String> q = new LinkedList<>();
    String temp;
    boolean level = false;

    // pushing given string as
    // starting node into queue
    q.add(str);
    visit.add(str);
    while (!q.isEmpty())
    {
        str = q.peek(); q.remove();
        if (isValidString(str))
        {
            System.out.println(str);

            // If answer is found, make level true
            // so that valid string of only that level
            // are processed.
            level = true;
        }
        if (level)
            continue;
        for (int i = 0; i < str.length(); i++)
        {
            if (!isParenthesis(str.charAt(i)))
                continue;

            // Removing parenthesis from str and
            // pushing into queue,if not visited already
            temp = str.substring(0, i) + str.substring(i + 1);
            if (!visit.contains(temp))
            {
                q.add(temp);
                visit.add(temp);
            }
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String expression = "()())()";
    removeInvalidParenthesis(expression);

    expression = "()v)";
    removeInvalidParenthesis(expression);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to remove invalid parenthesis

# Method checks if character is parenthesis(open
# or closed)
def isParenthesis(c):
    return ((c == '(') or (c == ')'))

# method returns true if contains valid
# parenthesis
def isValidString(str):
    cnt = 0
    for i in range(len(str)):
        if (str[i] == '('):
            cnt += 1
        elif (str[i] == ')'):
            cnt -= 1
        if (cnt < 0):
            return False
    return (cnt == 0)

# method to remove invalid parenthesis
def removeInvalidParenthesis(str):
    if (len(str) == 0):
        return

    # visit set to ignore already visited
    visit = set()

    # queue to maintain BFS
    q = []
    temp = 0
    level = 0

    # pushing given as starting node into queu
    q.append(str)
    visit.add(str)
    while(len(q)):
        str = q[0]
        q.pop()
        if (isValidString(str)):
            print(str)

            # If answer is found, make level true
            # so that valid of only that level
            # are processed.
            level = True
        if (level):
            continue
        for i in range(len(str)):
            if (not isParenthesis(str[i])):
                continue

            # Removing parenthesis from str and
            # pushing into queue,if not visited already
            temp = str[0:i] + str[i + 1:]
            if temp not in visit:
                q.append(temp)
                visit.add(temp)

# Driver Code
expression = "()())()"
removeInvalidParenthesis(expression)
expression = "()v)"
removeInvalidParenthesis(expression)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to remove invalid parenthesis
using System;
using System.Collections.Generic;

class GFG
{

// method checks if character is
// parenthesis(open or closed)
static bool isParenthesis(char c)
{
    return ((c == '(') || (c == ')'));
}

// method returns true if string contains
// valid parenthesis
static bool isValidString(String str)
{
    int cnt = 0;
    for (int i = 0; i < str.Length; i++)
    {
        if (str[i] == '(')
            cnt++;
        else if (str[i] == ')')
            cnt--;
        if (cnt < 0)
            return false;
    }
    return (cnt == 0);
}

// method to remove invalid parenthesis
static void removeInvalidParenthesis(String str)
{
    if (str == null || str == "")
        return;

    // visit set to ignore already visited string
    HashSet<String> visit = new HashSet<String>();

    // queue to maintain BFS
    Queue<String> q = new Queue<String>();
    String temp;
    bool level = false;

    // pushing given string as
    // starting node into queue
    q.Enqueue(str);
    visit.Add(str);
    while (q.Count != 0)
    {
        str = q.Peek(); q.Dequeue();
        if (isValidString(str))
        {
            Console.WriteLine(str);

            // If answer is found, make level true
            // so that valid string of only that level
            // are processed.
            level = true;
        }

        if (level)
            continue;
        for (int i = 0; i < str.Length; i++)
        {
            if (!isParenthesis(str[i]))
                continue;

            // Removing parenthesis from str and
            // pushing into queue,if not visited already
            temp = str.Substring(0, i) +
                   str.Substring(i + 1);
            if (!visit.Contains(temp))
            {
                q.Enqueue(temp);
                visit.Add(temp);
            }
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    String expression = "()())()";
    removeInvalidParenthesis(expression);

    expression = "()v)";
    removeInvalidParenthesis(expression);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to remove invalid parenthesis

// method checks if character is parenthesis(open
// or closed)
function isParenthesis(c)
{
    return ((c == '(') || (c == ')'));
}

// method returns true if string contains valid
// parenthesis
function isValidString(str)
{
    let cnt = 0;
    for (let i = 0; i < str.length; i++)
    {
        if (str[i] == '(')
            cnt++;
        else if (str[i] == ')')
            cnt--;
        if (cnt < 0)
            return false;
    }
    return (cnt == 0);
}

// method to remove invalid parenthesis
function removeInvalidParenthesis(str)
{
    if (str.length==0)
        return;

    // visit set to ignore already visited string
    let visit = new Set();

    // queue to maintain BFS
    let q = [];
    let temp;
    let level = false;

    // pushing given string as
    // starting node into queue
    q.push(str);
    visit.add(str);
    while (q.length!=0)
    {
        str = q.shift();
        if (isValidString(str))
        {
            document.write(str+"<br>");

            // If answer is found, make level true
            // so that valid string of only that level
            // are processed.
            level = true;
        }
        if (level)
            continue;
        for (let i = 0; i < str.length; i++)
        {
            if (!isParenthesis(str[i]))
                continue;

            // Removing parenthesis from str and
            // pushing into queue,if not visited already
            temp = str.substring(0, i) + str.substring(i + 1);
            if (!visit.has(temp))
            {
                q.push(temp);
                visit.add(temp);
            }
        }
    }
}

// Driver Code
let expression = "()())()";
removeInvalidParenthesis(expression);

expression = "()v)";
removeInvalidParenthesis(expression);

// This code is contributed by rag2127

</script>
```

**输出:**

```
(())()
()()()
(v)
()v
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。