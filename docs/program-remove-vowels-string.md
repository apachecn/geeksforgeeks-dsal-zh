# 从字符串中删除元音的程序

> 原文:[https://www.geeksforgeeks.org/program-remove-vowels-string/](https://www.geeksforgeeks.org/program-remove-vowels-string/)

给定一个字符串，去掉字符串中的元音，打印不带元音的字符串。

**例:**

```
Input : welcome to geeksforgeeks
Output : wlcm t gksfrgks

Input : what is your name ?
Output : wht s yr nm ?
```

设计了一个循环，遍历由该字符串的字符组成的列表，删除元音，然后将它们连接起来。

## c++ 14

```
// C++ program to remove vowels from a String
#include <bits/stdc++.h>
using namespace std;

string remVowel(string str)
{
    vector<char> vowels = {'a', 'e', 'i', 'o', 'u',
                           'A', 'E', 'I', 'O', 'U'};

    for (int i = 0; i < str.length(); i++)
    {
        if (find(vowels.begin(), vowels.end(),
                      str[i]) != vowels.end())
        {
            str = str.replace(i, 1, "");
            i -= 1;
        }
    }
    return str;
}

// Driver Code
int main()
{
    string str = "GeeeksforGeeks - A Computer"
                 " Science Portal for Geeks";
    cout << remVowel(str) << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
// and corrected by alreadytaken
```

## Java

```
// Java program to remove vowels from a String

import java.util.Arrays;
import java.util.List;

class Test
{   
    static String remVowel(String str)
    {
         Character vowels[] = {'a', 'e', 'i', 'o', 'u','A','E','I','O','U'};

         List<Character> al = Arrays.asList(vowels);

         StringBuffer sb = new StringBuffer(str);

         for (int i = 0; i < sb.length(); i++) {

             if(al.contains(sb.charAt(i))){
                sb.replace(i, i+1, "") ;
                i--;
             }
        }

        return sb.toString();
    }
    // Driver method to test the above function
    public static void main(String[] args)
    {
        String str = "GeeeksforGeeks - A Computer Science Portal for Geeks";

        System.out.println(remVowel(str));
    }
}
```

## Python

```
# Python program to remove vowels from a string
# Function to remove vowels
def rem_vowel(string):
    vowels = ['a','e','i','o','u']
    result = [letter for letter in string if letter.lower() not in vowels]
    result = ''.join(result)
    print(result)

# Driver program
string = "GeeksforGeeks - A Computer Science Portal for Geeks"
rem_vowel(string)
string = "Loving Python LOL"
rem_vowel(string)
```

## c#

T3

## Javascript

```
<script>

// Javascript program to remove
// vowels from a String
function remVowel(str)
{
    let al = [ 'a', 'e', 'i', 'o', 'u',
               'A', 'E', 'I', 'O', 'U' ];
    let result = "";

    for(let i = 0; i < str.length; i++)
    {

        if (!al.includes(str[i]))
        {
            result += str[i];
        }
    }
    return result;
}

// Driver code
let str = "GeeeksforGeeks - A Computer Science " +
          "Portal for Geeks";
document.write(remVowel(str));

// This code is contributed by rag2127

</script>
```

T28】输出

```
GksfrGks -  Cmptr Scnc Prtl fr Gks

```