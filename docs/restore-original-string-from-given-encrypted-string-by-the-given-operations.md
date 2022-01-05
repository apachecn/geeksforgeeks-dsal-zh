# 通过给定的操作从给定的加密字符串恢复原始字符串

> 原文:[https://www . geeksforgeeks . org/restore-original-string-from-给定-加密-按给定-字符串-操作/](https://www.geeksforgeeks.org/restore-original-string-from-given-encrypted-string-by-the-given-operations/)

给定一个字符串 **str** 和一个正整数 **N** ，任务是反转 **N** 个字符，跳过 **N** 个字符，直到字符串结束，生成加密消息。

**示例:**

> **输入:** str = "ihTs suohld ebeas！y "，K = 3
> T3】输出:这个应该很容易！
> **解释:**
> 反向“ihT”->“Thi”
> “s”不变
> “uoh”->“Hou”等等。
> 
> **输入:** str = "！ysae eb dluohs sihT "，K = 30
> T3】输出:这个应该很容易！
> **说明:**
> 由于 30 大于给定字符串的长度(= 20)，只需打印字符串的反面即可。

**方法:**按照以下步骤解决问题:

*   遍历给定的字符串。
*   将迭代器增加 **2 * N** 。
*   逐步反转 **N** 字符。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to decrypt and print the
// original strings
int decryptString(string s, unsigned int N)
{

    for (unsigned int i = 0; i < s.size();
         i += 2 * N) {
        auto end = s.begin() + i + N;

        // If length is exceeded
        if (i + N > s.size())
            end = s.end();

        // Reverse the string
        reverse(s.begin() + i, end);

    }

    cout << s << endl;
}

// Driver Code
int main()
{
    string s = "ihTs suohld  ebeas!y";
    unsigned int N = 3;
    decryptString(s, N);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to decrypt and print the
# original strings
def decryptString(s, N):

    for i in range(0, len(s), 2 * N):
        if (i + N < len(s)):
            end = s[i + N]

        # If length is exceeded
        if (i + N > len(s)):
            end = s[-1]

        # Reverse the string
        if (i == 0):
            s = s[i + N - 1::-1] + s[i + N:]
        else:
            s = s[:i] + s[i + N - 1:i - 1:-1] + s[i + N:]

    print(s)

# Driver Code
if __name__ == "__main__":

    s = "ihTs suohld  ebeas!y"
    N = 3

    decryptString(s, N)

# This code is contributed by ukasp
```

**Output:** 

```
This should be easy!
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*