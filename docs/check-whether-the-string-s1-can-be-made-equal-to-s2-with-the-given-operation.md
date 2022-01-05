# 用给定的操作

检查弦 S1 是否可以等于 S2

> 原文:[https://www . geesforgeks . org/check-string-S1-是否可以用给定的操作使-等于-S2/](https://www.geeksforgeeks.org/check-whether-the-string-s1-can-be-made-equal-to-s2-with-the-given-operation/)

给定两根弦 **S1** 和 **S2** ，任务是通过对弦 **S1** 执行给定的操作来检查两根弦是否可以相等。在一次操作中，奇数索引处的任何字符都可以与奇数索引处的任何其他字符交换，偶数索引处的字符也是如此。
**举例:**

> **输入:**S1 =“ABCD”，S2 =“cbad”
> **输出:**是
> 在 S1 交换‘a’和‘c’，结果
> 字符串等于 S2。
> **输入:**S1 =“ABCD”，S2 =“abcdcd”
> **输出:**否

**进场:**

*   根据来自 **S1** 的偶数索引处的字符创建一个字符串**偶数 _s1** 。
*   同样，生成字符串**偶数 _s2** 、**奇数 _s1** 和**奇数 _s2** 。
*   对前面步骤中的所有四个字符串进行排序。
*   如果**偶数 _s1 =偶数 _s2** 和**奇数 _s1 =奇数 _s2** 则打印**是**。
*   否则打印**否**，因为字符串不能相等。

以下是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the string formed
// by the odd indexed characters of s
string partOdd(string s)
{
    string st = "";
    for(int i = 0; i < s.length(); i++)
    {
        if (i % 2 != 0)
        st += s[i];
    }
    return st;
}

// Function to return the string formed
// by the even indexed characters of s
string partEven(string str)
{
    string s = "";
    for(int i = 0; i < str.length(); i++)
    {
        if (i % 2 == 0)
        s += str[i];
    }
    return s;
}

// Function that returns true if s1
// can be made equal to s2
// with the given operation
bool canBeMadeEqual(string s1, string s2)
{

    // Get the string formed by the
    // even indexed characters of s1
    string even_s1 = partEven(s1);

    // Get the string formed by the
    // even indexed characters of s2
    string even_s2 = partEven(s2);

    // Get the string formed by the
    // odd indexed characters of s1
    string odd_s1 = partOdd(s1);

    // Get the string formed by the
    // odd indexed characters of s2
    string odd_s2 = partOdd(s2);

    // Sorting all the lists
    sort(even_s1.begin(), even_s1.end());
    sort(even_s2.begin(), even_s2.end());
    sort(odd_s1.begin(), odd_s1.end());
    sort(odd_s2.begin(), odd_s2.end());

    // If the strings can be made equal
    if (even_s1 == even_s2 and odd_s1 == odd_s2)
        return true;

    return false;
}

// Driver code
int main()
{
    string s1 = "cdab";
    string s2 = "abcd";
    if(canBeMadeEqual(s1, s2))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the string formed
    // by the odd indexed characters of s
    static String partOdd(String s)
    {
        String st = "";
        for (int i = 0; i < s.length(); i++)
        {
            if (i % 2 != 0)
                st += s.charAt(i);
        }

        return st;
    }

    // Function to return the string formed
    // by the even indexed characters of s
    static String partEven(String str)
    {
        String s = "";
        for (int i = 0; i < str.length(); i++)
        {
            if (i % 2 == 0)
                s += str.charAt(i);
        }
        return s;
    }

    // Function that returns true if s1
    // can be made equal to s2
    // with the given operation
    static boolean canBeMadeEqual(String s1,
                                  String s2)
    {

        // Get the string formed by the
        // even indexed characters of s1
        char[] even1 = partEven(s1).toCharArray();

        // Get the string formed by the
        // even indexed characters of s2
        char[] even2 = partEven(s2).toCharArray();

        // Get the string formed by the
        // odd indexed characters of s1
        char[] odd1 = partOdd(s1).toCharArray();

        // Get the string formed by the
        // odd indexed characters of s2
        char[] odd2 = partOdd(s2).toCharArray();

        // Sorting all the lists
        Arrays.sort(even1);
        Arrays.sort(even2);
        Arrays.sort(odd1);
        Arrays.sort(odd2);

        String even_s1 = new String(even1);
        String even_s2 = new String(even2);
        String odd_s1 = new String(odd1);
        String odd_s2 = new String(odd2);

        // If the strings can be made equal
        if (even_s1.equals(even_s2) &&
             odd_s1.equals(odd_s2))
            return true;
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s1 = "cdab";
        String s2 = "abcd";

        if (canBeMadeEqual(s1, s2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the string formed
# by the odd indexed characters of s
def partOdd(s):
    odd = []
    for i in range(len(s)):
        if i % 2 != 0:
            odd.append(s[i])
    return odd

# Function to return the string formed
# by the even indexed characters of s
def partEven(s):
    even = []
    for i in range(len(s)):
        if i % 2 == 0:
            even.append(s[i])
    return even

# Function that returns true if s1
# can be made equal to s2
# with the given operation
def canBeMadeEqual(s1, s2):

    # Get the string formed by the
    # even indexed characters of s1
    even_s1 = partEven(s1)

    # Get the string formed by the
    # even indexed characters of s2
    even_s2 = partEven(s2)

    # Get the string formed by the
    # odd indexed characters of s1
    odd_s1 = partOdd(s1)

    # Get the string formed by the
    # odd indexed characters of s2
    odd_s2 = partOdd(s2)

    # Sorting all the lists
    even_s1.sort()
    even_s2.sort()
    odd_s1.sort()
    odd_s2.sort()

    # If the strings can be made equal
    if even_s1 == even_s2 and odd_s1 == odd_s2:
        return True

    return False

# Driver code
s1 = "cdab"
s2 = "abcd"
if canBeMadeEqual(s1, s2):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the string formed
    // by the odd indexed characters of s
    static string partOdd(string s)
    {
        string st = "";
        for (int i = 0; i < s.Length; i++)
        {
            if (i % 2 != 0)
                st += s[i];
        }

        return st;
    }

    // Function to return the string formed
    // by the even indexed characters of s
    static string partEven(string str)
    {
        string s = "";
        for (int i = 0; i < str.Length; i++)
        {
            if (i % 2 == 0)
                s += str[i];
        }
        return s;
    }

    // Function that returns true if s1
    // can be made equal to s2
    // with the given operation
    static bool canBeMadeEqual(string s1,
                                string s2)
    {

        // Get the string formed by the
        // even indexed characters of s1
        char[] even1 = partEven(s1).ToCharArray();

        // Get the string formed by the
        // even indexed characters of s2
        char[] even2 = partEven(s2).ToCharArray();

        // Get the string formed by the
        // odd indexed characters of s1
        char[] odd1 = partOdd(s1).ToCharArray();

        // Get the string formed by the
        // odd indexed characters of s2
        char[] odd2 = partOdd(s2).ToCharArray();

        // Sorting all the lists
        Array.Sort(even1);
        Array.Sort(even2);
        Array.Sort(odd1);
        Array.Sort(odd2);

        string even_s1 = new string(even1);
        string even_s2 = new string(even2);
        string odd_s1 = new string(odd1);
        string odd_s2 = new string(odd2);

        // If the strings can be made equal
        if (even_s1.Equals(even_s2) &&
            odd_s1.Equals(odd_s2))
            return true;
        return false;
    }

    // Driver Code
    public static void Main()
    {
        string s1 = "cdab";
        string s2 = "abcd";

        if (canBeMadeEqual(s1, s2))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach

      // Function to return the string formed
      // by the odd indexed characters of s
      function partOdd(s) {
        var st = "";
        for (var i = 0; i < s.length; i++) {
          if (i % 2 !== 0) st += s[i];
        }

        return st;
      }

      // Function to return the string formed
      // by the even indexed characters of s
      function partEven(str) {
        var s = "";
        for (var i = 0; i < str.length; i++) {
          if (i % 2 === 0) s += str[i];
        }
        return s;
      }

      // Function that returns true if s1
      // can be made equal to s2
      // with the given operation
      function canBeMadeEqual(s1, s2) {
        // Get the string formed by the
        // even indexed characters of s1
        var even1 = partEven(s1).split("");

        // Get the string formed by the
        // even indexed characters of s2
        var even2 = partEven(s2).split("");

        // Get the string formed by the
        // odd indexed characters of s1
        var odd1 = partOdd(s1).split("");

        // Get the string formed by the
        // odd indexed characters of s2
        var odd2 = partOdd(s2).split("");

        // Sorting all the lists
        even1.sort();
        even2.sort();
        odd1.sort();
        odd2.sort();

        var even_s1 = even1.join("");
        var even_s2 = even2.join("");
        var odd_s1 = odd1.join("");
        var odd_s2 = odd2.join("");

        // If the strings can be made equal
        if (even_s1 === even_s2 && odd_s1 === odd_s2) return true;
        return false;
      }

      // Driver Code
      var s1 = "cdab";
      var s2 = "abcd";

      if (canBeMadeEqual(s1, s2)) document.write("Yes");
      else document.write("No");

 </script>
```

**Output:** 

```
Yes
```