# 最短回文子串

> 原文:[https://www . geesforgeks . org/最短-回文-子串/](https://www.geeksforgeeks.org/shortest-palindromic-substring/)

给定一个字符串，你需要找到该字符串最短的回文子串。如果有多个答案，输出字典上最小的。

**示例:**

```
Input: zyzz
Output:y

Input: abab
Output: a
```

**天真方法:**

*   这种方法类似于寻找最长的回文子串。我们跟踪偶数和奇数长度的子串，并将其存储在一个向量中。
*   之后，我们将对向量进行排序，并打印字典上最小的子串。这可能还包括空的子字符串，但是我们需要忽略它们。

下面是上述方法的实现:

## C++

```
// C++ program to find the shortest
// palindromic substring
#include <bits/stdc++.h>
using namespace std;

// Function return the shortest
// palindromic substring
string ShortestPalindrome(string s)
{
    int n = s.length();

    vector<string> v;

    // One by one consider every character 
    // as center point of even and length
    // palindromes
    for (int i = 0; i < n; i++)
    {
        int l = i;
        int r = i;
        string ans1 = "";
        string ans2 = "";

        // Find the longest odd length palindrome
        // with center point as i
        while (l >= 0 && r < n && s[l] == s[r])
        {
            ans1 += s[l];
            l--;
            r++;
        }
        l = i - 1;
        r = i;

        // Find the even length palindrome 
        // with center points as i-1 and i.
        while (l >= 0 && r < n && s[l] == s[r])
        {
            ans2 += s[l];
            l--;
            r++;
        }
        v.push_back(ans1);
        v.push_back(ans2);
    }
    string ans = v[0];

    // Smallest substring which is
    // not empty
    for (int i = 0; i < v.size(); i++)
    {
        if (v[i] != "")
        {
            ans = min(ans, v[i]);
        }
    }
    return ans;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    cout << ShortestPalindrome(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the shortest
// palindromic substring
import java.util.*;
import java.io.*;

class GFG{

// Function return the shortest
// palindromic substring
public static String ShortestPalindrome(String s)
{
    int n = s.length();
    Vector<String> v = new Vector<String>();

    // One by one consider every character 
    // as center point of even and length
    // palindromes
    for(int i = 0; i < n; i++)
    {
        int l = i;
        int r = i;
        String ans1 = "";
        String ans2 = "";

        // Find the longest odd length palindrome
        // with center point as i    
        while (l >= 0 && r < n &&
          s.charAt(l) == s.charAt(r))
        {
            ans1 += s.charAt(l);
            l--;
            r++;
        }
        l = i - 1;
        r = i;

        // Find the even length palindrome 
        // with center points as i-1 and i.
        while (l >= 0 && r < n &&
          s.charAt(l) == s.charAt(r))
        {
            ans2 += s.charAt(l);
            l--;
            r++;
        }

        v.add(ans1);
        v.add(ans2);
    }

    String ans = v.get(0);

    // Smallest substring which is
    // not empty
    for(int i = 0; i < v.size(); i++)
    {
        if (v.get(i) != "")
        {
            if (ans.charAt(0) >=
                v.get(i).charAt(0))
            {
                ans = v.get(i);
            }
        }
    }
    return ans;
}

// Driver code
public static void main(String []args)
{
    String s = "geeksforgeeks";

    System.out.println(ShortestPalindrome(s));
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to find the shortest
# palindromic substring

# Function return the shortest
# palindromic substring
def ShortestPalindrome(s) :

    n = len(s)

    v = []

    # One by one consider every character
    # as center point of even and length
    # palindromes
    for i in range(n) :

        l = i
        r = i
        ans1 = ""
        ans2 = ""

        # Find the longest odd length palindrome
        # with center point as i
        while ((l >= 0) and (r < n) and (s[l] == s[r])) :

            ans1 += s[l]
            l -= 1
            r += 1

        l = i - 1
        r = i

        # Find the even length palindrome
        # with center points as i-1 and i.
        while ((l >= 0) and (r < n) and (s[l] == s[r])) :

            ans2 += s[l]
            l -= 1
            r += 1

        v.append(ans1)
        v.append(ans2)

    ans = v[0]

    # Smallest substring which is
    # not empty
    for i in range(len(v)) :

        if (v[i] != "") :

            ans = min(ans, v[i])

    return ans

s = "geeksforgeeks"

print(ShortestPalindrome(s))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the shortest
// palindromic substring
using System;
using System.Collections.Generic;
class GFG
{

  // Function return the shortest
  // palindromic substring
  static string ShortestPalindrome(string s)
  {
    int n = s.Length;
    List<string> v = new List<string>();

    // One by one consider every character 
    // as center point of even and length
    // palindromes   
    for(int i = 0; i < n; i++)
    {
      int l = i;
      int r = i;
      string ans1 = "";
      string ans2 = "";

      // Find the longest odd length palindrome
      // with center point as i       
      while(l >= 0 && r < n && s[l] == s[r])
      {
        ans1 += s[l];
        l--;
        r++;
      }
      l = i - 1;
      r = i;

      // Find the even length palindrome 
      // with center points as i-1 and i.
      while(l >= 0 && r < n && s[l] == s[r])
      {
        ans2 += s[l];
        l--;
        r++;
      }
      v.Add(ans1);
      v.Add(ans2);
    }
    string ans = v[0];

    // Smallest substring which is
    // not empty
    for(int i = 0; i < v.Count; i++)
    {
      if(v[i] != "")
      {
        if(ans[0] >= v[i][0])
        {
          ans = v[i];
        }
      }
    }
    return ans;
  }

  // Driver code
  static public void Main ()
  {
    string s = "geeksforgeeks";
    Console.WriteLine(ShortestPalindrome(s));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
    // Javascript program to find the shortest
    // palindromic substring

    // Function return the shortest
    // palindromic substring
    function ShortestPalindrome(s)
    {
      let n = s.length;
      let v = [];

      // One by one consider every character
      // as center point of even and length
      // palindromes  
      for(let i = 0; i < n; i++)
      {
        let l = i;
        let r = i;
        let ans1 = "";
        let ans2 = "";

        // Find the longest odd length palindrome
        // with center point as i      
        while(l >= 0 && r < n && s[l] == s[r])
        {
          ans1 += s[l];
          l--;
          r++;
        }
        l = i - 1;
        r = i;

        // Find the even length palindrome
        // with center points as i-1 and i.
        while(l >= 0 && r < n && s[l] == s[r])
        {
          ans2 += s[l];
          l--;
          r++;
        }
        v.push(ans1);
        v.push(ans2);
      }
      let ans = v[0];

      // Smallest substring which is
      // not empty
      for(let i = 0; i < v.length; i++)
      {
        if(v[i] != "")
        {
          if(ans[0] >= v[i][0])
          {
            ans = v[i];
          }
        }
      }
      return ans;
    }

    let s = "geeksforgeeks";
    document.write(ShortestPalindrome(s));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
e
```

**时间复杂度:** O(N^2)，其中 n 是字符串的长度。

**有效方法:**

*   这里的一个观察是，单个字符也是回文。因此，我们只需要打印字符串中字典序上最小的字符。

下面是上述方法的实现:

## C++

```
// C++ program to find the shortest
// palindromic substring
#include <bits/stdc++.h>
using namespace std;

// Function return the shortest
// palindromic substring
char ShortestPalindrome(string s)
{
    int n = s.length();
    char ans = s[0];

    // Finding the smallest character
    // present in the string
    for(int i = 1; i < n ; i++)
    {
        ans = min(ans, s[i]);
    }

    return ans;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    cout << ShortestPalindrome(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the shortest
// palindromic subString

class GFG{

// Function return the shortest
// palindromic subString
static char ShortestPalindrome(String s)
{
    int n = s.length();
    char ans = s.charAt(0);

    // Finding the smallest character
    // present in the String
    for(int i = 1; i < n; i++)
    {
        ans = (char) Math.min(ans, s.charAt(i));
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    System.out.print(ShortestPalindrome(s));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the shortest
# palindromic substring

# Function return the shortest
# palindromic substring
def ShortestPalindrome(s):

    n = len(s)
    ans = s[0]

    # Finding the smallest character
    # present in the string
    for i in range(1, n):
        ans = min(ans, s[i])

    return ans

# Driver code
s = "geeksforgeeks"

print(ShortestPalindrome(s))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the shortest
// palindromic subString
using System;

class GFG{

// Function return the shortest
// palindromic subString
static char ShortestPalindrome(String s)
{
    int n = s.Length;
    char ans = s[0];

    // Finding the smallest character
    // present in the String
    for(int i = 1; i < n; i++)
    {
        ans = (char) Math.Min(ans, s[i]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String s = "geeksforgeeks";
    Console.Write(ShortestPalindrome(s));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the shortest
// palindromic subString

// Function return the shortest
// palindromic subString
function ShortestPalindrome(s)
{
    let n = s.length;
    let ans = s[0].charCodeAt();

    // Finding the smallest character
    // present in the String
    for(let i = 1; i < n; i++)
    {
        ans = Math.min(ans, s[i].charCodeAt());
    }
    return String.fromCharCode(ans);
}

// Driver code
let s = "geeksforgeeks";
document.write(ShortestPalindrome(s));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
e
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。