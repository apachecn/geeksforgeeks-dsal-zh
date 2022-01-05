# 重新排列字符串，得到最长回文子串

> 原文:[https://www . geeksforgeeks . org/relay-string-to-get-最长回文-substring/](https://www.geeksforgeeks.org/rearrange-string-to-obtain-longest-palindromic-substring/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是重新排列给定的字符串，得到[最长的回文子字符串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:** eegksfskgeeor
> **说明:** eegksfskgee 是重排字符串后最长的回文子串。
> 因此，所需输出为 eegksfskgeeor。
> 
> **输入:** str = "engineering"
> **输出:**eginen igener

**方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决问题。想法是计算给定字符串中每个字符的[频率。如果字符的出现次数超过 1，则在结果字符串的左侧追加其频率的一半(地板值)，在结果字符串的右侧追加剩余的一半。对于剩余的字符，在结果字符串的中间追加一个字符，其余的在结果字符串的开头或结尾追加。按照以下步骤解决问题:](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)

1.  初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，说**哈希【256】**存储每个字符的[频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
2.  要有效地在结果字符串的两侧追加字符，请初始化三个字符串 **res1、** **res2** 和 **res3** 。
3.  字符串 **res1** 存储最长可能回文子串的左半部分， **res2** 存储最长可能回文子串的右半部分， **res3** 存储剩余字符。
4.  [遍历**hash【】**数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于字符，说**hash【I】**，检查其频率是否大于 1。如果发现为真，则在 **res1** 中追加字符**floor(hash[I/2)】**次，在 **res2** 中追加字符**floor(hash[I/2)】**次。
5.  否则，将不满足上述条件的第一个字符追加到 **res1** 中，并将所有剩余的此类字符追加到 **res3** 中。
6.  最后，返回字符串 **res1 + reverse(res2) + res3** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the string to
// get the longest palindromic substring
string longestPalinSub(string str) {

    // Stores the length of str
    int N = str.length();

    // Store the count of occurrence
    // of each character
    int hash[256] = {0};

    // Traverse the string, str
    for(int i = 0; i < N;
    i++) {

        // Count occurrence of
        // each character
        hash[str[i]]++;
    }

    // Store the left half of the
    // longest palindromic substring
    string res1 = "";

    // Store the right half of the
    // longest palindromic substring
    string res2 = "";

    // Traverse the array, hash[]
    for(int i = 0; i< 256; i++) {
        // Append half of the
        // characters  to res1
        for(int j = 0; j < hash[i] / 2;
        j++) {
            res1.push_back(i);
        }

        // Append half of the
        // characters  to res2
        for(int j = (hash[i] + 1)/2;
        j < hash[i]; j++) {
            res2.push_back(i);
        }
    }

    // reverse string res2 to make
    // res1 + res2 palindrome
    reverse(res2.begin(), res2.end());

    // Store the remaining characters
    string res3;

    // Check If any odd character
    // appended to the middle of
    // the resultant string or not
    bool f = false;

    // Append all the character which
    // occurs odd number of times
    for(int i = 0; i < 256; i++) {

        // If count of occurrence
        // of characters is odd
        if(hash[i]%2) {
            if(!f) {
               res1.push_back(i);
               f = true;
            }
            else {
                res3.push_back(i);
            }
        }
    }

    return (res1 + res2 + res3);   
}

// Driver Code
int main() {
    string str = "geeksforgeeks";
    cout<<longestPalinSub(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to rearrange the string to 
// get the longest palindromic substring
static String longestPalinSub(String str)
{

    // Stores the length of str
    int N = str.length();

    // Store the count of occurrence
    // of each character
    int[] hash = new int[256];

    // Traverse the string, str
    for(int i = 0; i < N; i++)
    {

        // Count occurrence of 
        // each character
        hash[str.charAt(i)]++;
    }

    // Store the left half of the 
    // longest palindromic substring
    StringBuilder res1 = new StringBuilder();

    // Store the right half of the 
    // longest palindromic substring
    StringBuilder res2 = new StringBuilder();

    // Traverse the array, hash[]
    for(int i = 0; i < 256; i++)
    {

        // Append half of the 
        // characters  to res1
        for(int j = 0; j < hash[i] / 2; j++)
        {
            res1.append((char)i);
        }

        // Append half of the 
        // characters to res2
        for(int j = (hash[i] + 1) / 2;
                j < hash[i]; j++)
        {
            res2.append((char)i);
        }
    }

    // reverse string res2 to make
    // res1 + res2 palindrome
    StringBuilder tmp = res2.reverse();

    // Store the remaining characters
    StringBuilder res3 = new StringBuilder();

    // Check If any odd character
    // appended to the middle of 
    // the resultant string or not 
    boolean f = false;

    // Append all the character which
    // occurs odd number of times 
    for(int i = 0; i < 256; i++)
    {

        // If count of occurrence 
        // of characters is odd
        if (hash[i] % 2 == 1)
        {
            if (!f)
            {
               res1.append((char)i);
               f = true; 
            }
            else
            {
                res3.append((char)i);
            }
        }
    }

    return (res1.toString() +
             tmp.toString() +
            res3.toString());    
}

// Driver code
public static void main (String[] args)
{
    String str = "geeksforgeeks";

    System.out.println(longestPalinSub(str));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to rearrange the
# string to get the longest
# palindromic substring
def longestPalinSub(st):

    # Stores the length of
    # str
    N = len(st)

    # Store the count of
    # occurrence of each
    # character
    hash1 = [0] * 256

    # Traverse the string,
    # str
    for i in range(N):

        # Count occurrence of
        # each character
        hash1[ord(st[i])] += 1

    # Store the left half of the
    # longest palindromic substring
    res1 = ""

    # Store the right half of the
    # longest palindromic substring
    res2 = ""

    # Traverse the array, hash[]
    for i in range(256):

        # Append half of the
        # characters  to res1
        for j in range(hash1[i] // 2):
            res1 += chr(i)

        # Append half of the
        # characters  to res2
        for j in range((hash1[i] + 1)//2,
                        hash1[i]):
            res2 += chr(i)

    # reverse string res2 to make
    # res1 + res2 palindrome
    p = list(res2)
    p.reverse()
    res2 = ''.join(p)

    # Store the remaining characters
    res3 = ""

    # Check If any odd character
    # appended to the middle of
    # the resultant string or not
    f = False

    # Append all the character which
    # occurs odd number of times
    for i in range(256):

        # If count of occurrence
        # of characters is odd
        if(hash1[i] % 2):
            if(not f):
                res1 += chr(i)
                f = True
            else:
                res3 += chr(i)

    return (res1 + res2 + res3)

# Driver Code
if __name__ == "__main__":

    st = "geeksforgeeks"
    print(longestPalinSub(st))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Text;
class GFG{

// Reverse string
static String reverse(String input)
{
  char[] a = input.ToCharArray();
  int l, r = a.Length - 1;
  for (l = 0; l < r; l++, r--)
  {
    char temp = a[l];
    a[l] = a[r];
    a[r] = temp;
  }
  return String.Join("", a);
}

// Function to rearrange the string to 
// get the longest palindromic substring
static String longestPalinSub(String str)
{
  // Stores the length of str
  int N = str.Length;

  // Store the count of occurrence
  // of each character
  int[] hash = new int[256];

  // Traverse the string, str
  for(int i = 0; i < N; i++)
  {
    // Count occurrence of 
    // each character
    hash[str[i]]++;
  }

  // Store the left half of the 
  // longest palindromic substring
  StringBuilder res1 = new StringBuilder();

  // Store the right half of the 
  // longest palindromic substring
  StringBuilder res2 = new StringBuilder();

  // Traverse the array, hash[]
  for(int i = 0; i < 256; i++)
  {
    // Append half of the 
    // characters  to res1
    for(int j = 0; j < hash[i] / 2; j++)
    {
      res1.Append((char)i);
    }

    // Append half of the 
    // characters to res2
    for(int j = (hash[i] + 1) / 2;
            j < hash[i]; j++)
    {
      res2.Append((char)i);
    }
  }

  // reverse string res2 to make
  // res1 + res2 palindrome
  String tmp = reverse(res2.ToString());

  // Store the remaining characters
  StringBuilder res3 = new StringBuilder();

  // Check If any odd character
  // appended to the middle of 
  // the resultant string or not 
  bool f = false;

  // Append all the character which
  // occurs odd number of times 
  for(int i = 0; i < 256; i++)
  {
    // If count of occurrence 
    // of characters is odd
    if (hash[i] % 2 == 1)
    {
      if (!f)
      {
        res1.Append((char)i);
        f = true; 
      }
      else
      {
        res3.Append((char)i);
      }
    }
  }
  return (res1.ToString() +
          tmp.ToString() +
          res3.ToString());    
}

// Driver code
public static void Main(String[] args)
{
  String str = "geeksforgeeks";
  Console.WriteLine(longestPalinSub(str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to rearrange the string to
// get the longest palindromic substring
function longestPalinSub(str)
{

    // Stores the length of str
    var N = str.length;

    // Store the count of occurrence
    // of each character
    var hash = Array(256).fill(0);

    // Traverse the string, str
    for(var i = 0; i < N; i++)
    {

        // Count occurrence of
        // each character
        hash[str[i].charCodeAt(0)]++;
    }

    // Store the left half of the
    // longest palindromic substring
    var res1 = [];

    // Store the right half of the
    // longest palindromic substring
    var res2 = [];

    // Traverse the array, hash[]
    for(var i = 0; i< 256; i++)
    {

        // Append half of the
        // characters  to res1
        for(var j = 0; j < parseInt(hash[i] / 2); j++)
        {
            res1.push(String.fromCharCode(i));
        }

        // Append half of the
        // characters  to res2
        for(var j = parseInt((hash[i] + 1) / 2);
                j < hash[i]; j++)
        {
            res2.push(String.fromCharCode(i));
        }
    }

    // Reverse string res2 to make
    // res1 + res2 palindrome
    res2 = res2.reverse();

    // Store the remaining characters
    var res3 = [];

    // Check If any odd character
    // appended to the middle of
    // the resultant string or not
    var f = false;

    // Append all the character which
    // occurs odd number of times
    for(var i = 0; i < 256; i++)
    {

        // If count of occurrence
        // of characters is odd
        if (hash[i] % 2)
        {
            if(!f)
            {
                res1.push(String.fromCharCode(i));
                f = true;
            }
            else
            {
                res3.push(String.fromCharCode(i));
            }
        }
    }
    return (res1.join('') +
            res2.join('') +
            res3.join(''));   
}

// Driver Code
var str = "geeksforgeeks";
document.write(longestPalinSub(str));

// This code is contributed by noob2000

</script>
```

**Output**

```
eegksfskgeeor
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)