# 子串以元音开始，以辅音结束，反之亦然

> 原文:[https://www . geesforgeks . org/substrings-start-元音-end-辅音-反之亦然/](https://www.geeksforgeeks.org/substrings-starting-vowel-ending-consonants-vice-versa/)

给定一个字符串 s，计算其中的特殊子字符串。如果满足以下任一属性，则称子串是特殊的。

*   它以元音开头，以辅音结尾。
*   它以辅音开头，以元音结尾。

**示例:**

```
Input : S = "aba"
Output : 2
Substrings of S are : a, ab, aba, b, ba, a 
Out of these only 'ab' and 'ba' satisfy the
condition for special Substring. So the 
answer is 2.

Input : S = "adceba"
Output : 9
```

一个**简单的解决方案**是[生成所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)。对于每个子串，检查特殊串的条件。如果是，增加计数。
一个**高效的解决方案**是统计字符串每个后缀中的元音和辅音。数完这些之后，我们从头开始遍历字符串。对于每一个辅音，我们在它后面加上元音数作为结果。同样，对于每一个元音，我们在其后加一些辅音。

## C++

```
// CPP program to count special strings
#include <bits/stdc++.h>
using namespace std;

// Returns true if ch is vowel
bool isVowel(char ch)
{
    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// function to check consonant
bool isCons(char ch)
{
    return (ch != 'a' && ch != 'e' &&
            ch != 'i' && ch != 'o' &&
            ch != 'u');
}

int countSpecial(string &str)
{
    int len = str.length();

      //in case of empty string, we can't fullfill the
      //required condition, hence we return ans as 0.
      if(len == 0)
      return 0;

    // co[i] is going to store counts
    // of consonants from str[len-1]
    // to str[i].
    // vo[i] is going to store counts
    // of vowels from str[len-1]
    // to str[i].
    int co[len + 1];
    int vo[len + 1];
    memset(co, 0, sizeof(co));
    memset(vo, 0, sizeof(vo));

    // Counting consonants and vowels
    // from end of string.
    if (isCons(str[len - 1]) == 1)
        co[len-1] = 1;
    else
        vo[len-1] = 1;
    for (int i = len-2; i >= 0; i--)
    {
        if (isCons(str[i]) == 1)
        {
            co[i] = co[i + 1] + 1;
            vo[i] = vo[i + 1];
        }
        else
        {
            co[i] = co[i + 1];
            vo[i] = vo[i + 1] + 1;
        }
    }

    // Now we traverse string from beginning
    long long ans = 0;
    for (int i = 0; i < len; i++)
    {
        // If vowel, then count of substrings
        // starting with str[i] is equal to
        // count of consonants after it.
        if (isVowel(str[i]))
           ans = ans + co[i + 1];

        // If consonant, then count of
        // substrings starting with str[i]
        // is equal to count of vowels
        // after it.
        else
           ans = ans + vo[i + 1];
    }

    return ans;
}

// driver program
int main()
{
    string str = "adceba";
    cout << countSpecial(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count special strings
class GfG
{

// Returns true if ch is vowel
static boolean isVowel(char ch)
{
    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// function to check consonant
static boolean isCons(char ch)
{
    return (ch != 'a' && ch != 'e' &&
            ch != 'i' && ch != 'o' &&
            ch != 'u');
}

static int countSpecial(char []str)
{
    int len = str.length;

      //in case of empty string, we can't fullfill the
      //required condition, hence we return ans as 0.
      if(len == 0)
          return 0;

    // co[i] is going to store counts
    // of consonants from str[len-1]
    // to str[i].
    // vo[i] is going to store counts
    // of vowels from str[len-1]
    // to str[i].
    int co[] = new int[len + 1];
    int vo[] = new int[len + 1];

    // Counting consonants and vowels
    // from end of string.
    if (isCons(str[len - 1]) == true)
        co[len-1] = 1;
    else
        vo[len-1] = 1;
    for (int i = len-2; i >= 0; i--)
    {
        if (isCons(str[i]) == true)
        {
            co[i] = co[i + 1] + 1;
            vo[i] = vo[i + 1];
        }
        else
        {
            co[i] = co[i + 1];
            vo[i] = vo[i + 1] + 1;
        }
    }

    // Now we traverse string from beginning
    long ans = 0;
    for (int i = 0; i < len; i++)
    {
        // If vowel, then count of substrings
        // starting with str[i] is equal to
        // count of consonants after it.
        if (isVowel(str[i]))
        ans = ans + co[i + 1];

        // If consonant, then count of
        // substrings starting with str[i]
        // is equal to count of vowels
        // after it.
        else
        ans = ans + vo[i + 1];
    }

    return (int) ans;
}

// Driver program
public static void main(String[] args)
{
    String str = "adceba";
    System.out.println(countSpecial(str.toCharArray()));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count special strings

# Returns true if ch is vowel
def isVowel(ch):
    return (ch == 'a' or ch == 'e' or
            ch == 'i' or ch == 'o' or
            ch == 'u')

# Function to check consonant
def isCons( ch):
    return (ch != 'a' and ch != 'e' and
            ch != 'i' and ch != 'o' and
            ch != 'u')

def countSpecial(str):
    lent = len(str)

    #in case of empty string, we can't fullfill the
      #required condition, hence we return ans as 0.
      if lent == 0:
      return 0;

    # co[i] is going to store counts
    # of consonants from str[len-1]
    # to str[i].
    # vo[i] is going to store counts
    # of vowels from str[len-1]
    # to str[i].
    co = []
    vo = []

    for i in range(0, lent + 1):
        co.append(0)

    for i in range(0, lent + 1):
        vo.append(0)

    # Counting consonants and vowels
    # from end of string.
    if isCons(str[lent - 1]) == 1:
        co[lent-1] = 1
    else:
        vo[lent - 1] = 1

    for i in range(lent-2, -1,-1):

        if isCons(str[i]) == 1:
            co[i] = co[i + 1] + 1
            vo[i] = vo[i + 1]

        else:
            co[i] = co[i + 1]
            vo[i] = vo[i + 1] + 1

    # Now we traverse string from beginning
    ans = 0

    for i in range(lent):

        #If vowel, then count of substrings
        # starting with str[i] is equal to
        # count of consonants after it.
        if isVowel(str[i]):
            ans = ans + co[i + 1]

        #If consonant, then count of
        # substrings starting with str[i]
        # is equal to count of vowels
        # after it.
        else:
            ans = ans + vo[i + 1]

    return ans

# Driver Code
str = "adceba"
print(countSpecial(str))

# This code is contributed by Upendra singh bartwal
```

## C#

```
// C# program to count special strings
using System;

class GFG
{

// Returns true if ch is vowel
static Boolean isVowel(char ch)
{
    return (ch == 'a' || ch == 'e' ||
            ch == 'i' || ch == 'o' ||
            ch == 'u');
}

// function to check consonant
static Boolean isCons(char ch)
{
    return (ch != 'a' && ch != 'e' &&
            ch != 'i' && ch != 'o' &&
            ch != 'u');
}

static int countSpecial(char []str)
{
    int len = str.Length;

      //in case of empty string, we can't fullfill the
      //required condition, hence we return ans as 0.
      if(len == 0)
          return 0;

    // co[i] is going to store counts
    // of consonants from str[len-1]
    // to str[i].
    // vo[i] is going to store counts
    // of vowels from str[len-1]
    // to str[i].
    int []co = new int[len + 1];
    int []vo = new int[len + 1];

    // Counting consonants and vowels
    // from end of string.
    if (isCons(str[len - 1]) == true)
        co[len - 1] = 1;
    else
        vo[len - 1] = 1;
    for (int i = len - 2; i >= 0; i--)
    {
        if (isCons(str[i]) == true)
        {
            co[i] = co[i + 1] + 1;
            vo[i] = vo[i + 1];
        }
        else
        {
            co[i] = co[i + 1];
            vo[i] = vo[i + 1] + 1;
        }
    }

    // Now we traverse string from beginning
    long ans = 0;
    for (int i = 0; i < len; i++)
    {
        // If vowel, then count of substrings
        // starting with str[i] is equal to
        // count of consonants after it.
        if (isVowel(str[i]))
        ans = ans + co[i + 1];

        // If consonant, then count of
        // substrings starting with str[i]
        // is equal to count of vowels
        // after it.
        else
        ans = ans + vo[i + 1];
    }
    return (int) ans;
}

// Driver program
public static void Main(String[] args)
{
    String str = "adceba";
    Console.WriteLine(countSpecial(str.ToCharArray()));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to count special strings
// Returns true if ch is vowel
function isVowel(ch)
{
    return(ch === "a" || ch === "e" ||
           ch === "i" || ch === "o" ||
           ch === "u");
}

// Function to check consonant
function isCons(ch)
{
    return(ch !== "a" && ch !== "e" &&
           ch !== "i" && ch !== "o" &&
           ch !== "u");
}

function countSpecial(str)
{
    var len = str.length;

    //in case of empty string, we can't fullfill the
      //required condition, hence we return ans as 0.
    if(len == 0)
        return 0;

    // co[i] is going to store counts
    // of consonants from str[len-1]
    // to str[i].
    // vo[i] is going to store counts
    // of vowels from str[len-1]
    // to str[i].
    var co = new Array(len + 1).fill(0);
    var vo = new Array(len + 1).fill(0);

    // Counting consonants and vowels
    // from end of string.
    if (isCons(str[len - 1]) === true) co[len - 1] = 1;
    else vo[len - 1] = 1;

    for(var i = len - 2; i >= 0; i--)
    {
        if (isCons(str[i]) === true)
        {
            co[i] = co[i + 1] + 1;
            vo[i] = vo[i + 1];
        }
        else
        {
            co[i] = co[i + 1];
            vo[i] = vo[i + 1] + 1;
        }
    }

    // Now we traverse string from beginning
    var ans = 0;
    for(var i = 0; i < len; i++)
    {

        // If vowel, then count of substrings
        // starting with str[i] is equal to
        // count of consonants after it.
        if (isVowel(str[i])) ans = ans + co[i + 1];

        // If consonant, then count of
        // substrings starting with str[i]
        // is equal to count of vowels
        // after it.
        else ans = ans + vo[i + 1];
    }
    return parseInt(ans);
}

// Driver code
var str = "adceba";

document.write(countSpecial(str.split("")));

// This code is contributed by rdtank

</script>
```

**Output**

```
9
```