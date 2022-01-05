# 从字符串中找到网站的唯一标识和域名

> 原文:[https://www . geesforgeks . org/find-unique-id-和-域名-网站-从字符串中提取/](https://www.geeksforgeeks.org/find-unique-id-and-domain-name-of-a-website-from-a-string/)

给定一个由唯一网站的唯一 **ID** 和 [**域名**](https://www.geeksforgeeks.org/python-extract-domain-name-from-email-address/) 组成的大小为 **N** 的[字符串 **S** ，如果 **ID** 的形式为**【char，char，char，char，char，digit，digit，digit，digit，char**](https://www.geeksforgeeks.org/string-data-structure/)

**示例:**

> **输入:** S =“感谢 ABCDE1234F 访问我们并购买产品项目 AMZrr@！k .欲了解更多优惠，请访问我们的网站:
> **输出:**
> ID =**abcde 1234 f
> Domain = Amazon.com**
> 
> ****输入:** S = "Hi PQRST5678D，很荣幸能招待您。查看 www.oyo.com，我们未来停留的官方网站“
> **输出:**
> ID =**pqrst 5678d
> 域名= oyo.com****

******方法:**解决给定问题最简单的方法是[将字符串拆分成单词](https://www.geeksforgeeks.org/split-a-sentence-into-words-in-cpp/)并查找拆分后的字符串是 **ID** 还是 **Domain** 。按照以下步骤解决问题:****

*   ****首先[将字符串中由空格分隔的单词](https://www.geeksforgeeks.org/split-a-sentence-into-words-in-cpp/)拆分并存储在字符串的[向量](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)中，说**单词[]** 。****
*   ****初始化两个空字符串，说 **ID** 和**域名**来存储结果 **ID** 和**域名**。****
*   ****[遍历字符串的向量](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **单词[]** ，并执行以下步骤:

    *   初始化一个变量，说**标记**为**假**存储当前字符串是否满足**标识**的格式。
    *   如果当前字符串的长度为 **10** ，并且如果第一个 **5** 字符和最后一个字符是非字母字符或者字符串的任何剩余字符是非数字字符，那么将**标志**标记为 **true** 。
    *   如果**标志**的值为**假**，则将当前字符串分配给**标识**。
    *   如果当前字符串的第一个[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)，在范围**【0，2】**上说 **SS** 是“ **www** ”，[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)在范围**【SS . length()–3，SS . length()–1】**是“ **com** ”，那么在范围**【3，SS】上分配域名即[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)****** 
*   ****完成以上步骤后，打印 **ID** 和**域**的值作为结果。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a character is
// alphabet or not
bool ischar(char x)
{
    if ((x >= 'A' && x <= 'Z')
        || (x >= 'a' && x <= 'z')) {
        return 1;
    }

    return 0;
}

// Function to check if a character is
// a numeric or not
bool isnum(char x)
{
    if (x >= '0' && x <= '9')
        return 1;
    return 0;
}

// Function to find ID and Domain
// name from a given string
void findIdandDomain(string S, int N)
{
    // Stores ID and the domain names
    string ID, Domain;

    // Stores the words of string S
    vector<string> words;

    // Stores the temporary word
    string curr = "";

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If the current character
        // is space
        if (S[i] == ' ') {

            // Push the curr in words
            words.push_back(curr);

            // Update the curr
            curr = "";
        }

        // Otherwise
        else {
            if (S[i] == '.') {

                if (i + 1 == N
                    || (i + 1 < N
                        && S[i + 1] == ' '))
                    continue;
            }
            curr += S[i];
        }
    }

    // If curr is not empty
    if (curr.length())
        words.push_back(curr);

    for (string ss : words) {

        // If length of ss is 10
        if (ss.size() == 10) {
            bool flag = 0;

            // Traverse the string ss
            for (int j = 0; j <= 9; j++) {

                // If j is in the range
                // [5, 9)
                if (j >= 5 && j < 9) {

                    // If current character
                    // is not numeric
                    if (isnum(ss[j]) == 0)

                        // Mark flag 1
                        flag = 1;
                }

                // Otherwise
                else {

                    // If current character
                    // is not alphabet
                    if (ischar(ss[j]) == 0)

                        // Mark flag 1
                        flag = 1;
                }
            }

            // If flag is false
            if (!flag) {

                // Assign ss to ID
                ID = ss;
            }
        }

        // If substring formed by the
        // first 3 character is "www"
        // and last 3 character is "moc"
        if (ss.substr(0, 3) == "www"
            && ss.substr(
                   ss.length() - 3, 3)
                   == "com") {

            // Update the domain name
            Domain = ss.substr(
                4, ss.size() - 4);
        }
    }

    // Print ID and Domain
    cout << "ID = " << ID
         << endl;
    cout << "Domain = " << Domain;
}

// Driver Code
int main()
{
    string S = "We thank ABCDE1234F for visiting "
               "us and buying "
               "products item AMZrr@!k. For more "
               "offers, visit "
               "us at www.amazon.com";
    int N = S.length();
    findIdandDomain(S, N);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if a character is
// alphabet or not
static boolean ischar(char x)
{
    if ((x >= 'A' && x <= 'Z') ||
        (x >= 'a' && x <= 'z'))
    {
        return true;
    }
    return false;
}

// Function to check if a character is
// a numeric or not
static boolean isnum(char x)
{
    if (x >= '0' && x <= '9')
        return true;

    return false;
}

// Function to find ID and Domain
// name from a given String
static void findIdandDomain(String S, int N)
{

    // Stores ID and the domain names
    String ID = "", Domain = "";

    // Stores the words of String S
    Vector<String> words = new Vector<String>();

    // Stores the temporary word
    String curr = "";

    // Traverse the String S
    for(int i = 0; i < N; i++)
    {

        // If the current character
        // is space
        if (S.charAt(i) == ' ')
        {

            // Push the curr in words
            words.add(curr);

            // Update the curr
            curr = "";
        }

        // Otherwise
        else
        {
            if (S.charAt(i) == '.')
            {

                if (i + 1 == N || (i + 1 < N &&
                    S.charAt(i + 1) == ' '))
                    continue;
            }
            curr += S.charAt(i);
        }
    }

    // If curr is not empty
    if (curr.length() > 0)
        words.add(curr);

    for(String ss : words)
    {

        // If length of ss is 10
        if (ss.length() == 10)
        {
            boolean flag = false;

            // Traverse the String ss
            for(int j = 0; j <= 9; j++)
            {

                // If j is in the range
                // [5, 9)
                if (j >= 5 && j < 9)
                {

                    // If current character
                    // is not numeric
                    if (isnum(ss.charAt(j)) == false)

                        // Mark flag 1
                        flag = true;
                }

                // Otherwise
                else
                {

                    // If current character
                    // is not alphabet
                    if (ischar(ss.charAt(j)) == false)

                        // Mark flag 1
                        flag = true;
                }
            }

            // If flag is false
            if (!flag)
            {

                // Assign ss to ID
                ID = ss;
            }
        }

        // If subString formed by the
        // first 3 character is "www"
        // and last 3 character is "moc"
        if (ss.length() > 2 && ss.substring(0, 3).equals("www") &&
            ss.substring(ss.length() - 3).equals("com"))
        {

            // Update the domain name
            Domain = ss.substring(4, ss.length());
        }
    }

    // Print ID and Domain
    System.out.print("ID = " +  ID + "\n");
    System.out.print("Domain = " +  Domain);
}

// Driver Code
public static void main(String[] args)
{
    String S = "We thank ABCDE1234F for visiting " +
               "us and buying products item AMZrr@!k. " +
               "For more offers, visit us at www.amazon.com";
    int N = S.length();

    findIdandDomain(S, N);
}
}

// This code is contributed by 29AjayKumar**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to check if a character is
# alphabet or not
def ischar(x):

    if ((x >= 'A' and x <= 'Z') or
        (x >= 'a' and x <= 'z')):
        return 1

    return 0

# Function to check if a character is
# a numeric or not
def isnum(x):

    if (x >= '0' and x <= '9'):
        return 1

    return 0

# Function to find ID and Domain
# name from a given
def findIdandDomain(S, N):

    # Stores ID and the domain names
    ID, Domain = "", ""

    # Stores the words of  S
    words = []

    # Stores the temporary word
    curr = ""

    # Traverse the  S
    for i in range(N):

        # If the current character
        # is space
        if (S[i] == ' '):

            # Push the curr in words
            words.append(curr)

            # Update the curr
            curr = ""

        # Otherwise
        else:
            if (S[i] == '.'):
                if (i + 1 == N or (i + 1 < N and
                  S[i + 1] == ' ')):
                    continue

            curr += S[i]

    # If curr is not empty
    if (len(curr)):
        words.append(curr)

    for ss in words:

        # If length of ss is 10
        if (len(ss) == 10):
            flag = 0

            # Traverse the  ss
            for j in range(10):

                # If j is in the range
                # [5, 9)
                if (j >= 5 and j < 9):

                    # If current character
                    # is not numeric
                    if (isnum(ss[j]) == 0):

                        # Mark flag 1
                        flag = 1

                # Otherwise
                else:

                    # If current character
                    # is not alphabet
                    if (ischar(ss[j]) == 0):

                        # Mark flag 1
                        flag = 1

            # If flag is false
            if (not flag):

                # Assign ss to ID
                ID = ss

        # If sub formed by the
        # first 3 character is "www"
        # and last 3 character is "moc"
        if (ss[0: 3] == "www" and ss[len(ss) - 3: ]== "com"):

            # Update the domain name
            Domain = ss[4: len(ss) ]

    # Print ID and Domain
    print("ID =", ID)
    print("Domain =", Domain)

# Driver Code
if __name__ == '__main__':

    S = "We thank ABCDE1234F for visiting us "\
        "and buying products item AMZrr@!k. "\
        "For more offers, visit us at www.amazon.com"
    N = len(S)

    findIdandDomain(S, N)

# This code is contributed by mohit kumar 29**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to check if a character is
// alphabet or not
static bool ischar(char x)
{
    if ((x >= 'A' && x <= 'Z') ||
        (x >= 'a' && x <= 'z'))
    {
        return true;
    }
    return false;
}

// Function to check if a character is
// a numeric or not
static bool isnum(char x)
{
    if (x >= '0' && x <= '9')
        return true;

    return false;
}

// Function to find ID and Domain
// name from a given String
static void findIdandDoMain(String S, int N)
{

    // Stores ID and the domain names
    String ID = "", Domain = "";

    // Stores the words of String S
    List<String> words = new List<String>();

    // Stores the temporary word
    String curr = "";

    // Traverse the String S
    for(int i = 0; i < N; i++)
    {

        // If the current character
        // is space
        if (S[i] == ' ')
        {

            // Push the curr in words
            words.Add(curr);

            // Update the curr
            curr = "";
        }

        // Otherwise
        else
        {
            if (S[i] == '.')
            {

                if (i + 1 == N || (i + 1 < N &&
                    S[i + 1] == ' '))
                    continue;
            }
            curr += S[i];
        }
    }

    // If curr is not empty
    if (curr.Length > 0)
        words.Add(curr);

    foreach(String ss in words)
    {

        // If length of ss is 10
        if (ss.Length == 10)
        {
            bool flag = false;

            // Traverse the String ss
            for(int j = 0; j <= 9; j++)
            {

                // If j is in the range
                // [5, 9)
                if (j >= 5 && j < 9)
                {

                    // If current character
                    // is not numeric
                    if (isnum(ss[j]) == false)

                        // Mark flag 1
                        flag = true;
                }

                // Otherwise
                else
                {

                    // If current character
                    // is not alphabet
                    if (ischar(ss[j]) == false)

                        // Mark flag 1
                        flag = true;
                }
            }

            // If flag is false
            if (!flag)
            {

                // Assign ss to ID
                ID = ss;
            }
        }

        // If subString formed by the
        // first 3 character is "www"
        // and last 3 character is "moc"
        if (ss.Length > 2 && ss.Substring(0, 3).Equals("www") &&
            ss.Substring(ss.Length - 3).Equals("com"))
        {

            // Update the domain name
            Domain = ss.Substring(4, ss.Length-4);
        }
    }

    // Print ID and Domain
    Console.Write("ID = " +  ID + "\n");
    Console.Write("Domain = " +  Domain);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "We thank ABCDE1234F for visiting " +
               "us and buying products item AMZrr@!k. " +
               "For more offers, visit us at www.amazon.com";
    int N = S.Length;

    findIdandDoMain(S, N);
}
}

// This code is contributed by 29AjayKumar**
```

## ****java 描述语言****

```
**<script>

// JavaScript program for the above approach

// Function to check if a character is
// alphabet or not
function ischar(x)
{
    if ((x >= 'A' && x <= 'Z') ||
        (x >= 'a' && x <= 'z'))
    {
        return true;
    }
    return false;
}

// Function to check if a character is
// a numeric or not
function isnum(x)
{
    if (x >= '0' && x <= '9')
        return true;

    return false;
}

// Function to find ID and Domain
// name from a given string
function findIdandDomain(S, N)
{

    // Stores ID and the domain names
    let ID, Domain;

    // Stores the words of string S
    let words = [];

    // Stores the temporary word
    let curr = "";

    // Traverse the string S
    for(let i = 0; i < N; i++)
    {

        // If the current character
        // is space
        if (S[i] == ' ')
        {

            // Push the curr in words
            words.push(curr);

            // Update the curr
            curr = "";
        }

        // Otherwise
        else
        {
            if (S[i] == '.')
            {

                if (i + 1 == N ||
                   (i + 1 < N && S[i + 1] == ' '))
                    continue;
            }
            curr += S[i];
        }
    }

    // If curr is not empty
    if (curr.length >= 1)
        words.push(curr);

    for(let i = 0; i < words.length; i++)
    {

        // If length of ss is 10
        if (words[i].length == 10)
        {
            let flag = 0;

            // Traverse the string ss
            for(let j = 0; j <= 9; j++)
            {

                // If j is in the range
                // [5, 9)
                if (j >= 5 && j < 9)
                {

                    // If current character
                    // is not numeric
                    if (isnum(words[i][j]) == 0)

                        // Mark flag 1
                        flag = 1;
                }

                // Otherwise
                else
                {

                    // If current character
                    // is not alphabet
                    if (ischar(words[i][j]) == 0)

                        // Mark flag 1
                        flag = 1;
                }
            }

            // If flag is false
            if (!flag)
            {

                // Assign ss to ID
                ID = words[i];
            }
        }

        // If substring formed by the
        // first 3 character is "www"
        // and last 3 character is "moc"

        if (words[i].substring(0, 3) == "www" &&
            words[i].substring(
                words[i].length - 3) == "com")
        {

            // Update the domain name
            Domain = words[i].substring(4);
        }
    }

    // Print ID and Domain
    document.write("ID = " + ID + "<br>");

    document.write("Domain = " + Domain);
}

// Driver Code
let S = "We thank ABCDE1234F for visiting " +
        "us and buying products item AMZrr@!k. " +
        "For more offers, visit us at www.amazon.com";
let N = S.length;
findIdandDomain(S, N);

// This code is contributed by Dharanendra L V.

</script>**
```

******Output:** 

```
ID = ABCDE1234F
Domain = amazon.com
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(N)****