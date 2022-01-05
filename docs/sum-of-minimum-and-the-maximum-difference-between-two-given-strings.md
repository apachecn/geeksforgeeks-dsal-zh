# 两个给定字符串之间的最小和最大差值之和

> 原文:[https://www . geesforgeks . org/两个给定字符串的最小和最大差值之和/](https://www.geeksforgeeks.org/sum-of-minimum-and-the-maximum-difference-between-two-given-strings/)

给定两根相同长度的弦 **S1** 和 **S2** 。任务是找到两个给定字符串之间的最小和最大差的和，如果允许您用任何其他字符替换字符串中的字符'+'。
**注意:**如果两个字符串在每个索引处都有相同的字符，那么它们之间的差异为零。
**示例:**

> **输入:**S1 =“a+c”，S2 =“++b”
> **输出:** 4
> **说明:**
> 最小差= 1。最小差异:
> 在字符串 S1 =“a+c”中，“+”可以替换为“b”，从而使 S1 =“ABC”
> 在字符串 S2 =“++b”中，“++”可以替换为“ab”，从而使 S2 =“abb”
> 在上面，只有第三个索引具有不同的字符。所以，最小差= 1
> 最大差= 1。最大差异:
> 在字符串 S1 =“a+c”中，可以用“z”替换“+”从而使 S1 =“azc”
> 在字符串 S2 =“++b”中，可以用“bz”替换“++”从而使 S2 =“bzb”
> 以上，所有的索引都有差异字符。所以，最大差值= 3
> 最小差值+最大差值= 1 + 3 = 4
> **输入:**S1 =“+++a”，S2 =“+++a”
> T21】输出: 3
> **解释:**
> 最小差值= 0。对于最小差异:
> 在字符串 S1 =“+++a”中，“+++”可以被“aaa”替换，从而使 S1 =“aaaA”
> 在字符串 S2 =“+++a”中，“++++”可以被“AAA”替换，从而使 S2 =“AAAA”
> 以上，所有的索引都具有相同的字符。所以，最小差= 0
> 最大差= 3。最大差异:
> 在字符串 S1 =“+++a”中，“+++”可以替换为“aaa”，从而使 S1 =“AAAA”
> 在字符串 S2 =“+++a”中，“++++”可以替换为“bbb”，从而使 S2 =“bbba”
> 以上，除了最后一个之外的所有索引都具有差异字符。所以，最大差值= 3
> 最小差值+最大差值= 0 + 3 = 3

**进场:**

1.  **最小差:**为了得到字符串之间的最小差，所有出现的“+”都可以用同一个字符替换。因此，如果在任何位置都有一个“+”，那么这个特定的索引就可以等于另一个字符串。因此，我们只计算字符串和不相同字符中字符不是“+”的索引数。
2.  **最大差异:**为了得到字符串之间的最大差异，所有出现的“+”都可以用不同的字符替换。因此，如果在任何位置都有一个“+”，那么这个特定的索引可以用不同于第二个字符串中的字符替换。因此，我们计算字符串中字符为“+”的索引数和不相同的字符数。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of the
// minimum and the maximum difference
// between two given strings
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the
// minimum and the maximum difference
// between two given strings
void solve(string a, string b)
{
    int l = a.length();

    // Variables to store the minimum
    // difference and the maximum difference
    int min = 0, max = 0;

    // Iterate through the length of the string as
    // both the given strings are of the same length
    for (int i = 0; i < l; i++) {

        // For the maximum difference, we can replace
        // "+" in both the strings with different char
        if (a[i] == '+' || b[i] == '+' || a[i] != b[i])
            max++;

        // For the minimum difference, we can replace
        // "+" in both the strings with the same char
        if (a[i] != '+' && b[i] != '+' && a[i] != b[i])
            min++;
    }

    cout << min + max << endl;
}

// Driver code
int main()
{
    string s1 = "a+c", s2 = "++b";
    solve(s1, s2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// minimum and the maximum difference
// between two given Strings
class GFG{

// Function to find the sum of the
// minimum and the maximum difference
// between two given Strings
static void solve(char []a, char []b)
{
    int l = a.length;

    // Variables to store the minimum
    // difference and the maximum difference
    int min = 0, max = 0;

    // Iterate through the length of the String as
    // both the given Strings are of the same length
    for (int i = 0; i < l; i++) {

        // For the maximum difference, we can replace
        // "+" in both the Strings with different char
        if (a[i] == '+' || b[i] == '+' || a[i] != b[i])
            max++;

        // For the minimum difference, we can replace
        // "+" in both the Strings with the same char
        if (a[i] != '+' && b[i] != '+' && a[i] != b[i])
            min++;
    }

    System.out.print(min + max +"\n");
}

// Driver code
public static void main(String[] args)
{
    String s1 = "a+c", s2 = "++b";
    solve(s1.toCharArray(), s2.toCharArray());
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the sum of the
# minimum and the maximum difference
# between two given strings

# Function to find the sum of the
# minimum and the maximum difference
# between two given strings
def solve(a, b):
    l = len(a)

    # Variables to store the minimum
    # difference and the maximum difference
    min = 0
    max = 0

    # Iterate through the length of the as
    # both the given strings are of the same length
    for i in range(l):

        # For the maximum difference, we can replace
        # "+" in both the strings with different char
        if (a[i] == '+' or b[i] == '+' or a[i] != b[i]):
            max += 1

        # For the minimum difference, we can replace
        # "+" in both the strings with the same char
        if (a[i] != '+' and b[i] != '+' and a[i] != b[i]):
            min += 1

    print(min + max)

# Driver code
if __name__ == '__main__':
    s1 = "a+c"
    s2 = "++b"
    solve(s1, s2)

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to find the sum of the
// minimum and the maximum difference
// between two given Strings
using System;

class GFG{

// Function to find the sum of the
// minimum and the maximum difference
// between two given Strings
static void solve(char []a, char []b)
{
    int l = a.Length;

    // Variables to store the minimum
    // difference and the maximum difference
    int min = 0, max = 0;

    // Iterate through the length of the String as
    // both the given Strings are of the same length
    for (int i = 0; i < l; i++) {

        // For the maximum difference, we can replace
        // "+" in both the Strings with different char
        if (a[i] == '+' || b[i] == '+' || a[i] != b[i])
            max++;

        // For the minimum difference, we can replace
        // "+" in both the Strings with the same char
        if (a[i] != '+' && b[i] != '+' && a[i] != b[i])
            min++;
    }

    Console.Write(min + max +"\n");
}

// Driver code
public static void Main(String[] args)
{
    String s1 = "a+c", s2 = "++b";
    solve(s1.ToCharArray(), s2.ToCharArray());
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the sum of the
// minimum and the maximum difference
// between two given strings

// Function to find the sum of the
// minimum and the maximum difference
// between two given strings
function solve(a, b)
{
    var l = a.length;

    // Variables to store the minimum
    // difference and the maximum difference
    var min = 0, max = 0;

    // Iterate through the length of the string as
    // both the given strings are of the same length
    for (var i = 0; i < l; i++) {

        // For the maximum difference, we can replace
        // "+" in both the strings with different char
        if (a[i] == '+' || b[i] == '+' || a[i] != b[i])
            max++;

        // For the minimum difference, we can replace
        // "+" in both the strings with the same char
        if (a[i] != '+' && b[i] != '+' && a[i] != b[i])
            min++;
    }

    document.write(min + max);
}

// Driver code
var s1 = "a+c", s2 = "++b";
solve(s1, s2);

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)