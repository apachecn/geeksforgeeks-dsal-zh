# 用姓氏打印姓名首字母的程序

> 原文:[https://www . geeksforgeeks . org/program-to-print-姓名首字母搭配姓氏/](https://www.geeksforgeeks.org/program-to-print-the-initials-of-a-name-with-the-surname/)

给定一个字符串形式的全名，任务是打印名字的首字母，简而言之，以及完整的姓氏。

**示例:**

```
Input: Devashish Kumar Gupta
Output: D. K. Gupta

Input: Ishita Bhuiya
Output: I. Bhuiya

```

**做法:**基本做法是一个个提取单词，然后打印单词的第一个字母，后面跟着一个点(。).对于姓氏，提取并打印整个单词。

以下是上述方法的实现:

## C++

```
// C++ program to print the initials
// of a name with the surname
#include <bits/stdc++.h>
using namespace std;

void printInitials(string str) 
{
    int len = str.length();

    // to remove any leading or trailing spaces
    str.erase(0, str.find_first_not_of(' '));
    str.erase(str.find_last_not_of(' ') + 1);

    // to store extracted words
    string t = "";
    for (int i = 0; i < len; i++) 
    {
        char ch = str[i];

        if (ch != ' ')

            // forming the word
            t = t + ch;

        // when space is encountered
        // it means the name is completed
        // and thereby extracted
        else
        {
            // printing the first letter
            // of the name in capital letters
            cout << (char)toupper(t[0]) << ". ";
            t = "";
        }
    }

    string temp = "";

    // for the surname, we have to print the entire
    // surname and not just the initial
    // string "t" has the surname now
    for (int j = 0; j < t.length(); j++) 
    {
        // first letter of surname in capital letter
        if (j == 0) temp = temp + (char)toupper(t[0]);

        // rest of the letters in small
        else
            temp = temp + (char)tolower(t[j]);
    }

    // printing surname
    cout << temp << endl;
}

// Driver Code
int main() 
{
    string str = "ishita bhuiya";
    printInitials(str);
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the initials
// of a name with the surname
import java.util.*;

class Initials {
    public static void printInitials(String str)
    {
        int len = str.length();

        // to remove any leading or trailing spaces
        str = str.trim();

        // to store extracted words
        String t = "";
        for (int i = 0; i < len; i++) {
            char ch = str.charAt(i);

            if (ch != ' ') {

                // forming the word
                t = t + ch;
            }

            // when space is encountered
            // it means the name is completed
            // and thereby extracted
            else {
                // printing the first letter
                // of the name in capital letters
                System.out.print(Character.toUpperCase(t.charAt(0))
                                 + ". ");
                t = "";
            }
        }

        String temp = "";

        // for the surname, we have to print the entire
        // surname and not just the initial
        // string "t" has the surname now
        for (int j = 0; j < t.length(); j++) {

            // first letter of surname in capital letter
            if (j == 0)
                temp = temp + Character.toUpperCase(t.charAt(0));

            // rest of the letters in small
            else
                temp = temp + Character.toLowerCase(t.charAt(j));
        }

        // printing surname
        System.out.println(temp);
    }

    public static void main(String[] args)
    {
        String str = "ishita bhuiya";
        printInitials(str);
    }
}
```

## 蟒蛇 3

```
# Python program to print the initials
# of a name with the surname
def printInitials(string: str):
    length = len(string)

    # to remove any leading or trailing spaces
    string.strip()

    # to store extracted words
    t = ""
    for i in range(length):
        ch = string[i]
        if ch != ' ':

            # forming the word
            t += ch

        # when space is encountered
        # it means the name is completed
        # and thereby extracted
        else:

            # printing the first letter
            # of the name in capital letters
            print(t[0].upper() + ". ", end="")
            t = ""

    temp = ""

    # for the surname, we have to print the entire
    # surname and not just the initial
    # string "t" has the surname now
    for j in range(len(t)):

        # first letter of surname in capital letter
        if j == 0:
            temp += t[0].upper()

        # rest of the letters in small
        else:
            temp += t[j].lower()

    # printing surname
    print(temp)

# Driver Code
if __name__ == "__main__":

    string = "ishita bhuiya"
    printInitials(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print the initials 
// of a name with the surname 
using System;

class Initials { 

    public static void printInitials(string str) 
    { 
        int len = str.Length ;

        // to remove any leading or trailing spaces 
        str = str.Trim(); 

        // to store extracted words 
        String t = ""; 
        for (int i = 0; i < len; i++) { 
            char ch = str[i]; 

            if (ch != ' ') { 

                // forming the word 
                t = t + ch; 
            } 

            // when space is encountered 
            // it means the name is completed 
            // and thereby extracted 
            else { 
                // printing the first letter 
                // of the name in capital letters 
                Console.Write(Char.ToUpper(t[0]) 
                                + ". "); 
                t = ""; 
            } 
        } 

        string temp = ""; 

        // for the surname, we have to print the entire 
        // surname and not just the initial 
        // string "t" has the surname now 
        for (int j = 0; j < t.Length; j++) { 

            // first letter of surname in capital letter 
            if (j == 0) 
                temp = temp + Char.ToUpper(t[0]); 

            // rest of the letters in small 
            else
                temp = temp + Char.ToLower(t[j]); 
        } 

        // printing surname 
        Console.WriteLine(temp); 
    } 

    public static void Main() 
    { 
        string str = "ishita bhuiya"; 
        printInitials(str); 
    } 
    // This code is contributed by Ryuga
} 
```

**Output:**

```
I. Bhuiya

```