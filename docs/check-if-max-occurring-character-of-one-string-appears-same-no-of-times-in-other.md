# 检查一个字符串的最大出现字符在其他

中出现的次数是否相同

> 原文:[https://www . geesforgeks . org/check-if-max-occurrent-of-character-on-other-no-of-time-in-other/](https://www.geeksforgeeks.org/check-if-max-occurring-character-of-one-string-appears-same-no-of-times-in-other/)

给定两个字符串，我们需要取第一个字符串中出现次数最多的字符，然后我们必须检查该特定字符在第二个字符串中出现的次数是否与它在第一个字符串中出现的次数相同。
**例:**

```
Input : s1 = "sssgeek", s2 = "geeksss"
Output : Yes
Max occurring character in s1 is
's'. It occurs same number of times
in s2.

Input :  geekyarticle
         gfggfggfg
Output : No
```

在第一个字符串中存储字符数，并找到最大计数。现在遍历第二个字符串，检查最大出现字符出现的次数是否相同。
下面程序来说明上面的问题

## C++

```
// C++ program to check the problem
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define ASCIISIZE 256

int match(string s1, string s2)
{
    // Create array to keep the count of individual
    // characters and initialize the array as 0
    int count[ASCIISIZE] = { 0 };

    // Construct character count array from the input
    // string.
    for (int i = 0; i < s1.length(); i++)
        count[s1[i]]++;

    // Count occurrences of maximum occurring character
    int mx_cnt = 0, mx_chr;
    for (int i = 0; i < ASCIISIZE; i++) {
        if (count[i] > mx_cnt) {
            mx_cnt = count[i];
            mx_chr = i;
        }
    }

    // look if that character is present, the same
    // number of times it is present in second string
    for (int i = 0; i < s2.length(); i++)
        if (mx_chr == s2[i])
            mx_cnt--;

    // check if sum is greater or equal to number
    // return 1
    if (mx_cnt == 0)
        return 1;
}

// Driver program to test the above function
int main()
{
    string s1 = "geekforgeeks", s2 = "geekisgeeky";
    if (match(s1, s2))
        cout << "Yes ";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check the problem
class GFG
{
static int ASCIISIZE = 256;
static int match(String s1,    
                 String s2)
{
// Create array to keep the
// count of individual characters
// and initialize the array as 0
int count[] = new int[ASCIISIZE];

// Construct character count
// array from the input string.
char []s3 = s1.toCharArray();
for (int i = 0; i < s3.length; i++)
    count[s3[i]]++;

// Count occurrences of
// maximum occurring character
int mx_cnt = 0;
int mx_chr = 0;
for (int i = 0; i < ASCIISIZE; i++)
{
    if (count[i] > mx_cnt)
    {
        mx_cnt = count[i];
        mx_chr = i;
    }
}

// look if that character is
// present, the same number
// of times it is present in
// second string
char []s4 = s2.toCharArray();
for (int i = 0; i < s4.length; i++)
    if (mx_chr == s4[i])
        mx_cnt--;

// check if sum is greater or
// equal to number return 1
if (mx_cnt == 0)
    return 1;
else
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    String s1 = "geekforgeeks",
           s2 = "geekisgeeky";
    int p = match(s1, s2);
    if (p == 1)
        System.out.println("Yes ");
    else
        System.out.println("No");
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to
# check the problem

# define function for Check
# if max occurring character
# of one string appears same
# no. of times in other
def match(s1, s2) :

    # declare empty list
    count_list = []

    # iterate through each
    # character of the string
    for char in s1 :

        # find occurrence of
        # the character
        count = s1.count(char)

        # append tuple value
        # to the list
        count_list.append((count,char))

    # return tuple of max count
    max_occ = max(count_list)

    # store max count in mx_cnt
    mx_cnt = max_occ[0]

    # store max count
    # character in mx_chr
    mx_chr = max_occ[1]

    # look if max count character
    # is present in s1, the same
    # number of times it is present
    # in second string s2 or not
    # if present return True
    # otherwise False.
    if mx_cnt == s2.count(mx_chr) :
        return True
    else :
        return False

# Driver Code
if __name__ == "__main__" :

    s1 = "geeksforgeeks"
    s2 = "geekisgeeky"

    if match(s1,s2) :
        print("Yes")
    else :
        print("No")

# This code is contributed
# by Ankit Rai
```

## C#

```
// C# program to check the problem
using System;

class GFG
{
static int ASCIISIZE = 256;
static int match(String s1,
                 String s2)
{
// Create array to keep the
// count of individual characters
// and initialize the array as 0
int []count = new int[ASCIISIZE];

// Construct character count                                    
// array from the input string.
for (int i = 0; i < s1.Length; i++)
    count[s1[i]]++;

// Count occurrences of
// maximum occurring character
int mx_cnt = 0;
int mx_chr = 0;
for (int i = 0; i < ASCIISIZE; i++)
{
    if (count[i] > mx_cnt)
    {
        mx_cnt = count[i];
        mx_chr = i;
    }
}

// look if that character is
// present, the same number
// of times it is present
// in second string
for (int i = 0; i < s2.Length; i++)
    if (mx_chr == s2[i])
        mx_cnt--;

// check if sum is greater
// or equal to number return 1
if (mx_cnt == 0)
    return 1;
else
    return 0;
}

// Driver Code
public static void Main()
{
    String s1 = "geekforgeeks",
           s2 = "geekisgeeky";
    int p = match(s1, s2);
    if (p == 1)
        Console.Write("Yes ");
    else
        Console.Write("No");
}
}

// This code is contributed
// by ChitraNayal
```

## java 描述语言

```
<script>

// Javascript program to check the problem

    let ASCIISIZE = 256;
function match(s1,s2)
{
    // Create array to keep the
// count of individual characters
// and initialize the array as 0
let count = new Array(ASCIISIZE);
for(let i=0;i<ASCIISIZE;i++)
{
    count[i]=0;
}
// Construct character count
// array from the input string.
let s3 = s1.split("");
for (let i = 0; i < s3.length; i++)
    count[s3[i]]++;

// Count occurrences of
// maximum occurring character
let mx_cnt = 0;
let mx_chr = 0;
for (let i = 0; i < ASCIISIZE; i++)
{
    if (count[i] > mx_cnt)
    {
        mx_cnt = count[i];
        mx_chr = i;
    }
}

// look if that character is
// present, the same number
// of times it is present in
// second string
let s4 = s2.split("");
for (let i = 0; i < s4.length; i++)
    if (mx_chr == s4[i])
        mx_cnt--;

// check if sum is greater or
// equal to number return 1
if (mx_cnt == 0)
    return 1;
else
    return 0;
}

// Driver Code
let s1 = "geekforgeeks",
           s2 = "geekisgeeky";
let p = match(s1, s2);
if (p == 1)
    document.write("Yes ");
else
    document.write("No");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
Yes
```