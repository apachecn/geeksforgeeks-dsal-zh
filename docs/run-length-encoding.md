# 游程编码

> 原文:[https://www.geeksforgeeks.org/run-length-encoding/](https://www.geeksforgeeks.org/run-length-encoding/)

给定一个输入字符串，编写一个函数，返回输入字符串的[游程编码的](http://en.wikipedia.org/wiki/Run-length_encoding)字符串。
例如，如果输入字符串是“wwwwwwaaadexxxxx”，那么函数应该返回“w4a3d1e1x6”

a)从源字符串中选择第一个字符。
b)将选取的字符追加到目标字符串中。
c)计算所选字符的后续出现次数，并将该次数附加到目标字符串中。
d)选择下一个字符，如果没有到达字符串的末尾，重复步骤 b)、c)和 d)。

## C++

```
// CPP program to implement run length encoding
#include <bits/stdc++.h>
using namespace std;

void printRLE(string str)
{
    int n = str.length();
    for (int i = 0; i < n; i++) {

        // Count occurrences of current character
        int count = 1;
        while (i < n - 1 && str[i] == str[i + 1]) {
            count++;
            i++;
        }

        // Print character and its count
        cout << str[i] << count;
    }
}

int main()
{
    string str = "wwwwaaadexxxxxxywww";
    printRLE(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement run length encoding

public class RunLength_Encoding {
    public static void printRLE(String str)
    {
        int n = str.length();
      int count = 1;
        for (int i = 1; i < n; i++) {

            // Count occurrences of current character

            if(str.charAt(i) == str.charAt(i-1)){
              count++
            }
          else{
            System.out.print(str.charAt(i));
            System.out.print(count);
            count = 1
          }

            // Print character and its count
            System.out.print(str.charAt(i));
            System.out.print(count);
        }
    }

    public static void main(String[] args)
    {
        String str = "wwwwaaadexxxxxxywww";
        printRLE(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# run length encoding
def printRLE(st):

    n = len(st)
    i = 0
    while i < n- 1:

        # Count occurrences of
        # current character
        count = 1
        while (i < n - 1 and
               st[i] == st[i + 1]):
            count += 1
            i += 1
        i += 1

        # Print character and its count
        print(st[i - 1] +
              str(count),
              end = "")

# Driver code
if __name__ == "__main__":

    st = "wwwwaaadexxxxxxywww"
    printRLE(st)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement run length encoding
using System;
class GFG
{
public class RunLength_Encoding
{
    public static void printRLE(String str)
    {
        int n = str.Length;
        for (int i = 0; i < n; i++)
        {

            // Count occurrences of current character
            int count = 1;
            while (i < n - 1 && str[i] == str[i + 1])
            {
                count++;
                i++;
            }

            // Print character and its count
            Console.Write(str[i]);
            Console.Write(count);
        }
    }

    public static void Main(String[] args)
    {
        String str = "wwwwaaadexxxxxxywww";
        printRLE(str);
    }
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program to implement run length encoding
    function printRLE(str)
    {
        let n = str.length;
        for (let i = 0; i < n; i++)
        {
            // Count occurrences of current character
            let count = 1;
            while (i < n - 1 && str[i] == str[i+1])
            {
                count++;
                i++;
            }

            // Print character and its count
            document.write(str[i]);
            document.write(count);
        }
    }

    let str = "wwwwaaadexxxxxxywww";
    printRLE(str);

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
w4a3d1e1x6y1w3
```

**C 执行**T2】

## C

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define MAX_RLEN 50

/* Returns the Run Length Encoded string for the
   source string src */
char* encode(char* src)
{
    int rLen;
    char count[MAX_RLEN];
    int len = strlen(src);

    /* If all characters in the source string are different,
    then size of destination string would be twice of input string.
    For example if the src is "abcd", then dest would be "a1b1c1d1"
    For other inputs, size would be less than twice.  */
    char* dest = (char*)malloc(sizeof(char) * (len * 2 + 1));

    int i, j = 0, k;

    /* traverse the input string one by one */
    for (i = 0; i < len; i++) {

        /* Copy the first occurrence of the new character */
        dest[j++] = src[i];

        /* Count the number of occurrences of the new character */
        rLen = 1;
        while (i + 1 < len && src[i] == src[i + 1]) {
            rLen++;
            i++;
        }

        /* Store rLen in a character array count[] */
        sprintf(count, "%d", rLen);

        /* Copy the count[] to destination */
        for (k = 0; *(count + k); k++, j++) {
            dest[j] = count[k];
        }
    }

    /*terminate the destination string */
    dest[j] = '\0';
    return dest;
}

/*driver program to test above function */
int main()
{
    char str[] = "geeksforgeeks";
    char* res = encode(str);
    printf("%s", res);
    getchar();
}
```

**Output:** 

```
g1e2k1s1f1o1r1g1e2k1s1
```

时间复杂度:O(n)
参考文献:
[http://en.wikipedia.org/wiki/Run-length_encoding](http://en.wikipedia.org/wiki/Run-length_encoding)
如果发现以上代码/算法不正确，请写评论，或者找到更好的方法解决同样的问题。