# 重复 K 次的字符串中作为“ab”的子序列数

> 原文:[https://www . geesforgeks . org/number-subseries-ab-string-repeated-k-times/](https://www.geeksforgeeks.org/number-subsequences-ab-string-repeated-k-times/)

给定一个字符串 S，考虑一个新的字符串，它是通过重复 S 正好 K 次而形成的。我们需要在新形成的字符串中找到作为“ab”的子序列数。

**示例:**

```
Input : S = "abcb"
        K = 2
Output : 6
Here, Given string is repeated 2 times and
we get a new string "abcbabcb"
Below are 6 occurrences of "ab"
abcbabcb
abcbabcb
abcbabcb
abcbabcb
abcbabcb
abcbabcb

Input : S = "aacbd"
        K = 1
Output : 2
```

**天真方法**:寻找“ab”的子序列数，其实就是寻找一对 s[i]，s[j] (i < j)，其中 s[i] = 'a '，s[j] = 'b '。
我们可以通过使用两个嵌套的 for 循环来实现这一点，并计算对的数量。
我们可以在字符串的单次遍历中改进这种方法。让我们考虑一个索引 j， **s[j] ='b'** ，如果我们发现索引 I 的编号为 **s[i] = 'a'** 和 i < j，那么它与“ab”直到 j 的子序列的编号相同。这可以通过遍历数组来保持 a 的计数，并将该计数添加到我们的答案中 s[i] ='b .
**时间复杂度**:O(| S | *)

**有效方法:**
让 T 成为新形成的弦
T = s1 + s2 + s3 + …..+sk；
这里 si 是 S 串的第几个出现
这里 T 中“ab”的出现如下:
1)“ab”完全在于 S 串的一些出现，所以我们可以简单的找到 Si 中“ab”的出现。假设是 C，那么 T 中“ab”出现的总次数就是 **C*K** 。
2)否则，“a”严格地位于某些弦 Si 内，“b”位于另一些弦 Sj 内，(i < j)。这样，找到“ab”的出现次数将是从 K 个出现次数 **( <sub>KC2)</sub>** 中选择字符串 S 的两个出现次数，并将其与 Si 中“a”的出现次数和 Sj 中“b”的出现次数相乘。
As，Si = Sj = S。

**时间复杂度:** O(|S|)，用于计算“a”的个数和“b”的个数

## C++

```
// CPP code to find number of subsequences of
// "ab" in the string S which is repeated K times.
#include <bits/stdc++.h>
using namespace std;

int countOccurrences(string s, int K)
{
    int n = s.length();
    int C, c1 = 0, c2 = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] == 'a')
            c1++; // Count of 'a's
        if (s[i] == 'b') {
            c2++; // Count of 'b's
            C += c1; // occurrence of "ab"s in string S
        }
    }

    // Add following two :
    // 1) K * (Occurrences of "ab" in single string)
    // 2) a is from one string and b is from other.
    return C * K + (K * (K - 1) / 2) * c1 * c2;
}

// Driver code
int main()
{
    string S = "abcb";
    int k = 2;
    cout << countOccurrences(S, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find number of subsequences of
// "ab" in the string S which is repeated K times.

import java.io.*;

class GFG {

    static int countOccurrences(String s, int K)
    {
        int n = s.length();
        int C = 0, c1 = 0, c2 = 0;
        for (int i = 0; i < n; i++) {
            if (s.charAt(i) == 'a')
                c1++; // Count of 'a's
            if (s.charAt(i) == 'b') {
                c2++; // Count of 'b's

                // occurrence of "ab"s
                // in string S
                C += c1;
            }
        }

        // Add following two :
        // 1) K * (Occurrences of "ab" in single string)
        // 2) a is from one string and b is from other.
        return C * K + (K * (K - 1) / 2) * c1 * c2;
    }

    // Driver code
    public static void main(String[] args)
    {
        String S = "abcb";
        int k = 2;

        System.out.println(countOccurrences(S, k));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 code to find number of
# subsequences of "ab" in the
# string S which is repeated K times.

def countOccurrences (s, K):
    n = len(s)
    c1 = 0
    c2 = 0
    C = 0
    for i in range(n):
        if s[i] == 'a':
            c1+= 1 # Count of 'a's
        if s[i] == 'b':
            c2+= 1 # Count of 'b's

            # occurrence of "ab"s in string S
            C += c1

    # Add following two :
    # 1) K * (Occurrences of "ab" in single string)
    # 2) a is from one string and b is from other.
    return C * K + (K * (K - 1) / 2) * c1 * c2

# Driver code
S = "abcb"
k = 2
print (countOccurrences(S, k))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# code to find number of subsequences
// of "ab" in the string S which is
// repeated K times.
using System;

class GFG {

    static int countOccurrences(string s, int K)
    {

        int n = s.Length;
        int C = 0, c1 = 0, c2 = 0;

        for (int i = 0; i < n; i++) {

            if (s[i] == 'a')

                // Count of 'a's
                c1++;
            if (s[i] == 'b') {

                // Count of 'b's
                c2++;

                // occurrence of "ab"s
                // in string S
                C += c1;
            }
        }

        // Add following two :
        // 1) K * (Occurrences of "ab" in
        // single string)
        // 2) a is from one string and b
        // is from other.
        return C * K + (K * (K - 1) / 2) * c1 * c2;
    }

    // Driver code
    public static void Main()
    {

        string S = "abcb";
        int k = 2;

        Console.WriteLine(
            countOccurrences(S, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find number of
// subsequences of "ab" in the
// string S which is repeated K times.

function countOccurrences($s, $K)
{
    $n = strlen($s);
    $C = 0; $c1 = 0; $c2 = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($s[$i] == 'a')
            // Count of 'a's
            $c1++;
        if ($s[$i] == 'b')
        {
            // Count of 'b's
            $c2++;

            // occurrence of "ab"s
            // in string S
            $C = $C+ $c1;
        }
    }

    // Add following two :
    // 1) K * (Occurrences of "ab"
    //    in single string)
    // 2) a is from one string and
    //    b is from other.
    return $C * $K + ($K * ($K - 1) / 2) *
                                $c1 * $c2;
}

// Driver code
$S = "abcb";
$k = 2;
echo countOccurrences($S, $k), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript code to find number of subsequences of
// "ab" in the string S which is repeated K times.
function countOccurrences(s, K)
{
    let n = s.length;
    let C = 0, c1 = 0, c2 = 0;

    for(let i = 0; i < n; i++)
    {
        if (s[i] == 'a')
            c1++; // Count of 'a's
        if (s[i] == 'b')
        {
            c2++; // Count of 'b's

            // Occurrence of "ab"s
            // in string S
            C += c1;
        }
    }

    // Add following two :
    // 1) K * (Occurrences of "ab" in single string)
    // 2) a is from one string and b is from other.
    return C * K + (K * (K - 1) / 2) * c1 * c2;
}

// Driver Code
let S = "abcb";
let k = 2;

document.write(countOccurrences(S, k));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
 6 
```

**时间复杂度:** O(|S|)。