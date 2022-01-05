# 生成一次性密码或唯一标识网址

> 原文:[https://www . geesforgeks . org/generate-一次性-密码-唯一-标识-url/](https://www.geeksforgeeks.org/generate-one-time-password-unique-identification-url/)

一次性密码是在计算机系统或其他数字设备上仅对一次登录会话或事务有效的密码。更多详情请参考[本](https://en.wikipedia.org/wiki/One-time_password)。
 **算法**
从我们所有的可能性中随机挑选字符，并从中生成所需长度的字符串。OTP 一般为 6-7 个字符，6-7 个字符的随机性几乎保证了安全的登录方式。

**应用程序**

*   OTP 广泛应用于脸书、谷歌登录、无线接入、铁路门户登录等网站。
*   即使是极客代码编辑器 [IDE](https://ide.geeksforgeeks.org/) 也有一个唯一的字符串来表示通过它编译的所有代码。例如，[https://ide.geeksforgeeks.org/Ks84Ck](https://ide.geeksforgeeks.org/Ks84Ck)在末尾有唯一的字符串–**“Ks84CK”**，该字符串仅对该代码唯一。

**它是如何产生的？**
他们很有可能使用与生成动态口令相同的算法。如果偶然(非常罕见)生成的唯一字符串之前已经生成，并且与不同的代码相关联，则使用另一个随机字符串。

根据现在的情况，似乎只有六个字符串是随机生成的，用于所有代码的唯一标识。总有一天，所有可能的六个字符串可能会耗尽。所以，是的，即使是网络相关的东西也严重依赖随机性。

**两个 OTP 碰撞的概率**

*   动态口令的长度是 6，动态口令中所有可能字符的设定大小是 62。因此该对 OTP 的可能集合的总数是 **62 <sup>12</sup>** 。
*   其中一些是–[{ aaaaa，aaaaa}，{ aaaaa，aaaaab}，…..{456789, 456788}, {456789, 456789}]
*   但是等对 OTP 的可能集合是: **62 <sup>6</sup>** 。其中一些是–[{ aaaaa，aaaaa}，{aaaaab，aaaaab}，…..{456788, 456788}, {456789, 456789}]
*   因此两个 OTP 碰撞的概率为:
    **62<sup>6</sup>/62<sup>12</sup>= 1/62<sup>6</sup>= 1/56800235584 = 1.7605561<sup>-11</sup>**

所以两个 OTP 相撞的概率和你在地球上存在生命的概率一样小(你能活的年数与宇宙开始和存在的一切的年数之比)。所以，是的，OTP 比静态密码更安全！

**实施**T2】

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A C/C++ Program to generate OTP (One Time Password)
#include<bits/stdc++.h>
using namespace std;

// A Function to generate a unique OTP everytime
string generateOTP(int len)
{
    // All possible characters of my OTP
    string str = "abcdefghijklmnopqrstuvwxyzABCD"
               "EFGHIJKLMNOPQRSTUVWXYZ0123456789";
    int n = str.length();

    // String to hold my OTP
    string OTP;

    for (int i=1; i<=len; i++)
        OTP.push_back(str[rand() % n]);

    return(OTP);
}

// Driver Program to test above functions
int main()
{
    // For different values each time we run the code
    srand(time(NULL));

    // Declare the length of OTP
    int len = 6;
    printf("Your OTP is - %s", generateOTP(len).c_str());

    return(0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java Program to generate OTP (One Time Password)
class GFG{

// A Function to generate a unique OTP everytime
static String generateOTP(int len)
{
    // All possible characters of my OTP
    String str = "abcdefghijklmnopqrstuvwxyzABCD"
            +"EFGHIJKLMNOPQRSTUVWXYZ0123456789";
    int n = str.length();

    // String to hold my OTP
    String OTP="";

    for (int i = 1; i <= len; i++)
        OTP += (str.charAt((int) ((Math.random()*10) % n)));

    return(OTP);
}

// Driver code
public static void main(String[] args)
{

    // Declare the length of OTP
    int len = 6;
    System.out.printf("Your OTP is - %s", generateOTP(len));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# A Python3 Program to generate OTP (One Time Password)
import random

# A Function to generate a unique OTP everytime
def generateOTP(length):

        # All possible characters of my OTP
    str = "abcdefghijklmnopqrstuvwxyzAB\
    CDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    n = len(str);

    # String to hold my OTP
    OTP = "";

    for i in range(1,length+1):
        OTP += str[int(random.random()*10) % n];

    return (OTP);

# Driver code
if __name__ == '__main__':

    # Declare the length of OTP
    length = 6;
    print("Your OTP is - ", generateOTP(length));

# This code contributed by Rajput-Ji
```

输出(每次运行可能不同):

```
Your OTP is - 8qOtzy

```

**时间复杂度:** O(N)，其中 N =我们的 OTP 中的字符数

**辅助空间:**除了包含所有可能字符的字符串之外，我们还需要 O(N)个空间来保存动态口令，其中 N =动态口令中的字符数

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。