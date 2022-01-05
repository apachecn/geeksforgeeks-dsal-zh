# 找到由数字串组成的数组的 GCD

> 原文:[https://www . geesforgeks . org/find-the-gcd-of-array-由数字字符串组成/](https://www.geeksforgeeks.org/find-the-gcd-of-an-array-made-up-of-numeric-strings/)

给定一个由数字字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算给定数组的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。

> 考虑到字符串**‘A’**和**‘B’**，“ **B 分 A** ”当且仅当 **A** 不止一次是 **B** 的串联。找出将 **A** 和 **B** 分开的最大字符串。

**示例:**

> **输入:**arr[]= {“GFGGFG”、“GFGGFG”}
> **输出:**“GFGGFG”
> **说明:**
> “GFGGFG”是分割整个数组元素的最大字符串。
> 
> **输入:** arr = {“极客”、“GFG”}
> T3】输出:

**方法:**按照以下步骤解决问题:

*   计算给定数组所有字符串长度的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) ，比如 **GCD** 。
*   检查给定数组的所有字符串是否都可以通过连接子字符串**{ arr[0][0]}来组成，..，arr[0][GCD–1]}**任意次或不任意次。如果发现是真的，那么打印 **{arr[0][0]，..，arr[0][GCD–1]}**。
*   否则，打印一个空字符串。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function
// to return gcd of A and B
int GCD(int lena, int lenb)
{

  if (lena == 0)
    return lenb;

  if (lenb == 0)
    return lena;

  // Base case
  if (lena == lenb)
    return lena;

  // Length of A is greater
  if (lena > lenb)
    return GCD(lena - lenb, lenb);

  return GCD(lena, lenb - lena);
}

// Calculate GCD
string StringGCD(string a, string b)
{

  // Store the GCD of the
  // length of the strings
  int gcd = GCD(a.size(), b.size());
  if (a.substr(0, gcd) == b.substr(0, gcd))
  {
    int x = ((int)b.size()/gcd);
    int y = ((int)a.size()/gcd);
    string r="",s="";

    while (x--) s += a;
    while (y--) r += b;

    if (s == r)
      return a.substr(0, gcd);
  }
  return "-1";
}

// Driver Code
int main()
{
  string a = "geeksgeeks";
  string b = "geeks";

  // Function call
  cout<<(StringGCD(a, b));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program for the above approach
import java.util.*;
class GFG
{

// Recursive function
// to return gcd of A and B
static int GCD(int lena, int lenb)
{
  if (lena == 0)
    return lenb;
  if (lenb == 0)
    return lena;

  // Base case
  if (lena == lenb)
    return lena;

  // Length of A is greater
  if (lena > lenb)
    return GCD(lena - lenb, lenb);
  return GCD(lena, lenb - lena);
}

// Calculate GCD
static String StringGCD(String a, String b)
{

  // Store the GCD of the
  // length of the Strings
  int gcd = GCD(a.length(), b.length());
  if (a.substring(0, gcd).equals(b.substring(0, gcd)))
  {
    int x = ((int)b.length()/gcd);
    int y = ((int)a.length()/gcd);
    String r="",s="";

    while (x-- >0) s += a;
    while (y-- >0) r += b;

    if (s.equals(r))
      return a.substring(0, gcd);
  }
  return "-1";
}

// Driver Code
public static void main(String[] args)
{
  String a = "geeksgeeks";
  String b = "geeks";

  // Function call
  System.out.print(StringGCD(a, b));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Recursive function
# to return gcd of A and B
def GCD(lena, lenb):   

  if (lena == 0):
    return lenb

  if (lenb == 0):
    return lena

  # Base case
  if (lena == lenb):
    return lena

  # Length of A is greater
  if (lena > lenb):
    return GCD(lena-lenb, lenb)
  return GCD(lena, lenb-lena)

# Calculate GCD
def StringGCD(a, b):

  # Store the GCD of the
  # length of the strings
  gcd = GCD(len(a), len(b))
  if a[:gcd] == b[:gcd]:

    if a*(len(b)//gcd) == b*(len(a)//gcd):
      return a[:gcd]

  return -1

# Driver Code
a = 'geeksgeeks'
b = 'geeks'

# Function call
print(StringGCD(a, b))
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Recursive function
// to return gcd of A and B
static int GCD(int lena, int lenb)
{
  if (lena == 0)
    return lenb;
  if (lenb == 0)
    return lena;

  // Base case
  if (lena == lenb)
    return lena;

  // Length of A is greater
  if (lena > lenb)
    return GCD(lena - lenb, lenb);
  return GCD(lena, lenb - lena);
}

// Calculate GCD
static String StringGCD(String a, String b)
{

  // Store the GCD of the
  // length of the Strings
  int gcd = GCD(a.Length, b.Length);
  if (a.Substring(0, gcd).Equals(b.Substring(0, gcd)))
  {
    int x = ((int)b.Length/gcd);
    int y = ((int)a.Length/gcd);
    String r="", s="";

    while (x-- >0) s += a;
    while (y-- >0) r += b;
    if (s.Equals(r))
      return a.Substring(0, gcd);
  }
  return "-1";
}

// Driver Code
public static void Main(String[] args)
{
  String a = "geeksgeeks";
  String b = "geeks";

  // Function call
  Console.Write(StringGCD(a, b));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JAVASCRIPT program for the above approach

// Recursive function
// to return gcd of A and B
function GCD(lena,lenb)
{
    if (lena == 0)
        return lenb;
      if (lenb == 0)
        return lena;

      // Base case
      if (lena == lenb)
        return lena;

      // Length of A is greater
      if (lena > lenb)
        return GCD(lena - lenb, lenb);
      return GCD(lena, lenb - lena);
}

// Calculate GCD
function StringGCD(a,b)
{
    // Store the GCD of the
      // length of the Strings
      let gcd = GCD(a.length, b.length);
      if (a.substring(0, gcd) == (b.substring(0, gcd)))
      {
        let x = Math.floor(b.length/gcd);
        let y = Math.floor(a.length/gcd);
        let r="",s="";

        while (x-- >0)
            s += a;
        while (y-- >0)
            r += b;

        if (s == (r))
              return a.substring(0, gcd);
      }
      return "-1";
}

// Driver Code
let a = "geeksgeeks";
let b = "geeks";

// Function call
document.write(StringGCD(a, b));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
geeks
```

***时间复杂度:** O(N * M)，其中 M 为弦的长度*
***辅助** **空间:** O(1)*