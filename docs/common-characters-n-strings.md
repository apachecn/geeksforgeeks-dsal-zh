# n 个字符串中的常用字符

> 原文:[https://www.geeksforgeeks.org/common-characters-n-strings/](https://www.geeksforgeeks.org/common-characters-n-strings/)

给定 n 个字符串，找出所有字符串中的常见字符。简单地说，找到出现在所有字符串中的字符，并按字母顺序或词典顺序显示它们。

**注意*** 我们将考虑字符串只包含小写字母。

**示例**:

```
Input :  geeksforgeeks
         gemkstones
         acknowledges
         aguelikes

Output : e g k s

Input :  apple 
         orange

Output : a e

```

我们将使用两个大小为 26 的散列数组(对于 a-z，其中 0 是 a，z 是 25)。
方法很简单，如果我们之前见过一个角色，我们会标记它，如果我们没有见过，那么忽略这个角色，因为它不是一个常见的角色。

PSU 代码:

```
commonCharacters :
for i= 0 to n-1:

   // here m is length of ith string 
   for j = 0 to m-1:  
      if ( character seen before ) :
         mark the character
      else : 
         ignore it

display all the marked characters 

```

## C++

```
// CPP Program to find all the common characters
// in n strings
#include <bits/stdc++.h>
using namespace std;

const int MAX_CHAR = 26;

void commonCharacters(string str[], int n)
{
    // primary array for common characters 
    // we assume all characters are seen before.
    bool prim[MAX_CHAR];
    memset(prim, true, sizeof(prim));

    // for each string
    for (int i = 0; i < n; i++) {

        // secondary array for common characters
        // Initially marked false
        bool sec[MAX_CHAR] = { false };

        // for every character of ith string
        for (int j = 0; str[i][j]; j++) {

            // if character is present in all 
            // strings before, mark it.
            if (prim[str[i][j] - 'a'])
                sec[str[i][j] - 'a'] = true; 
        }

        // copy whole secondary array into primary
        memcpy(prim, sec, MAX_CHAR);
    }

    // displaying common characters
    for (int i = 0; i < 26; i++)
        if (prim[i])
            printf("%c ", i + 'a');
}

// Driver's Code
int main()
{
    string str[] = { "geeksforgeeks",
                    "gemkstones",
                    "acknowledges",
                    "aguelikes" };
    int n = sizeof(str)/sizeof(str[0]);
    commonCharacters(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find all the common characters
// in n strings
import java.util.*;
import java.lang.*;

class GFG {

    static int MAX_CHAR = 26;

    public static void commonCharacters(String str[],
                                               int n)
    {

        // primary array for common characters 
        // we assume all characters are seen before.
        Boolean[] prim = new Boolean[MAX_CHAR];
        Arrays.fill(prim, new Boolean(true));

        // for each string
        for (int i = 0; i < n; i++) {

            // secondary array for common characters
            // Initially marked false
            Boolean[] sec = new Boolean[MAX_CHAR];
            Arrays.fill(sec, new Boolean(false));

            // for every character of ith string
            for (int j = 0; j < str[i].length(); j++)
            {

                // if character is present in all 
                // strings before, mark it.
                if (prim[str[i].charAt(j) - 'a'])
                sec[str[i].charAt(j) - 'a'] = true; 
            }

            // copy whole secondary array into primary
            System.arraycopy(sec, 0, prim, 0, MAX_CHAR);
        }

        // displaying common characters
        for (int i = 0; i < 26; i++)
            if (prim[i]){
                System.out.print(Character.toChars(i 
                                               + 97));
                System.out.print(" ");
            } 
    }

    // Driver code
    public static void main(String[] args)
    {
        String str[] = { "geeksforgeeks",
                         "gemkstones",
                         "acknowledges",
                         "aguelikes" };

        int n = str.length;
        commonCharacters(str, n);
    }
}

// This code is contributed by Prasad Kshirsagar
```

## 蟒蛇 3

```
# Python3 Program to find all the 
# common characters in n strings
MAX_CHAR = 26

def commonCharacters(strings, n) :

    # primary array for common characters 
    # we assume all characters are seen before. 
    prim = [True] * MAX_CHAR 

    # for each strings 
    for i in range(n):

        # secondary array for common characters 
        # Initially marked false 
        sec = [False] * MAX_CHAR 

        # for every character of ith strings 
        for j in range(len(strings[i])):

            # if character is present in all 
            # strings before, mark it. 
            if (prim[ord(strings[i][j]) - ord('a')]) :
                sec[ord(strings[i][j]) - 
                    ord('a')] = True

        # copy whole secondary array
        # into primary 
        for i in range(MAX_CHAR):
            prim[i] = sec[i]

    # displaying common characters 
    for i in range(26):
        if (prim[i]) :
            print("%c " % (i + ord('a')), 
                               end = "")

# Driver's Code 
strings = [ "geeksforgeeks", "gemkstones", 
            "acknowledges", "aguelikes" ]
n = len(strings)
commonCharacters(strings, n) 

# This code is contributed by Niwesh Gupta
```

## C#

```
// C# Program to find all the 
// common characters in n strings
using System; 

class GFG 
{

    static int MAX_CHAR = 26;

    public static void commonCharacters(String []str,
                                            int n)
    {

        // primary array for common characters 
        // we assume all characters are seen before.
        Boolean[] prim = new Boolean[MAX_CHAR];

        for(int i = 0; i < prim.Length; i++)
            prim[i] = true;

        // for each string
        for (int i = 0; i < n; i++)
        {

            // secondary array for common characters
            // Initially marked false
            Boolean[] sec = new Boolean[MAX_CHAR];

            for(int s = 0; s < sec.Length; s++)
                sec[s]=false;

            // for every character of ith string
            for (int j = 0; j < str[i].Length; j++)
            {

                // if character is present in all 
                // strings before, mark it.
                if (prim[str[i][j] - 'a'])
                sec[str[i][j] - 'a'] = true; 
            }

            // Copy whole secondary array into primary
            Array.Copy(sec, 0, prim, 0, MAX_CHAR);
        }

        // Displaying common characters
        for (int i = 0; i < 26; i++)
            if (prim[i])
            {
                Console.Write((char)(i + 97));
                Console.Write(" ");
            } 
    }

    // Driver code
    public static void Main(String[] args)
    {
        String []str = { "geeksforgeeks",
                        "gemkstones",
                        "acknowledges",
                        "aguelikes" };

        int n = str.Length;
        commonCharacters(str, n);
    }
}

// This code is contributed by Rajput-JI
```

**输出:**

```
e g k s

```

本文由 [**舒巴姆拉纳**](https://auth.geeksforgeeks.org/profile.php?user=shubham_rana_77) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。