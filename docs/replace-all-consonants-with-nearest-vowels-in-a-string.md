# 用字符串中最接近的元音替换所有辅音

> 原文:[https://www . geesforgeks . org/将所有辅音替换为字符串中最近的元音/](https://www.geeksforgeeks.org/replace-all-consonants-with-nearest-vowels-in-a-string/)

给定一个包含小写英文字母的字符串。任务是用最近的元音替换字符串中的所有辅音。如果一个辅音靠近两个元音，那么就用英语字母表中第一个辅音替换它。
**注**:字符串中已经存在的元音必须保持原样。
T4【示例】T5:

```
Input : str = "geeksforgeeks"
Output : eeeiueooeeeiu

Input : str = "gfg"
Output : eee
```

一种**简单的方法**是将辅音和元音进行比较，以确定最近的元音。首先，检查辅音是否落在两个元音之间。如果它落在两个元音之间，那么找出辅音的 ASCII 值和两个元音的 ASCII 值之间的绝对差异。
换成那个元音，绝对差别最小。
但是如果辅音的 ASCII 码不在两个元音之间，那么辅音可以是‘v’、‘w’、‘x’、‘y’、‘z’。因此，在这种情况下，答案是“u”。
以下是上述方法的实施:

## C++

```
// C++ program to replace all consonants
// with nearest vowels in a string
#include <bits/stdc++.h>
using namespace std;

// Function to check if a character is
// vowel or not
bool isVowel(char ch)
{
    if (ch != 'a' && ch != 'e' && ch != 'i'
        && ch != 'o' && ch != 'u')
        return false;

    return true;
}

// Function to replace consonant with
// nearest vowels
string replacingConsonants(string s)
{
    for (int i = 0; i < s.length(); i++) {

        // if, string element is vowel,
        // jump to next element
        if (isVowel(s[i]))
            continue;

        // check if consonant lies between two vowels,
        // if it lies, than replace it with nearest vowel
        else {

            if (s[i] > 'a' && s[i] < 'e') {

                // here the absolute difference of
                // ascii value is considered
                if (abs(s[i] - 'a') > abs(s[i] - 'e'))
                    s[i] = 'e';
                else
                    s[i] = 'a';
            }
            else if (s[i] > 'e' && s[i] < 'i') {
                if (abs(s[i] - 'e') > abs(s[i] - 'i'))
                    s[i] = 'i';
                else
                    s[i] = 'e';
            }
            else if (s[i] > 'i' && s[i] < 'o') {
                if (abs(s[i] - 'i') > abs(s[i] - 'o'))
                    s[i] = 'o';
                else
                    s[i] = 'i';
            }
            else if (s[i] > 'o' && s[i] < 'u') {
                if (abs(s[i] - 'o') > abs(s[i] - 'u'))
                    s[i] = 'u';
                else
                    s[i] = 'o';
            }

            // when s[i] is equal to either
            // 'v', 'w', 'x', 'y', 'z'
            else if (s[i] > 'u')
                s[i] = 'u';
        }
    }

    return s;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    cout << replacingConsonants(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace all consonants
// with nearest vowels in a string

import java.util.*;
class Solution{

// Function to check if a character is
// vowel or not
static boolean isVowel(char ch)
{
    if (ch != 'a' && ch != 'e' && ch != 'i'
        && ch != 'o' && ch != 'u')
        return false;

    return true;
}

// Function to replace consonant with
// nearest vowels
static String replacingConsonants(String s)
{
    for (int i = 0; i < s.length(); i++) {

        // if, string element is vowel,
        // jump to next element
        if (isVowel(s.charAt(i)))
            continue;

        // check if consonant lies between two vowels,
        // if it lies, than replace it with nearest vowel
        else {

            if (s.charAt(i) > 'a' && s.charAt(i) < 'e') {

                // here the bsolute difference of
                // ascii value is considered
                if (Math.abs(s.charAt(i) - 'a') > Math.abs(s.charAt(i) - 'e'))
                    s = s.substring(0,i)+'e'+s.substring(i+1);
                else
                    s=  s.substring(0,i)+'a'+s.substring(i+1);
            }
            else if (s.charAt(i) > 'e' && s.charAt(i) < 'i') {
                if (Math.abs(s.charAt(i) - 'e') > Math.abs(s.charAt(i) - 'i'))
                    s =  s.substring(0,i)+'i'+s.substring(i+1);
                else
                    s =  s.substring(0,i)+'e'+s.substring(i+1);
            }
            else if (s.charAt(i) > 'i' && s.charAt(i) < 'o') {
                if (Math.abs(s.charAt(i) - 'i') > Math.abs(s.charAt(i) - 'o'))
                    s= s.substring(0,i)+'o'+s.substring(i+1);
                    else
                    s= s.substring(0,i)+'i'+s.substring(i+1);
                }
            else if (s.charAt(i) > 'o' && s.charAt(i) < 'u') {
                if (Math.abs(s.charAt(i) - 'o') > Math.abs(s.charAt(i) - 'u'))
                    s= s.substring(0,i)+'u'+s.substring(i+1);
                else
                    s= s.substring(0,i)+'o'+s.substring(i+1);
            }

            // when s.charAt(i) is equal to either
            // 'v', 'w', 'x', 'y', 'z'
            else if (s.charAt(i) > 'u')
                s =s.substring(0,i)+'u'+s.substring(i+1);
        }
    }

    return s;
}

// Driver code
public static void main(String args[])
{
    String s = "geeksforgeeks";

    System.out.print( replacingConsonants(s));

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to replace all consonants
# with nearest vowels in a string

# Function to check if a
# character is vowel or not
def isVowel(ch):

    if (ch != 'a' and ch != 'e' and ch != 'i'
        and ch != 'o' and ch != 'u'):
        return False

    return True

# Function to replace consonant
# with nearest vowels
def replacingConsonants(s):

    for i in range(0, len(s)): 

        # if, string element is vowel,
        # jump to next element
        if isVowel(s[i]):
            continue

        # check if consonant lies between two vowels,
        # if it lies, than replace it with nearest vowel
        else: 

            if s[i] > 'a' and s[i] < 'e': 

                # here the absolute difference of
                # ascii value is considered
                if (abs(ord(s[i]) - ord('a')) > abs(ord(s[i]) - ord('e'))):
                    s[i] = 'e'
                else:
                    s[i] = 'a'

            elif s[i] > 'e' and s[i] < 'i': 
                if (abs(ord(s[i]) - ord('e')) > abs(ord(s[i]) - ord('i'))):
                    s[i] = 'i'
                else:
                    s[i] = 'e'

            elif (s[i] > 'i' and s[i] < 'o'): 
                if (abs(ord(s[i]) - ord('i')) > abs(ord(s[i]) - ord('o'))):
                    s[i] = 'o'
                else:
                    s[i] = 'i'

            elif (s[i] > 'o' and s[i] < 'u'): 
                if (abs(ord(s[i]) - ord('o')) > abs(ord(s[i]) - ord('u'))):
                    s[i] = 'u'
                else:
                    s[i] = 'o'

            # when s[i] is equal to either
            # 'v', 'w', 'x', 'y', 'z'
            elif (s[i] > 'u'):
                s[i] = 'u'

    return ''.join(s)

# Driver code
if __name__ == "__main__":

    s = "geeksforgeeks"
    print(replacingConsonants(list(s)))

# This code is contributed by Rituraj Jain
```

## C#

```

// C# program to replace all consonants
// with nearest vowels in a string
using System;
public class Solution{

    // Function to check if a character is
    // vowel or not
    static bool isVowel(char ch)
    {
        if (ch != 'a' && ch != 'e' && ch != 'i'
            && ch != 'o' && ch != 'u')
            return false;

        return true;
    }

    // Function to replace consonant with
    // nearest vowels
    static String replacingConsonants(String s)
    {
        for (int i = 0; i < s.Length; i++) {

            // if, string element is vowel,
            // jump to next element
            if (isVowel(s[i]))
                continue;

            // check if consonant lies between two vowels,
            // if it lies, than replace it with nearest vowel
            else {

                if (s[i] > 'a' && s[i] < 'e') {

                    // here the bsolute difference of
                    // ascii value is considered
                    if (Math.Abs(s[i] - 'a') > Math.Abs(s[i] - 'e'))
                        s = s.Substring(0,i)+'e'+s.Substring(i+1);
                    else
                        s=  s.Substring(0,i)+'a'+s.Substring(i+1);
                }
                else if (s[i] > 'e' && s[i] < 'i') {
                    if (Math.Abs(s[i] - 'e') > Math.Abs(s[i] - 'i'))
                        s =  s.Substring(0,i)+'i'+s.Substring(i+1);
                    else
                        s =  s.Substring(0,i)+'e'+s.Substring(i+1);
                }
                else if (s[i] > 'i' && s[i] < 'o') {
                    if (Math.Abs(s[i] - 'i') > Math.Abs(s[i] - 'o'))
                        s= s.Substring(0,i)+'o'+s.Substring(i+1);
                        else
                        s= s.Substring(0,i)+'i'+s.Substring(i+1);
                    }
                else if (s[i] > 'o' && s[i] < 'u') {
                    if (Math.Abs(s[i] - 'o') > Math.Abs(s[i] - 'u'))
                        s= s.Substring(0,i)+'u'+s.Substring(i+1);
                    else
                        s= s.Substring(0,i)+'o'+s.Substring(i+1);
                }

                // when s[i] is equal to either
                // 'v', 'w', 'x', 'y', 'z'
                else if (s[i] > 'u')
                    s =s.Substring(0,i)+'u'+s.Substring(i+1);
            }
        }

        return s;
    }

    // Driver code
    public static void Main()
    {
        String s = "geeksforgeeks";

        Console.WriteLine( replacingConsonants(s));

    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript program to replace all consonants
      // with nearest vowels in a string
      // Function to check if a character is
      // vowel or not
      function isVowel(ch) {
        if (ch !== "a" && ch !== "e" && ch !== "i" && ch !== "o" && ch !== "u")
          return false;

        return true;
      }

      // Function to replace consonant with
      // nearest vowels
      function replacingConsonants(s) {
        for (var i = 0; i < s.length; i++) {
          // if, string element is vowel,
          // jump to next element
          if (isVowel(s[i])) continue;
          // check if consonant lies between two vowels,
          // if it lies, than replace it with nearest vowel
          else {
            if (s[i] > "a" && s[i] < "e") {
              // here the bsolute difference of
              // ascii value is considered
              if (
                Math.abs(s[i].charCodeAt(0) - "a".charCodeAt(0)) >
                Math.abs(s[i].charCodeAt(0) - "e".charCodeAt(0))
              )
                s = s.substring(0, i) + "e" + s.substring(i + 1);
              else s = s.substring(0, i) + "a" + s.substring(i + 1);
            } else if (s[i] > "e" && s[i] < "i") {
              if (
                Math.abs(s[i].charCodeAt(0) - "e".charCodeAt(0)) >
                Math.abs(s[i].charCodeAt(0) - "i".charCodeAt(0))
              )
                s = s.substring(0, i) + "i" + s.substring(i + 1);
              else s = s.substring(0, i) + "e" + s.substring(i + 1);
            } else if (s[i] > "i" && s[i] < "o") {
              if (
                Math.abs(s[i].charCodeAt(0) - "i".charCodeAt(0)) >
                Math.abs(s[i].charCodeAt(0) - "o".charCodeAt(0))
              )
                s = s.substring(0, i) + "o" + s.substring(i + 1);
              else s = s.substring(0, i) + "i" + s.substring(i + 1);
            } else if (s[i] > "o" && s[i] < "u") {
              if (
                Math.abs(s[i].charCodeAt(0) - "o".charCodeAt(0)) >
                Math.abs(s[i].charCodeAt(0) - "u".charCodeAt(0))
              )
                s = s.substring(0, i) + "u" + s.substring(i + 1);
              else s = s.substring(0, i) + "o" + s.substring(i + 1);
            }

            // when s[i] is equal to either
            // 'v', 'w', 'x', 'y', 'z'
            else if (s[i] > "u")
              s = s.substring(0, i) + "u" + s.substring(i + 1);
          }
        }

        return s;
      }

      // Driver code

      var s = "geeksforgeeks";
      document.write(replacingConsonants(s));
    </script>
```

**Output:** 

```
eeeiueooeeeiu
```

更好的方法是制作一个大小为 26 的数组，为每个字符存储最近的元音。

## C++

```
// C++ program to replace all consonants
// with nearest vowels in a string
#include <bits/stdc++.h>
using namespace std;

// Function to replace consonant with
// nearest vowels
string replacingConsonants(string s)
{
    char nVowel[] = "aaaeeeeiiiiioooooouuuuuuuu";
    for (int i = 0; i < s.length(); i++)
        s[i] = nVowel[s[i] - 'a'];
    return s;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    cout << replacingConsonants(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace all consonants
// with nearest vowels in a string
import java.util.*;

class solution
{

// Function to replace consonant with
// nearest vowels
static String replacingConsonants(String s)
{

      String str = "aaaeeeeiiiiioooooouuuuuuuu";
      char[] st = s.toCharArray();
    for (int i = 0; i < s.length(); i++)
    {
       int index = st[i]-'a';
       st[i] = str.charAt(index);
    }
    String str1 = new String(st);
    return str1;
}

// Driver code
public static void main(String arr[])
{
    String s = "geeksforgeeks";

    System.out.println(replacingConsonants(s));

}

}
// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to replace all consonants
# with nearest vowels in a string

# Function to replace consonant with
# nearest vowels
def replacingConsonants(s):

    nVowel = "aaaeeeeiiiiioooooouuuuuuuu"

    for i in range (0, len(s)):
        s = s.replace(s[i], nVowel[ord(s[i]) - 97])

    return s

# Driver code
s = "geeksforgeeks";

print(replacingConsonants(s));

# This code is contributed by
# archana_kumari.
```

## C#

```

// C# program to replace all consonants
// with nearest vowels in a string
using System;

public class solution{

    // Function to replace consonant with
    // nearest vowels
    static String replacingConsonants(String s)
    {

          String str = "aaaeeeeiiiiioooooouuuuuuuu";
          char[] st = s.ToCharArray();
        for (int i = 0; i < s.Length; i++)
        {
           int index = st[i]-'a';
           st[i] = str[index];
        }
        String str1 = new String(st);
        return str1;
    }

    // Driver code
    public static void Main()
    {
        String s = "geeksforgeeks";

        Console.WriteLine(replacingConsonants(s));

    }

}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to replace all consonants
// with nearest vowels in a string

// Function to replace consonant with
// nearest vowels
function replacingConsonants(s)
{
    var nVowel = "aaaeeeeiiiiioooooouuuuuuuu";
    for (var i = 0; i < s.length; i++)
        s[i] = nVowel[s[i].charCodeAt(0) - 'a'.charCodeAt(0)];
    return s.join('');
}

// Driver code
var s = "geeksforgeeks".split('');
document.write( replacingConsonants(s));

</script>
```

**Output:** 

```
eeeiueooeeeiu
```