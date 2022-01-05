# 分割一个二进制数，使每个部分都能被 2 整除的方法数

> 原文:[https://www . geeksforgeeks . org/分割二进制数的方法数，这样每个部分都可以被 2 整除/](https://www.geeksforgeeks.org/number-of-ways-to-split-a-binary-number-such-that-every-part-is-divisible-by-2/)

给定一个二进制字符串 **S** ，任务是找到将它分成多个部分的方法，使得每个部分都可以被 **2** 整除。

**示例:**

> **输入:** S = "100"
> **输出:** 2
> 拆分字符串有两种方式:
> {“10”、“0”}和{“100”}
> **输入:** S = "110"
> **输出:** 1

**进场:**一个观察是，绳子只能在一个 **0** 后才能劈开。因此，计算字符串中零的数量。我们把这个计数叫做 **c_zero** 。假设字符串为偶数的情况下，除了最右边的一个之外，对于每一个 **0** ，有两个选择，即要么在那个零之后切字符串，要么不切。因此，对于偶数字符串，最终答案变为**2<sup>(c _ zero–1)</sup>**。
字符串不能拆分的情况是在一个 **1** 结束的情况。因此，对于奇数字符串，答案总是零，因为最后一个分割部分总是奇数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define maxN 20
#define maxM 64

// Function to return the required count
int cntSplits(string s)
{
    // If the splitting is not possible
    if (s[s.size() - 1] == '1')
        return 0;

    // To store the count of zeroes
    int c_zero = 0;

    // Counting the number of zeroes
    for (int i = 0; i < s.size(); i++)
        c_zero += (s[i] == '0');

    // Return the final answer
    return (int)pow(2, c_zero - 1);
}

// Driver code
int main()
{
    string s = "10010";

    cout << cntSplits(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int maxN = 20;
static int maxM = 64;

// Function to return the required count
static int cntSplits(String s)
{
    // If the splitting is not possible
    if (s.charAt(s.length() - 1) == '1')
        return 0;

    // To store the count of zeroes
    int c_zero = 0;

    // Counting the number of zeroes
    for (int i = 0; i < s.length(); i++)
        c_zero += (s.charAt(i) == '0') ? 1 : 0;

    // Return the final answer
    return (int)Math.pow(2, c_zero - 1);
}

// Driver code
public static void main(String []args)
{
    String s = "10010";

    System.out.println(cntSplits(s));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required count
def cntSplits(s) :

    # If the splitting is not possible
    if (s[len(s) - 1] == '1') :
        return 0;

    # To store the count of zeroes
    c_zero = 0;

    # Counting the number of zeroes
    for i in range(len(s)) :
        c_zero += (s[i] == '0');

    # Return the final answer
    return int(pow(2, c_zero - 1));

# Driver code
if __name__ == "__main__" :

    s = "10010";

    print(cntSplits(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int maxN = 20;
static int maxM = 64;

// Function to return the required count
static int cntSplits(String s)
{
    // If the splitting is not possible
    if (s[s.Length - 1] == '1')
        return 0;

    // To store the count of zeroes
    int c_zero = 0;

    // Counting the number of zeroes
    for (int i = 0; i < s.Length; i++)
        c_zero += (s[i] == '0') ? 1 : 0;

    // Return the final answer
    return (int)Math.Pow(2, c_zero - 1);
}

// Driver code
public static void Main(String []args)
{
    String s = "10010";

    Console.WriteLine(cntSplits(s));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var maxN = 20;
var maxM = 64;

// Function to return the required count
function cntSplits(s)
{
    // If the splitting is not possible
    if (s[s.length - 1] == '1')
        return 0;

    // To store the count of zeroes
    var c_zero = 0;

    // Counting the number of zeroes
    for (var i = 0; i < s.length; i++)
        c_zero += (s[i] == '0');

    // Return the final answer
    return Math.pow(2, c_zero - 1);
}

// Driver code
var s = "10010";
document.write( cntSplits(s));

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)