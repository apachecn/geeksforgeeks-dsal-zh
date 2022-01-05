# 通过删除 K 个连续的相同字符来减少字符串

> 原文:[https://www . geesforgeks . org/通过删除 k 个连续的相同字符来减少字符串/](https://www.geeksforgeeks.org/reduce-the-string-by-removing-k-consecutive-identical-characters/)

给定一个字符串 **str** 和一个整数 **K，**，任务是通过多次应用以下操作来减少字符串，直到不再可能:

> 选择一组 **K** 个连续的相同字符，并将其从字符串中删除。

最后，打印缩小的字符串。

**示例:**

> **输入:** K = 2，str = "geeksforgeeks"
> **输出:** gksforgks
> **解释:**在去除了两个出现的子串“ee”之后，该字符串简化为“gksforgks”。
> 
> **输入:** K = 3，str = " qdxxxd "
> **输出:** q
> **解释:**
> 去掉“xxx”将字符串修改为“qddd”。
> 同样，删除“ddd”会将字符串修改为“q”。

**方法:**这个问题可以使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)数据结构来解决。按照以下步骤解决问题:

*   初始化一堆[对<字符，int >](https://www.geeksforgeeks.org/pair-in-cpp-stl/) ，以存储字符及其各自的连续频率。
*   [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
*   如果当前角色与当前出现在堆栈顶部的角色不同，则将其频率设置为 **1** 。
*   否则，如果当前角色与堆叠顶部[的角色相同，则增加 **1** 的频率。](https://www.geeksforgeeks.org/stack-top-c-stl/)
*   如果堆栈顶部[的字符](https://www.geeksforgeeks.org/stack-top-c-stl/)的[频率为 **K** ，](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)[将该字符弹出堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
*   最后，打印堆栈中剩余的字符作为结果字符串。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Basic Approach is to create a Stack that store the
// Character and its continuous repetition number This is
// done using pair<char,int> Further we check at each
// iteration, whether the character matches the top of stack
// if it does then check for number of repetitions
// else add to top of stack with count 1

class Solution {
public:
    string remove_k_char(int k, string s)
    {

        // Base Case
        // If k=1 then all characters
        // can be removed at each
        // instance
        if (k == 1)
            return "";
        // initialize string
        string output = "";

        // create a stack using pair<> for storing each
        // character and corresponding
        // repetition
        stack<pair<char, int> > stk;

        // iterate through the string
        for (int i = 0; i < s.length(); i++) {

            // if stack is empty then simply add the
            // character with count 1 else check if
            // character is same as top of stack
            if (stk.empty() == true) {
                stk.push(make_pair(s[i], 1));
            }
            else {

                // if character at top of stack is same as
                // current character increase the number of
                // repetitions in the top of stack by 1
                if (s[i] == (stk.top()).first) {
                    stk.push(
                        { s[i], stk.top().second + 1 });
                    if (stk.top().second == k) {
                        int x = k;
                        while (x) {
                            stk.pop();
                            x--;
                        }
                    }
                }
                else {

                    // if character at top of stack is not
                    // same as current character push the
                    // character along with count 1 into the
                    // top of stack
                    stk.push(make_pair(s[i], 1));
                }
            }
        }

        // Iterate through the stack
        // Use string(int,char) in order to replicate the
        // character multiple times and convert into string
        // then add in front of output string
        while (!stk.empty()) {
            output += stk.top().first;
            stk.pop();
        }
        reverse(output.begin(), output.end());
        return output;
    }
};

// Driver Code
int main()
{

    string s = "geeksforgeeks";
    int k  = 2;
    Solution obj;
    cout << obj.remove_k_char(k, s) << "\n";

    return 0;
}

// This code has been contributed by Navansh Goel
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to find the reduced string
    public static String reduced_String(int k, String s)
    {
        // Base Case
        if (k == 1) {
            String ans = "";
            return ans;
        }

        // Creating a stack of type Pair
        Stack<Pair> st = new Stack<Pair>();

        // Length of the string S
        int l = s.length();
        int ctr = 0;

        // iterate through the string
        for (int i = 0; i < l; i++) {

            // if stack is empty then simply add the
            // character with count 1 else check if
            // character is same as top of stack
            if (st.size() == 0) {
                st.push(new Pair(s.charAt(i), 1));
                continue;
            }

            // if character at top of stack is same as
            // current character increase the number of
            // repetitions in the top of stack by 1
            if (st.peek().c == s.charAt(i)) {
                Pair p = st.peek();
                st.pop();
                p.ctr += 1;
                if (p.ctr == k) {
                    continue;
                }
                else {
                    st.push(p);
                }
            }
            else {

                // if character at top of stack is not
                // same as current character push the
                // character along with count 1 into the
                // top of stack
                st.push(new Pair(s.charAt(i), 1));
            }
        }

        // iterate through the stack
        // Use string(int,char) in order to replicate the
        // character multiple times and convert into string
        // then add in front of output string
        String ans = "";
        while (st.size() > 0) {
            char c = st.peek().c;
            int cnt = st.peek().ctr;
            while (cnt-- > 0)
                ans = c + ans;
            st.pop();
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int k = 2;
        String st = "geeksforgeeks";
        String ans = reduced_String(k, st);
        System.out.println(ans);
    }

    static class Pair {
        char c;
        int ctr;
        Pair(char c, int ctr)
        {
            this.c = c;
            this.ctr = ctr;
        }
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Pair class to store character and freq
class Pair:
    def __init__(self,c ,ctr):
        self.c= c
        self.ctr = ctr

class Solution:

    # Function to find the reduced string
    def reduced_String(self , k , s):

        #Base Case
        if (k == 1):
            return ""

        # Creating a stack of type Pair
        st = []

        # iterate through given string
        for i in range(len(s)):

            # if stack is empty then simply add the
            # character with count 1 else check if
            # character is same as top of stack
            if (len(st) == 0):
                st.append((Pair(s[i] , 1)))
                continue

            # if character at top of stack is same as
            # current character increase the number of
            # repetitions in the top of stack by 1
            if (st[-1].c == s[i]):

                pair = st.pop()
                pair.ctr +=1

                if (pair.ctr == k):
                    continue

                else:
                    st.append(pair)

            else:

                # if character at top of stack is not
                # same as current character push the
                # character along with count 1 into the
                # top of stack
                st.append((Pair(s[i] , 1)))

        # Iterate through the stack
        # Use string(int,char) in order to replicate the
        # character multiple times and convert into string
        # then add in front of output string
        ans = ""
        while(len(st) > 0):

            c = st[-1].c
            cnt = st[-1].ctr

            while(cnt >0):
                ans  = c + ans
                cnt -= 1

            st.pop()

        return (ans)

# Driver code
if __name__ == "__main__":

    k = 2
    s = "geeksforgeeks"
    obj = Solution()
    print(obj.reduced_String(k,s))

    # This code is contributed by chantya17.
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
public class GFG {

    // Function to find the reduced string
    public static String reduced_String(int k, String s)
    {
        // Base Case
        if (k == 1) {

            return "";
        }

        // Creating a stack of type Pair
        Stack<Pair> st = new Stack<Pair>();

        // Length of the string S
        int l = s.Length;

        // iterate through the string
        for (int i = 0; i < l; i++) {

            // if stack is empty then simply add the
            // character with count 1 else check if
            // character is same as top of stack
            if (st.Count == 0) {
                st.Push(new Pair(s[i], 1));
                continue;
            }

            // if character at top of stack is same as
            // current character increase the number of
            // repetitions in the top of stack by 1
            if (st.Peek().c == s[i]) {
                Pair p = st.Peek();
                st.Pop();
                p.ctr += 1;
                if (p.ctr == k) {
                    continue;
                }
                else {
                    st.Push(p);
                }
            }
            else {

                // if character at top of stack is not
                // same as current character push the
                // character along with count 1 into the
                // top of stack
                st.Push(new Pair(s[i], 1));
            }
        }

        // iterate through the stack
        // Use string(int,char) in order to replicate the
        // character multiple times and convert into string
        // then add in front of output string
        String ans = "";
        while (st.Count > 0) {
            char c = st.Peek().c;
            int cnt = st.Peek().ctr;
            while (cnt-- > 0)
                ans = c + ans;
            st.Pop();
        }
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int k = 2;
        String st = "geeksforgeeks";
        String ans = reduced_String(k, st);
        Console.Write(ans);
    }

    public class Pair {
        public char c;
        public int ctr;
        public Pair(char c, int ctr)
        {
            this.c = c;
            this.ctr = ctr;
        }
    }
}
// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

class Pair
{
    constructor(c,ctr)
    {
        this.c = c;
            this.ctr = ctr;
    }
}

// Function to find the reduced string
function reduced_String(k,s)
{
    // Base Case
        if (k == 1) {
            let ans = "";
            return ans;
        }

        // Creating a stack of type Pair
        let st = [];

        // Length of the string S
        let l = s.length;
        let ctr = 0;

        // iterate through the string
        for (let i = 0; i < l; i++) {

            // if stack is empty then simply add the
            // character with count 1 else check if
            // character is same as top of stack
            if (st.length == 0) {
                st.push(new Pair(s[i], 1));
                continue;
            }

            // if character at top of stack is same as
            // current character increase the number of
            // repetitions in the top of stack by 1
            if (st[st.length-1].c == s[i]) {
                let p = st[st.length-1];
                st.pop();
                p.ctr += 1;
                if (p.ctr == k) {
                    continue;
                }
                else {
                    st.push(p);
                }
            }
            else {

                // if character at top of stack is not
                // same as current character push the
                // character along with count 1 into the
                // top of stack
                st.push(new Pair(s[i], 1));
            }
        }

        // iterate through the stack
        // Use string(int,char) in order to replicate the
        // character multiple times and convert into string
        // then add in front of output string
        let ans = "";
        while (st.length > 0) {
            let c = st[st.length-1].c;
            let cnt = st[st.length-1].ctr;
            while (cnt-- > 0)
                ans = c + ans;
            st.pop();
        }
        return ans;
}

// Driver code
let k = 2;
let st = "geeksforgeeks";
let ans = reduced_String(k, st);
document.write(ans+"<br>");

// This code is contributed by rag2127
</script>
```

**Output**

```
gksforgks
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)