# 非平凡波动数

> 原文:[https://www.geeksforgeeks.org/nontrivial-undulant-numbers/](https://www.geeksforgeeks.org/nontrivial-undulant-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否为非平凡波动数。

> 非平凡波动数是以 10 为基数大于 100 的数，其形式为 aba，abab，亚的斯亚贝巴，…，其中 a！= b。

**示例:**

> **输入:** N = 121
> **输出:**是
> **说明:**
> 121 为 aba 形式
> 
> **输入:**N = 123
> T3】输出:否

**方法:**思路是把数字转换成字符串。如果字符串的长度是偶数，那么我们将检查字符串的前半部分是否等于后半部分。如果长度是奇数，我们将在字符串的最后添加字符串的第二个字符，使其长度为偶数。最后，检查字符串的前半部分是否等于后半部分。

下面是上述方法的实现:

## C++

```
// C++ implementation to check if N
// is a Nontrivial undulant number

#include<bits/stdc++.h>
using namespace std;

// Function to check if a string
// is double string or not
bool isDouble(int num)
{
    string s = to_string(num);
    int l = s.length();

    // a and b should not be equal
    if(s[0] == s[1])
       return false;

    // Condition to check
    // if length is odd
    // make length even
    if(l % 2 == 1)
    {
        s = s + s[1];
        l++;
    }

    // first half of s
    string s1 = s.substr(0, l/2);
    // second half of s
    string s2 = s.substr(l/2);

    // Double string if first
    // and last half are equal
    return s1 == s2;
}

// Function to check if N is an
// Nontrivial undulant number
bool isNontrivialUndulant(int N)
{   
    return N > 100 && isDouble(N);
}

// Driver Code
int main()
{
    int n = 121;
    if (isNontrivialUndulant(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if N
// is a Nontrivial undulant number
class GFG{

// Function to check if a string
// is double string or not
static boolean isDouble(int num)
{
    String s = Integer.toString(num);
    int l = s.length();

    // a and b should not be equal
    if(s.charAt(0) == s.charAt(1))
       return false;

    // Condition to check if length
    // is odd make length even
    if(l % 2 == 1)
    {
        s = s + s.charAt(1);
        l++;
    }

    // First half of s
    String s1 = s.substring(0, l / 2);

    // Second half of s
    String s2 = s.substring(l / 2);

    // Double string if first
    // and last half are equal
    return s1.equals(s2);
}

// Function to check if N is an
// Nontrivial undulant number
static boolean isNontrivialUndulant(int N)
{
    return N > 100 && isDouble(N);
}

// Driver code
public static void main(String[] args)
{
    int n = 121;

    if (isNontrivialUndulant(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation to check if N
# is a Nontrivial undulant number

# Function to check if a string
# is double string or not
def isDouble(num):

    s = str(num)
    l = len(s)

    # a and b should not be equal
    if(s[0] == s[1]):
        return False

    # Condition to check
    # if length is odd
    # make length even
    if(l % 2 == 1):

        s = s + s[1]
        l += 1

    # First half of s
    s1 = s[:l // 2]

    # Second half of s
    s2 = s[l // 2:]

    # Double string if first
    # and last half are equal
    return s1 == s2

# Function to check if N is an
# Nontrivial undulant number
def isNontrivialUndulant(N):

    return N > 100 and isDouble(N)

# Driver Code
n = 121

if (isNontrivialUndulant(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by vishu2908
```

## C#

```
// C# implementation to check if N
// is a Nontrivial undulant number
using System;
class GFG{

// Function to check if a string
// is double string or not
static bool isDouble(int num)
{
    String s = num.ToString();
    int l = s.Length;

    // a and b should not be equal
    if(s[0] == s[1])
       return false;

    // Condition to check if length
    // is odd make length even
    if(l % 2 == 1)
    {
        s = s + s[1];
        l++;
    }

    // First half of s
    String s1 = s.Substring(0, l / 2);

    // Second half of s
    String s2 = s.Substring(l / 2);

    // Double string if first
    // and last half are equal
    return s1.Equals(s2);
}

// Function to check if N is an
// Nontrivial undulant number
static bool isNontrivialUndulant(int N)
{
    return N > 100 && isDouble(N);
}

// Driver code
public static void Main(String[] args)
{
    int n = 121;

    if (isNontrivialUndulant(n))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript implementation to check if N
// is a Nontrivial undulant number

// Function to check if a string
// is double string or not
function isDouble(num)
{
    let s = num.toString();
    let l = s.length;

    // a and b should not be equal
    if (s[0] == s.charAt[1])
       return false;

    // Condition to check if length
    // is odd make length even
    if (l % 2 == 1)
    {
        s = s + s[1];
        l++;
    }

    // First half of s
    let s1 = s.substr(0, l / 2);

    // Second half of s
    let s2 = s.substr(l / 2);

    // Double string if first
    // and last half are equal
    return (s1 == s2);
}

// Function to check if N is an
// Nontrivial undulant number
function isNontrivialUndulant(N)
{
    return N > 100 && isDouble(N);
}

// Driver Code
let n = 121;

if (isNontrivialUndulant(n))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(|N|)

**参考文献:**[OEIS](http://oeis.org/A046075)T4】