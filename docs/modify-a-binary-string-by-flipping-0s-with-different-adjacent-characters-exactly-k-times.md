# 用不同的邻居翻转给定二进制字符串中的所有 0K 次

> 原文:[https://www . geeksforgeeks . org/modify-a-二进制字符串-通过用不同的相邻字符翻转-0s-恰好-k-times/](https://www.geeksforgeeks.org/modify-a-binary-string-by-flipping-0s-with-different-adjacent-characters-exactly-k-times/)

给定大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和正整数 **K** ，任务是通过在每次迭代中翻转所有相邻字符不同的 **0s** 来重复修改给定字符串 **K** 的次数。

> **注意:**对于出现在 **0 <sup>th</sup>** 索引处的字符 **0** ，那么只有当**1<sup>ST</sup>T13】索引字符为 **1** 时，它才会变为 **1** ，如果最后一个索引字符为 **0** ，那么如果第二个最后一个索引字符为**【1】****

**示例:**

> ***输入:** S = "01001 "，K = 2*
> ***输出:** 11111*
> ***解释:***
> *以下是执行的操作 K(= 2)次次数:|*
> ***操作 1:** 在索引 0、2、3 处翻转字符串后，字符串修改为“11111”。*
> ***操作 2:** 对于修改后的字符串 S = "11111 "不存在这种可能的翻转。*
> *经过以上操作，修改后的字符串为“11111”。*
> 
> ***输入:** S = "10010001 "，K = 3*
> T5**输出:**111111011

**方法:**给定的问题可以通过执行给定的操作 **K** 次数，然后打印形成的结果字符串来解决。按照以下步骤解决此问题:

*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K–1】**，并执行以下步骤:
    *   使用变量 **j** 在范围**【0，N–1】**内遍历给定的字符串 **S** ，并执行以下步骤:
        *   如果**0**索引处的字符为 **0** ，则用第一个索引值替换该值。
        *   否则，如果字符 **0** 出现在最后一个索引处，则用**第二个最后一个索引**字符替换该值。
        *   否则，如果相邻字符不同，将所有 **0s** 转换为 **1** 。
    *   经过以上步骤，如果修改前字符串保持不变，则[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印字符串 **S** 作为结果修改字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify the given string
// K number of times by flipping 0s
// having different adjacent characters
void convertString(string S, int k)
{
    // Size of the string
    int n = S.length();

    // Stores modified string after
    // each iteration
    string temp = S;

    // Iterate over the range [0 k]
    for (int i = 0; i < k; i++) {

        // Traverse the string S
        for (int j = 0; j < n; j++) {

            // If '0' is present at
            // 0th index then replace
            // it with 1st index
            if (j == 0 && S[j] == '0') {

                temp[j] = S[j + 1];
            }

            // If '0' is present at the
            // last index then replace
            // it with last index - 1
            // character
            else if (j == n - 1
                     && S[j] == '0') {

                temp[j] = S[j - 1];
            }

            // Otherwise, convert 0s
            // to 1 if the adjacent
            // characters are different
            else if (S[j - 1] != S[j + 1]
                     && S[j] == '0') {

                temp[j] = '1';
            }
        }

        // If during this iteration
        // there is no change in the
        // string then break this loop
        if (S == temp) {
            break;
        }

        // Update the string S
        S = temp;
    }

    // Print the updated string
    cout << S;
}

// Driver Code
int main()
{
    string S = "10010001";
    int K = 1;
    convertString(S, K);

    return 0;
}
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to modify the given string
# K number of times by flipping 0s
# having different adjacent characters
def convertString(S, k):
    # Size of the string
    n = len(S)

    # Stores modified string after
    # each iteration
    temp = S
    temp = list(temp)

    # Iterate over the range [0 k]
    for i in range(k):
        # Traverse the string S
        for j in range(n-1):
            # If '0' is present at
            # 0th index then replace
            # it with 1st index
            if (j == 0 and S[j] == '0'):

                temp[j] = S[j + 1]

            # If '0' is present at the
            # last index then replace
            # it with last index - 1
            # character
            elif (j == n - 1 and S[j] == '0'):

                temp[j] = S[j - 1]

            # Otherwise, convert 0s
            # to 1 if the adjacent
            # characters are different
            elif (S[j - 1] != S[j + 1] and S[j] == '0'):
                temp[j] = '1'

        # If during this iteration
        # there is no change in the
        # string then break this loop
        if (S == temp):
            break
        temp = ''.join(temp)
        # Update the string S
        S = temp

    # Print the updated string
    print(S)

# Driver Code
if __name__ == '__main__':
    S = "10010001"
    K = 1
    convertString(S, K)

    # This code s contributed by ipg2016107.
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(N)*