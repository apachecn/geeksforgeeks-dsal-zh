# 在给定的两个字符串之间按照字典顺序找到一个字符串

> 原文:[https://www . geesforgeks . org/find-string-词典顺序-给定-两个字符串/](https://www.geeksforgeeks.org/find-string-lexicographic-order-given-two-strings/)

给定两个字符串 S 和 T，找到一个长度相同的字符串，该字符串在字典上大于 S 而小于 T。如果没有形成这样的字符串，请打印“-1”。(标准>测试)

**注:**字符串 S = s1s2… sn 据说在字典序上小于字符串 T = t1t2… tn，如果存在 I，那么 s1 = t1，s2 = t2，…si–1 = ti–1，si < ti。

**示例:**

```
Input : S = "aaa", T = "ccc"
Output : aab
Explanation: 
Here, 'b' is greater than any 
letter in S[]('a') and smaller 
than any letter in T[]('c').

Input : S = "abcde", T = "abcdf"
Output : -1
Explanation: 
There is no other string between
S and T.              
```

**方法:**找到一个按字典顺序大于字符串 S 的字符串，并检查它是否小于字符串 T，如果是，则打印该字符串，否则打印“-1”。
要查找字符串，请以相反的顺序迭代字符串 S，如果最后一个字母不是“z”，则将该字母增加 1(移动到下一个字母)。如果是“z”，将其更改为“a”，并移动到第二个最后一个字符。
将结果字符串与字符串 T 进行比较，如果两个字符串相等，则打印“-1”，否则打印结果字符串。

下面是上述方法的实现:

## C++

```
// CPP program to find the string
// in lexicographic order which is
// in between given two strings
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically 
// next string
string lexNext(string s, int n)
{  
    // Iterate from last character
    for (int i = n - 1; i >= 0; i--)
    {  
        // If not 'z', increase by one
        if (s[i] != 'z')
        {
            s[i]++;
            return s;
        }

        // if 'z', change it to 'a'
        s[i] = 'a';
    }
}

// Driver Code
int main()
{
    string S = "abcdeg", T = "abcfgh";
    int n = S.length();
    string res = lexNext(S, n);

    // If not equal, print the
    // resultant string
    if (res != T)
        cout << res << endl;   
    else
        cout << "-1" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find the string
// in lexicographic order which is
// in between given two strings

class GFG {

// Function to find the lexicographically 
// next string
    static String lexNext(String str, int n) {
        char[] s = str.toCharArray();
        // Iterate from last character
        for (int i = n - 1; i >= 0; i--) {
            // If not 'z', increase by one
            if (s[i] != 'z') {
                s[i]++;
                return String.valueOf(s);
            }

            // if 'z', change it to 'a'
            s[i] = 'a';
        }
        return null;
    }

// Driver Code
    static public void main(String[] args) {
        String S = "abcdeg", T = "abcfgh";
        int n = S.length();
        String res = lexNext(S, n);

        // If not equal, print the
        // resultant string
        if (res != T) {
            System.out.println(res);
        } else {
            System.out.println("-1");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the string
# in lexicographic order which is
# in between given two strings

# Function to find the lexicographically
# next string
def lexNext(s, n):

    # Iterate from last character
    for i in range(n - 1, -1, -1):

        # If not 'z', increase by one
        if s[i] != 'z':
            k = ord(s[i])
            s[i] = chr(k + 1)
            return ''.join(s)

        # if 'z', change it to 'a'
        s[i] = 'a'

# Driver Code
if __name__ == "__main__":
    S = "abcdeg"
    T = "abcfgh"
    n = len(S)

    S = list(S)
    res = lexNext(S, n)

    # If not equal, print the
    # resultant string
    if res != T:
        print(res)
    else:
        print(-1)

# This code is contributed by
# sanjeev2552
```

## C#

```
//C# program to find the string
// in lexicographic order which is
// in between given two strings
using System;

public class GFG {

// Function to find the lexicographically 
// next string
    static String lexNext(String str, int n) {
        char[] s = str.ToCharArray();
        // Iterate from last character
        for (int i = n - 1; i >= 0; i--) {
            // If not 'z', increase by one
            if (s[i] != 'z') {
                s[i]++;
                return new String(s);
            }

            // if 'z', change it to 'a'
            s[i] = 'a';
        }
        return null;
    }

// Driver Code
    static public void Main() {
        String S = "abcdeg", T = "abcfgh";
        int n = S.Length;
        String res = lexNext(S, n);

        // If not equal, print the
        // resultant string
        if (res != T) {
            Console.Write(res);
        } else {
            Console.Write("-1");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the string
// in lexicographic order which is
// in between given two strings

// Function to find the lexicographically 
// next string
function lexNext( s, n){  
    // Iterate from last character
    for (let i = n - 1; i >= 0; i--)
    {  
        // If not 'z', increase by one
        if (s[i] != 'z')
        {
            let code = s.charCodeAt(i)+1;
            let str = String.fromCharCode(code);
            return s.substr(0,i)+str+s.substr(i+1);

        }

        // if 'z', change it to 'a'
        s[i] = 'a';
    }

}

// Driver Code
let S = "abcdeg";
let T = "abcfgh";
let n = S.length;
let res = lexNext(S, n);

// If not equal, print the
// resultant string
if (res != T)
   document.write( res,'<br>'); 
    else
     document.write("-1 <br>" );

</script>
```

**输出:**

```
abcdeh

```