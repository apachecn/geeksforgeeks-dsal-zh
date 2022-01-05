# 检查最多 K 次将括号移动到任意一端是否可以获得平衡括号

> 原文:[https://www . geesforgeks . org/check-如果有可能通过将括号移动到最多 k 次的任一端来获得平衡括号/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-obtain-a-balanced-parenthesis-by-shifting-brackets-to-either-end-at-most-k-times/)

给定一个大小为 **N** 的字符串 **S** ，该字符串仅由**(“**和**)”**和一个正整数 **K** 组成，任务是通过将字符串 **S** 的任意字符最多移动 K 次到字符串**的任意一端来检查给定字符串是否可以成为有效的括号序列。**

**示例:**

> **输入:** S = ")("，K = 1
> **输出:**是
> **说明:**将 S[0]移动到字符串末尾。
> 现在修改后的字符串 S 为“()”，平衡了。因此，所需的移动次数为 1( = K)。
> 
> **输入:** S =())”，K = 0
> T3】输出:是

**方法:**给定的问题可以基于以下观察来解决:

*   如果 [N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)或者左右括号的个数不相等，则不可能构成有效的括号序列。
*   其思想是[遍历给定的序列](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/)并跟踪开括号和闭括号计数的**差值**，如果在任何一个索引处**差值**变为负数，那么在当前索引之后移动一些开括号并将其移动到开头。

按照以下步骤解决问题:

*   如果 [N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)或左右括号的[计数不相等，则不可能构成有效的括号序列。于是，打印**“否”**。否则，请执行以下步骤:](https://www.geeksforgeeks.org/number-of-closing-brackets-needed-to-complete-a-regular-bracket-sequence/)
*   初始化两个变量，比如**计数**和 **ans** 为 **0** ，分别记录开合括号的差值和所需的移动次数。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   如果当前字符 **S[i]** 是“ **(** )，那么将**计数**的值增加 **1** 。
    *   否则，将**计数**的值递减 **1** 。
    *   如果**计数**小于 **0** ，则将**计数**更新为 **0** ，并将**和**的值增加 **1** 。
*   完成以上步骤后，如果 **ans** 的值最多为 **K** ，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a valid parenthesis
// can be obtained by moving characters
// to either end at most K number of times
void minimumMoves(string s, int n, int k)
{
    // Base Case 1
    if (n & 1) {
        cout << "No";
        return;
    }

    // Count of '(' and ')'
    int countOpen = count(s.begin(),
                          s.end(), '(');
    int countClose = count(s.begin(),
                           s.end(), ')');

    // Base Case 2
    if (countOpen != countClose) {
        cout << "No";
        return;
    }

    // Store the count of moves required
    // to make a valid parenthesis
    int ans = 0;
    int cnt = 0;

    // Traverse the string
    for (int i = 0; i < n; ++i) {

        // Increment cnt if opening
        // bracket has occurred
        if (s[i] == '(')
            ++cnt;

        // Otherwise, decrement cnt by 1
        else {

            // Decrement cnt by 1
            --cnt;

            // If cnt is negative
            if (cnt < 0) {

                // Update the cnt
                cnt = 0;

                // Increment the ans
                ++ans;
            }
        }
    }

    // If ans is at most K, then
    // print Yes. Otherwise print No
    if (ans <= k)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    string S = ")(";
    int K = 1;
    minimumMoves(S, S.length(), K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if a valid parenthesis
// can be obtained by moving characters
// to either end at most K number of times
static void minimumMoves(String s, int n, int k)
{

    // Base Case 1
    if (n % 2 == 1)
    {
        System.out.println("No");
        return;
    }

    // Count of '(' and ')'
    int countOpen = 0, countClose = 0;
    for(char ch : s.toCharArray())
        if (ch == '(')
            countOpen++;
        else if (ch == ')')
            countClose++;

    // Base Case 2
    if (countOpen != countClose)
    {
        System.out.println("No");
        return;
    }

    // Store the count of moves required
    // to make a valid parenthesis
    int ans = 0;
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < n; ++i)
    {

        // Increment cnt if opening
        // bracket has occurred
        if (s.charAt(i) == '(')
            ++cnt;

        // Otherwise, decrement cnt by 1
        else
        {

            // Decrement cnt by 1
            --cnt;

            // If cnt is negative
            if (cnt < 0)
            {

                // Update the cnt
                cnt = 0;

                // Increment the ans
                ++ans;
            }
        }
    }

    // If ans is at most K, then
    // print Yes. Otherwise print No
    if (ans <= k)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver Code
public static void main(String[] args)
{
    String S = ")(";
    int K = 1;

    minimumMoves(S, S.length(), K);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to check if a valid parenthesis
# can be obtained by moving characters
# to either end at most K number of times

def minimumMoves(s, n, k):

    # Base Case 1
    if (n & 1):
        print("No")
        return

    # Count of '(' and ')'
    countOpen = s.count('(')
    countClose = s.count(')')

    # Base Case 2
    if (countOpen != countClose):
        print("No")
        return

    # Store the count of moves required
    # to make a valid parenthesis
    ans = 0
    cnt = 0

    # Traverse the string
    for i in range(n):

        # Increment cnt if opening
        # bracket has occurred
        if (s[i] == '('):
            cnt += 1

        # Otherwise, decrement cnt by 1
        else:

            # Decrement cnt by 1
            cnt -= 1

            # If cnt is negative
            if (cnt < 0):

                # Update the cnt
                cnt = 0

                # Increment the ans
                ans += 1

    # If ans is at most K, then
    # print Yes. Otherwise print No
    if (ans <= k):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == "__main__":

    S = ")("
    K = 1
    minimumMoves(S, len(S), K)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a valid parenthesis
// can be obtained by moving characters
// to either end at most K number of times
static void minimumMoves(string s, int n, int k)
{

    // Base Case 1
    if (n % 2 == 1)
    {
         Console.WriteLine("No");
        return;
    }

    // Count of '(' and ')'
    int countOpen = 0, countClose = 0;
    foreach(char ch in s.ToCharArray())
        if (ch == '(')
            countOpen++;
        else if (ch == ')')
            countClose++;

    // Base Case 2
    if (countOpen != countClose)
    {
        Console.WriteLine("No");
        return;
    }

    // Store the count of moves required
    // to make a valid parenthesis
    int ans = 0;
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < n; ++i)
    {

        // Increment cnt if opening
        // bracket has occurred
        if (s[i] == '(')
            ++cnt;

        // Otherwise, decrement cnt by 1
        else
        {

            // Decrement cnt by 1
            --cnt;

            // If cnt is negative
            if (cnt < 0)
            {

                // Update the cnt
                cnt = 0;

                // Increment the ans
                ++ans;
            }
        }
    }

    // If ans is at most K, then
    // print Yes. Otherwise print No
    if (ans <= k)
         Console.WriteLine("Yes");
    else
         Console.WriteLine("No");
}

// Driver Code
static void Main()
{
    string S = ")(";
    int K = 1;

    minimumMoves(S, S.Length, K);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if a valid parenthesis
// can be obtained by moving characters
// to either end at most K number of times
function minimumMoves(s,n,k)
{
    // Base Case 1
    if (n & 1) {
        document.write("No");
        return;
    }

    // Count of '(' and ')'
    var countOpen = 0;
    var i;
    for(i=0;i<s.length;i++){
         if(s[i]=="(")
             countOpen++;
    }
    var countClose = 0;
    for(i=0;i<s.length;i++){
         if(s[i]==")")
             countClose++;
    };

    // Base Case 2
    if (countOpen != countClose) {
        document.write("No");
        return;
    }

    // Store the count of moves required
    // to make a valid parenthesis
    var ans = 0;
    var cnt = 0;

    // Traverse the string
    for (i = 0; i < n; ++i) {

        // Increment cnt if opening
        // bracket has occurred
        if (s[i] == '(')
            ++cnt;

        // Otherwise, decrement cnt by 1
        else {

            // Decrement cnt by 1
            --cnt;

            // If cnt is negative
            if (cnt < 0) {

                // Update the cnt
                cnt = 0;

                // Increment the ans
                ++ans;
            }
        }
    }

    // If ans is at most K, then
    // print Yes. Otherwise print No
    if (ans <= k)
        document.write("Yes");
    else
        document.write("No");

}

// Driver Code
    var S = ")(";
    var K = 1;
    minimumMoves(S, S.length, K);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)