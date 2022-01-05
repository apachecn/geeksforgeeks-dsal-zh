# 处理退格字符后的字符串

> 原文:[https://www . geesforgeks . org/字符串-处理后-退格-字符/](https://www.geeksforgeeks.org/string-after-processing-backspace-characters/)

给定一个字符串 **S** ，包含**字母**和“ **#** ”。“ **#** ”代表**退格**。任务是打印不带“ **#** ”的新字符串。
**示例:**

```
Input : S = "abc#de#f#ghi#jklmn#op#"
Output : abdghjklmo

Input : S = "##geeks##for##geeks#"
Output : geefgeek
```

**方法:**用德克尔解决这个问题的简单方法如下:

> *   Traverse the string S. 。
> *   If you find any characters except "#", please push them back to Dege.
> *   If the character "#" is found, a character pops up from behind Deqing.
> *   Finally, all elements pop up from Deqing to make new strings.

**以下是上述方法的实施:**

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find new final String
string newString(string S)
{
    deque<char> q;

    for (int i = 0; i < S.length(); ++i) {

        if (S[i] != '#')
            q.push_back(S[i]);
        else if (!q.empty())
            q.pop_back();
    }

    // build final string
    string ans = "";

    while (!q.empty()) {
        ans += q.front();
        q.pop_front();
    }

    // return final string
    return ans;
}

// Driver program
int main()
{
    string S = "##geeks##for##geeks#";

    // function call to print required answer
    cout << newString(S);

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class GFG
{

// Function to find new final String
static String newString(String S)
{
    Stack<Character> q = new Stack<Character>();

    for (int i = 0; i < S.length(); ++i)
    {
        if (S.charAt(i) != '#')
            q.push(S.charAt(i));
        else if (!q.isEmpty())
            q.pop();
    }

    // build final string
    String ans = "";

    while (!q.isEmpty())
    {
        ans += q.pop();
    }

    // return final string
    String answer = "";
    for(int j = ans.length() - 1; j >= 0; j--)
    {
        answer += ans.charAt(j);
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    String S = "##geeks##for##geeks#";

    // function call to print
    // required answer
    System.out.println(newString(S));
}
}

// This code is contributed
// by prerna saini
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find new final String
def newString(S):

    q = []

    for i in range(0, len(S)):

        if S[i] != '#':
            q.append(S[i])
        elif len(q) != 0:
            q.pop()

    # Build final string
    ans = ""

    while len(q) != 0:
        ans += q[0]
        q.pop(0)

    # return final string
    return ans

# Driver Code
if __name__ == "__main__":

    S = "##geeks##for##geeks#"

    # Function call to print
    # required answer
    print(newString(S))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System.Collections.Generic;
using System;

class GFG
{

// Function to find new final String
static String newString(String S)
{
    Stack<Char> q = new Stack<Char>();

    for (int i = 0; i < S.Length; ++i)
    {
        if (S[i] != '#')
            q.Push(S[i]);
        else if (q.Count!=0)
            q.Pop();
    }

    // build final string
    String ans = "";

    while (q.Count!=0)
    {
        ans += q.Pop();
    }

    // return final string
    String answer = "";
    for(int j = ans.Length - 1; j >= 0; j--)
    {
        answer += ans[j];
    }
    return answer;
}

// Driver Code
public static void Main(String []args)
{
    String S = "##geeks##for##geeks#";

    // function call to print
    // required answer
    Console.WriteLine(newString(S));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find new final String
function newString(S)
{
    let q = [];

    for (let i = 0; i < S.length; ++i)
    {
        if (S[i] != '#')
            q.push(S[i]);
        else if (q.length!=0)
            q.pop();
    }

    // build final string
    let ans = "";

    while (q.length!=0)
    {
        ans += q.pop();
    }

    // return final string
    let answer = "";
    for(let j = ans.length - 1; j >= 0; j--)
    {
        answer += ans[j];
    }
    return answer;
}

// Driver Code
let S = "##geeks##for##geeks#";

// function call to print
// required answer
document.write(newString(S)+"<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
geefgeek
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。