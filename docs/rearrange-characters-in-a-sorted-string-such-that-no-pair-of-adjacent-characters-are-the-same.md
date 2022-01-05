# 重新排列排序后的字符串中的字符，使得没有一对相邻的字符是相同的

> 原文:[https://www . geeksforgeeks . org/重排排序字符串中的字符，这样相邻字符对就不会相同/](https://www.geeksforgeeks.org/rearrange-characters-in-a-sorted-string-such-that-no-pair-of-adjacent-characters-are-the-same/)

给定由小写字符 **N** 组成的排序后的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是重新排列给定字符串中的字符，使得没有两个相邻的字符相同。如果无法按照给定的标准重新排列，则打印**-1”**。

**示例:**

> **输入:**S =【aaabc】
> T3】输出:阿巴卡
> 
> **输入:**S = " aa "
> T3】输出: -1

**方法:**给定的问题可以使用[两点技巧](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决此问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，检查在[字符串](https://www.geeksforgeeks.org/string-data-structure/)中是否没有两个相邻的字符相同，然后打印字符串 **S** 。
*   否则，如果字符串的大小为 **2** 并且具有相同的字符，则打印**-1”**。
*   初始化三个变量，比如说， **i** 为 **0** 、 **j** 为 **1** 、 **k** 为 **2** 遍历字符串 **S** 。
*   当 **k** 小于 **N** 时迭代，并执行以下步骤:
    *   如果 **S[i]** 不等于 **S[j]** ，那么将 **i** 和 **j** 增加 **1** ，将 **k** 增加 **1** ，如果 **j** 的值等于 **k** 。
    *   否则，如果 **S[j]** 等于 **S[k]** ，则将 **k** 增加 **1** 。
    *   否则，[交换](https://www.geeksforgeeks.org/swapping-characters-string-java/)T2 s【j】和【T4 s【k】并将 **i** 和 **j** 增加 **1** ，如果 **j** 等于 **k，**则将 **k** 增加 **1** 。
*   完成以上步骤[后，反转弦](https://www.geeksforgeeks.org/reverse-a-string-in-java/) **S** 。
*   最后，[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，检查是否没有两个相邻的字符相同。如果发现是**真**那么打印字符串 **S** 。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a string S
// contains pair of adjacent
// characters that are equal or not
bool isAdjChar(string& s)
{
    // Traverse the string S
    for (int i = 0; i < s.size() - 1; i++) {

        // If S[i] and S[i+1] are equal
        if (s[i] == s[i + 1])
            return true;
    }

    // Otherwise, return false
    return false;
}

// Function to rearrange characters
// of a string such that no pair of
// adjacent characters are the same
void rearrangeStringUtil(string& S, int N)
{
    // Initialize 3 variables
    int i = 0, j = 1, k = 2;

    // Iterate until k < N
    while (k < N) {

        // If S[i] is not equal
        // to S[j]
        if (S[i] != S[j]) {

            // Increment i and j by 1
            i++;
            j++;

            // If j equals k and increment
            // the value of K by 1
            if (j == k) {
                k++;
            }
        }

        // Else
        else {

            // If S[j] equals S[k]
            if (S[j] == S[k]) {

                // Increment k by 1
                k++;
            }

            // Else
            else {

                // Swap
                swap(S[k], S[j]);

                // Increment i and j
                // by 1
                i++;
                j++;

                // If j equals k
                if (j == k) {

                    // Increment k by 1
                    k++;
                }
            }
        }
    }
}

// Function to rearrange characters
// in a string so that no two
// adjacent characters are same
string rearrangeString(string& S, int N)
{

    // If string is already valid
    if (isAdjChar(S) == false) {
        return S;
    }

    // If size of the string is 2
    if (S.size() == 2)
        return "-1";

    // Function Call
    rearrangeStringUtil(S, N);

    // Reversing the string
    reverse(S.begin(), S.end());

    // Function Call
    rearrangeStringUtil(S, N);

    // If the string is valid
    if (isAdjChar(S) == false) {
        return S;
    }

    // Otherwise
    return "-1";
}

// Driver Code
int main()
{
    string S = "aaabc";
    int N = S.length();
    cout << rearrangeString(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{
    static char []S = "aaabc".toCharArray();

// Function to check if a String S
// contains pair of adjacent
// characters that are equal or not
static boolean isAdjChar()
{

    // Traverse the String S
    for (int i = 0; i < S.length - 1; i++)
    {

        // If S[i] and S[i+1] are equal
        if (S[i] == S[i + 1])
            return true;
    }

    // Otherwise, return false
    return false;
}

// Function to rearrange characters
// of a String such that no pair of
// adjacent characters are the same
static void rearrangeStringUtil(int N)
{

    // Initialize 3 variables
    int i = 0, j = 1, k = 2;

    // Iterate until k < N
    while (k < N) {

        // If S[i] is not equal
        // to S[j]
        if (S[i] != S[j]) {

            // Increment i and j by 1
            i++;
            j++;

            // If j equals k and increment
            // the value of K by 1
            if (j == k) {
                k++;
            }
        }

        // Else
        else {

            // If S[j] equals S[k]
            if (S[j] == S[k]) {

                // Increment k by 1
                k++;
            }

            // Else
            else {

                // Swap
                swap(k,j);

                // Increment i and j
                // by 1
                i++;
                j++;

                // If j equals k
                if (j == k) {

                    // Increment k by 1
                    k++;
                }
            }
        }
    }
}
static void swap(int i, int j)
{
    char temp = S[i];
    S[i] = S[j];
    S[j] = temp; 
}
// Function to rearrange characters
// in a String so that no two
// adjacent characters are same
static String rearrangeString(int N)
{

    // If String is already valid
    if (isAdjChar() == false) {
        return String.valueOf(S);
    }

    // If size of the String is 2
    if (S.length == 2)
        return "-1";

    // Function Call
    rearrangeStringUtil(N);

    // Reversing the String
    reverse();

    // Function Call
    rearrangeStringUtil(N);

    // If the String is valid
    if (isAdjChar() == false) {
        return String.valueOf(S);
    }

    // Otherwise
    return "-1";
}
static void reverse() {

    int l, r = S.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = S[l];
        S[l] = S[r];
        S[r] = temp;
    }
}

// Driver Code
public static void main(String[] args)
{

    int N = S.length;
    System.out.print(rearrangeString(N));

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program for the above approach
S = "aaabc"

# Function to check if a string S
# contains pair of adjacent
# characters that are equal or not
def isAdjChar(s):

    # Traverse the string S
    for i in range(len(s)-1):

        # If S[i] and S[i+1] are equal
        if (s[i] == s[i + 1]):
            return True

    # Otherwise, return false
    return False

# Function to rearrange characters
# of a string such that no pair of
# adjacent characters are the same
def rearrangeStringUtil(N):
    global S
    S = list(S)
    # Initialize 3 variables
    i = 0
    j = 1
    k = 2

    # Iterate until k < N
    while (k < N):

        # If S[i] is not equal
        # to S[j]
        if (S[i] != S[j]):

            # Increment i and j by 1
            i += 1
            j += 1

            # If j equals k and increment
            # the value of K by 1
            if (j == k):
                k += 1

        # Else
        else:

            # If S[j] equals S[k]
            if (S[j] == S[k]):

                # Increment k by 1
                k += 1

            # Else
            else:

                # Swap
                temp = S[k]
                S[k] = S[j]
                S[j] = temp
                # Increment i and j
                # by 1
                i += 1
                j += 1

                # If j equals k
                if (j == k):

                    # Increment k by 1
                    k += 1
    S = ''.join(S)

# Function to rearrange characters
# in a string so that no two
# adjacent characters are same
def rearrangeString(N):
    global S

    # If string is already valid
    if (isAdjChar(S) == False):
        return S

    # If size of the string is 2
    if (len(S) == 2):
        return "-1"

    # Function Call
    rearrangeStringUtil(N)

    # Reversing the string
    S = S[::-1]

    # Function Call
    rearrangeStringUtil(N)

    # If the string is valid
    if (isAdjChar(S) == False):
        return S

    # Otherwise
    return "-1"

# Driver Code
if __name__ == '__main__':
    N = len(S)
    print(rearrangeString(N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{
    static char []S = "aaabc".ToCharArray();

// Function to check if a String S
// contains pair of adjacent
// characters that are equal or not
static bool isAdjChar()
{

    // Traverse the String S
    for (int i = 0; i < S.Length - 1; i++)
    {

        // If S[i] and S[i+1] are equal
        if (S[i] == S[i + 1])
            return true;
    }

    // Otherwise, return false
    return false;
}

// Function to rearrange characters
// of a String such that no pair of
// adjacent characters are the same
static void rearrangeStringUtil(int N)
{

    // Initialize 3 variables
    int i = 0, j = 1, k = 2;

    // Iterate until k < N
    while (k < N) {

        // If S[i] is not equal
        // to S[j]
        if (S[i] != S[j]) {

            // Increment i and j by 1
            i++;
            j++;

            // If j equals k and increment
            // the value of K by 1
            if (j == k) {
                k++;
            }
        }

        // Else
        else {

            // If S[j] equals S[k]
            if (S[j] == S[k]) {

                // Increment k by 1
                k++;
            }

            // Else
            else {

                // Swap
                swap(k,j);

                // Increment i and j
                // by 1
                i++;
                j++;

                // If j equals k
                if (j == k) {

                    // Increment k by 1
                    k++;
                }
            }
        }
    }
}
static void swap(int i, int j)
{
    char temp = S[i];
    S[i] = S[j];
    S[j] = temp; 
}

// Function to rearrange characters
// in a String so that no two
// adjacent characters are same
static String rearrangeString(int N)
{

    // If String is already valid
    if (isAdjChar() == false) {
        return String.Join("",S);
    }

    // If size of the String is 2
    if (S.Length == 2)
        return "-1";

    // Function Call
    rearrangeStringUtil(N);

    // Reversing the String
    reverse();

    // Function Call
    rearrangeStringUtil(N);

    // If the String is valid
    if (isAdjChar() == false) {
        return String.Join("",S);
    }

    // Otherwise
    return "-1";
}
static void reverse() {

    int l, r = S.Length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = S[l];
        S[l] = S[r];
        S[r] = temp;
    }
}

// Driver Code
public static void Main(String[] args)
{

    int N = S.Length;
    Console.Write(rearrangeString(N));

}
}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
acaba
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)