# 二进制数的 1 和 2 的补码

> 原文:[https://www . geesforgeks . org/1s-2s-补码-二进制-数字/](https://www.geeksforgeeks.org/1s-2s-complement-binary-number/)

给定一个二进制数作为字符串，打印它的 1 和 2 的补码。

**一个二进制数的 1 的补码**是另一个二进制数，通过切换其中的所有位获得，即将 0 位转换为 1，将 1 位转换为 0。

**示例:**

```
1's complement of "0111" is "1000"
1's complement of "1100" is  "0011" 
```

**二进制数的 2 的补码**是 1，加到二进制数的 1 的补码上。

**示例:**

```
2's complement of "0111" is  "1001"
2's complement of "1100" is  "0100" 
```

#### 另一个寻找二进制补码的技巧:

**步骤 1:** 从最低有效位开始，向左遍历，直到找到 1。直到你找到 1，比特保持不变

**第二步:**一旦找到 1，就让 1 保持原样，现在

**第三步:**将剩下的所有位翻转为 1。

#### 说明

假设我们需要找到 100100 的 2s 补码

**第 1 步:**遍历并让位保持不变，直到找到 1。这里 x 还不知道。答案= xxxx 00–

**第二步**:你找到了 1。让它保持不变。答案= xxx100

**第三步:**将剩下的所有位翻转为 1。答案= 011100。

因此，100100 的 2s 补码是 011100。

对于补码，我们只需要翻转所有位。
对于 2 的补码，我们先找 1 的补码。我们从最低有效位开始遍历 1 的补码，寻找 0。我们翻转所有 1(变为 0)，直到找到 0。最后，我们翻转找到的 0。例如，2 的补码“01000”是“11000”(注意，我们首先发现 01000 的补码是 10111)。如果所有的 1 都是 1(在补码中)，我们在字符串中多加一个 1。例如，2 的补码“000”是“1000”(1 的补码“000”是“111”)。

下面是实现。

## C++

```
// C++ program to print 1's and 2's complement of
// a binary number
#include <bits/stdc++.h>
using namespace std;

// Returns '0' for '1' and '1' for '0'
char flip(char c) {return (c == '0')? '1': '0';}

// Print 1's and 2's complement of binary number
// represented by "bin"
void printOneAndTwosComplement(string bin)
{
    int n = bin.length();
    int i;

    string ones, twos;
    ones = twos = "";

    //  for ones complement flip every bit
    for (i = 0; i < n; i++)
        ones += flip(bin[i]);

    //  for two's complement go from right to left in
    //  ones complement and if we get 1 make, we make
    //  them 0 and keep going left when we get first
    //  0, make that 1 and go out of loop
    twos = ones;
    for (i = n - 1; i >= 0; i--)
    {
        if (ones[i] == '1')
            twos[i] = '0';
        else
        {
            twos[i] = '1';
            break;
        }
    }

    // If No break : all are 1  as in 111  or  11111;
    // in such case, add extra 1 at beginning
    if (i == -1)
        twos = '1' + twos;

    cout << "1's complement: " << ones << endl;
    cout << "2's complement: " << twos << endl;
}

// Driver program
int main()
{
    string bin = "1100";
    printOneAndTwosComplement(bin);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print 1's and 2's complement of
// a binary number

class GFG
{

    // Returns '0' for '1' and '1' for '0'
    static char flip(char c)
    {
        return (c == '0') ? '1' : '0';
    }

    // Print 1's and 2's complement of binary number
    // represented by "bin"
    static void printOneAndTwosComplement(String bin)
    {
        int n = bin.length();
        int i;

        String ones = "", twos = "";
        ones = twos = "";

        // for ones complement flip every bit
        for (i = 0; i < n; i++)
        {
            ones += flip(bin.charAt(i));
        }

        // for two's complement go from right to left in
        // ones complement and if we get 1 make, we make
        // them 0 and keep going left when we get first
        // 0, make that 1 and go out of loop
        twos = ones;
        for (i = n - 1; i >= 0; i--)
        {
            if (ones.charAt(i) == '1')
            {
                twos = twos.substring(0, i) + '0' + twos.substring(i + 1);
            }
            else
            {
                twos = twos.substring(0, i) + '1' + twos.substring(i + 1);
                break;
            }
        }

        // If No break : all are 1 as in 111 or 11111;
        // in such case, add extra 1 at beginning
        if (i == -1)
        {
            twos = '1' + twos;
        }

        System.out.println("1's complement: " + ones);;
        System.out.println("2's complement: " + twos);
    }

    // Driver code
    public static void main(String[] args)
    {
        String bin = "1100";
        printOneAndTwosComplement(bin);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print 1's and 2's
# complement of a binary number

# Returns '0' for '1' and '1' for '0'
def flip(c):
    return '1' if (c == '0') else '0'

# Print 1's and 2's complement of
# binary number represented by "bin"
def printOneAndTwosComplement(bin):

    n = len(bin)
    ones = ""
    twos = ""

    # for ones complement flip every bit
    for i in range(n):
        ones += flip(bin[i])

    # for two's complement go from right
    # to left in ones complement and if
    # we get 1 make, we make them 0 and
    # keep going left when we get first
    # 0, make that 1 and go out of loop
    ones = list(ones.strip(""))
    twos = list(ones)
    for i in range(n - 1, -1, -1):

        if (ones[i] == '1'):
            twos[i] = '0'
        else:        
            twos[i] = '1'
            break

    i -= 1   
    # If No break : all are 1 as in 111 or 11111
    # in such case, add extra 1 at beginning
    if (i == -1):
        twos.insert(0, '1')

    print("1's complement: ", *ones, sep = "")
    print("2's complement: ", *twos, sep = "")

# Driver Code
if __name__ == '__main__':
    bin = "1100"
    printOneAndTwosComplement(bin.strip(""))

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to print 1's and 2's complement of
// a binary number
using System;

class GFG
{

    // Returns '0' for '1' and '1' for '0'
    static char flip(char c)
    {
        return (c == '0') ? '1' : '0';
    }

    // Print 1's and 2's complement of binary number
    // represented by "bin"
    static void printOneAndTwosComplement(String bin)
    {
        int n = bin.Length;
        int i;

        String ones = "", twos = "";
        ones = twos = "";

        // for ones complement flip every bit
        for (i = 0; i < n; i++)
        {
            ones += flip(bin[i]);
        }

        // for two's complement go from right to left in
        // ones complement and if we get 1 make, we make
        // them 0 and keep going left when we get first
        // 0, make that 1 and go out of loop
        twos = ones;
        for (i = n - 1; i >= 0; i--)
        {
            if (ones[i] == '1')
            {
                twos = twos.Substring(0, i) + '0' +
                twos.Substring(i + 1,twos.Length-(i+1));
            }
            else
            {
                twos = twos.Substring(0, i) + '1' +
                twos.Substring(i + 1,twos.Length-(i+1));
                break;
            }
        }

        // If No break : all are 1 as in 111 or 11111;
        // in such case, add extra 1 at beginning
        if (i == -1)
        {
            twos = '1' + twos;
        }

        Console.WriteLine("1's complement: " + ones);;
        Console.WriteLine("2's complement: " + twos);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String bin = "1100";
        printOneAndTwosComplement(bin);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to print 1's and 2's complement of
// a binary number

// Returns '0' for '1' and '1' for '0'
function flip (c) {return (c == '0')? '1': '0';}

// Print 1's and 2's complement of binary number
// represented by "bin"
function printOneAndTwosComplement(bin)
{
    var n = bin.length;
    var i;

    var ones, twos;
    ones = twos = "";

    //  for ones complement flip every bit
    for (i = 0; i < n; i++)
        ones += flip(bin[i]);

    //  for two's complement go from right to left in
    //  ones complement and if we get 1 make, we make
    //  them 0 and keep going left when we get first
    //  0, make that 1 and go out of loop
    twos = ones;
    twos = twos.split('')
    for (i = n - 1; i >= 0; i--)
    {
        if (ones[i] == '1')
            twos[i] = '0';
        else
        {
            twos[i] = '1';
            break;
        }
    }
    twos = twos.join('')
    // If No break : all are 1  as in 111  or  11111;
    // in such case, add extra 1 at beginning
    if (i == -1)
        twos = '1' + twos;

    document.write( "1's complement: " + ones + "<br>");
    document.write( "2's complement: " + twos + "<br>");
}

// Driver program
var bin = "1100";
printOneAndTwosComplement(bin);

</script>
```

**输出:**

```
1's complement: 0011
2's complement: 0100
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

感谢 [Utkarsh Trivedi](http://qa.geeksforgeeks.org/user/utkarsh111) 的上述解决方案。
作为旁注，有符号数一般使用 2 的补码表示。正值按原样存储，负值以 2 的补码形式存储。需要一个额外的位来指示数字是正数还是负数。例如，c 中的 char 是 8 位。如果 char 使用 2 的补码表示，则按原样存储 127，即 01111111，其中前 0 表示正。但是-127 存储为 10000001。
**相关帖子:**
[**二进制字符串 2 补码的高效方法**](https://www.geeksforgeeks.org/efficient-method-2s-complement-binary-string/)
如果您发现任何不正确的地方，或者您想分享更多关于上述主题的信息，请写评论。
**参考文献:**
[http://QA . geesforgeks . org/6439/write-program-compute-one-and-2s-complex-of-number](http://qa.geeksforgeeks.org/6439/write-program-calculate-ones-and-twos-complement-of-number)
[http://geesquiz . com/what-difference-1s-complex-and-2s-complex/](http://geeksquiz.com/whats-difference-between-1s-complement-and-2s-complement/)