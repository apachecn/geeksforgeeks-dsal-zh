# 凯撒串联

> 原文:[https://www.geeksforgeeks.org/caesar-concatenation/](https://www.geeksforgeeks.org/caesar-concatenation/)

给定两个包含字母数字字符的[字符串](https://www.geeksforgeeks.org/strings-in-c-2/) **str1** 和 **str2** 以及一个数字 **N** 。任务是形成一个新的加密字符串，该字符串包含带有 **N** 字符的[凯撒加密](https://www.geeksforgeeks.org/caesar-cipher-in-cryptography/)的字符串 **str1** ，以及带有奇数索引的 **N** 字符的凯撒加密的字符串 **str2** 。
**例:**

> **输入:**str1 =“geekforgeks”，str2 =“geeks 123”，N = 4
> **输出:**kiojskiowkeikw 163
> **解释:**
> 移位为 4 的字符串 str 1 的凯撒文本为“kiojskiow”
> 在所有偶数索引处移位为 4 的字符串 str 2 的凯撒文本为“keikw 163”
> 结果字符串为“kiojskiow”+“keikw 163 N = 9
> **输出:** JKlmN12nfma1w
> **解释:**
> 移位 9 的字符串 str1 的凯撒文本为“jklmn 12”
> 移位 9 的字符串 str2 的凯撒文本为“nfma1w”
> 结果字符串为“jklmn 12”+“nfma1w”=“jklmn 12 nfma1w”

**方法:**
这个问题是[凯撒密码在密码学中的一个应用](https://www.geeksforgeeks.org/caesar-cipher-in-cryptography/)。下面是步骤:
思路是遍历给定的字符串 **str1** 和 **str2** ，在下面 3 种情况的基础上
移位 **N** 将 **str1** 每个索引处和 **str2** 偶数索引处的所有字符进行转换

1.  **情况 1:** 如果字符位于‘A’和‘Z’之间，则当前字符被加密为:

```
new_character = ( (current_character - 65 + N) % 26 ) + 65;
```

2.  **情况 2:** 如果字符位于‘a’和‘z’之间，则当前字符被加密为:

```
new_character = ( (current_character - 97 + N) % 26 ) + 97;
```

2.  **情况 3:** 如果字符位于‘A’和‘Z’之间，则当前字符被加密为:

```
new_character = ( (current_character - 48 + N) % 10 ) + 48;
```

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above
// approach
#include <bits/stdc++.h>
using namespace std;

void printCaesarText(string str1,
                     string str2, int N)
{

    // Traverse the string str1
    for (int i = 0; str1[i]; i++) {

        // Current character
        char ch = str1[i];

        // Case 1:
        if (ch >= 'A' && ch <= 'Z') {
            str1[i] = (ch - 65 + N) % 26 + 65;
        }

        // Case 2:
        else if (ch >= 'a' && ch <= 'z') {
            str1[i] = (ch - 97 + N) % 26 + 97;
        }

        // Case 3:
        else if (ch >= '0' && ch <= '9') {
            str1[i] = (ch - 48 + N) % 10 + 48;
        }
    }

    for (int i = 0; str2[i]; i++) {

        // If current index is odd, then
        // do nothing
        if (i & 1)
            continue;

        // Current character
        char ch = str2[i];

        // Case 1:
        if (ch >= 'A' && ch <= 'Z') {
            str2[i] = (ch - 65 + N) % 26 + 65;
        }

        // Case 2:
        else if (ch >= 'a' && ch <= 'z') {
            str2[i] = (ch - 97 + N) % 26 + 97;
        }

        // Case 3:
        else if (ch >= '0' && ch <= '9') {
            str2[i] = (ch - 48 + N) % 10 + 48;
        }
    }

    // Print the concatenated strings
    // str1 + str2
    cout << str1 + str2;
}

// Driver Code
int main()
{

    string str1 = "GeekforGeeks";
    string str2 = "Geeks123";
    int N = 4;

    printCaesarText(str1, str2, N);

    return 0;
}
```

**Output:** 

```
KiiojsvKiiowKeikw163
```

**时间复杂度:** O(N + M)，其中 N 和 M 是两个给定字符串的长度。