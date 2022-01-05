# 检查两个字符串是否有共同的子字符串

> 原文:[https://www . geesforgeks . org/check-two-strings-common-substring/](https://www.geeksforgeeks.org/check-two-strings-common-substring/)

给你两个字符串 str1 和 str2。您必须检查这两个字符串是否共享一个公共子字符串。
**例:**

```
Input : str1 = "HELLO"
        str2 = "WORLD"
Output : YES
Explanation :  The substrings "O" and
"L" are common to both str1 and str2

Input : str1 = "HI"
        str2 = "ALL"
Output : NO
Explanation : Because str1 and str2 
have no common substrings
```

一种**基本方法**在 O(n^2 运行)，我们将字符串 1 的每个字符与字符串 2 的每个字符进行比较，并用“_”替换每个匹配的字符，并将标志变量设置为 true。
一种**高效的方法**在 O(n)工作。我们基本上需要检查是否有共同的特征。我们为字母创建一个大小为 26 的向量，并将它们初始化为 0。对于字符串 1 中的每个字符，我们增加该字符的向量索引，例如:v[s1[i]-'a']++，对于字符串 2 中的每个字符，如果 v[s2[i]-'a'] > 0，我们检查公共字符的向量，然后设置 flag = true 和 v[S2[I]-' a ']–这样字符串 2 中的一个字符只与字符串 1 中的一个字符进行比较。

## C++

```
// CPP program to heck if two strings have
// common substring
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

// function to return true if strings have
// common substring and no if strings have
// no common substring
bool twoStrings(string s1, string s2) {

  // vector for storing character occurrences
  vector<bool> v(MAX_CHAR, 0);

  // increment vector index for every
  // character of str1
  for (int i = 0; i < s1.length(); i++)
    v[s1[i] - 'a'] = true;

  // checking common substring of str2 in str1
  for (int i = 0; i < s2.length(); i++)
    if (v[s2[i] - 'a'])
       return true;

  return false;       
}

// driver program
int main() {
  string str1 = "hello";
  string str2 = "world";
  if (twoStrings(str1, str2))
     cout << "Yes";
  else
     cout << "No";
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two strings have
// common substring
import java.util.Arrays;

class GFG
{
    static int MAX_CHAR = 26;

    // function to return true if strings have
    // common substring and no if strings have
    // no common substring
    static boolean twoStrings(String s1, String s2)
    {
        // vector for storing character occurrences
        boolean v[]=new boolean[MAX_CHAR];
        Arrays.fill(v,false);

        // increment vector index for every
        // character of str1
        for (int i = 0; i < s1.length(); i++)
            v[s1.charAt(i) - 'a'] = true;

        // checking common substring of str2 in str1
        for (int i = 0; i < s2.length(); i++)
            if (v[s2.charAt(i) - 'a'])
            return true;

        return false;    
    }

    // Driver code
    public static void main (String[] args)
    {
        String str1 = "hello";
        String str2 = "world";
        if (twoStrings(str1, str2))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}

// This code is contributed by Anant Agarwal.
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-2">巨蟒 3</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-2" data-code-lang="Python3"></gfg-panel>

```
 # Python 3 program to heck if two 
# strings have common substring
MAX_CHAR = 26

# function to return true if 
# strings have common substring 
# and no if strings have no
# common substring
def twoStrings(s1, s2) :

    # vector for storing character
    # occurrences
    v = [0] * (MAX_CHAR)

    # increment vector index for every
    # character of str1
    for i in range(len(s1)):
        v[ord(s1[i]) - ord('a')] = True

    # checking common substring 
    # of str2 in str1
    for i in range(len(s2)) :
        if (v[ord(s2[i]) - ord('a')]) :
            return True

    return False

# Driver Code
if __name__ == "__main__":
    str1 = "hello"
    str2 = "world"
    if (twoStrings(str1, str2)):
        print("Yes")
    else:
        print("No")

# This code is contributed 
# by ChitraNayal 
```

## C#

```
// C# program to check if two
// strings have common substring
using System;

class GFG
{
    static int MAX_CHAR = 26;

    // function to return true if strings have
    // common substring and no if strings have
    // no common substring
    static bool twoStrings(String s1, String s2)
    {
        // vector for storing character occurrences
        bool []v = new bool[MAX_CHAR];

    // Arrays.fill(v,false);
    for(int i = 0; i < MAX_CHAR; i++)
    v[i]=false;

        // increment vector index for
        // every character of str1
        for (int i = 0; i < s1.Length; i++)
            v[s1[i] - 'a'] = true;

        // checking common substring of str2 in str1
        for (int i = 0; i < s2.Length; i++)
            if (v[s2[i] - 'a'])
            return true;

        return false;    
    }

    // Driver code
    public static void Main ()
    {
        String str1 = "hello";
        String str2 = "world";
        if (twoStrings(str1, str2))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// javascript program to heck if two strings have
// common substring

var MAX_CHAR = 26;

// function to return true if strings have
// common substring and no if strings have
// no common substring
function twoStrings(s1, s2) {

  // vector for storing character occurrences
  var v = Array(MAX_CHAR).fill(0);

  // increment vector index for every
  // character of str1
  for (var i = 0; i < s1.length; i++)
    v[s1[i] - 'a'] = true;

  // checking common substring of str2 in str1
  for (var i = 0; i < s2.length; i++)
    if (v[s2[i] - 'a'])
       return true;

  return false;       
}

// driver program
var str1 = "hello";
var str2 = "world";
if (twoStrings(str1, str2))
   document.write( "Yes");
else
   document.write("No");

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)