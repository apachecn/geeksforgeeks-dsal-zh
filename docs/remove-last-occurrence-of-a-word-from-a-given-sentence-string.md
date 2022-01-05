# 从给定的句子串中删除最后出现的单词

> 原文:[https://www . geesforgeks . org/remove-从给定的句子字符串中删除最后出现的单词/](https://www.geeksforgeeks.org/remove-last-occurrence-of-a-word-from-a-given-sentence-string/)

给定两个大小分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **W** ，任务是从 **S** 中移除最后一个出现的 **W** 。如果 **S** 中没有出现 **W** ，则按原样打印 **S** 。

**示例:**

> **输入:** S =“这是 GeeksForGeeks”，W =“Geeks”
> **输出:**这是 GeeksFor
> **解释:**
> 字符串中最后出现的“Geeks”是范围[16，20]内的子字符串。
> 
> **输入:** S="Hello World "，W="Hell"
> **输出:** o World
> **解释:**
> 字符串中最后出现的“Hell”是范围[0，3]内的子字符串。

**方法:**通过对字符串 **S** 的每个索引 **i** 进行迭代，检查是否有一个从索引 **i** 开始的子串，该子串等于字符串 **W** ，可以解决这个问题。按照以下步骤解决问题:

*   如果 **N** 小于 **M** ，打印 **S** ，因为 **S** 中不可能出现 **W** 。
*   将变量 **i** 初始化为 **N-M** 到[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 。
*   迭代直到 **i** 大于 **0** ，并执行以下步骤:
    *   检查**【I，I+M-1】**范围内的子串是否等于字符串 **W** 。如果相等，则[从字符串 **S** 中删除超出范围**【I，I+M-1】**的子字符串](https://www.geeksforgeeks.org/stdstringerase-in-cpp/)，然后[断开](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   最后，完成以上步骤后，打印字符串 **S** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove last occurrence
// of W from S
string removeLastOccurrence(string S, string W, int N,
                            int M)
{

    // If M is greater than N
    if (M > N)
        return S;

    // Iterate while i is greater than
    // or equal to 0
    for (int i = N - M; i >= 0; i--) {
        // Stores if occurrence of W has
        // been found or not
        int flag = 0;

        // Iterate over the range [0, M]
        for (int j = 0; j < M; j++) {

            // If S[j+1] is not equal to
            // W[j]
            if (S[j + i] != W[j]) {

                // Mark flag true and break
                flag = 1;
                break;
            }
        }

        // If occurrence has been found
        if (flag == 0) {

            // Delete the substring over the
            // range [i, i+M]
            for (int j = i; j < N - M; j++)
                S[j] = S[j + M];

            // Resize the string S
            S.resize(N - M);
            break;
        }
    }

    // Return S
    return S;
}
// Driver Code
int main()
{
    // Input
    string S = "This is GeeksForGeeks";
    string W = "Geeks";
    int N = S.length();
    int M = W.length();

    // Function call
    cout << removeLastOccurrence(S, W, N, M) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to remove last occurrence
// of W from S
static String removeLastOccurrence(String S, String W,
                                   int N, int M)
{

    // If M is greater than N
    char[] ch = S.toCharArray();
    if (M > N)
        return S;

    // Iterate while i is greater than
    // or equal to 0
    for(int i = N - M; i >= 0; i--)
    {

        // Stores if occurrence of W has
        // been found or not
        int flag = 0;

        // Iterate over the range [0, M]
        for(int j = 0; j < M; j++)
        {

            // If S[j+1] is not equal to
            // W[j]
            if (ch[j + i] != W.charAt(j))
            {

                // Mark flag true and break
                flag = 1;
                break;
            }
        }

        // If occurrence has been found
        if (flag == 0)
        {

            // Delete the substring over the
            // range [i, i+M]
            for(int j = i; j < N - M; j++)
                ch[j] = ch[j + M];

            break;
        }
    }

    char[] chh = new char[N - M];

    // Resize the string S
    for(int i = 0; i < N - M; i++)
    {
        chh[i] = ch[i];
    }

    // Return S
    return String.valueOf(chh);
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String S = "This is GeeksForGeeks";
    String W = "Geeks";
    int N = S.length();
    int M = W.length();

    // Function call
    System.out.print(removeLastOccurrence(S, W, N, M));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to remove last occurrence
# of W from S
def removeLastOccurrence(S, W, N, M):
    S = [i for i in S]
    W = [i for i in W]

    # If M is greater than N
    if (M > N):
        return S

    # Iterate while i is greater than
    # or equal to 0
    for i in range(N - M, -1, -1):
        # of W has
        # been found or not
        flag = 0

        # Iterate over the range [0, M]
        for j in range(M):
            # If S[j+1] is not equal to
            # W[j]
            if (S[j + i] != W[j]):

                # Mark flag true and break
                flag = 1
                break

        # If occurrence has been found
        if (flag == 0):

            # Delete the subover the
            # range [i, i+M]
            for j in range(i,N-M):
                S[j] = S[j + M]

            # Resize the S
            S = S[:N - M]
            break

    # Return S
    return "".join(S)

# Driver Code
if __name__ == '__main__':
    # Input
    S = "This is GeeksForGeeks"
    W = "Geeks"
    N = len(S)
    M = len(W)

    # Function call
    print (removeLastOccurrence(S, W, N, M))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to remove last occurrence
// of W from S
static string removeLastOccurrence(string S, string W, int N,
                            int M)
{

    // If M is greater than N
   char[] ch = S.ToCharArray();
    if (M > N)
        return S;

    // Iterate while i is greater than
    // or equal to 0
    for (int i = N - M; i >= 0; i--)
    {

        // Stores if occurrence of W has
        // been found or not
        int flag = 0;

        // Iterate over the range [0, M]
        for (int j = 0; j < M; j++) {

            // If S[j+1] is not equal to
            // W[j]
            if (ch[j + i] != W[j]) {

                // Mark flag true and break
                flag = 1;
                break;
            }
        }

        // If occurrence has been found
        if (flag == 0) {

            // Delete the substring over the
            // range [i, i+M]
            for (int j = i; j < N - M; j++)
                ch[j] = ch[j + M];

            // Resize the string S
            Array.Resize(ref ch,N - M);
            break;
        }
    }
     S = string.Concat(ch);

    // Return S
    return S;
}

// Driver Code
public static void Main()
{
    // Input
    string S = "This is GeeksForGeeks";
    string W = "Geeks";
    int N = S.Length;
    int M = W.Length;

    // Function call
    Console.Write(removeLastOccurrence(S, W, N, M));
}
}

// This code is contributed by bgangwar59.
```

**Output**

```
This is GeeksFor
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(1)*