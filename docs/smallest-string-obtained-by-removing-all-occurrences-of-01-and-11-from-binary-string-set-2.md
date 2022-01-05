# 通过从二进制字符串|集合 2

中移除 01 和 11 的所有出现而获得的最小字符串

> 原文:[https://www . geesforgeks . org/minist-string-通过从二进制字符串集合-2 中移除所有出现的-01 和-11 获得/](https://www.geeksforgeeks.org/smallest-string-obtained-by-removing-all-occurrences-of-01-and-11-from-binary-string-set-2/)

给定一个长度为 **N** 、的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是通过移除所有出现的 [子字符串](https://www.geeksforgeeks.org/substring-in-java/)S**【01】**和**【11】**找到可能的最小字符串。删除任何子字符串后，连接字符串的其余部分。

**示例:**

> **输入:**S =“1010”
> **输出:** 2
> **解释:**去除子串“01”将字符串 S 修改为“10”。
> 
> **输入:**S = " 111 "
> T3】输出:1**T6】**

[**堆叠**](https://www.geeksforgeeks.org/stack-data-structure/) **【基于】的方法:**参考[上一篇文章](https://www.geeksforgeeks.org/smallest-string-obtained-by-removing-all-occurrences-of-01-and-11-from-binary-string/)找到给定操作可能的最小字符串的长度。

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**空间优化方法:**上述方法可以通过只存储未删除字符的长度进行空间优化。按照以下步骤解决问题:

*   初始化一个变量，比如说 **st** 为 **0，**来存储可能的最小字符串的长度。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下步骤:
    *   如果 **st** 大于 **0** 且**S【I】**等于“ **1** ，则通过将 **st** 递减 **1** 来弹出最后一个元素。
    *   否则，将 **st** 增加 **1。**
*   最后，完成以上步骤后，打印 **st** 中得到的答案。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of
// the smallest string possible by
// removing substrings "01" and "11"
int shortestString(string S, int N)
{
    // Stores the length of
    // the smallest string
    int st = 0;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If st is greater
        // than 0 and S[i] is '1'
        if (st && S[i] == '1') {

            // Delete the last
            // character and
            // decrement st by 1
            st--;
        }

        // Otherwise
        else {

            // Increment st by 1
            st++;
        }
    }

    // Return the answer in st
    return st;
}

// Driver Code
int main()
{
    // Input
    string S = "1010";

    int N = S.length();

    // Function call
    cout << shortestString(S, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG_JAVA {

    // Function to find the length of
    // the smallest string possible by
    // removing substrings "01" and "11"
    static int shortestString(String S, int N)
    {
        // Stores the length of
        // the smallest string
        int st = 0;

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // If st is greater
            // than 0 and S[i] is '1'
            if (st > 0 && S.charAt(i) == '1') {

                // Delete the last
                // character and
                // decrement st by 1
                st--;
            }

            // Otherwise
            else {

                // Increment st by 1
                st++;
            }
        }

        // Return the answer in st
        return st;
    }

    // Driver code
    public static void main(String[] args)
    {
      // Input
        String S = "1010";
        int N = S.length();

        // Function call
        System.out.println(shortestString(S, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of
# the smallest string possible by
# removing substrings "01" and "11"
def shortestString(S, N) :

    # Stores the length of
    # the smallest string
    st = 0;

    # Traverse the string S
    for i in range(N) :

        # If st is greater
        # than 0 and S[i] is '1'
        if (st and S[i] == '1') :

            # Delete the last
            # character and
            # decrement st by 1
            st -= 1;

        # Otherwise
        else :

            # Increment st by 1
            st += 1;

    # Return the answer in st
    return st;

# Driver Code
if __name__ == "__main__" :

    # Input
    S = "1010";

    N = len(S);

    # Function call
    print(shortestString(S, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG_JAVA {

    // Function to find the length of
    // the smallest string possible by
    // removing substrings "01" and "11"
    static int shortestString(string S, int N)
    {

        // Stores the length of
        // the smallest string
        int st = 0;

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // If st is greater
            // than 0 and S[i] is '1'
            if (st > 0 && S[i] == '1') {

                // Delete the last
                // character and
                // decrement st by 1
                st--;
            }

            // Otherwise
            else {

                // Increment st by 1
                st++;
            }
        }

        // Return the answer in st
        return st;
    }

    // Driver code
    public static void Main(string[] args)
    {
      // Input
        string S = "1010";
        int N = S.Length;

        // Function call
        Console.WriteLine(shortestString(S, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the length of
    // the smallest string possible by
    // removing substrings "01" and "11"
    function shortestString(S, N)
    {

        // Stores the length of
        // the smallest string
        let st = 0;

        // Traverse the string S
        for (let i = 0; i < N; i++) {

            // If st is greater
            // than 0 and S[i] is '1'
            if (st > 0 && S[i] == '1') {

                // Delete the last
                // character and
                // decrement st by 1
                st--;
            }

            // Otherwise
            else {

                // Increment st by 1
                st++;
            }
        }

        // Return the answer in st
        return st;
    }

    // Input
    let S = "1010";
    let N = S.length;

    // Function call
    document.write(shortestString(S, N));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)