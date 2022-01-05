# 通过最大化可被 K 整除的子部分的数量来分割数字 N

> 原文:[https://www . geeksforgeeks . org/通过最大化可被 k 整除的子部分的数量来分割数字 n/](https://www.geeksforgeeks.org/split-the-number-n-by-maximizing-the-count-of-subparts-divisible-by-k/)

给定一个数字串 **N** 和一个**整数 K** ，任务是将 **N** 的数字分割成子部分，使得可被 **K** 整除的段数最大化。
***注:**我们可以在相邻的数字对之间进行任意数量的垂直切割。*

**示例:**

> **输入:** N = 32，K = 4
> **输出:** 1
> **说明:**
> 32 可被 4 整除，但如果其位数可单独整除，则不可整除，因此我们不执行任何拆分。
> **输入:** N = 2050，K = 5
> **输出:** 3
> **说明:**
> 2050 可以拆分为 2、0、5、0，其中 0、5、0 可被 5 整除。
> **输入:** N = 00001242，K = 3
> **输出:** 6
> **解释:**
> 00001242 可以拆分为 0、0、0、0、12、42，其中所有部分都可以被 3 整除。

**方法:**
为了解决上面提到的问题，我们将尝试使用[递归](https://www.geeksforgeeks.org/recursion/)方法。

*   检查当前字符和下一个字符之间是否有垂直分区，如果没有，那么我们为下一个索引再次执行递归，并通过连接当前字符来更新子字符串值。
*   现在，如果在当前字符和下一个字符之间有一个垂直分区，那么存在两种情况:
    1.  如果**现在的 subStr 可以被 X** 整除，那么我们加上 1，因为现在的 subStr 是可能答案的 1，然后对下一个索引重复出现，并将 subStr 更新为空字符串。
    2.  如果**现在的 subStr 不能被 X** 整除，那么我们简单地重现下一个索引，并将 subStr 更新为空字符串。
*   返回上面提到的两种可能情况中的最大值。

下面是上述逻辑的实现

## C++

```
// C++ program to split the number N
// by maximizing the count
// of subparts divisible by K

#include <bits/stdc++.h>
using namespace std;

// Function to count the subparts
int count(string N, int X,
          string subStr,
          int index, int n)
{

    if (index == n)
        return 0;

    // Total subStr till now
    string a = subStr + N[index];

    // b marks the subString uptil now
    // is divisible by X or not,

    // If it can be divided,
    // then this substring is one
    // of the possible answer
    int b = 0;

    // Convert string to long long and
    // check if its divisible with X
    if (stoll(a) % X == 0)
        b = 1;

    // Consider there is no vertical
    // cut between this index and the
    // next one, hence take total
    // carrying total substr a.
    int m1 = count(N, X, a, index + 1, n);

    // If there is vertical
    // cut between this index
    // and next one, then we
    // start again with subStr as ""
    // and add b for the count
    // of subStr upto now
    int m2 = b + count(N, X, "",
                       index + 1, n);

    // Return max of both the cases
    return max(m1, m2);
}

// Driver code
int main()
{
    string N = "00001242";

    int K = 3;

    int l = N.length();

    cout << count(N, K, "", 0, l)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split the number N
// by maximizing the count
// of subparts divisible by K
class GFG{

// Function to count the subparts
static int count(String N, int X,
                 String subStr,
                 int index, int n)
{
    if (index == n)
        return 0;

    // Total subStr till now
    String a = subStr + N.charAt(index);

    // b marks the subString uptil now
    // is divisible by X or not,

    // If it can be divided,
    // then this subString is one
    // of the possible answer
    int b = 0;

    // Convert String to long and
    // check if its divisible with X
    if (Long.valueOf(a) % X == 0)
        b = 1;

    // Consider there is no vertical
    // cut between this index and the
    // next one, hence take total
    // carrying total substr a.
    int m1 = count(N, X, a, index + 1, n);

    // If there is vertical
    // cut between this index
    // and next one, then we
    // start again with subStr as ""
    // and add b for the count
    // of subStr upto now
    int m2 = b + count(N, X, "",
                       index + 1, n);

    // Return max of both the cases
    return Math.max(m1, m2);
}

// Driver code
public static void main(String[] args)
{
    String N = "00001242";

    int K = 3;

    int l = N.length();

    System.out.print(count(N, K, "", 0, l) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to split the number N
# by maximizing the count
# of subparts divisible by K

# Function to count the subparts
def count(N, X, subStr, index, n):

    if (index == n):
        return 0

    # Total subStr till now
    a = subStr + N[index]

    # b marks the subString uptil now
    # is divisible by X or not,

    # If it can be divided,
    # then this substring is one
    # of the possible answer
    b = 0

    # Convert string to long long and
    # check if its divisible with X
    if (int(a) % X == 0):
        b = 1

    # Consider there is no vertical
    # cut between this index and the
    # next one, hence take total
    # carrying total substr a.
    m1 = count(N, X, a, index + 1, n)

    # If there is vertical
    # cut between this index
    # and next one, then we
    # start again with subStr as ""
    # and add b for the count
    # of subStr upto now
    m2 = b + count(N, X, "", index + 1, n)

    # Return max of both the cases
    return max(m1, m2)

# Driver code
N = "00001242"
K = 3

l = len(N)

print(count(N, K, "", 0, l))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to split the number N
// by maximizing the count
// of subparts divisible by K
using System;
class GFG{

// Function to count the subparts
static int count(String N, int X,
                 String subStr,
                 int index, int n)
{
    if (index == n)
        return 0;

    // Total subStr till now
    String a = subStr + N[index];

    // b marks the subString uptil now
    // is divisible by X or not,

    // If it can be divided,
    // then this subString is one
    // of the possible answer
    int b = 0;

    // Convert String to long and
    // check if its divisible with X
    if (long. Parse(a) % X == 0)
        b = 1;

    // Consider there is no vertical
    // cut between this index and the
    // next one, hence take total
    // carrying total substr a.
    int m1 = count(N, X, a, index + 1, n);

    // If there is vertical
    // cut between this index
    // and next one, then we
    // start again with subStr as ""
    // and add b for the count
    // of subStr upto now
    int m2 = b + count(N, X, "",
                  index + 1, n);

    // Return max of both the cases
    return Math.Max(m1, m2);
}

// Driver code
public static void Main(String[] args)
{
    String N = "00001242";

    int K = 3;

    int l = N.Length;

    Console.Write(count(N, K, "", 0, l) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to split the number N
// by maximizing the count
// of subparts divisible by K

// Function to count the subparts
function count(N, X,
                 subStr,
                 index, n)
{
    if (index == n)
        return 0;

    // Total subStr till now
    let a = subStr + N[index];

    // b marks the subString uptil now
    // is divisible by X or not,

    // If it can be divided,
    // then this subString is one
    // of the possible answer
    let b = 0;

    // Convert String to long and
    // check if its divisible with X
    if (parseInt(a) % X == 0)
        b = 1;

    // Consider there is no vertical
    // cut between this index and the
    // next one, hence take total
    // carrying total substr a.
    let m1 = count(N, X, a, index + 1, n);

    // If there is vertical
    // cut between this index
    // and next one, then we
    // start again with subStr as ""
    // and add b for the count
    // of subStr upto now
    let m2 = b + count(N, X, "",
                       index + 1, n);

    // Return max of both the cases
    return Math.max(m1, m2);
}

// Driver Code

    let N = "00001242";

    let K = 3;

    let l = N.length;

    document.write(count(N, K, "", 0, l) + "\n");

</script>
```

**Output:** 

```
6
```