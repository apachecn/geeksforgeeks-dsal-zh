# 检查两个字符串是否包含相同顺序的相同字符

> 原文:[https://www . geesforgeks . org/check-two-string-是否包含相同顺序的相同字符/](https://www.geeksforgeeks.org/check-whether-two-strings-contain-same-characters-in-same-order/)

给定两个字符串 **s1** 和 **s2** ，任务是找出这两个字符串是否包含以相同顺序出现的相同字符。例如:字符串**“极客”**和字符串**“Geks”**包含相同顺序的相同字符。

**示例:**

> **输入:** s1 =“极客”，S2 =“Geks”
> T3】输出:是
> 
> **输入:**S1 =“Arnab”，S2 =“Andrew”
> T3】输出:否

**方法:**我们有两个字符串，现在我们必须检查字符串是否包含相同顺序的相同字符。因此，我们将用单个元素替换连续的相似元素，即如果我们有**“eee”**，我们将用单个**“e”**替换它。现在我们将检查两个字符串是否相等。如果相等，则打印**是**否则**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

string getString(char x)
{
    // string class has a constructor
    // that allows us to specify size of
    // string as first parameter and character
    // to be filled in given size as second
    // parameter.
    string s(1, x);

    return s;
}

// Function that returns true if
// the given strings contain same
// characters in same order
bool solve(string s1, string s2)
{
    // Get the first character of both strings
    string a = getString(s1[0]), b = getString(s2[0]);

    // Now if there are adjacent similar character
    // remove that character from s1
    for (int i = 1; i < s1.length(); i++)
        if (s1[i] != s1[i - 1]) {
            a += getString(s1[i]);
        }

    // Now if there are adjacent similar character
    // remove that character from s2
    for (int i = 1; i < s2.length(); i++)
        if (s2[i] != s2[i - 1]) {
            b += getString(s2[i]);
        }

    // If both the strings are equal
    // then return true
    if (a == b)
        return true;

    return false;
}

// Driver code
int main()
{
    string s1 = "Geeks", s2 = "Geks";

    if (solve(s1, s2))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class temp
{
static String getString(char x)
{

    // String class has a constructor
    // that allows us to specify size of
    // String as first parameter and character
    // to be filled in given size as second
    // parameter.
    String s = String.valueOf(x);
    return s;
}

// Function that returns true if
// the given Strings contain same
// characters in same order
static boolean solve(String s1, String s2)
{
    // Get the first character of both Strings
    String a = getString(s1.charAt(0)),
           b = getString(s2.charAt(0));

    // Now if there are adjacent similar character
    // remove that character from s1
    for (int i = 1; i < s1.length(); i++)
        if (s1.charAt(i) != s1.charAt(i - 1))
        {
            a += getString(s1.charAt(i));
        }

    // Now if there are adjacent similar character
    // remove that character from s2
    for (int i = 1; i < s2.length(); i++)
        if (s2.charAt(i) != s2.charAt(i - 1))
        {
            b += getString(s2.charAt(i));
        }

    // If both the Strings are equal
    // then return true
    if (a.equals(b))
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    String s1 = "Geeks", s2 = "Geks";

    if (solve(s1, s2))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by ankush_953
```

## 蟒蛇 3

```
# Python3 implementation of the approach

def getString(x):

    # string class has a constructor
    # that allows us to specify the size of
    # string as first parameter and character
    # to be filled in given size as the second
    # parameter.
    return x

# Function that returns true if
# the given strings contain same
# characters in same order
def solve(s1, s2):

    # Get the first character of both strings
    a = getString(s1[0])
    b = getString(s2[0])

    # Now if there are adjacent similar character
    # remove that character from s1
    for i in range(1, len(s1)):
        if s1[i] != s1[i - 1]:
            a += getString(s1[i])

    # Now if there are adjacent similar character
    # remove that character from s2
    for i in range(1, len(s2)):
        if s2[i] != s2[i - 1]:
            b += getString(s2[i])

    # If both the strings are equal
    # then return true
    if a == b:
        return True
    return False

# Driver code
s1 = "Geeks"
s2 = "Geks"
if solve(s1, s2):
    print("Yes")
else:
    print("No")

# This code is contributed by ankush_953
```

## C#

```
// C# implementation of the approach
using System;

public class temp
{

static String getString(char x)
{

    // String class has a constructor
    // that allows us to specify size of
    // String as first parameter and character
    // to be filled in given size as second
    // parameter.
    String s = String.Join("",x);
    return s;
}

// Function that returns true if
// the given Strings contain same
// characters in same order
static Boolean solve(String s1, String s2)
{
    // Get the first character of both Strings
    String a = getString(s1[0]),
        b = getString(s2[0]);

    // Now if there are adjacent similar character
    // remove that character from s1
    for (int i = 1; i < s1.Length; i++)
        if (s1[i] != s1[i - 1]) {
            a += getString(s1[i]);
        }

    // Now if there are adjacent similar character
    // remove that character from s2
    for (int i = 1; i < s2.Length; i++)
        if (s2[i] != s2[i - 1]) {
            b += getString(s2[i]);
        }

    // If both the strings are equal
    // then return true
    if (a == b)
        return true;

    return false;
}

// Driver code
public static void Main(String[] args)
{
    String s1 = "Geeks", s2 = "Geks";

    if (solve(s1, s2))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function getString(x)
{
    // string class has a constructor
    // that allows us to specify size of
    // string as first parameter and character
    // to be filled in given size as second
    // parameter.
    return x
}

// Function that returns true if
// the given strings contain same
// characters in same order
function solve(s1, s2)
{
    // Get the first character of both strings
    var a = getString(s1[0]), b = getString(s2[0]);

    // Now if there are adjacent similar character
    // remove that character from s1
    for (var i = 1; i < s1.length; i++)
        if (s1[i] != s1[i - 1]) {
            a += getString(s1[i]);
        }

    // Now if there are adjacent similar character
    // remove that character from s2
    for (var i = 1; i < s2.length; i++)
        if (s2[i] != s2[i - 1]) {
            b += getString(s2[i]);
        }

    // If both the strings are equal
    // then return true
    if (a == b)
        return true;

    return false;
}

// Driver code
var s1 = "Geeks", s2 = "Geks";
if (solve(s1, s2))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Yes
```

**使用递归**

## C++

```
#include <iostream>

using namespace std;
bool checkSequence(string a, string b)
{
      // if length of the b = 0
      // then we return true
      if(b.size() == 0)
        return true;

      // if length of a = 0
      // that means b is not present in
      // a so we return false
    if(a.size() == 0)
        return false;

    if(a[0] == b[0])
        return checkSequence(a.substr(1), b.substr(1));
    else
        return checkSequence(a.substr(1), b);
}

int main()
{
    string s1 = "Geeks", s2 = "Geks";

    if (checkSequence(s1, s2))
        cout << "Yes";
    else
        cout << "No";
}

// This code is contributed by SoumikMondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
      public static boolean checkSequence(String a, String b) {
          //if length of the b = 0
          //then we return true
          if(b.length()==0)
            return true;

          //if length of a = 0
          //that means b is not present in
          //a so we return false
        if(a.length() == 0)
            return false;

        if(a.charAt(0) == b.charAt(0))
            return checkSequence(a.substring(1), b.substring(1));
        else
            return checkSequence(a.substring(1), b);
    }
    public static void main(String[] args)
    {
        String s1 = "Geeks", s2 = "Geks";

        if (checkSequence(s1, s2))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
```

## 计算机编程语言

```
# Python3 implementation of approach
def checkSequence(a,  b):

    # if length of the b = 0
    # then we return true
    if len(b) == 0:
        return True

    # if length of a = 0
    # that means b is not present in
    # a so we return false
    if len(a) == 0:
        return False

    if(a[0] == b[0]):
        return checkSequence(a[1:], b[1:])
    else:
        return checkSequence(a[1:], b)

if __name__ == '__main__':
    s1 = "Geeks"
    s2 = "Geks"

    if (checkSequence(s1, s2)):
        print("Yes")
    else:
        print("No")

# This code is contributed by nirajgusain5
```

## C#

```
// C# implementation of the approach
using System;

public class temp
{
public static bool checkSequence(String a, String b)
{

          // if length of the b = 0
          // then we return true
          if(b.Length == 0)
            return true;

          // if length of a = 0
          // that means b is not present in
          // a so we return false
        if(a.Length == 0)
            return false;

        if(a[0] == b[0])
            return checkSequence(a.Substring(1), b.Substring(1));
        else
            return checkSequence(a.Substring(1), b);
    }

// Driver code
public static void Main(String[] args)
{
    String s1 = "Geeks", s2 = "Geks";

    if (checkSequence(s1, s2))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

function checkSequence(a, b)
{

    // If length of the b = 0
    // then we return true
    if (b.length == 0)
        return true;

    // If length of a = 0
    // that means b is not present in
    // a so we return false
    if (a.length == 0)
        return false;

    if (a[0] == b[0])
        return checkSequence(a.substring(1),
                             b.substring(1));
    else
        return checkSequence(a.substring(1), b);
}

// Driver code
let s1 = "Geeks", s2 = "Geks";

if (checkSequence(s1, s2))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by mukesh07

</script>
```

**输出:**

```
Yes
```