# 汉明码在 C/C++中的实现

> 原文:[https://www . geesforgeks . org/hamming-code-implementation-in-c-CPP/](https://www.geeksforgeeks.org/hamming-code-implementation-in-c-cpp/)

**先决条件:** [汉明码](https://www.geeksforgeeks.org/hamming-code-in-computer-network/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **msgBit[]** 形式的消息位，任务是找到给定消息位的汉明码。

**示例:**

> **输入:** S = "0101"
> **输出:**
> 生成码字:
> r1 r2 m1 r4 m2 m3 M4
> 0 1 0 1 0 1
> T9】解释:
> 最初 R1、R2、R4 设置为‘0’。
> r1 =第 0 位位置为“1”的所有位位置的按位异或。
> r2 =第一位位置为“1”的所有位的按位异或。
> r3 =第二位位置为“1”的所有位的按位异或。
> 
> **输入:** S = "0111"
> **输出:**
> 生成码字:
> R1 R2 m1 R4 m2 m3 M4
> 0 0 1 1 1 1 1

**方法:**思路是先用 **1** 初始化 **r** 后每次递增 **1** 找到可以找到的冗余比特数，而 **2 <sup>r</sup>** 小于 **(m + r + 1)** ，其中 **m** 为输入报文中的比特数。按照以下步骤解决问题:

*   通过 **1** 初始化 **r** ，并通过 **1** 递增，直到 **2 <sup>r</sup>** 小于 **m+r+1** 。
*   初始化一个大小为 **r + m** 的向量**汉明码**，这将是输出消息的长度。
*   通过从 **i = 0 遍历到 r–1**并设置**汉明码【2<sup>I</sup>–<sup>1】=-1</sup>**，用 **-1** 初始化所有冗余位的位置。然后将输入信息位按 **0 < = j < (r + m)** 的顺序放置在**汉明码【j】**不是 **-1** 的所有位置。
*   用 **0** 初始化一个变量**1 _ count**存储 1 的个数，然后从 **i = 0** 遍历到**(r+m–1)**。
*   如果当前位，即**汉明码【I】**不是 **-1** ，则通过从 **j = i+2 到 r+m** 遍历**1 _ count**加 **1** 如果 **(j & (1 】,则在**日志<sub>2</sub>(I+1)**位置找到包含设置位的消息位**
*   如果对于索引 **i** ， **one_count** 为偶数，则设置**汉明码[i] = 0** 否则设置**汉明码[i] = 1** 。
*   遍历后，打印**汉明码[]** 向量作为输出消息。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include <math.h>
#include <stdio.h>

// Store input bits
int input[32];

// Store hamming code
int code[32];

int ham_calc(int, int);
void solve(int input[], int);

// Function to calculate bit for
// ith position
int ham_calc(int position, int c_l)
{
    int count = 0, i, j;
    i = position - 1;

    // Traverse to store Hamming Code
    while (i < c_l) {

        for (j = i; j < i + position; j++) {

            // If current boit is 1
            if (code[j] == 1)
                count++;
        }

        // Update i
        i = i + 2 * position;
    }

    if (count % 2 == 0)
        return 0;
    else
        return 1;
}

// Function to calculate hamming code
void solve(int input[], int n)
{
    int i, p_n = 0, c_l, j, k;
    i = 0;

    // Find msg bits having set bit
    // at x'th position of number
    while (n > (int)pow(2, i) - (i + 1)) {
        p_n++;
        i++;
    }

    c_l = p_n + n;

    j = k = 0;

    // Traverse the msgBits
    for (i = 0; i < c_l; i++) {

        // Update the code
        if (i == ((int)pow(2, k) - 1)) {
            code[i] = 0;
            k++;
        }

        // Update the code[i] to the
        // input character at index j
        else {
            code[i] = input[j];
            j++;
        }
    }

    // Traverse and update the
    // hamming code
    for (i = 0; i < p_n; i++) {

        // Find current position
        int position = (int)pow(2, i);

        // Find value at current position
        int value = ham_calc(position, c_l);

        // Update the code
        code[position - 1] = value;
    }

    // Print the Hamming Code
    printf("\nThe generated Code Word is: ");
    for (i = 0; i < c_l; i++) {
        printf("%d", code[i]);
    }
}

// Driver Code
void main()
{
    // Given input message Bit
    input[0] = 0;
    input[1] = 1;
    input[2] = 1;
    input[3] = 1;

    int N = 4;

    // Function Call
    solve(input, N);
}
```

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate hamming code
vector<int> generateHammingCode(
    vector<int> msgBits, int m, int r)
{
    // Stores the Hamming Code
    vector<int> hammingCode(r + m);

    // Find positions of redundant bits
    for (int i = 0; i < r; ++i) {

        // Placing -1 at redundant bits
        // place to identify it later
        hammingCode[pow(2, i) - 1] = -1;
    }

    int j = 0;

    // Iterate to update the code
    for (int i = 0; i < (r + m); i++) {

        // Placing msgBits where -1 is
        // absent i.e., except redundant
        // bits all positions are msgBits
        if (hammingCode[i] != -1) {
            hammingCode[i] = msgBits[j];
            j++;
        }
    }

    for (int i = 0; i < (r + m); i++) {

        // If current bit is not redundant
        // bit then continue
        if (hammingCode[i] != -1)
            continue;

        int x = log2(i + 1);
        int one_count = 0;

        // Find msg bits containing
        // set bit at x'th position
        for (int j = i + 2;
             j <= (r + m); ++j) {

            if (j & (1 << x)) {
                if (hammingCode[j - 1] == 1) {
                    one_count++;
                }
            }
        }

        // Generating hamming code for
        // even parity
        if (one_count % 2 == 0) {
            hammingCode[i] = 0;
        }
        else {
            hammingCode[i] = 1;
        }
    }

    // Return the generated code
    return hammingCode;
}

// Function to find the hamming code
// of the given message bit msgBit[]
void findHammingCode(vector<int>& msgBit)
{

    // Message bit size
    int m = msgBit.size();

    // r is the number of redundant bits
    int r = 1;

    // Find no. of redundant bits
    while (pow(2, r) < (m + r + 1)) {
        r++;
    }

    // Generating Code
    vector<int> ans
        = generateHammingCode(msgBit, m, r);

    // Print the code
    cout << "Message bits are: ";
    for (int i = 0; i < msgBit.size(); i++)
        cout << msgBit[i] << " ";

    cout << "\nHamming code is: ";
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";
}

// Driver Code
int main()
{
    // Given message bits
    vector<int> msgBit = { 0, 1, 0, 1 };

    // Function Call
    findHammingCode(msgBit);

    return 0;
}
```

**Output:** 

```
The generated Code Word is: 0001111
```

***时间复杂度:** O((M + R) <sup>2</sup> )其中 M 为输入消息中的位数，R 为冗余位数*
***辅助空间:** O(M + R)*