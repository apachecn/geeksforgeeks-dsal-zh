# 检查给定的字符串是否是线性的

> 原文:[https://www . geeksforgeeks . org/check-如果给定的字符串是线性或非线性/](https://www.geeksforgeeks.org/check-if-the-given-string-is-linear-or-not/)

给定字符串 **str** ，任务是检查给定字符串是否是线性的。如果是线性，则打印**“是”**否则打印**“否”**。

> 让字符串为“abcdefghij”。可以分解为:
> 【a】
> 【BC】
> 【def】
> 【ghij】
> 如果字符 a、b、c 和相等，那么给定的字符串是线性的，否则不是。
> 因此，如果字符串的形式为“xxabxabcxabcdxabdexab……”那么它被称为**线性字符串**。

**示例:**

> **输入:**str = " aapaxayaziabcde "
> **输出:**是
> **解释:**T8】a
> AP
> axy
> ayzi
> abcde
> 所有断串的字符都与第一个字符相同。
> **输入:** str = "bbobfycd"
> **输出:**No
> T21【解释:
> b
> bo
> bfy
> CD
> 这里 b=b=b！=c

**方法:**要检查给定字符串的形式是否为**“xxabxabcxabcdexaab……”**那么我们必须检查索引 **0、1、3、6、10、…** 处的字符是否相等。
如果上述索引处的所有字符相等，则给定的字符串为**线性字符串**，否则不相等。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given
// string is linear or not
int is_linear(string s)
{
    int tmp = 0;

    char first = s[0];

    // Iterate over string
    for (int pos = 0; pos < s.length();
        pos += tmp) {

        // If character is not same as
        // the first character then
        // return false
        if (s[pos] != first) {
            return false;
        }

        // Increment the tmp
        tmp++;
    }

    return true;
}

// Driver Code
int main()
{
    // Given String str
    string str = "aapaxyayziabcde";

    // Function Call
    if (is_linear(str)) {
        cout << "Yes" << endl;
    }
    else {
        cout << "No" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the given
// string is linear or not
static boolean is_linear(String s)
{
    int tmp = 0;
    char first = s.charAt(0);

    // Iterate over string
    for(int pos = 0; pos < s.length();
            pos += tmp)
    {

        // If character is not same as
        // the first character then
        // return false
        if (s.charAt(pos) != first)
        {
            return false;
        }

        // Increment the tmp
        tmp++;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{

    // Given String str
    String str = "aapaxyayziabcde";

    // Function call
    if (is_linear(str))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the given
# is linear or not
def is_linear(s):

    tmp = 0
    first = s[0]
    pos = 0

    # Iterate over string
    while pos < len(s):

        # If character is not same as
        # the first character then
        # return false
        if (s[pos] != first):
            return False

        # Increment the tmp
        tmp += 1
        pos += tmp

    return True

# Driver Code
if __name__ == '__main__':

    # Given String str
    str = "aapaxyayziabcde"

    # Function call
    if (is_linear(str)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the given
// string is linear or not
static bool is_linear(String s)
{
    int tmp = 0;
    char first = s[0];

    // Iterate over string
    for(int pos = 0; pos < s.Length;
            pos += tmp)
    {

        // If character is not same as
        // the first character then
        // return false
        if (s[pos] != first)
        {
            return false;
        }

        // Increment the tmp
        tmp++;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{

    // Given String str
    String str = "aapaxyayziabcde";

    // Function call
    if (is_linear(str))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the given
// string is linear or not
function is_linear(s)
{
    let tmp = 0;
    let first = s[0];

    // Iterate over string
    for(let pos = 0; pos < s.length;
            pos += tmp)
    {

        // If character is not same as
        // the first character then
        // return false
        if (s[pos] != first)
        {
            return false;
        }

        // Increment the tmp
        tmp++;
    }
    return true;
}

// Driver Code

    // Given String str
    let str = "aapaxyayziabcde";

    // Function call
    if (is_linear(str))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(log N)*
T5】辅助空间: *O(1)*