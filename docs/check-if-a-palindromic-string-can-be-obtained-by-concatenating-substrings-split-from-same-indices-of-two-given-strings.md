# 检查是否可以通过连接从两个给定字符串的相同索引中分离出来的子字符串来获得回文字符串

> 原文:[https://www . geesforgeks . org/check-if-a-回文字符串-可通过串联-子字符串-从两个给定字符串的相同索引中拆分获得/](https://www.geeksforgeeks.org/check-if-a-palindromic-string-can-be-obtained-by-concatenating-substrings-split-from-same-indices-of-two-given-strings/)

给定两个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **A** 和 **B** ，任务是检查两个字符串中是否有任何一个是通过在任意索引**I**(0≤I≤N–1)处拆分两个字符串并将**A【0，I】**和**B【I，N–1】**或**A【I，N–1】**和**B【I，N–1】连接而形成的如果发现是真的，打印**“是”**。否则，打印**“否”**。**

**示例:**

> **输入:**A =“x”，B =“y”
> **输出:**是
> **解释:**
> 让字符串在索引 0 处拆分，然后
> 从索引 0 处拆分 A:“+”x“A[0，0] =”和 A[1，1]=“x”。
> 从索引 0 拆分 B:“+”y“B[0，0] =”和 B[1，1]=“y”。
> A[0，0]和 B[1，1]的串联为=“y”，是回文串。
> 
> **输入:** A = "xbdef "，B = " xecab "
> T3】输出:否

**方法:**思路是使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)和[在范围**【0，N–1】**内遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，检查子串**A【0，I–1】**和**B【I，N–1】**的连接是否为子串**A【I，N–1】**和**B【0，I–1】**的连接如果发现任何连接是回文，则打印**“是”**否则打印**“否”**。****

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is palindrome or not
bool isPalindrome(string str)
{
  // Start and end of the
  // string
  int i = 0, j = str.size() - 1;

  // Iterate the string
  // until i > j
  while (i < j)
  {
    // If there is a mismatch
    if (str[i] != str[j])
      return false;

    // Increment first pointer
    // and decrement the other
    i++;
    j--;
  }

  // Given string is a
  // palindrome
  return true;
}

// Function two check if
// the strings can be
// combined to form a palindrome
void formPalindrome(string a,
                    string b, int n)
{
  // Initialize array of
  // characters
  char aa[n + 2];
  char bb[n + 2];
  for (int i = 0; i < n + 2; i++)
  {
    aa[i] = ' ';
    bb[i] = ' ';
  }
  // Stores character of string
  // in the character array
  for (int i = 1; i <= n; i++)
  {
    aa[i] = a[i - 1];
    bb[i] = b[i - 1];
  }

  bool ok = false;

  for (int i = 0; i <= n + 1; i++)
  {
    // Find left and right parts
    // of strings a and b
    string la = "";
    string ra = "";
    string lb = "";
    string rb = "";

    for (int j = 1; j <= i - 1; j++)
    {
      // Substring a[j...i-1]
      if (aa[j] == ' ')
        la += "";
      else
        la += aa[j];

      // Substring b[j...i-1]
      if (bb[j] == ' ')
        lb += "";
      else
        lb += bb[j];
    }

    for (int j = i; j <= n + 1; j++)
    {
      // Substring a[i...n]
      if (aa[j] == ' ')
        ra += "";
      else
        ra += aa[j];

      // Substring b[i...n]
      if (bb[j] == ' ')
        rb += "";
      else
        rb += bb[j];
    }

    // Check is left part of a +
    // right part of b or vice
    // versa is a palindrome
    if (isPalindrome(la + rb) ||
        isPalindrome(lb + ra))
    {
      ok = true;
      break;
    }
  }

  // Print the result
  if (ok)
    cout << ("Yes");

  // Otherwise
  else
    cout << ("No");
}

// Driver Code
int main()
{
  string A = "bdea";
  string B = "abbb";
  int N = 4;
  formPalindrome(A, B, N);
}

// This code is contributed by gauravrajput1
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to check if a string
    // is palindrome or not
    static boolean isPalindrome(String str)
    {

        // Start and end of the string
        int i = 0, j = str.length() - 1;

        // Iterate the string until i > j
        while (i < j) {

            // If there is a mismatch
            if (str.charAt(i)
                != str.charAt(j))
                return false;

            // Increment first pointer and
            // decrement the other
            i++;
            j--;
        }

        // Given string is a palindrome
        return true;
    }

    // Function two check if the strings can
    // be combined to form a palindrome
    static void formPalindrome(
        String a, String b, int n)
    {
        // Initialize array of characters
        char aa[] = new char[n + 2];
        char bb[] = new char[n + 2];

        Arrays.fill(aa, ' ');
        Arrays.fill(bb, ' ');

        // Stores character of string
        // in the character array
        for (int i = 1; i <= n; i++) {
            aa[i] = a.charAt(i - 1);
            bb[i] = b.charAt(i - 1);
        }

        boolean ok = false;

        for (int i = 0; i <= n + 1; i++) {

            // Find left and right parts
            // of strings a and b
            StringBuilder la
                = new StringBuilder();
            StringBuilder ra
                = new StringBuilder();
            StringBuilder lb
                = new StringBuilder();
            StringBuilder rb
                = new StringBuilder();

            for (int j = 1;
                 j <= i - 1; j++) {

                // Substring a[j...i-1]
                la.append((aa[j] == ' ')
                              ? ""
                              : aa[j]);

                // Substring b[j...i-1]
                lb.append((bb[j] == ' ')
                              ? ""
                              : bb[j]);
            }

            for (int j = i;
                 j <= n + 1; j++) {

                // Substring a[i...n]
                ra.append((aa[j] == ' ')
                              ? ""
                              : aa[j]);

                // Substring b[i...n]
                rb.append((bb[j] == ' ')
                              ? ""
                              : bb[j]);
            }

            // Check is left part of a +
            // right part of b or vice
            // versa is a palindrome
            if (isPalindrome(la.toString()
                             + rb.toString())
                || isPalindrome(lb.toString()
                                + ra.toString())) {
                ok = true;
                break;
            }
        }

        // Print the result
        if (ok)
            System.out.println("Yes");

        // Otherwise
        else
            System.out.println("No");
    }

    // Driver Code
    public static void main(String[] args)
    {
        String A = "bdea";
        String B = "abbb";

        int N = 4;

        formPalindrome(A, B, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check if
# a string is palindrome
# or not
def isPalindrome(st):

    # Start and end of
    # the string
    i = 0
    j = len(st) - 1

    # Iterate the string
    # until i > j
    while (i < j):

        # If there is a mismatch
        if (st[i] != st[j]):
            return False

        # Increment first pointer
        # and decrement the other
        i += 1
        j -= 1

    # Given string is a
    # palindrome
    return True

# Function two check if
# the strings can be
# combined to form a
# palindrome
def formPalindrome(a, b, n):

    # Initialize array of
    # characters
    aa = [' '] * (n + 2)
    bb = [' '] * (n + 2)

    # Stores character of string
    # in the character array
    for i in range(1, n + 1):
        aa[i] = a[i - 1]
        bb[i] = b[i - 1]

    ok = False

    for i in range(n + 2):

        # Find left and right parts
        # of strings a and b
        la = ""
        ra = ""
        lb = ""
        rb = ""

        for j in range(1, i):

            # Substring a[j...i-1]
            if (aa[j] == ' '):
                la += ""
            else:
                la += aa[j]

            # Substring b[j...i-1]
            if (bb[j] == ' '):
                lb += ""
            else:
                lb += bb[j]

        for j in range(i, n + 2):

            # Substring a[i...n]
            if (aa[j] == ' '):
                ra += ""
            else:
                ra += aa[j]

            # Substring b[i...n]
            if (bb[j] == ' '):
                rb += ""
            else:
                rb += bb[j]

        # Check is left part of a +
        # right part of b or vice
        # versa is a palindrome
        if (isPalindrome(str(la) +
                         str(rb))
            or isPalindrome(str(lb) +
                            str(ra))):
            ok = True
            break

    # Print the result
    if (ok):
        print("Yes")

    # Otherwise
    else:
        print("No")

# Driver Code
if __name__ == "__main__":

    A = "bdea"
    B = "abbb"
    N = 4
    formPalindrome(A, B, N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the
// above approach
using System;
using System.Text;
class GFG{

// Function to check if a string
// is palindrome or not
static bool isPalindrome(String str)
{
  // Start and end of the string
  int i = 0, j = str.Length - 1;

  // Iterate the string
  // until i > j
  while (i < j)
  {
    // If there is a mismatch
    if (str[i] != str[j])
      return false;

    // Increment first pointer
    // and decrement the other
    i++;
    j--;
  }

  // Given string is
  // a palindrome
  return true;
}

// Function two check if the strings can
// be combined to form a palindrome
static void formPalindrome(String a,
                           String b, int n)
{
  // Initialize array of
  // characters
  char []aa = new char[n + 2];
  char []bb = new char[n + 2];

  for(int i = 0; i < n + 2; i++)
  {
    aa[i] = ' ';
    bb[i] = ' ';
  }

  // Stores character of string
  // in the character array
  for (int i = 1; i <= n; i++)
  {
    aa[i] = a[i-1];
    bb[i] = b[i-1];
  }

  bool ok = false;

  for (int i = 0;
           i <= n + 1; i++)
  {
    // Find left and right parts
    // of strings a and b
    StringBuilder la =
          new StringBuilder();
    StringBuilder ra =
          new StringBuilder();
    StringBuilder lb =
          new StringBuilder();
    StringBuilder rb =
          new StringBuilder();

    for (int j = 1;
             j <= i - 1; j++)
    {
      // Substring a[j...i-1]
      la.Append((aa[j] == ' ') ?
                ' ' : aa[j]);

      // Substring b[j...i-1]
      lb.Append((bb[j] == ' ') ?
                ' ' : bb[j]);
    }

    for (int j = i;
             j <= n + 1; j++)
    {
      // Substring a[i...n]
      ra.Append((aa[j] == ' ') ?
                ' ' : aa[j]);

      // Substring b[i...n]
      rb.Append((bb[j] == ' ') ?
                ' ' : bb[j]);
    }

    // Check is left part of a +
    // right part of b or vice
    // versa is a palindrome
    if (isPalindrome(la.ToString() +
                     rb.ToString()) ||
        isPalindrome(lb.ToString() +
                     ra.ToString()))
    {
      ok = true;
      break;
    }
  }

  // Print the result
  if (!ok)
    Console.WriteLine("Yes");

  // Otherwise
  else
    Console.WriteLine("No");
}

// Driver Code
public static void Main(String[] args)
{
  String A = "bdea";
  String B = "abbb";
  int N = 4;
  formPalindrome(A, B, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to check if a string
// is palindrome or not
function isPalindrome(str)
{

  // Start and end of the
  // string
  var i = 0, j = str.length - 1;

  // Iterate the string
  // until i > j
  while (i < j)
  {

    // If there is a mismatch
    if (str[i] != str[j])
      return false;

    // Increment first pointer
    // and decrement the other
    i++;
    j--;
  }

  // Given string is a
  // palindrome
  return true;
}

// Function two check if
// the strings can be
// combined to form a palindrome
function formPalindrome( a, b, n)
{

  // Initialize array of
  // characters
  var aa= new Array(n + 2);
  var bb=new Array(n + 2);
  for (var i = 0; i < n + 2; i++)
  {
    aa[i] = ' ';
    bb[i] = ' ';
  }

  // Stores character of string
  // in the character array
  for (var i = 1; i <= n; i++)
  {
    aa[i] = a[i - 1];
    bb[i] = b[i - 1];
  }

  var ok = Boolean(false);

  for (var i = 0; i <= n + 1; i++)
  {

    // Find left and right parts
    // of strings a and b
    var la = "";
    var ra = "";
    var lb = "";
    var rb = "";

    for (var j = 1; j <= i - 1; j++)
    {

      // Substring a[j...i-1]
      if (aa[j] == ' ')
        la += "";
      else
        la += aa[j];

      // Substring b[j...i-1]
      if (bb[j] == ' ')
        lb += "";
      else
        lb += bb[j];
    }

    for (var j = i; j <= n + 1; j++)
    {

      // Substring a[i...n]
      if (aa[j] == ' ')
        ra += "";
      else
        ra += aa[j];

      // Substring b[i...n]
      if (bb[j] == ' ')
        rb += "";
      else
        rb += bb[j];
    }

    // Check is left part of a +
    // right part of b or vice
    // versa is a palindrome
    if (isPalindrome(la + rb) || isPalindrome(lb + ra))
    {
      ok = true;
      break;
    }
  }

  // Print the result
  if (ok)
    document.write ("Yes");

  // Otherwise
  else
    document.write ("No");
}
  var A = "bdea";
  var B = "abbb";
  var N = 4;
  formPalindrome(A, B, N);

// This code is contributed by SoumikMondal
</script>
```

**Output**

```
Yes
```

***时间复杂度:** O(N <sup>2</sup> )其中 N 是给定字符串的长度。*
***辅助空间:** O(N)*

**替代 Python 方法(两个指针+切片):**

这种方法遵循以下路径:

1.  定义功能检查
2.  分别在 0，n-1 位置取两个指针 I，j
3.  如果 a 的第一个字符和 b 的第二个字符不匹配，我们就中断(因为我们在搜索回文)
4.  如果匹配，我们只需增加指针
5.  我们将连接第一个字符串的形式 a[i:j+1]和第二个字符串的形式 b[i:j+1]，并检查回文的条件
6.  如果是，我们返回真

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

string rev(string str)
{
  int st = 0;
  int ed = str.length() - 1;
  string s = str;

  while(st < ed)
  {
    swap(s[st],
         s[ed]);
    st++;
    ed--;
  }
  return s;
}

bool check(string a,
           string b, int n)
{
  int i = 0;
  int j = n - 1;

  // iterate through the
  // length if we could
  // find a[i]==b[j] we could
  // increment I and decrement j
  while(i < n)
  {
    if(a[i] != b[j])
      break;

    // else we could just break
    // the loop as its not a
    // palindrome type sequence
    i += 1;
    j -= 1;

    // we could concatenate the
    // a's left part +b's right
    // part in a variable a and
    // a's right part+b's left
    // in the variable b
    string xa = a.substr(i, j + 1 - i);
    string xb = b.substr(i, j + 1 - i);

    // we would check for the
    // palindrome condition if
    // yes we print True else False
    if((xa == rev(xa)) or
       (xb == rev(xb)))
      return true;
  }
  return false;
}

// Driver code
int main()
{
  string a = "xbdef";
  string b = "cabex";
  if (check(a, b,
            a.length()) == true or
      check(b, a,
            a.length()) == true)
    cout << "True";
  else
    cout << "False";
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.io.*;

class GFG{

public static String rev(String str)
{
    int st = 0;
    int ed = str.length() - 1;
    char[] s = str.toCharArray();

    while(st < ed)
    {
        char temp = s[st];
        s[st] = s[ed];
        s[ed] = temp;
        st++;
        ed--;
    }
    return (s.toString());
}

public static boolean check(String a,
                            String b, int n)
{
    int i = 0;
    int j = n - 1;

    // Iterate through the
    // length if we could
    // find a[i]==b[j] we could
    // increment I and decrement j
    while(i < n)
    {
        if (a.charAt(i) != b.charAt(j))
            break;

        // Else we could just break
        // the loop as its not a
        // palindrome type sequence
        i += 1;
        j -= 1;

        // We could concatenate the
        // a's left part +b's right
        // part in a variable a and
        // a's right part+b's left
        // in the variable b
        String xa = a.substring(i, j + 1);
        String xb = b.substring(i, j + 1);

        // We would check for the
        // palindrome condition if
        // yes we print True else False
        StringBuffer XA = new StringBuffer(xa);
        XA.reverse();
        StringBuffer XB = new StringBuffer(xb);
        XB.reverse();

        if (xa == XA.toString() ||
            xb == XB.toString())
        {
            return true;
        }
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{
    String a = "xbdef";
    String b = "cabex";

    if (check(a, b, a.length()) ||
        check(b, a, a.length()))
        System.out.println("True");
    else
        System.out.println("False");
}
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
def check(a, b, n):
    i, j = 0, n - 1

    # iterate through the length if
    # we could find a[i]==b[j] we could
    # increment I and decrement j
    while(i < n):
        if(a[i] != b[j]):

            # else we could just break
            # the loop as its not a palindrome
            # type sequence
            break 

        i += 1
        j -= 1

        # we could concatenate the a's left part
        # +b's right part in a variable a and  a's
        # right part+b's left in the variable b
        xa = a[i:j+1]
        xb = b[i:j+1]

        # we would check for the palindrome condition
        # if yes we print True else False
        if(xa == xa[::-1] or xb == xb[::-1]):
            return True

a = "xbdef"
b = "cabex"
if check(a, b, len(a)) == True or check(b, a, len(a)) == True:
    print(True)
else:
    print(False)

# CODE CONTRIBUTED BY SAIKUMAR KUDIKALA
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG {

    static string rev(string str)
    {
      int st = 0;
      int ed = str.Length - 1;
      char[] s = str.ToCharArray();

      while(st < ed)
      {
        char temp = s[st];
        s[st] = s[ed];
        s[ed] = temp;
        st++;
        ed--;
      }
      return new string(s);
    }

    static bool check(string a,
               string b, int n)
    {
      int i = 0;
      int j = n - 1;

      // iterate through the
      // length if we could
      // find a[i]==b[j] we could
      // increment I and decrement j
      while(i < n)
      {
        if(a[i] != b[j])
          break;

        // else we could just break
        // the loop as its not a
        // palindrome type sequence
        i += 1;
        j -= 1;

        // we could concatenate the
        // a's left part +b's right
        // part in a variable a and
        // a's right part+b's left
        // in the variable b
        string xa = a.Substring(i, j + 1 - i);
        string xb = b.Substring(i, j + 1 - i);

        // we would check for the
        // palindrome condition if
        // yes we print True else False
        char[] XA = xa.ToCharArray();
        Array.Reverse(XA);
        char[] XB = xb.ToCharArray();
        Array.Reverse(XB);

        if(string.Compare(xa, new string(XA)) == 0 ||
           string.Compare(xb, new string(XB)) == 0)
          return true;
      }
      return false;
    }

  // Driver code
  static void Main()
  {
      string a = "xbdef";
      string b = "cabex";
      if (check(a, b, a.Length) || check(b, a, a.Length))
        Console.WriteLine("True");
      else
        Console.WriteLine("False");
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach
      function rev(str) {
        var st = 0;
        var ed = str.length - 1;
        var s = str.split("");

        while (st < ed) {
          var temp = s[st];
          s[st] = s[ed];
          s[ed] = temp;
          st++;
          ed--;
        }
        return s.join();
      }

      function check(a, b, n) {
        var i = 0;
        var j = n - 1;

        // iterate through the
        // length if we could
        // find a[i]==b[j] we could
        // increment I and decrement j
        while (i < n) {
          if (a[i] !== b[j]) break;

          // else we could just break
          // the loop as its not a
          // palindrome type sequence
          i += 1;
          j -= 1;

          // we could concatenate the
          // a's left part +b's right
          // part in a variable a and
          // a's right part+b's left
          // in the variable b
          var xa = a.substring(i, j + 1 - i);
          var xb = b.substring(i, j + 1 - i);

          // we would check for the
          // palindrome condition if
          // yes we print True else False
          var XA = xa.split("");
          XA.sort().reverse();
          var XB = xb.split("");
          XB.sort().reverse();

          if (xa === XA.join("") || xb === XB.join("")) return true;
        }
        return false;
      }

      // Driver code
      var a = "xbdef";
      var b = "cabex";
      if (check(a, b, a.length) || check(b, a, a.length))
        document.write("True");
      else document.write("False");

</script>
```

**输出:**

```
False
```