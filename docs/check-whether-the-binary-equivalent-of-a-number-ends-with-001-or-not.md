# 检查一个数字的二进制等价物是否以“001”结尾

> 原文:[https://www . geesforgeks . org/check-数字的二进制等价形式是否以-001 结尾/](https://www.geeksforgeeks.org/check-whether-the-binary-equivalent-of-a-number-ends-with-001-or-not/)

给定一个正整数 **N** ，任务是检查该整数的二进制等价物是否以“001”结尾。
如果以“001”结尾，则打印“**是**”。否则，打印“**否**”。
**示例:**

> **输入** : N = 9
> **输出**:是
> **解释**
> 9 = 1001 的二进制，以 001
> **结束输入** : N = 5
> **输出**:否
> 5 = 101 的二进制，不以 001
> 结束

**天真的方法**
找到 **N** 的[二进制等价物](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)，检查 **001** 是否是其二进制等价物的[后缀](https://www.geeksforgeeks.org/check-if-a-string-is-suffix-of-another/)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function returns true if
// s1 is suffix of s2
bool isSuffix(string s1,
              string s2)
{
    int n1 = s1.length();
    int n2 = s2.length();
    if (n1 > n2)
        return false;
    for (int i = 0; i < n1; i++)
        if (s1[n1 - i - 1]
            != s2[n2 - i - 1])
            return false;
    return true;
}

// Function to check if binary equivalent
// of a number ends in "001" or not
bool CheckBinaryEquivalent(int N)
{

    // To store the binary
    // number
    int B_Number = 0;
    int cnt = 0;

    while (N != 0) {

        int rem = N % 2;
        int c = pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store
        // exponent value
        cnt++;
    }

    string bin = to_string(B_Number);
    return isSuffix("001", bin);
}

// Driver code
int main()
{

    int N = 9;
    if (CheckBinaryEquivalent(N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function returns true if
// s1 is suffix of s2
static boolean isSuffix(String s1, String s2)
{
    int n1 = s1.length();
    int n2 = s2.length();

    if (n1 > n2)
        return false;

    for(int i = 0; i < n1; i++)
       if (s1.charAt(n1 - i - 1) !=
           s2.charAt(n2 - i - 1))
           return false;
    return true;
}

// Function to check if binary equivalent
// of a number ends in "001" or not
static boolean CheckBinaryEquivalent(int N)
{

    // To store the binary
    // number
    int B_Number = 0;
    int cnt = 0;

    while (N != 0)
    {

        int rem = N % 2;
        int c = (int)Math.pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store
        // exponent value
        cnt++;
    }
    String bin = Integer.toString(B_Number);
    return isSuffix("001", bin);
}

// Driver code
public static void main (String[] args)
{
    int N = 9;

    if (CheckBinaryEquivalent(N))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function returns true if
# s1 is suffix of s2
def isSuffix(s1, s2) :

    n1 = len(s1);
    n2 = len(s2);
    if (n1 > n2) :
        return False;
    for i in range(n1) :
        if (s1[n1 - i - 1] != s2[n2 - i - 1]) :
            return False;
    return True;

# Function to check if binary equivalent
# of a number ends in "001" or not
def CheckBinaryEquivalent(N) :

    # To store the binary
    # number
    B_Number = 0;
    cnt = 0;

    while (N != 0) :

        rem = N % 2;
        c = 10 ** cnt;
        B_Number += rem * c;
        N //= 2;

        # Count used to store
        # exponent value
        cnt += 1;

    bin = str(B_Number);
    return isSuffix("001", bin);

# Driver code
if __name__ == "__main__" :

    N = 9;
    if (CheckBinaryEquivalent(N)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function returns true if
// s1 is suffix of s2
static bool isSuffix(string s1, string s2)
{
    int n1 = s1.Length;
    int n2 = s2.Length;

    if (n1 > n2)
        return false;

    for(int i = 0; i < n1; i++)
       if (s1[n1 - i - 1] !=
           s2[n2 - i - 1])
           return false;
    return true;
}

// Function to check if binary equivalent
// of a number ends in "001" or not
static bool CheckBinaryEquivalent(int N)
{

    // To store the binary
    // number
    int B_Number = 0;
    int cnt = 0;

    while (N != 0)
    {
        int rem = N % 2;
        int c = (int)Math.Pow(10, cnt);
        B_Number += rem * c;
        N /= 2;

        // Count used to store
        // exponent value
        cnt++;
    }
    string bin = B_Number.ToString();
    return isSuffix("001", bin);
}

// Driver code
public static void Main (string[] args)
{
    int N = 9;

    if (CheckBinaryEquivalent(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the above approach

// Function returns true if
// s1 is suffix of s2
function isSuffix( s1,  s2)
{
    var n1 = s1.length;
    var n2 = s2.length;

    if (n1 > n2)
        return false;

    for(var i = 0; i < n1; i++)
       if (s1[n1 - i - 1] !=
           s2[n2 - i - 1])
           return false;
    return true;
}

// Function to check if binary equivalent
// of a number ends in "001" or not
function CheckBinaryEquivalent( N)
{

    // To store the binary
    // number
    var B_Number = 0;
    var cnt = 0;

    while (N != 0)
    {
        var rem = N % 2;
        var c = Math.pow(10, cnt);
        B_Number += rem * c;
        N = Math.floor(N/ 2);

        // Count used to store
        // exponent value
        cnt++;
    }
     console.log(B_Number);
    var bin = B_Number.toString();
    return isSuffix("001", bin);
}

// Driver code

    var N = 9;

    if (CheckBinaryEquivalent(N))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*
**高效逼近**
我们可以观察到，一个数的二进制等价只有在**(N–1)**可被 8 整除时才以**【001】**结束。

> **图解:**
> 顺序 **1、9、17、25、33……**在其二进制表示中有 **001** 作为后缀。
> N <sup>上述序列的第</sup>项用 **8 * N + 1**
> 表示，所以只有当**(N–1)% 8 = = 0**
> 时，一个数的二进制等价物才以**“001”**结束

以下是上述方法的实现:

## C++

```
// C++ implementation of the above
// approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if binary
// equivalent of a number ends
// in "001" or not
bool CheckBinaryEquivalent(int N)
{
    // To check if binary equivalent
    // of a number ends in
    // "001" or not
    return (N - 1) % 8 == 0;
}

// Driver code
int main()
{

    int N = 9;
    if (CheckBinaryEquivalent(N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to check if binary
// equivalent of a number ends
// in "001" or not
static boolean CheckBinaryEquivalent(int N)
{

    // To check if binary equivalent
    // of a number ends in
    // "001" or not
    return (N - 1) % 8 == 0;
}

// Driver code
public static void main (String[] args)
{
    int N = 9;

    if (CheckBinaryEquivalent(N))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to check if binary
# equivalent of a number ends
# in "001" or not
def CheckBinaryEquivalent(N):

    # To check if binary equivalent
    # of a number ends in
    # "001" or not
    return (N - 1) % 8 == 0;

# Driver code
if __name__ == "__main__":

    N = 9;

    if (CheckBinaryEquivalent(N)):
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to check if binary
// equivalent of a number ends
// in "001" or not
static bool CheckBinaryEquivalent(int N)
{

    // To check if binary equivalent
    // of a number ends in
    // "001" or not
    return (N - 1) % 8 == 0;
}

// Driver code
public static void Main (string[] args)
{
    int N = 9;

    if (CheckBinaryEquivalent(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above
// approach

// Function to check if binary
// equivalent of a number ends
// in "001" or not
function CheckBinaryEquivalent(N)
{
    // To check if binary equivalent
    // of a number ends in
    // "001" or not
    return (N - 1) % 8 == 0;
}

// Driver code
var N = 9;
if (CheckBinaryEquivalent(N))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*