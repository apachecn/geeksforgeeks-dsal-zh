# 检查给定的字符串是 IPv4 还是 IPv6 或者无效

> 原文:[https://www . geesforgeks . org/check-如果给定的字符串是-IP v4-或-IPv6-或-无效/](https://www.geeksforgeeks.org/check-if-the-given-string-is-ipv4-or-ipv6-or-invalid/)

给定一个由 **N** 字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是检查给定的字符串 **S** 是 [IPv4](https://www.geeksforgeeks.org/what-is-ipv4/) 还是 [IPv6](https://www.geeksforgeeks.org/what-is-ipv6/) 或无效。如果给定的字符串 **S** 是有效的 **IPv4** ，则打印**“IP v4”**，如果字符串 **S** 是有效的 **IPv6** ，则打印**“IP v4”**。否则，打印**-1”**。

> **有效的 IPv4** 地址是一个形式为“x <sub>1</sub> 的 IP。x <sub>2</sub> 。x <sub>3</sub> 。x <sub>4</sub> ”其中 0 ≤ x <sub>i</sub> ≤ 255，x <sub>i</sub> **不能包含**前导零。
> 
> **有效的 IPv6** 地址是一个 IP，其形式为“x<sub>1</sub>:x<sub>2</sub>:x<sub>3</sub>:x<sub>4</sub>:x<sub>5</sub>:x<sub>6</sub>:x<sub>7</sub>:x<sub>8</sub>”其中:
> 
> *   1 ≤ x <sub>i</sub> 。长度≤ 4
> *   x <sub>i</sub> 是一个**十六进制字符串**，它可能包含数字、小写英文字母(' A '到' F ')和大写英文字母(' A '到' F ')。
> *   x <sub>i</sub> 中允许前导零。

**示例:**

> ***输入:**S = " 192 . 168 . 0 . 1 "*
> ***输出:** IPv4*
> ***解释:***
> *给定的字符串 S 是有效的 IPv4 地址，因为它的形式是*x<sub>1</sub>。x <sub>2</sub> 。x <sub>3</sub> 。x <sub>4</sub> ”其中 0 ≤ x <sub>i</sub> ≤ 255。
> 
> ***输入:**S = " 2001:0db 8:85 a3:0000:0000:8a2e:0370:7334 "*
> ***输出:** IPv6*

**方法:**给定的问题可以通过相对于**‘分裂弦’来解决**检查 **IPv4** 地址和**:“**检查 IPv6 地址，检查字符串为 [IPv4](https://www.geeksforgeeks.org/what-is-ipv4/) 或 [IPv6](https://www.geeksforgeeks.org/what-is-ipv6/) 或无效的条件。

按照以下步骤检查字符串是否为 IPv4:

*   初始化一个布尔变量，**和**为**真**，检查字符串是否为 IPv4。
*   存储**出现的[次数。](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/)**在给定的字符串中， **S** 在变量 **cnt** 中。
*   如果 **cnt** 的值不等于 **3** ，则**T5】将 **ans** 的值更新为 **false** 。否则，[根据字符**标记字符串**](https://www.geeksforgeeks.org/tokenizing-a-string-cpp/)、 **S** '**并将标记化字符串存储在[数组](https://www.geeksforgeeks.org/array-data-structure/) **V** 中。
*   检查 **V** 的[大小是否等于 **4** 。如果不相等，将 **ans** 的值更新为 **false** 。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)
*   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **V** ，对于每个字符串， **V** 中的**字符串**检查它是否在**【0，255】**范围内，并且不包含前导 0。如果不是，那么将 **ans** 的值更新为 **false** 。
*   如果**和**的值为真，则该字符串是有效的 IPv4 地址，否则不是有效的 IPv4 地址。

按照以下步骤检查字符串是否为 IPv6:

*   初始化一个布尔变量，**和**为**真**，检查字符串是否是 IPv6。
*   在变量 **cnt** 中存储给定字符串、 **S** 中**:“**的[出现次数。](https://www.geeksforgeeks.org/program-count-occurrence-given-character-string/)
*   如果 **cnt** 的值不等于 **7** ，则更新 **ans** 为**假**。否则，[对字符串](https://www.geeksforgeeks.org/tokenizing-a-string-cpp/)、 **S** w.r.t 字符**:'**进行标记化，并将标记化后的字符串存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **V** 中。
*   检查 **V** 的[大小是否等于 **8** 。如果不相等，将 **ans** 更新为 **false** 。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)
*   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **V** ，对于每个字符串， **V** 中的**字符串**检查其长度是否在**【1，4】**范围内，是否为有效的[十六进制数](https://www.geeksforgeeks.org/check-if-a-string-represents-a-hexadecimal-number-or-not/)。如果不是，那么将 **ans** 的值更新为 **false** 。
*   如果**和**的值为真，则该字符串是有效的 IPv6 地址。否则，它不是有效的 IPv6 地址。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the given string
// S is IPv4 or not
bool checkIPv4(string s)
{
    // Store the count of occurrence
    // of '.' in the given string
    int cnt = 0;

    // Traverse the string s
    for (int i = 0; i < s.size(); i++) {
        if (s[i] == '.')
            cnt++;
    }

    // Not a valid IP address
    if (cnt != 3)
        return false;

    // Stores the tokens
    vector<string> tokens;

    // stringstream class check1
    stringstream check1(s);
    string intermediate;

    // Tokenizing w.r.t. '.'
    while (getline(check1,
                   intermediate, '.')) {
        tokens.push_back(intermediate);
    }

    if (tokens.size() != 4)
        return false;

    // Check if all the tokenized strings
    // lies in the range [0, 255]
    for (int i = 0; i < tokens.size(); i++) {
        int num = 0;

        // Base Case
        if (tokens[i] == "0")
            continue;

        if (tokens[i].size() == 0)
            return false;

        for (int j = 0;
             j < tokens[i].size();
             j++) {
            if (tokens[i][j] > '9'
                || tokens[i][j] < '0')
                return false;

            num *= 10;
            num += tokens[i][j] - '0';

            if (num == 0)
                return false;
        }

        // Range check for num
        if (num > 255 || num < 0)
            return false;
    }

    return true;
}

// Function to check if the string
// represents a hexadecimal number
bool checkHex(string s)
{
    // Size of string s
    int n = s.length();

    // Iterate over string
    for (int i = 0; i < n; i++) {
        char ch = s[i];

        // Check if the character
        // is invalid
        if ((ch < '0' || ch > '9')
            && (ch < 'A' || ch > 'F')
            && (ch < 'a' || ch > 'f')) {
            return false;
        }
    }

    return true;
}

// Function to check if the given
// string S is IPv6 or not
bool checkIPv6(string s)
{
    // Store the count of occurrence
    // of ':' in the given string
    int cnt = 0;

    for (int i = 0; i < s.size();
         i++) {
        if (s[i] == ':')
            cnt++;
    }

    // Not a valid IP Address
    if (cnt != 7)
        return false;

    // Stores the tokens
    vector<string> tokens;

    // stringstream class check1
    stringstream check1(s);
    string intermediate;

    // Tokenizing w.r.t. ':'
    while (getline(
        check1,
        intermediate, ':')) {
        tokens.push_back(intermediate);
    }

    if (tokens.size() != 8)
        return false;

    // Check if all the tokenized strings
    // are in hexadecimal format
    for (int i = 0;
         i < tokens.size(); i++) {

        int len = tokens[i].size();

        if (!checkHex(tokens[i])
            || len > 4 || len < 1) {
            return false;
        }
    }
    return true;
}

// Function to check if the string
// S is IPv4 or IPv6 or Invalid
void checkIPAddress(string s)
{
    // Check if the string is IPv4
    if (checkIPv4(s))
        cout << "IPv4";

    // Check if the string is IPv6
    else if (checkIPv6(s))
        cout << "IPv6";

    // Otherwise, print "Invalid"
    else
        cout << "Invalid";
}

// Driver Code
int main()
{
    string S = "192.168.0.1";
    checkIPAddress(S);
    return 0;
}
```

**Output:**

```
IPv4

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)