# 从字符串中删除最少的字符，在给定的约束条件下将其分成三个子字符串

> 原文:[https://www . geeksforgeeks . org/remove-从字符串中删除最少字符-在给定约束条件下将其拆分为三个子字符串/](https://www.geeksforgeeks.org/remove-minimum-characters-from-string-to-split-it-into-three-substrings-under-given-constraints/)

给定一个由小写字母组成的字符串 **str** ，任务是从给定的字符串中删除最少的字符，这样字符串就可以分成 3 个子字符串 **str1** 、 **str2** 和 **str3** ，这样每个子字符串都可以是空的或者只包含字符**“a”**、**“b”**和**“c”**。
**例:**

> **输入:**str = " aaaaaaaaccac "
> T3】输出: 3
> **解释:**
> 字符串去掉 b、x、a 后，字符串 str 变成“aaaaaaccc”
> 现在 str 1 =“AAA AAA”，str2 =“，str 3 =“CCC”。
> 移除的最小字符为 3。
> **输入:**str =“baabbcdcca”
> **输出:** 4
> **解释:**
> 字符串去掉 b、c、d、a 后，字符串 str 变成“aabbbcc”
> 现在 str 1 =“aa”，str 2 =“BBB”，str 3 =“cc”。
> 移除的最小字符为 4。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。我们将使用三个[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来制作字符的前缀数组**“a”、“b”和“c”**。每个前缀数组将分别在任意索引 **i** 处存储字母**‘a’、‘b’和‘c’**的计数。以下是步骤:

1.  创建三个前缀数组如下:
    *   **pref<sub>a</sub>【I】**表示长度为 I 的前缀中字母“a”的计数
    *   **pref<sub>b</sub>【I】**表示长度为 I 的前缀中字母“b”的计数
    *   **pref<sub>c</sub>【I】**表示长度为 I 的前缀中字母“c”的计数
2.  为了删除最少的字符数，结果字符串应该是最大的。
3.  想法是把两个位置 **i** 和 **j** 串起来， **0？我吗？j&leq；N** ，为了将管柱分成所有可能长度的三部分，执行以下操作:
    *   从前缀中删除除**‘a’**以外的所有字符，前缀以 I 结尾，这将是字符串 **str1** 。
    *   从以 j 开头的后缀中删除除**‘c’**以外的所有字符，这将是字符串 **str3** 。
    *   移除除位置 I 和 j 之间的**【b】**以外的所有字符，这将是字符串 **str2** 。
4.  因此，结果字符串的总长度由下式给出:

> **(str 1+str 2+str 3)**=**(pref[I])+(pref b[j]–pref b[I])+(pref c[n]–pref c[j])**
> 总长度

1.  从给定字符串的长度中减去结果字符串的长度**字符串**以获得要删除的最少字符。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts minimum
// character that must be removed
void min_remove(string str)
{
    // Length of string
    int N = str.length();

    // Create prefix array
    int prefix_a[N + 1];
    int prefix_b[N + 1];
    int prefix_c[N + 1];

    // Initialize first position
    prefix_a[0] = 0;
    prefix_b[0] = 0;
    prefix_c[0] = 0;

    // Fill prefix array
    for (int i = 1; i <= N; i++) {
        prefix_a[i]
            = prefix_a[i - 1]
              + (str[i - 1] == 'a');

        prefix_b[i]
            = prefix_b[i - 1]
              + (str[i - 1] == 'b');

        prefix_c[i]
            = prefix_c[i - 1]
              + (str[i - 1] == 'c');
    }

    // Initialise maxi
    int maxi = INT_MIN;

    // Check all the possibilities by
    // putting i and j at different
    // position & find maximum among them
    for (int i = 0; i <= N; i++) {

        for (int j = i; j <= N; j++) {

            maxi = max(maxi,
                       (prefix_a[i]
                        + (prefix_b[j]
                           - prefix_b[i])
                        + (prefix_c[N]
                           - prefix_c[j])));
        }
    }

    // Print the characters to be removed
    cout << (N - maxi) << endl;
}

// Driver Code
int main()
{
    // Given String
    string str = "aaaabaaxccac";

    // Function Call
    min_remove(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that counts minimum
// character that must be removed
static void min_remove(String str)
{

    // Length of string
    int N = str.length();

    // Create prefix array
    int []prefix_a = new int[N + 1];
    int []prefix_b = new int[N + 1];
    int []prefix_c = new int[N + 1];

    // Initialize first position
    prefix_a[0] = 0;
    prefix_b[0] = 0;
    prefix_c[0] = 0;

    // Fill prefix array
    for(int i = 1; i <= N; i++)
    {
        prefix_a[i] = prefix_a[i - 1] +
                     (int)((str.charAt(
                            i - 1) == 'a') ? 1 : 0);

        prefix_b[i] = prefix_b[i - 1] +
                      (int)((str.charAt(i - 1) ==
                                     'b') ? 1 : 0);

        prefix_c[i] = prefix_c[i - 1] +
                      (int)((str.charAt(i - 1) ==
                                     'c') ? 1 : 0);
    }

    // Initialise maxi
    int maxi = Integer.MIN_VALUE;

    // Check all the possibilities by
    // putting i and j at different
    // position & find maximum among them
    for(int i = 0; i <= N; i++)
    {
        for(int j = i; j <= N; j++)
        {
            maxi = Math.max(maxi, (prefix_a[i] +
                                  (prefix_b[j] -
                                   prefix_b[i]) +
                                  (prefix_c[N] -
                                   prefix_c[j])));
        }
    }

    // Print the characters to be removed
    System.out.println((N - maxi));
}

// Driver Code
public static void main(String []args)
{

    // Given String
    String str = "aaaabaaxccac";

    // Function call
    min_remove(str);
}
}

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function that counts minimum
# character that must be removed
def min_remove(st):

    # Length of string
    N = len(st)

    # Create prefix array
    prefix_a = [0]*(N + 1)
    prefix_b = [0]*(N + 1)
    prefix_c = [0]*(N + 1)

    # Initialize first position
    prefix_a[0] = 0
    prefix_b[0] = 0
    prefix_c[0] = 0

    # Fill prefix array
    for i in range(1, N + 1):

        if (st[i - 1] == 'a'):
            prefix_a[i] = (prefix_a[i - 1] + 1)
        else:
            prefix_a[i] = prefix_a[i - 1]

        if (st[i - 1] == 'b'):
            prefix_b[i] = (prefix_b[i - 1] + 1)
        else:
            prefix_b[i]= prefix_b[i - 1]

        if (st[i - 1] == 'c'):
            prefix_c[i] = (prefix_c[i - 1] + 1)
        else:
            prefix_c[i] = prefix_c[i - 1]

    # Initialise maxi
    maxi = -sys.maxsize -1;

    # Check all the possibilities by
    # putting i and j at different
    # position & find maximum among them
    for i in range( N + 1):
        for j in range(i, N + 1):
            maxi = max(maxi,
                      (prefix_a[i] +
                      (prefix_b[j] -
                       prefix_b[i]) +
                      (prefix_c[N] -
                       prefix_c[j])))

    # Print the characters to be removed
    print((N - maxi))

# Driver Code
if __name__ == "__main__":

    # Given String
    st = "aaaabaaxccac"

    # Function Call
    min_remove(st)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that counts minimum
// character that must be removed
static void min_remove(string str)
{

    // Length of string
    int N = str.Length;

    // Create prefix array
    int []prefix_a = new int[N + 1];
    int []prefix_b = new int[N + 1];
    int []prefix_c = new int[N + 1];

    // Initialize first position
    prefix_a[0] = 0;
    prefix_b[0] = 0;
    prefix_c[0] = 0;

    // Fill prefix array
    for(int i = 1; i <= N; i++)
    {
        prefix_a[i] = prefix_a[i - 1] +
                    (int)((str[i - 1] == 'a') ?
                                   1 : 0);

        prefix_b[i] = prefix_b[i - 1] +
                    (int)((str[i - 1] == 'b') ?
                                   1 : 0);

        prefix_c[i] = prefix_c[i - 1] +
                    (int)((str[i - 1] == 'c') ?
                                   1 : 0);
    }

    // Initialise maxi
    int maxi = Int32.MinValue;

    // Check all the possibilities by
    // putting i and j at different
    // position & find maximum among them
    for(int i = 0; i <= N; i++)
    {
        for(int j = i; j <= N; j++)
        {
            maxi = Math.Max(maxi, (prefix_a[i] +
                                  (prefix_b[j] -
                                   prefix_b[i]) +
                                  (prefix_c[N] -
                                   prefix_c[j])));
        }
    }

    // Print the characters to be removed
    Console.WriteLine((N - maxi));
}

// Driver Code
public static void Main()
{

    // Given String
    string str = "aaaabaaxccac";

    // Function call
    min_remove(str);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function that counts minimum
// character that must be removed
function min_remove(str)
{

    // Length of string
    let N = str.length;

    // Create prefix array
    let prefix_a = Array.from({length: N + 1}, (_, i) => 0);
    let prefix_b = Array.from({length: N + 1}, (_, i) => 0);
    let prefix_c = Array.from({length: N + 1}, (_, i) => 0);

    // Initialize first position
    prefix_a[0] = 0;
    prefix_b[0] = 0;
    prefix_c[0] = 0;

    // Fill prefix array
    for(let i = 1; i <= N; i++)
    {
        prefix_a[i] = prefix_a[i - 1] +
                     ((str[
                            i - 1] == 'a') ? 1 : 0);

        prefix_b[i] = prefix_b[i - 1] +
                      ((str[i - 1] ==
                                     'b') ? 1 : 0);

        prefix_c[i] = prefix_c[i - 1] +
                      ((str[i - 1] ==
                                     'c') ? 1 : 0);
    }

    // Initialise maxi
    let maxi = Number.MIN_VALUE;

    // Check all the possibilities by
    // putting i and j at different
    // position & find maximum among them
    for(let i = 0; i <= N; i++)
    {
        for(let j = i; j <= N; j++)
        {
            maxi = Math.max(maxi, (prefix_a[i] +
                                  (prefix_b[j] -
                                   prefix_b[i]) +
                                  (prefix_c[N] -
                                   prefix_c[j])));
        }
    }

    // Prlet the characters to be removed
    document.write((N - maxi));
}

// Driver code

     // Given String
    let str = "aaaabaaxccac";

    // Function call
    min_remove(str);

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** *O(N <sup>2</sup> )* ，其中 N 为给定字符串的长度。
**空间复杂度:** *O(N)* ，其中 N 为给定字符串的长度。