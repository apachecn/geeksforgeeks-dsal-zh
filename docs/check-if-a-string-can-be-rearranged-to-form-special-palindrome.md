# 检查一个字符串是否可以重新排列形成特殊回文

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-重排形成特殊回文/](https://www.geeksforgeeks.org/check-if-a-string-can-be-rearranged-to-form-special-palindrome/)

给定一个字符串 *str* ，任务是检查它是否可以重新排列得到一个特殊的回文字符串。如果我们能让它打印是，否则打印否
一个字符串被称为特殊回文，它在回文位置包含一个大写字母和一个小写字母。**例-**abcba 是特殊回文，但 abcba 不是特殊回文。
**例:**

```
Input: str = "ABCcba"
Output: YES

Input: str = "ABCCBA"
Output: NO
```

**方法:**检查一个字符大写字母的出现是否与同一字符小写字母的出现相同。并且应该只有一个出现的字符。我们将每个大写字符的频率增加 1，将每个小写字符的频率减少 1。在此之后，频率数组中应该有零、1 或-1。如果出现任何其他情况，我们直接说“否”，否则打印“是”。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Driver code
int main()
{
    string s = "ABCdcba" ;

    // creating a array which stores the
    // frequency of each character
    int u[26] = {0};
    int n = s.length() ;

    for(int i = 0; i < n ; i++)
    {
        // Checking if a character is uppercase or not
        if(isupper(s[i]))
        {
            // Increasing by 1 if uppercase
            u[s[i] - 65] += 1;
        }
        else
        {
            // Decreasing by 1 if lower case
            u[s[i] - 97] -= 1 ;
        }

    }
    bool f1 = true ;

    // Storing the sum of positive
    // numbers in the frequency array
    int po = 0 ;

    // Storing the sum of negative
    // numbers in the frequency array
    int ne = 0 ;

    for (int i = 0 ; i < 26 ; i++)
    {
        if (u[i] > 0)
            po += u[i] ;

        if (u[i] < 0)
            ne += u[i] ;
    }

    // If all character balances out then its Yes
    if (po == 0 && ne == 0)
        cout << ("YES") << endl;

    // If there is only 1 character which
    // does not balances then also it is Yes
    else if (po == 1 && ne == 0)
        cout << ("YES") << endl;

    else if (po == 0 && ne == -1)
        cout << ("YES") << endl;

    else
        cout << ("NO") << endl;

}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
public class Improve {

    public static void main(String args[])
    {
        String s = "ABCdcba" ;

        // creating a array which stores the 
        // frequency of each character
        int u[] = new int[26];
        int n = s.length() ;

        for(int i = 0; i < n ; i++)
        {
            // Checking if a character is uppercase or not
            if(Character.isUpperCase(s.charAt(i)))
            {
                // Increasing by 1 if uppercase
                u[s.charAt(i) - 65] += 1 ;
            }
            else
            {
                // Decreasing by 1 if lower case
                u[s.charAt(i) - 97] -= 1 ;
            }

        }
        boolean f1 = true ;

        // Storing the sum of positive 
        // numbers in the frequency array
        int po = 0 ;

        // Storing the sum of negative 
        // numbers in the frequency array
        int ne = 0 ;

        for (int i = 0 ; i < 26 ; i++)
        {
            if (u[i] > 0)
                po += u[i] ;

            if (u[i] < 0)
                ne += u[i] ;
        }

        // If all character balances out then its Yes
        if (po == 0 && ne == 0)
            System.out.println("YES") ;

        // If there is only 1 character which 
        // does not balances then also it is Yes
        else if (po == 1 && ne == 0)
            System.out.println("YES") ;

        else if (po == 0 && ne == -1)
            System.out.println("YES") ;

        else
            System.out.println("NO") ;

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python implementation of the above approach
s = "ABCdcba"

# creating a list which stores the
# frequency of each character
u = [0] * 26 
n = len(s)
for i in range(n):
    # Checking if a character is uppercase or not
    if (s[i].isupper()): 
        # Increasing by 1 if uppercase
        u[ord(s[i]) - 65] += 1 
    else:
        # Decreasing by 1 if lower case
        u[ord(s[i]) - 97] -= 1 
fl = True

# Storing the sum of positive
# numbers in the frequency array
po = 0 

# Storing the sum of negative
# numbers in the frequency array
ne = 0 
for i in range(26):
    if (u[i] > 0):
        po += u[i]
    if (u[i] < 0):
        ne += u[i]

# If all character balances out then its Yes
if (po == 0 and ne == 0): 
    print("YES")

# If there is only 1 character which
# does not balances then also it is Yes
elif (po == 1 and ne == 0): 
    print("YES")
elif (po == 0 and ne == -1):
    print("YES")
else:
    print("NO")
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{
public static void Main()
{
    string s = "ABCdcba" ;

    // creating a array which stores
    // the frequency of each character
    int[] u = new int[26];
    int n = s.Length ;

    for(int i = 0; i < n ; i++)
    {
        // Checking if a character is
        // uppercase or not
        if(Char.IsUpper(s[i]))
        {
            // Increasing by 1 if uppercase
            u[s[i] - 65] += 1 ;
        }
        else
        {
            // Decreasing by 1 if lower case
            u[s[i] - 97] -= 1 ;
        }
    }

    // Storing the sum of positive
    // numbers in the frequency array
    int po = 0 ;

    // Storing the sum of negative
    // numbers in the frequency array
    int ne = 0 ;

    for (int i = 0 ; i < 26 ; i++)
    {
        if (u[i] > 0)
            po += u[i] ;

        if (u[i] < 0)
            ne += u[i] ;
    }

    // If all character balances
    // out then its Yes
    if (po == 0 && ne == 0)
        Console.Write("YES"+"\n") ;

    // If there is only 1 character which
    // does not balances then also it is Yes
    else if (po == 1 && ne == 0)
        Console.Write("YES"+"\n") ;

    else if (po == 0 && ne == -1)
        Console.Write("YES" + "\n") ;

    else
        Console.Write("NO" + "\n") ;
}
}

// This code is contributed
// by ChitraNayal
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// driver code

     let s = "ABCdcba" ;

        // creating a array which stores the 
        // frequency of each character
        let u = Array(26).fill(0);
        let n = s.length ;

        for(let i = 0; i < n ; i++)
        {
            // Checking if a character is
            // uppercase or not
            if(s[i].toUpperCase())
            {
                // Increasing by 1 if uppercase
                u[s[i] - 65] += 1 ;
            }
            else
            {
                // Decreasing by 1 if lower case
                u[s[i] - 97] -= 1 ;
            }

        }
        let f1 = true ;

        // Storing the sum of positive 
        // numbers in the frequency array
        let po = 0 ;

        // Storing the sum of negative 
        // numbers in the frequency array
        let ne = 0 ;

        for (let i = 0 ; i < 26 ; i++)
        {
            if (u[i] > 0)
                po += u[i] ;

            if (u[i] < 0)
                ne += u[i] ;
        }

        // If all character balances out then its Yes
        if (po == 0 && ne == 0)
            document.write("YES") ;

        // If there is only 1 character which 
        // does not balances then also it is Yes
        else if (po == 1 && ne == 0)
            document.write("YES") ;

        else if (po == 0 && ne == -1)
            document.write("YES") ;

        else
            document.write("NO") ;

</script>
```

**Output:** 

```
YES
```