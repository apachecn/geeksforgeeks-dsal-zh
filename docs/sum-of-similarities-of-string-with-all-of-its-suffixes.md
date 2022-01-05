# 字符串与其所有后缀的相似度之和

> 原文:[https://www . geeksforgeeks . org/字符串与其所有后缀的相似性总和/](https://www.geeksforgeeks.org/sum-of-similarities-of-string-with-all-of-its-suffixes/)

给定一个字符串 **str** ，任务是找出 **str** 与其每个后缀的相似性之和。
字符串的相似度 **A** 和 **B** 是两个字符串共有的最长前缀的长度，即“aabc”和“aab”的相似度为 **3** ，“qwer”和“abc”的相似度为 **0** 。
**举例:**

> **输入:** str =“亚贝巴”
> **输出:**9
> str 的后缀是“亚贝巴”、“巴巴”、“阿坝”、“巴”和“一”。这些字符串与原字符串“亚的斯亚贝巴”的相似之处分别是 5、0、3、0 & 1。
> 于是，答案是 5 + 0 + 3 + 0 + 1 = 9。
> **输入:**str = " aaabab "
> **输出:** 13

**方法:**使用 [Z 算法](https://www.geeksforgeeks.org/z-algorithm-linear-time-pattern-searching-algorithm/)计算 Z 数组–对于字符串[0..n-1]，Z 数组与字符串长度相同。Z 数组的元素 Z[i]存储从字符串[i]开始的最长子串的长度，字符串[i]也是字符串[0]的前缀..n-1]。Z 数组的第一个条目是字符串的长度。
现在，对 Z 数组的所有元素求和，得到所需的相似度之和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Function to calculate the Z-array for the given string
void getZarr(string str, int n, int Z[])
{
    int L, R, k;

    // [L, R] make a window which matches with prefix of s
    L = R = 0;
    for (int i = 1; i < n; ++i) {

        // if i>R nothing matches so we will calculate.
        // Z[i] using naive way.
        if (i > R) {
            L = R = i;

            // R-L = 0 in starting, so it will start
            // checking from 0'th index. For example,
            // for "ababab" and i = 1, the value of R
            // remains 0 and Z[i] becomes 0\. For string
            // "aaaaaa" and i = 1, Z[i] and R become 5
            while (R < n && str[R - L] == str[R])
                R++;
            Z[i] = R - L;
            R--;
        }
        else {

            // k = i-L so k corresponds to number which
            // matches in [L, R] interval.
            k = i - L;

            // if Z[k] is less than remaining interval
            // then Z[i] will be equal to Z[k].
            // For example, str = "ababab", i = 3, R = 5
            // and L = 2
            if (Z[k] < R - i + 1)
                Z[i] = Z[k];

            // For example str = "aaaaaa" and i = 2, R is 5,
            // L is 0
            else {
                // else start from R and check manually
                L = i;
                while (R < n && str[R - L] == str[R])
                    R++;
                Z[i] = R - L;
                R--;
            }
        }
    }
}

// Function to return the similarity sum
int sumSimilarities(string s, int n)
{
    int Z[n] = { 0 };

    // Compute the Z-array for the given string
    getZarr(s, n, Z);

    int total = n;

    // Summation of the Z-values
    for (int i = 1; i < n; i++)
        total += Z[i];

    return total;
}

// Driver code
int main()
{
    string s = "ababa";
    int n = s.length();

    cout << sumSimilarities(s, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG{

// Function to calculate the Z-array for the given string
static void getZarr(String str, int n, int Z[])
{
    int L, R, k;

    // [L, R] make a window which matches with prefix of s
    L = R = 0;
    for (int i = 1; i < n; ++i) {

        // if i>R nothing matches so we will calculate.
        // Z[i] using naive way.
        if (i > R) {
            L = R = i;

            // R-L = 0 in starting, so it will start
            // checking from 0'th index. For example,
            // for "ababab" and i = 1, the value of R
            // remains 0 and Z[i] becomes 0\. For string
            // "aaaaaa" and i = 1, Z[i] and R become 5
            while (R < n && str.charAt(R - L) == str.charAt(R))
                R++;
            Z[i] = R - L;
            R--;
        }
        else {

            // k = i-L so k corresponds to number which
            // matches in [L, R] interval.
            k = i - L;

            // if Z[k] is less than remaining interval
            // then Z[i] will be equal to Z[k].
            // For example, str = "ababab", i = 3, R = 5
            // and L = 2
            if (Z[k] < R - i + 1)
                Z[i] = Z[k];

            // For example str = "aaaaaa" and i = 2, R is 5,
            // L is 0
            else {
                // else start from R and check manually
                L = i;
                while (R < n && str.charAt(R - L) == str.charAt(R))
                    R++;
                Z[i] = R - L;
                R--;
            }
        }
    }
}

// Function to return the similarity sum
static int sumSimilarities(String s, int n)
{
    int Z[] = new int[n] ;

    // Compute the Z-array for the given string
    getZarr(s, n, Z);

    int total = n;

    // Summation of the Z-values
    for (int i = 1; i < n; i++)
        total += Z[i];

    return total;
}

// Driver code
public static void main(String []args)
{
    String s = "ababa";
    int n = s.length();

    System.out.println(sumSimilarities(s, n));
}
// This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def getZarr(s, n, Z):
    L, R, k = 0, 0, 0

    # [L, R] make a window which matches
    # with prefix of s
    for i in range(n):
        # if i>R nothing matches so we will
        # calculate Z[i] using naive way.
        if i > R:
            L, R = i, i

            '''
            R-L = 0 in starting, so it will start
            checking from 0'th index. For example,
            for "ababab" and i = 1, the value of R
            remains 0 and Z[i] becomes 0\. For string
            "aaaaaa" and i = 1, Z[i] and R become 5
            '''
            while R < n and s[R - L] == s[R]:
                R += 1
            Z[i] = R - L
            R -= 1
        else:

            # k = i-L so k corresponds to number
            # which matches in [L, R] interval.
            k = i - L

            # if Z[k] is less than remaining interval
            # then Z[i] will be equal to Z[k].
            # For example, str = "ababab", i = 3, R = 5
            # and L = 2
            if Z[k] < R - i + 1:
                Z[i] = Z[k]
            else:
                L = i
                while R < n and s[R - L] == s[R]:
                    R += 1
                Z[i] = R - L
                R -= 1

def sumSimilarities(s, n):
    Z = [0 for i in range(n)]

    # Compute the Z-array for the
    # given string
    getZarr(s, n, Z)

    total = n

    # summation of the Z-values
    for i in range(n):
        total += Z[i]
    return total

# Driver Code
s = "ababa"

n = len(s)

print(sumSimilarities(s, n))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
//C# implementation of the above approach
using System;

public class GFG{
    // Function to calculate the Z-array for the given string
static void getZarr(string str, int n, int []Z)
{
    int L, R, k;

    // [L, R] make a window which matches with prefix of s
    L = R = 0;
    for (int i = 1; i < n; ++i) {

        // if i>R nothing matches so we will calculate.
        // Z[i] using naive way.
        if (i > R) {
            L = R = i;

            // R-L = 0 in starting, so it will start
            // checking from 0'th index. For example,
            // for "ababab" and i = 1, the value of R
            // remains 0 and Z[i] becomes 0\. For string
            // "aaaaaa" and i = 1, Z[i] and R become 5
            while (R < n && str[R - L] == str[R])
                R++;
            Z[i] = R - L;
            R--;
        }
        else {

            // k = i-L so k corresponds to number which
            // matches in [L, R] interval.
            k = i - L;

            // if Z[k] is less than remaining interval
            // then Z[i] will be equal to Z[k].
            // For example, str = "ababab", i = 3, R = 5
            // and L = 2
            if (Z[k] < R - i + 1)
                Z[i] = Z[k];

            // For example str = "aaaaaa" and i = 2, R is 5,
            // L is 0
            else {
                // else start from R and check manually
                L = i;
                while (R < n && str[R - L] == str[R])
                    R++;
                Z[i] = R - L;
                R--;
            }
        }
    }
}

// Function to return the similarity sum
static int sumSimilarities(string s, int n)
{
    int []Z = new int[n] ;

    // Compute the Z-array for the given string
    getZarr(s, n, Z);

    int total = n;

    // Summation of the Z-values
    for (int i = 1; i < n; i++)
        total += Z[i];

    return total;
}

// Driver code
    static public void Main (){

    string s = "ababa";
    int n = s.Length;

    Console.WriteLine(sumSimilarities(s, n));
}
// This code is contributed by ajit.
}
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    // Function to calculate the Z-array
    // for the given string
    function getZarr(str, n, Z)
    {
        let L, R, k;

        // [L, R] make a window which matches
        // with prefix of s
        L = R = 0;
        for (let i = 1; i < n; ++i) {

            // if i>R nothing matches so
            // we will calculate.
            // Z[i] using naive way.
            if (i > R) {
                L = R = i;

                // R-L = 0 in starting, so it will start
                // checking from 0'th index. For example,
                // for "ababab" and i = 1, the value of R
                // remains 0 and Z[i] becomes 0\. For string
                // "aaaaaa" and i = 1, Z[i] and R become 5
                while (R < n && str[R - L] == str[R])
                    R++;
                Z[i] = R - L;
                R--;
            }
            else {

                // k = i-L so k corresponds
                // to number which
                // matches in [L, R] interval.
                k = i - L;

                // if Z[k] is less than
                // remaining interval
                // then Z[i] will be equal to Z[k].
                // For example, str = "ababab",
                // i = 3, R = 5
                // and L = 2
                if (Z[k] < R - i + 1)
                    Z[i] = Z[k];

                // For example str = "aaaaaa"
                // and i = 2, R is 5,
                // L is 0
                else {
                    // else start from R and
                    // check manually
                    L = i;
                    while (R < n && str[R - L] == str[R])
                        R++;
                    Z[i] = R - L;
                    R--;
                }
            }
        }
    }

    // Function to return the similarity sum
    function sumSimilarities(s, n)
    {
        let Z = new Array(n);
        Z.fill(0);

        // Compute the Z-array for the given string
        getZarr(s, n, Z);

        let total = n;

        // Summation of the Z-values
        for (let i = 1; i < n; i++)
            total += Z[i];

        return total;
    }

    let s = "ababa";
    let n = s.length;

    document.write(sumSimilarities(s, n));

</script>
```

**Output:** 

```
9
```

**时间复杂度:**ON)
T3】辅助空间: O(N)