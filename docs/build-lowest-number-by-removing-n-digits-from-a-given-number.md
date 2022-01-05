# 通过从给定数字中删除 n 个数字来构建最低数字

> 原文:[https://www . geeksforgeeks . org/build-通过从给定号码中删除 n 位数字获得最低号码/](https://www.geeksforgeeks.org/build-lowest-number-by-removing-n-digits-from-a-given-number/)

给定一个由数字组成的字符串“str”和一个整数“n”，通过从字符串中删除“n”个数字并且不改变输入数字的顺序来构建可能的最低数字。
**例:**

```
Input: str = "4325043", n = 3
Output: "2043"

Input: str = "765028321", n = 5
Output: "0221"

Input: str = "121198", n = 2
Output: "1118"
```

这个想法是基于这样一个事实，即第一(n+1)个字符中的一个字符必须在结果数中。因此，我们选择第一(n+1)个数字中最小的一个，并将其放入结果中，并对剩余的字符重复出现。下面是完整的算法。

```
Initialize result as empty string
     res = ""
buildLowestNumber(str, n, res)
1) If n == 0, then there is nothing to remove.
   Append the whole 'str' to 'res' and return

2) Let 'len' be length of 'str'. If 'len' is smaller or equal 
   to n, then everything can be removed
   Append nothing to 'res' and return

3) Find the smallest character among first (n+1) characters
   of 'str'.  Let the index of smallest character be minIndex.
   Append 'str[minIndex]' to 'res' and recur for substring after
   minIndex and for n = n-minIndex

     buildLowestNumber(str[minIndex+1..len-1], n-minIndex).
```

下面是上述算法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    public static String removeKdigits(String num, int k)
    {
        StringBuilder result = new StringBuilder();

        // We have to delete all digits
        if (k >= num.length()) {
            return "0";
        }
        // Nothing to delete
        if (k == 0) {
            return num;
        }
        Stack<Character> s = new Stack<Character>();

        for (int i = 0; i < num.length(); i++) {
            char c = num.charAt(i);

            // Removing all digits in stack that are greater
            // than this digit(since they have higher
            // weightage)
            while (!s.isEmpty() && k > 0 && s.peek() > c) {
                s.pop();
                k--;
            }
            // ignore pushing 0
            if (!s.isEmpty() || c != '0')
                s.push(c);
        }

        // If our k isnt 0 yet then we keep poping out the
        // stack until k becomes 0
        while (!s.isEmpty() && k > 0) {
            k--;
            s.pop();
        }
        if (s.isEmpty())
            return "0";
        while (!s.isEmpty()) {
            result.append(s.pop());
        }
        String str = result.reverse().toString();

        return str;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "765028321";
        int k = 5;
        System.out.println(removeKdigits(s, 5));
    }
}
// this code is contributed by gireeshgudaparthi
```

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

string removeKdigits(string num, int k)
{
    int n = num.size();
    stack<char> mystack;
    // Store the final string in stack
    for (char c : num) {
        while (!mystack.empty() && k > 0
               && mystack.top() > c) {
            mystack.pop();
            k -= 1;
        }

        if (!mystack.empty() || c != '0')
            mystack.push(c);
    }

    // Now remove the largest values from the top of the
    // stack
    while (!mystack.empty() && k--)
        mystack.pop();
    if (mystack.empty())
        return "0";

    // Now retrieve the number from stack into a string
    // (reusing num)
    while (!mystack.empty()) {
        num[n - 1] = mystack.top();
        mystack.pop();
        n -= 1;
    }
    return num.substr(n);
}

int main()
{
    string str = "765028321";
    int k = 5;
    cout << removeKdigits(str, k);
    return 0;
}
```

**输出:**

```
1118
```

下面是 Gaurav Mamgain 贡献的 C++优化代码

## C++14

```
// C++ program to build the smallest number by removing
// n digits from a given number
#include <bits/stdc++.h>
using namespace std;

void insertInNonDecOrder(deque<char>& dq, char ch)
{

    // If container is empty , insert the current digit
    if (dq.empty())
        dq.push_back(ch);

    else {
        char temp = dq.back();

        // Keep removing digits larger than current digit
        // from the back side of deque
        while (temp > ch && !dq.empty()) {
            dq.pop_back();
            if (!dq.empty())
                temp = dq.back();
        }

        // Insert the current digit
        dq.push_back(ch);
    }
    return;
}

string buildLowestNumber(string str, int n)
{
    int len = str.length();

    // Deleting n digits means we need to print k digits
    int k = len - n;

    deque<char> dq;
    string res = "";

    // Leaving rightmost k-1 digits we need to choose
    // minimum digit from rest of the string and print it
    int i;
    for (i = 0; i <= len - k; i++)

        // Insert new digit from the back side in
        // appropriate position and/ keep removing
        // digits larger than current digit
        insertInNonDecOrder(dq, str[i]);

    // Now the minimum digit is at front of deque
    while (i < len) {

        // keep the minimum digit in output string
        res += dq.front();

        // remove minimum digit
        dq.pop_front();

        // Again insert new digit from the back
        // side in appropriate position and keep
        // removing digits larger than current digit
        insertInNonDecOrder(dq, str[i]);
        i++;
    }

    // Now only one element will be there in the deque
    res += dq.front();
    dq.pop_front();
    return res;
}

string lowestNumber(string str, int n)
{
    string res = buildLowestNumber(str, n);

    // Remove all the leading zeroes
    string ans = "";
    int flag = 0;
    for (int i = 0; i < res.length(); i++) {
        if (res[i] != '0' || flag == 1) {
            flag = 1;
            ans += res[i];
        }
    }

    if (ans.length() == 0)
        return "0";
    else
        return ans;
}

// Driver program to test above function
int main()
{
    string str = "765028321";
    int n = 5;
    cout <<lowestNumber(str, n) << endl;
    return 0;
}
// This code is contributed by Gaurav Mamgain
```

**Output**

```
221
```

**输出:**

```
0221
```

***时间复杂度:** O(N)*
***空间复杂度:** O(N)*

**进场:2**

假设给定字符串 num 的长度是 n，那么结果字符串将包含 n-k 的长度。

当我们着手解决这个问题时，我们应该确保输出字符串在它们的高权重位置包含最小值。所以我们通过使用堆栈来确保。

1.  如果 k >=n，则返回 0，如果 k=0，则返回 num。
2.  创建一个堆栈，遍历 num string，如果该位置的值大于堆栈的顶部元素，则推送该位置的值。
3.  遍历 num 字符串，如果该位置的整数值小于堆栈顶部，我们将弹出堆栈并递减 k，直到达到堆栈顶部小于我们正在查看的值的条件(同时 k>0)(通过这种方式，我们确保结果的最高有效位置用最小值填充)。
4.  如果 k 仍然大于 0，我们将弹出堆栈，直到 k 变成 0。
5.  将堆栈中的元素追加到结果字符串中。
6.  从结果字符串中删除前导零。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    public static String removeKdigits(String num, int k)
    {
        StringBuilder result = new StringBuilder();

        // We have to delete all digits
        if (k >= num.length()) {
            return "0";
        }
        // Nothing to delete
        if (k == 0) {
            return num;
        }
        Stack<Character> s = new Stack<Character>();

        for (int i = 0; i < num.length(); i++) {
            char c = num.charAt(i);

            // Removing all digits in stack that are greater
            // than this digit(since they have higher
            // weightage)
            while (!s.isEmpty() && k > 0 && s.peek() > c) {
                s.pop();
                k--;
            }
            // ignore pushing 0
            if (!s.isEmpty() || c != '0')
                s.push(c);
        }

        // If our k isnt 0 yet then we keep poping out the
        // stack until k becomes 0
        while (!s.isEmpty() && k > 0) {
            k--;
            s.pop();
        }
        if (s.isEmpty())
            return "0";
        while (!s.isEmpty()) {
            result.append(s.pop());
        }
        String str = result.reverse().toString();

        return str;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "765028321";
        int k = 5;
        System.out.println(removeKdigits(s, 5));
    }
}
// this code is contributed by gireeshgudaparthi
```

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

string removeKdigits(string num, int k)
{
    int n = num.size();
    stack<char> mystack;
    // Store the final string in stack
    for (char c : num) {
        while (!mystack.empty() && k > 0
               && mystack.top() > c) {
            mystack.pop();
            k -= 1;
        }

        if (!mystack.empty() || c != '0')
            mystack.push(c);
    }

    // Now remove the largest values from the top of the
    // stack
    while (!mystack.empty() && k--)
        mystack.pop();
    if (mystack.empty())
        return "0";

    // Now retrieve the number from stack into a string
    // (reusing num)
    while (!mystack.empty()) {
        num[n - 1] = mystack.top();
        mystack.pop();
        n -= 1;
    }
    return num.substr(n);
}

int main()
{
    string str = "765028321";
    int k = 5;
    cout << removeKdigits(str, k);
    return 0;
}
```

**Output**

```
221
```

***时间复杂度:** O(N)*
***空间复杂度:** O(N)*

本文由 **Pallav Gurha** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。