# 验证 IP 地址的程序

> 原文:[https://www . geesforgeks . org/program-to-validate-an-IP-address/](https://www.geeksforgeeks.org/program-to-validate-an-ip-address/)

编写一个验证 IPv4 地址的程序。
根据维基百科， [IPv4 地址](http://en.wikipedia.org/wiki/IP_address)用点-十进制表示法规范地表示，该表示法由四个十进制数组成，每个十进制数的范围从 0 到 255，用点隔开，例如 172.16.254.1

以下是检查给定字符串是否是有效 IPv4 地址的步骤:

**步骤 1)** 用“.”解析字符串使用“ [strtok()](http://pubs.opengroup.org/onlinepubs/009695399/functions/strtok_r.html) 函数作为分隔符。

> 例如 ptr = strtok（p， DELIm）;

**步骤 2)**
A)如果 ptr 包含任何非数字字符，则返回 0
B)将“ptr”转换为十进制数字，如‘NUM’
C)如果 NUM 不在 0-255 范围内，则返回 0
D)如果 NUM 在 0-255 范围内，且 ptr 为非空，则将“dot_counter”增加 1
E)如果 ptr 为空，则转到步骤 3，否则转到步骤 1
**步骤 3)** 如果 dot _ If= 3 返回 0，否则返回 1

## C++

```
// Program to check if a given
// string is valid IPv4 address or not
#include <bits/stdc++.h>
using namespace std;
#define DELIM "."

/* function to check whether the
   string passed is valid or not */
bool valid_part(char* s)
{
    int n = strlen(s);

    // if length of passed string is
    // more than 3 then it is not valid
    if (n > 3)
        return false;

    // check if the string only contains digits
    // if not then return false
    for (int i = 0; i < n; i++)
        if ((s[i] >= '0' && s[i] <= '9') == false)
            return false;
    string str(s);

    // if the string is "00" or "001" or
    // "05" etc then it is not valid
    if (str.find('0') == 0 && n > 1)
        return false;
    stringstream geek(str);
    int x;
    geek >> x;

    // the string is valid if the number
    // generated is between 0 to 255
    return (x >= 0 && x <= 255);
}

/* return 1 if IP string is
valid, else return 0 */
int is_valid_ip(char* ip_str)
{
    // if empty string then return false
    if (ip_str == NULL)
        return 0;
    int i, num, dots = 0;
    int len = strlen(ip_str);
    int count = 0;

    // the number dots in the original
    // string should be 3
    // for it to be valid
    for (int i = 0; i < len; i++)
        if (ip_str[i] == '.')
            count++;
    if (count != 3)
        return false;

    // See following link for strtok()

    char *ptr = strtok(ip_str, DELIM);
    if (ptr == NULL)
        return 0;

    while (ptr) {

        /* after parsing string, it must be valid */
        if (valid_part(ptr))
        {
            /* parse remaining string */
            ptr = strtok(NULL, ".");
            if (ptr != NULL)
                ++dots;
        }
        else
            return 0;
    }

    /* valid IP string must contain 3 dots */
    // this is for the cases such as 1...1 where
    // originally the no. of dots is three but
    // after iteration of the string we find
    // it is not valid
    if (dots != 3)
        return 0;
    return 1;
}

// Driver code
int main()
{
    char ip1[] = "128.0.0.1";
    char ip2[] = "125.16.100.1";
    char ip3[] = "125.512.100.1";
    char ip4[] = "125.512.100.abc";
    is_valid_ip(ip1) ? cout<<"Valid\n" : cout<<"Not valid\n";
    is_valid_ip(ip2) ? cout<<"Valid\n" : cout<<"Not valid\n";
    is_valid_ip(ip3) ? cout<<"Valid\n" : cout<<"Not valid\n";
    is_valid_ip(ip4) ? cout<<"Valid\n" : cout<<"Not valid\n";
    return 0;
}
```

**Output**

```
Valid
Valid
Not valid
Not valid

```

本文由**纳伦德拉·康拉尔卡尔**整理。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。