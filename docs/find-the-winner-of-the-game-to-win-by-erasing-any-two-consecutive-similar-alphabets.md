# 通过擦除任意两个连续的相似字母

找到要获胜的游戏的获胜者

> 原文:[https://www . geesforgeks . org/通过擦除任意两个连续的相似字母来找到获胜游戏的获胜者/](https://www.geeksforgeeks.org/find-the-winner-of-the-game-to-win-by-erasing-any-two-consecutive-similar-alphabets/)

给定一个由小写字母组成的字符串。
**游戏规则:**

*   玩家可以选择一对相似的连续字符，并将其擦除。
*   有两个玩家在玩游戏，最后一步的玩家获胜。

任务是找到赢家，如果 A 先走，两人都发挥最佳。
**例:**

```
Input: str = "kaak" 
Output: B
Explanation:
    Initial String: "kaak"
    A's turn:
        removes: "aa"
        Remaining String: "kk"
    B's turn:
        removes: "kk"
        Remaining String: ""
    Since B was the last one to play
    B is the winner.

Input: str = "kk"
Output: A
```

**方法:**我们可以用一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)来简化问题。

*   每次我们遇到一个不同于堆栈顶部的字符时，我们都会将其添加到堆栈中。
*   如果栈顶和下一个字符匹配，我们从栈中弹出该字符并增加计数。
*   最后，我们只需要通过检查计数%2 来看看谁赢了。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to play the game
// and find the winner
void findWinner(string s)
{
    int i, count = 0, n;
    n = s.length();
    stack<char> st;

    // ckecking the top of the stack with
    // the i th character of the string
    // add it to the stack if they are different
    // otherwise increment count
    for (i = 0; i < n; i++) {
        if (st.empty() || st.top() != s[i]) {
            st.push(s[i]);
        }
        else {
            count++;
            st.pop();
        }
    }

    // Check who has won
    if (count % 2 == 0) {
        cout << "B" << endl;
    }
    else {
        cout << "A" << endl;
    }
}

// Driver code
int main()
{
    string s = "kaak";

    findWinner(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
import java.util.*;

class GFG
{

// Function to play the game
// and find the winner
static void findWinner(String s)
{
    int i, count = 0, n;
    n = s.length();
    Stack<Character> st = new Stack<Character>();

    // ckecking the top of the stack with
    // the i th character of the string
    // add it to the stack if they are different
    // otherwise increment count
    for (i = 0; i < n; i++)
    {
        if (st.isEmpty() ||
            st.peek() != s.charAt(i))
        {
            st.push(s.charAt(i));
        }
        else
        {
            count++;
            st.pop();
        }
    }

    // Check who has won
    if (count % 2 == 0)
    {
        System.out.println("B");
    }
    else
    {
        System.out.println("A");
    }
}

// Driver code
public static void main(String[] args)
{
    String s = "kaak";

    findWinner(s);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to play the game
# and find the winner
def findWinner(s) :

    count = 0
    n = len(s);
    st = [];

    # ckecking the top of the stack with
    # the i th character of the string
    # add it to the stack if they are different
    # otherwise increment count
    for i in range(n) :
        if (len(st) == 0 or st[-1] != s[i]) :
            st.append(s[i]);

        else :
            count += 1;
            st.pop();

    # Check who has won
    if (count % 2 == 0) :
        print("B");

    else :
        print("A");

# Driver code
if __name__ == "__main__" :

    s = "kaak";

    findWinner(s);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation for above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to play the game
// and find the winner
static void findWinner(String s)
{
    int i, count = 0, n;
    n = s.Length;
    Stack<char> st = new Stack<char>();

    // ckecking the top of the stack with
    // the i th character of the string
    // add it to the stack if they are different
    // otherwise increment count
    for (i = 0; i < n; i++)
    {
        if (st.Count == 0 ||
            st.Peek() != s[i])
        {
            st.Push(s[i]);
        }
        else
        {
            count++;
            st.Pop();
        }
    }

    // Check who has won
    if (count % 2 == 0)
    {
        Console.WriteLine("B");
    }
    else
    {
        Console.WriteLine("A");
    }
}

// Driver code
public static void Main(String[] args)
{
    String s = "kaak";

    findWinner(s);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation for above approach

    // Function to play the game
    // and find the winner
    function findWinner(s)
    {
        let i, count = 0, n;
        n = s.length;
        let st = [];

        // ckecking the top of the stack with
        // the i th character of the string
        // add it to the stack if they are different
        // otherwise increment count
        for (i = 0; i < n; i++)
        {
            if (st.length == 0 ||
                st[st.length - 1] != s[i])
            {
                st.push(s[i]);
            }
            else
            {
                count++;
                st.pop();
            }
        }

        // Check who has won
        if (count % 2 == 0)
        {
            document.write("B");
        }
        else
        {
            document.write("A");
        }
    }

    let s = "kaak";

    findWinner(s);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
B
```