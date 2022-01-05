# 实施安全散列算法–512(SHA-512)作为功能编程范例

> 原文:[https://www . geesforgeks . org/implement-secure-hashing-algorithm-512-sha-512-as-functional-programming-paradigm/](https://www.geeksforgeeks.org/implement-secure-hashing-algorithm-512-sha-512-as-functional-programming-paradigm/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)T2 S，任务是找到给定字符串 **S** 的 [SHA-512 哈希值](https://www.geeksforgeeks.org/sha-512-hash-in-java/)。

**示例:**

> **输入:**s = " geeksforgeeks "
> T3】输出:ACC 10c 4 e 0b 38617 f 59 e 88 e 4925 e 894 afae 5 EC 948 c 2 af 6 f 44903 f 039 f 9 Fe 47 a 9210 e 01d 5 CD 926 c 142 BDC 9179 c 2 ad 30 f 927 a 8 f 69421
> 
> **输入:**s = " hello world "
> T3】输出:
> 309 ECC 489 c112d 6 EB 4cc 40 f2c 902 f4b 4 d0s 0 和 77ee 511 a 7c7 a9 BCD 3 ca 86 D4 CD 86 f 989 DD 35 BC 5 ff 49670 da 34255 b 45 B0 CFD 830 和 81f605dcf

**方法:**按照以下步骤解决问题:

*   [将给定字符串转换为二进制形式](https://www.geeksforgeeks.org/convert-string-binary-sequence/)。
*   将**‘1’**附加到弦上，然后连续地**‘0’**直到弦的长度为<**(N %(1024–128))**。
*   在字符串 **S** 中添加 **N** 的 128 位[二进制表示](https://www.geeksforgeeks.org/binary-representations-in-digital-logic/)。
*   找到 **1024** 大小的组块数，并存储在变量中，比如**组块**为 **N/1024** 。
*   将[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 分割成 **16** 块 **64** 字符。
*   通过执行以下操作，将组块数量扩展至 **80** :
    *   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【16，80】**然后找到 **4** 值说出 **WordA，WordB，WordC，WordD** 为:
        *   **WordA = rotate_right(消息[g–2]，19) ^ rotate_right(消息[g–2，61) ^ shift_right(消息[g–2，6)** 。
        *   **word b = Message[g–7]**。
        *   **worc = rotate _ right(消息[g–15]，1) ^ rotate_right(消息[g–15]，8) ^ shift_right(消息[g–15，7)** 。
        *   **WordD = 消息 [g – 16]** .
    *   将**消息【g】**的值更新为**(WordA+WordB+WordC+WordD)**。
*   初始化 **8** 变量表示 64 位类型的 **A** 、 **B** 、 **C** 、 **D** 、 **E** 、 **F** 、 **G** 、 **H** 来存储给定字符串 **S** 的最终哈希值。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **区块【】**并执行以下步骤:
    *   使用哈希函数逐个旋转更新 **A** 、 **B** 、 **C** 、 **D** 、 **E** 、 **F** 、 **G** 、 **H** 的值，直到 80 次迭代。
    *   现在，通过 **A** 、 **B** 、**C**C**、**D**、 **E** 、 **F** 、 **G** 、 **H** 的前值之和更新 **A** 的值 **H** 以及 **A** 、 **B** 、 **C** 、 **D** 、 **E** 、 **F** 、 **G** 、 **H** 的最新更新值。**
*   完成上述步骤后，打印 **A** 、 **B** 、 **C** 、 **D** 、 **E** 、 **F** 、 **G** 、 **H** 的[十六进制值，得到给定字符串的哈希值。](https://www.geeksforgeeks.org/how-to-add-two-hexadecimal-numbers/)

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
typedef unsigned long long int int64;

int64 Message[80];

// Stores the hexadecimal values for
// calculating hash values
const int64 Constants[80]
    = { 0x428a2f98d728ae22, 0x7137449123ef65cd,
        0xb5c0fbcfec4d3b2f, 0xe9b5dba58189dbbc,
        0x3956c25bf348b538, 0x59f111f1b605d019,
        0x923f82a4af194f9b, 0xab1c5ed5da6d8118,
        0xd807aa98a3030242, 0x12835b0145706fbe,
        0x243185be4ee4b28c, 0x550c7dc3d5ffb4e2,
        0x72be5d74f27b896f, 0x80deb1fe3b1696b1,
        0x9bdc06a725c71235, 0xc19bf174cf692694,
        0xe49b69c19ef14ad2, 0xefbe4786384f25e3,
        0x0fc19dc68b8cd5b5, 0x240ca1cc77ac9c65,
        0x2de92c6f592b0275, 0x4a7484aa6ea6e483,
        0x5cb0a9dcbd41fbd4, 0x76f988da831153b5,
        0x983e5152ee66dfab, 0xa831c66d2db43210,
        0xb00327c898fb213f, 0xbf597fc7beef0ee4,
        0xc6e00bf33da88fc2, 0xd5a79147930aa725,
        0x06ca6351e003826f, 0x142929670a0e6e70,
        0x27b70a8546d22ffc, 0x2e1b21385c26c926,
        0x4d2c6dfc5ac42aed, 0x53380d139d95b3df,
        0x650a73548baf63de, 0x766a0abb3c77b2a8,
        0x81c2c92e47edaee6, 0x92722c851482353b,
        0xa2bfe8a14cf10364, 0xa81a664bbc423001,
        0xc24b8b70d0f89791, 0xc76c51a30654be30,
        0xd192e819d6ef5218, 0xd69906245565a910,
        0xf40e35855771202a, 0x106aa07032bbd1b8,
        0x19a4c116b8d2d0c8, 0x1e376c085141ab53,
        0x2748774cdf8eeb99, 0x34b0bcb5e19b48a8,
        0x391c0cb3c5c95a63, 0x4ed8aa4ae3418acb,
        0x5b9cca4f7763e373, 0x682e6ff3d6b2b8a3,
        0x748f82ee5defb2fc, 0x78a5636f43172f60,
        0x84c87814a1f0ab72, 0x8cc702081a6439ec,
        0x90befffa23631e28, 0xa4506cebde82bde9,
        0xbef9a3f7b2c67915, 0xc67178f2e372532b,
        0xca273eceea26619c, 0xd186b8c721c0c207,
        0xeada7dd6cde0eb1e, 0xf57d4f7fee6ed178,
        0x06f067aa72176fba, 0x0a637dc5a2c898a6,
        0x113f9804bef90dae, 0x1b710b35131c471b,
        0x28db77f523047d84, 0x32caab7b40c72493,
        0x3c9ebe0a15c9bebc, 0x431d67c49c100d4c,
        0x4cc5d4becb3e42b6, 0x597f299cfc657e2a,
        0x5fcb6fab3ad6faec, 0x6c44198c4a475817 };

// Function to convert a binary string
// to hexa-decimal value
string gethex(string bin)
{
    if (bin == "0000")
        return "0";
    if (bin == "0001")
        return "1";
    if (bin == "0010")
        return "2";
    if (bin == "0011")
        return "3";
    if (bin == "0100")
        return "4";
    if (bin == "0101")
        return "5";
    if (bin == "0110")
        return "6";
    if (bin == "0111")
        return "7";
    if (bin == "1000")
        return "8";
    if (bin == "1001")
        return "9";
    if (bin == "1010")
        return "a";
    if (bin == "1011")
        return "b";
    if (bin == "1100")
        return "c";
    if (bin == "1101")
        return "d";
    if (bin == "1110")
        return "e";
    if (bin == "1111")
        return "f";
}

// Function to convert a decimal value
// to hexa decimal value
string decimaltohex(int64 deci)
{
    // Stores the value as string
    string EQBIN = bitset<64>(deci).to_string();

    // Stores the equivalent hexa decimal
    string hexstring = "";
    string temp;

    // Traverse the string EQBIN
    for (unsigned int i = 0;
         i < EQBIN.length(); i += 4) {
        temp = EQBIN.substr(i, 4);
        hexstring += gethex(temp);
    }

    // Return the hexstring
    return hexstring;
}

// Function to convert a binary
// string to decimal value
int64 BintoDec(string bin)
{

    int64 value = bitset<64>(bin)
                      .to_ullong();
    return value;
}

// Function to right rotate x by n bits
int64 rotate_right(int64 x, int n)
{
    return (x >> n) | (x << (64 - n));
}

// Function to right shift x by n bits
int64 shift_right(int64 x, int n)
{
    return (x >> n);
}

// Function to divide the string
// into chunks
void separator(string getBlock)
{
    // Stores the size of chunks
    int chunknum = 0;

    // Traverse the string S
    for (unsigned int i = 0;
         i < getBlock.length();
         i += 64, ++chunknum) {

        // Update the Message[chunknum]
        Message[chunknum]
            = BintoDec(getBlock.substr(i, 64));
    }

    // Iterate over the range [16, 80]
    for (int g = 16; g < 80; ++g) {

        // Find the WordA
        int64 WordA = rotate_right(Message[g - 2], 19)
                      ^ rotate_right(Message[g - 2], 61)
                      ^ shift_right(Message[g - 2], 6);

        // Find the WordB
        int64 WordB = Message[g - 7];

        // Find the WordC
        int64 WordC = rotate_right(Message[g - 15], 1)
                      ^ rotate_right(Message[g - 15], 8)
                      ^ shift_right(Message[g - 15], 7);

        // Find the WordD
        int64 WordD = Message[g - 16];

        // Find the resultant code
        int64 T = WordA + WordB + WordC + WordD;

        // Return the resultant Hash Code
        Message[g] = T;
    }
}

// Function to find the major of a, b, c
int64 maj(int64 a, int64 b, int64 c)
{
    return (a & b) ^ (b & c) ^ (c & a);
}

// Function to find the ch value of a,
// b, and c
int64 Ch(int64 e, int64 f, int64 g)
{
    return (e & f) ^ (~e & g);
}

// Function to find the Bitwise XOR with
// the right rotate over 14, 18, and 41
int64 sigmaE(int64 e)
{
    // Return the resultant value
    return rotate_right(e, 14)
           ^ rotate_right(e, 18)
           ^ rotate_right(e, 41);
}

// Function to find the Bitwise XOR with
// the right rotate over 28, 34, and 39
int64 sigmaA(int64 a)
{

    // Return the resultant value
    return rotate_right(a, 28)
           ^ rotate_right(a, 34)
           ^ rotate_right(a, 39);
}

// Function to generate the hash code
void Func(int64 a, int64 b, int64 c,
          int64& d, int64 e, int64 f,
          int64 g, int64& h, int K)
{
    // Find the Hash Code
    int64 T1 = h + Ch(e, f, g) + sigmaE(e) + Message[K]
               + Constants[K];
    int64 T2 = sigmaA(a) + maj(a, b, c);

    d = d + T1;
    h = T1 + T2;
}

// Function to convert the hash value
// of a given string
string SHA512(string myString)
{
    // Stores the 8 blocks of size 64
    int64 A = 0x6a09e667f3bcc908;
    int64 B = 0xbb67ae8584caa73b;
    int64 C = 0x3c6ef372fe94f82b;
    int64 D = 0xa54ff53a5f1d36f1;
    int64 E = 0x510e527fade682d1;
    int64 F = 0x9b05688c2b3e6c1f;
    int64 G = 0x1f83d9abfb41bd6b;
    int64 H = 0x5be0cd19137e2179;

    int64 AA, BB, CC, DD, EE, FF, GG, HH;

    stringstream fixedstream;

    // Traverse the string S
    for (int i = 0;
         i < myString.size(); ++i) {

        // Add the character to stream
        fixedstream << bitset<8>(myString[i]);
    }

    // Stores string of size 1024
    string s1024;

    // Stores the string in the
    // fixedstream
    s1024 = fixedstream.str();

    // Stores the length of string
    int orilen = s1024.length();
    int tobeadded;

    // Find moded string length
    int modded = s1024.length() % 1024;

    // If 1024-128 is greater than modded
    if (1024 - modded >= 128) {
        tobeadded = 1024 - modded;
    }

    // Else if 1024-128 is less than modded
    else if (1024 - modded < 128) {
        tobeadded = 2048 - modded;
    }

    // Append 1 to string
    s1024 += "1";

    // Append tobeadded-129 zeros
    // in the string
    for (int y = 0; y < tobeadded - 129; y++) {
        s1024 += "0";
    }

    // Stores the binary representation
    // of string length
    string lengthbits
        = std::bitset<128>(orilen).to_string();

    // Append the lengthbits to string
    s1024 += lengthbits;

    // Find the count of chunks of
    // size 1024 each
    int blocksnumber = s1024.length() / 1024;

    // Stores the numbering of chunks
    int chunknum = 0;

    // Stores hash value of each blocks
    string Blocks[blocksnumber];

    // Traverse the string s1024
    for (int i = 0; i < s1024.length();
         i += 1024, ++chunknum) {
        Blocks[chunknum] = s1024.substr(i, 1024);
    }

    // Traverse tha array Blocks[]
    for (int letsgo = 0;
         letsgo < blocksnumber;
         ++letsgo) {

        // Divide the current string
        // into 80 blocks size 16 each
        separator(Blocks[letsgo]);

        AA = A;
        BB = B;
        CC = C;
        DD = D;
        EE = E;
        FF = F;
        GG = G;
        HH = H;

        int count = 0;

        // Find hash values
        for (int i = 0; i < 10; i++) {

            // Find the Hash Values

            Func(A, B, C, D, E, F, G, H, count);
            count++;
            Func(H, A, B, C, D, E, F, G, count);
            count++;
            Func(G, H, A, B, C, D, E, F, count);
            count++;
            Func(F, G, H, A, B, C, D, E, count);
            count++;
            Func(E, F, G, H, A, B, C, D, count);
            count++;
            Func(D, E, F, G, H, A, B, C, count);
            count++;
            Func(C, D, E, F, G, H, A, B, count);
            count++;
            Func(B, C, D, E, F, G, H, A, count);
            count++;
        }

        // Update the value of A, B, C,
        // D, E, F, G, H

        A += AA;
        B += BB;
        C += CC;
        D += DD;
        E += EE;
        F += FF;
        G += GG;
        H += HH;
    }

    stringstream output;

    // Print the hexadecimal value of
    // strings as the resultant SHA-512
    output << decimaltohex(A);
    output << decimaltohex(B);
    output << decimaltohex(C);
    output << decimaltohex(D);
    output << decimaltohex(E);
    output << decimaltohex(F);
    output << decimaltohex(G);
    output << decimaltohex(H);

    // Return the string
    return output.str();
}

// Driver Code
int main()
{
    // Input
    string S = "GeeksForGeeks";

    // Function Call
    cout << S << ": " << SHA512(S);

    return 0;
}
```

**Output:** 

```
GeeksForGeeks: 0acc10c4e0b38617f59e88e49215e2e894afaee5ec948c2af6f44039f03c9fe47a9210e01d5cd926c142bdc9179c2ad30f927a8faf69421ff60a5eaddcf8cb9c
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)