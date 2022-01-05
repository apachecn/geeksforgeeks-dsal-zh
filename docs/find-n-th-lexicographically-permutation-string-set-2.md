# 查找字符串的第 n 次字典排列|集合 2

> 原文:[https://www . geeksforgeeks . org/find-n-th-词典-排列-字符串-set-2/](https://www.geeksforgeeks.org/find-n-th-lexicographically-permutation-string-set-2/)

给定一个长度为 m 的字符串，其中只包含小写字母。我们需要按字典顺序找到字符串的第 n 个排列。
**例:**

```
Input: str[] = "abc", n = 3
Output: Result = "bac"
All possible permutation in 
sorted order: abc, acb, bac,
bca, cab, cba

Input: str[] = "aba", n = 2
Output: Result = "aba"
All possible permutation 
in sorted order: aab, aba, baa
```

**<u>【天真方法】</u> :** [使用 STL](https://www.geeksforgeeks.org/lexicographically-n-th-permutation-string/) 查找词典第 n 个排列。
**<u>高效方法:</u>** 解决这个问题的数学概念。

> 1.  The total number of strings consisting of n characters (all different) is **n!**
> 2.  The total number of strings consisting of n characters (where the frequency of character C1 is M1, C2 is M2… so the frequency of character Ck is Mk) is **n! /(M1！ * M2！ *….Mk！ )** 。
> 3.  After the first character is fixed, the total number of strings consisting of n characters (all different) is **(n-1)!**

可以遵循以下步骤来达成解决方案。

*   计算数组中所有字符的频率。
*   现在从字符串中出现的第一个最小字符(最小索引 I，使得 freq[i] > 0)开始，在将该特定的第 I 个字符设置为第一个字符后，计算可能的最大置换数。
*   如果该和值大于给定的 n，则将该字符设置为第一个结果输出字符，并递减 freq[i]。对剩余的 n-1 个字符继续相同的操作。
*   另一方面，如果计数小于所需的 n，则迭代查找频率表中的下一个字符，并一遍又一遍地更新计数，直到我们找到一个产生大于所需 n 的计数的字符。

## C++

```
// C++ program to print
// n-th permutation
#include <bits/stdc++.h>
using namespace std;

#define ll long long int

const int MAX_CHAR = 26;
const int MAX_FACT = 20;
ll fact[MAX_FACT];

// Utility for calculating factorials
void precomputeFactorials()
{
    fact[0] = 1;
    for (int i = 1; i < MAX_FACT; i++)
        fact[i] = fact[i - 1] * i;
}

// Function for nth permutation
void nPermute(char str[], int n)
{
    precomputeFactorials();

    // Length of given string
    int len = strlen(str);

    // Count frequencies of all
    // characters
    int freq[MAX_CHAR] = { 0 };
    for (int i = 0; i < len; i++)
        freq[str[i] - 'a']++;

    // Out string for output string
    char out[MAX_CHAR];

    // Iterate till sum equals n
    int sum = 0;
    int k = 0;

    // We update both n and sum in this
    // loop.
    while (sum != n) {

        sum = 0;
        // Check for characters present in freq[]
        for (int i = 0; i < MAX_CHAR; i++) {
            if (freq[i] == 0)
                continue;

            // Remove character
            freq[i]--;

            // Calculate sum after fixing
            // a particular char
            int xsum = fact[len - 1 - k];
            for (int j = 0; j < MAX_CHAR; j++)
                xsum /= fact[freq[j]];
            sum += xsum;

            // if sum > n fix that char as
            // present char and update sum
            // and required nth after fixing
            // char at that position
            if (sum >= n) {
                out[k++] = i + 'a';
                n -= (sum - xsum);
                break;
            }

            // if sum < n, add character back
            if (sum < n)
                freq[i]++;
        }
    }

    // if sum == n means this
    // char will provide its
    // greatest permutation
    // as nth permutation
    for (int i = MAX_CHAR - 1;
         k < len && i >= 0; i--)
        if (freq[i]) {
            out[k++] = i + 'a';
            freq[i++]--;
        }

    // append string termination
    // character and print result
    out[k] = '\0';
    cout << out;
}

// Driver program
int main()
{
    int n = 2;
    char str[] = "geeksquiz";

    nPermute(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// n-th permutation
public class PermuteString {
    final static int MAX_CHAR = 26;
    final static int MAX_FACT = 20;
    static long fact[] = new long[MAX_FACT];

    // Utility for calculating factorial
    static void precomputeFactorirals()
    {
        fact[0] = 1;
        for (int i = 1; i < MAX_FACT; i++)
            fact[i] = fact[i - 1] * i;
    }

    // Function for nth permutation
    static void nPermute(String str, int n)
    {
        precomputeFactorirals();

        // length of given string
        int len = str.length();

        // Count frequencies of all
        // characters
        int freq[] = new int[MAX_CHAR];
        for (int i = 0; i < len; i++)
            freq[str.charAt(i) - 'a']++;

        // out string for output string
        String out = "";

        // Iterate till sum equals n
        int sum = 10;
        int k = 0;

        // We update both n and sum
        // in this loop.
        while (sum >= n) {

            // Check for characters
            // present in freq[]
            for (int i = 0; i < MAX_CHAR; i++) {
                if (freq[i] == 0)
                    continue;

                // Remove character
                freq[i]--;

                // calculate sum after fixing
                // a particular char
                sum = 0;
                int xsum = (int)fact[len - 1 - k];
                for (int j = 0; j < MAX_CHAR; j++)
                    xsum /= fact[freq[j]];
                sum += xsum;

                // if sum > n fix that char as
                // present char and update sum
                // and required nth after fixing
                // char at that position
                if (sum >= n) {
                    out += (char)(i + 'a');
                    k++;
                    n -= (sum - xsum);
                    break;
                }

                // if sum < n, add character back
                if (sum < n)
                    freq[i]++;
            }
        }

        // if sum == n means this
        // char will provide its
        // greatest permutation
        // as nth permutation
        for (int i = MAX_CHAR - 1;
             k < len && i >= 0; i--)
            if (freq[i] != 0) {
                out += (char)(i + 'a');
                freq[i++]--;
            }

        // append string termination
        // character and print result
        System.out.println(out);
    }

    // Driver program to test above method
    public static void main(String[] args)
    {

        // TODO Auto-generated method stub
        int n = 2;
        String str = "geeksquiz";

        nPermute(str, n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to print n-th permutation

MAX_CHAR = 26
MAX_FACT = 20
fact = [None] * (MAX_FACT)

# Utility for calculating factorials
def precomputeFactorials():

    fact[0] = 1
    for i in range(1, MAX_FACT):
        fact[i] = fact[i - 1] * i

# Function for nth permutation
def nPermute(string, n):

    precomputeFactorials()

    # length of given string
    length = len(string)

    # Count frequencies of all
    # characters
    freq = [0] * (MAX_CHAR)
    for i in range(0, length):
        freq[ord(string[i]) - ord('a')] += 1

    # out string for output string
    out = [None] * (MAX_CHAR)

    # iterate till sum equals n
    Sum, k = 0, 0

    # We update both n and sum in
    # this loop.
    while Sum != n:

        Sum = 0

        # check for characters present in freq[]
        for i in range(0, MAX_CHAR):
            if freq[i] == 0:
                continue

            # Remove character
            freq[i] -= 1

            # calculate sum after fixing
            # a particular char
            xsum = fact[length - 1 - k]
            for j in range(0, MAX_CHAR):
                xsum = xsum // fact[freq[j]]
            Sum += xsum

            # if sum > n fix that char as
            # present char and update sum
            # and required nth after fixing
            # char at that position
            if Sum >= n:
                out[k] = chr(i + ord('a'))
                n -= Sum - xsum
                k += 1
                break

            # if sum < n, add character back
            if Sum < n:
                freq[i] += 1

    # if sum == n means this char will provide
    # its greatest permutation as nth permutation
    i = MAX_CHAR-1
    while k < length and i >= 0:
        if freq[i]:
            out[k] = chr(i + ord('a'))
            freq[i] -= 1
            i += 1
            k += 1

        i -= 1

    # print result
    print(''.join(out[:k]))

# Driver Code
if __name__ == "__main__":

    n = 2
    string = "geeksquiz"

    nPermute(string, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print n-th permutation
using System;

public class GFG {

    static int MAX_CHAR = 26;
    static int MAX_FACT = 20;
    static long[] fact = new long[MAX_FACT];

    // utility for calculating factorial
    static void precomputeFactorirals()
    {
        fact[0] = 1;
        for (int i = 1; i < MAX_FACT; i++)
            fact[i] = fact[i - 1] * i;
    }

    // function for nth permutation
    static void nPermute(String str, int n)
    {
        precomputeFactorirals();

        // length of given string
        int len = str.Length;

        // Count frequencies of all
        // characters
        int[] freq = new int[MAX_CHAR];

        for (int i = 0; i < len; i++)
            freq[str[i] - 'a']++;

        // out string for output string
        string ou = "";

        // iterate till sum equals n
        int sum = 10;
        int k = 0;

        // We update both n and sum in this
        // loop.
        while (sum >= n) {

            // check for characters present in freq[]
            for (int i = 0; i < MAX_CHAR; i++) {
                if (freq[i] == 0)
                    continue;

                // Remove character
                freq[i]--;

                // calculate sum after fixing
                // a particular char
                sum = 0;
                int xsum = (int)fact[len - 1 - k];

                for (int j = 0; j < MAX_CHAR; j++)
                    xsum /= (int)(fact[freq[j]]);

                sum += xsum;

                // if sum > n fix that char as
                // present char and update sum
                // and required nth after fixing
                // char at that position
                if (sum >= n) {
                    ou += (char)(i + 'a');
                    k++;
                    n -= (sum - xsum);
                    break;
                }

                // if sum < n, add character back
                if (sum < n)
                    freq[i]++;
            }
        }

        // if sum == n means this char will provide its
        // greatest permutation as nth permutation
        for (int i = MAX_CHAR - 1; k < len && i >= 0; i--)
            if (freq[i] != 0) {
                ou += (char)(i + 'a');
                freq[i++]--;
            }

        // append string termination
        // character and print result
        Console.Write(ou);
    }

    // Driver program to test above method
    public static void Main()
    {

        // TODO Auto-generated method stub
        int n = 2;
        String str = "geeksquiz";

        nPermute(str, n);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>
// Javascript program to print
// n-th permutation

let MAX_CHAR = 26;
let MAX_FACT = 20;

let fact=new Array(MAX_FACT);

 // Utility for calculating factorial
function precomputeFactorirals()
{
    fact[0] = 1;
        for (let i = 1; i < MAX_FACT; i++)
            fact[i] = fact[i - 1] * i;
}

// Function for nth permutation
function nPermute(str,n)
{
    precomputeFactorirals();

        // length of given string
        let len = str.length;

        // Count frequencies of all
        // characters
        let freq = new Array(MAX_CHAR);
        for(let i=0;i<MAX_CHAR;i++)
        {
            freq[i]=0;
        }
        for (let i = 0; i < len; i++)
            freq[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

        // out string for output string
        let out = "";

        // Iterate till sum equals n
        let sum = 10;
        let k = 0;

        // We update both n and sum
        // in this loop.
        while (sum >= n) {

            // Check for characters
            // present in freq[]
            for (let i = 0; i < MAX_CHAR; i++) {
                if (freq[i] == 0)
                    continue;

                // Remove character
                freq[i]--;

                // calculate sum after fixing
                // a particular char
                sum = 0;
                let xsum = fact[len - 1 - k];
                for (let j = 0; j < MAX_CHAR; j++)
                    xsum = Math.floor(xsum/fact[freq[j]]);
                sum += xsum;

                // if sum > n fix that char as
                // present char and update sum
                // and required nth after fixing
                // char at that position
                if (sum >= n) {
                    out += String.fromCharCode(i + 'a'.charCodeAt(0));
                    k++;
                    n -= (sum - xsum);
                    break;
                }

                // if sum < n, add character back
                if (sum < n)
                    freq[i]++;
            }
        }

        // if sum == n means this
        // char will provide its
        // greatest permutation
        // as nth permutation
        for (let i = MAX_CHAR - 1;
             k < len && i >= 0; i--)
            if (freq[i] != 0) {
                out += String.fromCharCode(i + 'a'.charCodeAt(0));
                freq[i++]--;
            }

        // append string termination
        // character and print result
        document.write(out);
}

// Driver program to test above method
// TODO Auto-generated method stub
let n = 2;
let str = "geeksquiz";

nPermute(str, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
eegikqszu
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为第 n 次排列。
*   **空间复杂度:** O(n)其中 n 是存储频率所需的空间。

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.linkedin.com/in/imanuj/)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。