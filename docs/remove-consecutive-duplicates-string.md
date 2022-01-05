# 从字符串中删除所有连续的重复项

> 原文:[https://www . geesforgeks . org/remove-continuous-duplicates-string/](https://www.geeksforgeeks.org/remove-consecutive-duplicates-string/)

给定一个字符串，删除所有连续的重复项。注意，这个问题不同于[递归删除所有相邻的重复](https://www.geeksforgeeks.org/recursively-remove-adjacent-duplicates-given-string/)。这里我们保留一个字符，并删除所有后续的相同字符。

**示例:**

```
Input  : aaaaabbbbbb
Output : ab

Input : geeksforgeeks
Output : geksforgeks

Input : aabccba
Output : abcba
```

**递归解:**

上述问题可以用递归来解决。

1.  如果字符串为空，则返回。
2.  否则比较字符串的相邻字符。如果它们相同，则将字符一个接一个地向左移动。在字符串 S 上调用递归
3.  如果它们不相同，那么从 S+1 字符串调用递归。

字符串 S = aabcca 的递归树如下所示。

```
        aabcca   S = aabcca
        /
       abcca     S = abcca        
       /
      bcca       S = abcca
      /
     cca         S = abcca
     /
    ca           S = abca
   /
  a              S = abca (Output String)
 /
empty string
```

下面是上述方法的实现:

## C++

```
// Recursive Program to remove consecutive
// duplicates from string S.
#include <bits/stdc++.h>
using namespace std;

// A recursive function that removes
// consecutive duplicates from string S
void removeDuplicates(char* S)
{
    // When string is empty, return
    if (S[0] == '\0')
        return;

    // if the adjacent characters are same
    if (S[0] == S[1]) {

        // Shift character by one to left
        int i = 0;
        while (S[i] != '\0') {
            S[i] = S[i + 1];
            i++;
        }

        // Check on Updated String S
        removeDuplicates(S);
    }

    // If the adjacent characters are not same
    // Check from S+1 string address
    removeDuplicates(S + 1);
}

// Driver Program
int main()
{
    char S1[] = "geeksforgeeks";
    removeDuplicates(S1);
    cout << S1 << endl;

    char S2[] = "aabcca";
    removeDuplicates(S2);
    cout << S2 << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    public static String removeConsecutiveDuplicates(String input) {
        if(input.length()<=1)
            return input;
        if(input.charAt(0)==input.charAt(1))
            return removeConsecutiveDuplicates(input.substring(1));
        else
            return input.charAt(0) + removeConsecutiveDuplicates(input.substring(1));
    }
    public static void main(String[] args)
    {
        String S1 = "geeksforgeeks";
        System.out.println(removeConsecutiveDuplicates(S1));

        String S2 = "aabcca";
        System.out.println(removeConsecutiveDuplicates(S2));
    }
}
```

## 蟒蛇 3

```
# Recursive Program to remove consecutive
# duplicates from string S.
def removeConsecutiveDuplicates(s):
    if len(s)<2:
        return s
    if s[0]!=s[1]:
        return s[0]+removeConsecutiveDuplicates(s[1:])
    return removeConsecutiveDuplicates(s[1:])

# This code is contributed by direwolf707
s1='geeksforgeeks'
print(removeConsecutiveDuplicates(s1)) #geksforgeks
s2='aabcca'
print(removeConsecutiveDuplicates(s2)) #ab

# This code is contributed by rahulsood707.
```

## C#

```
/*package whatever //do not write package name here */
using System;

class GFG {
    public static string removeConsecutiveDuplicates(string input) {
        if(input.Length <= 1)
            return input;
        if(input[0] == input[1])
            return removeConsecutiveDuplicates(input.Substring(1));
        else
            return input[0] + removeConsecutiveDuplicates(input.Substring(1));
    }
    public static void Main(String[] args)
    {
        string S1 = "geeksforgeeks";
        Console.WriteLine(removeConsecutiveDuplicates(S1));

        string S2 = "aabcca";
        Console.Write(removeConsecutiveDuplicates(S2));
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

function removeConsecutiveDuplicates(input)
{
    if(input.length<=1)
            return input;
        if(input[0]==input[1])
            return removeConsecutiveDuplicates(input.substring(1));
        else
            return input[0] +
            removeConsecutiveDuplicates(input.substring(1));
}

let S1 = "geeksforgeeks";
document.write(removeConsecutiveDuplicates(S1)+"<br>");

let  S2 = "aabcca";
document.write(removeConsecutiveDuplicates(S2)+"<br>");

// This code is contributed by rag2127

</script>
```

**Output**

```
geksforgeks
abca
```

上述解的最坏情况时间复杂度为 O(n <sup>2</sup> )。最糟糕的情况发生在所有角色都相同的时候。

**迭代解:**

其思想是检查当前字符是否等于下一个字符。如果当前字符等于下一个字符，我们将忽略它，当它不相等时，我们将把它添加到我们的答案中。因为，最后一个元素不会被选中，我们将把它推到字符串的末尾。例如:s = " aaaaa "

当我们运行循环 str= " "时，我们将在最后添加' a ',因为它是最后一个元素。

## C++

```
// C++ program to remove consecutive
// duplicates from a given string.
#include <bits/stdc++.h>
using namespace std;

// A iterative function that removes 
// consecutive duplicates from string S
string removeDuplicates(string s){

   int n = s.length();
   string str="";
   // We don't need to do anything for
   // empty string.
   if (n == 0)
     return str;

   // Traversing string
    for(int i=0;i<n-1;i++){
      //checking if s[i] is not same as s[i+1] then add it into str
        if(s[i]!=s[i+1]){
            str+=s[i];
        }
    }
  //Since the last character will not be inserted in the loop we add it at the end
   str.push_back(s[n-1]);
   return str;   
}

// Driver Program
int main() {

    string s1 = "geeksforgeeks";
    cout << removeDuplicates(s1) << endl;

    string s2 = "aabcca";
    cout << removeDuplicates(s2) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to remove consecutive
// duplicates from a given string.
import java.util.*;

class GFG
{

    // A iterative function that removes
    // consecutive duplicates from string S
    static void removeDuplicates(char[] S)
    {
        int n = S.length;

        // We don't need to do anything for
        // empty or single character string.
        if (n < 2)
        {
            return;
        }

        // j is used to store index is result
        // string (or index of current distinct
        // character)
        int j = 0;

        // Traversing string
        for (int i = 1; i < n; i++)
        {
            // If current character S[i]
            // is different from S[j]
            if (S[j] != S[i])
            {
                j++;
                S[j] = S[i];
            }
        }
        System.out.println(Arrays.copyOfRange(S, 0, j + 1));
    }

    // Driver code
    public static void main(String[] args)
    {
        char S1[] = "geeksforgeeks".toCharArray();
        removeDuplicates(S1);

        char S2[] = "aabcca".toCharArray();
        removeDuplicates(S2);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to remove consecutive
# duplicates from a given string.

# A iterative function that removes
# consecutive duplicates from string S
def removeDuplicates(S):

    n = len(S)

    # We don't need to do anything for
    # empty or single character string.
    if (n < 2) :
        return

    # j is used to store index is result
    # string (or index of current distinct
    # character)
    j = 0

    # Traversing string
    for i in range(n):

        # If current character S[i]
        # is different from S[j]
        if (S[j] != S[i]):
            j += 1
            S[j] = S[i]

    # Putting string termination
    # character.
    j += 1
    S = S[:j]
    return S

# Driver Code
if __name__ == '__main__':

    S1 = "geeksforgeeks"
    S1 = list(S1.rstrip())
    S1 = removeDuplicates(S1)
    print(*S1, sep = "")

    S2 = "aabcca"
    S2 = list(S2.rstrip())
    S2 = removeDuplicates(S2)
    print(*S2, sep = "")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to remove consecutive
// duplicates from a given string.
using System;

class GFG
{

    // A iterative function that removes
    // consecutive duplicates from string S
    static void removeDuplicates(char[] S)
    {
        int n = S.Length;

        // We don't need to do anything for
        // empty or single character string.
        if (n < 2)
        {
            return;
        }

        // j is used to store index is result
        // string (or index of current distinct
        // character)
        int j = 0;

        // Traversing string
        for (int i = 1; i < n; i++)
        {
            // If current character S[i]
            // is different from S[j]
            if (S[j] != S[i])
            {
                j++;
                S[j] = S[i];
            }
        }
        char []A = new char[j+1];
        Array.Copy(S,0, A, 0, j + 1);
        Console.WriteLine(A);
    }

    // Driver code
    public static void Main(String[] args)
    {
        char []S1 = "geeksforgeeks".ToCharArray();
        removeDuplicates(S1);

        char []S2 = "aabcca".ToCharArray();
        removeDuplicates(S2);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // duplicates from a given string.

    // A iterative function that removes
    // consecutive duplicates from string S
    const removeDuplicates = (s) => {

        let n = s.length;
        let str = "";
        // We don't need to do anything for
        // empty string.
        if (n == 0)
            return str;

        // Traversing string
        for (let i = 0; i < n - 1; i++) {
            //checking if s[i] is not same as s[i+1] then add it into str
            if (s[i] != s[i + 1]) {
                str += s[i];
            }
        }
        //Since the last character will not be inserted in the loop we add it at the end

        str += s[n-1];
        return str;
    }

    // Driver Program
    let s1 = "geeksforgeeks";
    document.write(`${removeDuplicates(s1)}<br/>`)
    let s2 = "aabcca";
    document.write(removeDuplicates(s2))

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
geksforgeks
abca
```

**时间复杂度:** O(n)

**辅助空间:** O(1)

本文由**安库尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。