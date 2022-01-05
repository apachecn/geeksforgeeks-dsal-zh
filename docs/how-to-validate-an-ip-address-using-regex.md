# 如何使用 ReGex

验证 IP 地址

> 原文:[https://www . geeksforgeeks . org/如何使用-regex/](https://www.geeksforgeeks.org/how-to-validate-an-ip-address-using-regex/) 验证 ip 地址

给定一个 [IP 地址](https://www.geeksforgeeks.org/program-determine-class-network-host-id-ipv4-address/)，任务是借助于 C++ 中的[正则表达式(Regex)将该 IP 地址验证为有效的](https://www.geeksforgeeks.org/regex-regular-expression-in-c/) [IPv4](https://www.geeksforgeeks.org/introduction-and-ipv4-datagram-header/) 地址或 [IPv6](https://www.geeksforgeeks.org/internet-protocol-version-6-ipv6/) 地址。如果 IP 地址无效，则打印无效的 IP 地址。

**示例:**

> **输入:** str = "203.120.223.13"
> **输出:**有效 IPv4
> 
> **输入:**str = " 000 . 12 . 234 . 23 . 23 "
> T3】输出:无效 IP
> 
> **输入:**str = " 2f 33:12a 0:3ea 0:0302 "
> T3】输出:无效 IP
> 
> **输入:**str = " I . am . not . an . ip "
> T3】输出:无效 IP

**进场:**

*   [c++中的 Regex(正则表达式)](https://www.geeksforgeeks.org/regex-regular-expression-in-c/)将用于检查 IP 地址。
*   **范围规范**
    指定字符或文字的范围是正则表达式中使用的最简单的标准之一。

```
i) [a-z]
ii) [A-Za-z0-9]
```

*   在上面的表达式([])中，方括号用于指定范围。
*   第一个表达式将正好匹配一个小写字符。
*   第二个表达式指定包含一个大写字符、一个小写字符和一个从 0 到 9 的数字的范围。
*   现在加入一个**”**作为表达的一部分，我们需要逃离**“”**这可以通过以下方式实现:

```
[\\.0-9]
```

上面的表达式表示一个“.”和 0 到 9 范围内的数字作为正则表达式。

*   **regex_match()** 函数用于匹配给定的模式。如果给定的表达式与字符串匹配，则此函数返回 true。否则，函数返回 false。

下面是上述方法的实现。

## C++

```
// C++ program to validate
// IP address using Regex

#include <bits/stdc++.h>
using namespace std;

// Function for Validating IP
string Validate_It(string IP)
{

    // Regex expression for validating IPv4
    regex ipv4("(([0-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])\\.){3}([0-9]|[1-9][0-9]|1[0-9][0-9]|2[0-4][0-9]|25[0-5])");

    // Regex expression for validating IPv6
    regex ipv6("((([0-9a-fA-F]){1,4})\\:){7}([0-9a-fA-F]){1,4}");

    // Checking if it is a valid IPv4 addresses
    if (regex_match(IP, ipv4))
        return "Valid IPv4";

    // Checking if it is a valid IPv6 addresses
    else if (regex_match(IP, ipv6))
        return "Valid IPv6";

    // Return Invalid
    return "Invalid IP";
}

// Driver Code
int main()
{
    // IP addresses to validate
    string IP = "203.120.223.13";
    cout << Validate_It(IP) << endl;

    IP = "fffe:3465:efab:23fe:2235:6565:aaab:0001";
    cout << Validate_It(IP) << endl;

    IP = "2F33:12a0:3Ea0:0302";
    cout << Validate_It(IP) << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to validate
# IP address using Regex
import re

# Function for Validating IP
def Validate_It(IP):

    # Regex expression for validating IPv4
    regex = "(([0-9]|[1-9][0-9]|1[0-9][0-9]|"\
            "2[0-4][0-9]|25[0-5])\\.){3}"\
            "([0-9]|[1-9][0-9]|1[0-9][0-9]|"\
            "2[0-4][0-9]|25[0-5])"

    # Regex expression for validating IPv6
    regex1 = "((([0-9a-fA-F]){1,4})\\:){7}"\
             "([0-9a-fA-F]){1,4}"

    p = re.compile(regex)
    p1 = re.compile(regex1)

    # Checking if it is a valid IPv4 addresses
    if (re.search(p, IP)):
        return "Valid IPv4"

    # Checking if it is a valid IPv6 addresses
    elif (re.search(p1, IP)):
        return "Valid IPv6"

    # Return Invalid
    return "Invalid IP"

# Driver Code

# IP addresses to validate
IP = "203.120.223.13"
print(Validate_It(IP))

IP = "fffe:3465:efab:23fe:2235:6565:aaab:0001"
print(Validate_It(IP))

IP = "2F33:12a0:3Ea0:0302"
print(Validate_It(IP))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
Valid IPv4
Valid IPv6
Invalid IP
```

***时间复杂度:** O (N)*
***辅助空间:** O (1)*