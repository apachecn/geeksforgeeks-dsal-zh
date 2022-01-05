# 强密码提示程序

> 原文:[https://www . geesforgeks . org/strong-密码-建议者-程序/](https://www.geeksforgeeks.org/strong-password-suggester-program/)

给定一个用户输入的密码，检查它的强度，如果不是很强，建议一些密码。

**强密码的标准如下:**
一个密码如果有就强:
1。至少 8 个字符
2。至少一个特殊字符
3。至少一个数字
4。至少一个大写和一个小写字符。

示例:

```
Input : keshav123
Output : Suggested Password
k(eshav12G3
keshav1@A23
kesh!Aav123
ke(shav12V3
keGshav1$23
kesXhav@123
keAshav12$3
kesKhav@123
kes$hav12N3
$kesRhav123

Input :rakesh@1995kumar
Output : Your Password is Strong
```

**方法:**
检查输入密码的强度，如果满足所有条件，则为强密码，否则检查其中缺失的字符，并将随机生成的密码返回给用户。

## C++

```
// CPP code to suggest strong password
#include <bits/stdc++.h>

using namespace std;

// adding more characters to suggest strong password
string add_more_char(string str, int need)
{
    int pos = 0;

    // all 26 letters
    string low_case = "abcdefghijklmnopqrstuvwxyz";

    for (int i = 0; i < need; i++) {
        pos = rand() % str.length();
        str.insert(pos, 1, low_case[rand() % 26]);
    }
    return str;
}

// make powerful string
string suggester(int l, int u, int d, int s, string str)
{

    // all digits
    string num = "0123456789";

    // all lower case, uppercase and special characters
    string low_case = "abcdefghijklmnopqrstuvwxyz";
    string up_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    string spl_char = "@#$_()!";

    // position at which place a character
    int pos = 0;

    // if there is no lowercase char in input string, add it
    if (l == 0) {
        // generate random integer under string length
        pos = rand() % str.length();

        // generate random integer under 26 for indexing of a to z
        str.insert(pos, 1, low_case[rand() % 26]);
    }

    // if there is no upper case char in input string, add it
    if (u == 0) {
        pos = rand() % str.length();
        str.insert(pos, 1, up_case[rand() % 26]);
    }

    // if there is no digit in input string, add it
    if (d == 0) {
        pos = rand() % str.length();
        str.insert(pos, 1, num[rand() % 10]);
    }

    // if there is no special character in input string, add it
    if (s == 0) {
        pos = rand() % str.length();
        str.insert(pos, 1, spl_char[rand() % 7]);
    }

    return str;
}

/* make_password function :This function is used to check
strongness and if input string is not strong, it will suggest*/
void generate_password(int n, string p)
{
    // flag for lower case, upper case, special
    // characters and need of more characters
    int l = 0, u = 0, d = 0, s = 0, need = 0;

    // password suggestions.
    string suggest;

    for (int i = 0; i < n; i++) {
        // password suggestions.
        if (p[i] >= 97 && p[i] <= 122)
            l = 1;
        else if (p[i] >= 65 && p[i] <= 90)
            u = 1;
        else if (p[i] >= 48 && p[i] <= 57)
            d = 1;
        else
            s = 1;
    }

    // Check if input string is strong that
    // means all flag are active.
    if ((l + u + d + s) == 4) {
        cout << "Your Password is Strong" << endl;
        return;
    }
    else
        cout << "Suggested password " << endl;

    /*suggest 10 strong strings */
    for (int i = 0; i < 10; i++) {
        suggest = suggester(l, u, d, s, p);
        need = 8 - suggest.length();
        if (need > 0)
            suggest = add_more_char(suggest, need);
        cout << suggest << endl;
    }
}

// Driver code
int main()
{
    string input_string = "geek@2018";
    srand(time(NULL));

    // srand function set Seed for rand().
    generate_password(input_string.length(), input_string);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to suggest strong password
import java.io.*;
import java.util.*;
import java.util.Random;

public class GFG {

    // adding more characters to suggest
    // strong password
    static StringBuilder add_more_char(
                        StringBuilder str, int need)
    {
        int pos = 0;
        Random randm = new Random();

        // all 26 letters
        String low_case = "abcdefghijklmnopqrstuvwxyz";

        for (int i = 0; i < need; i++) {
            pos = randm.nextInt(1000) % str.length();
            str.setCharAt(pos,low_case.charAt(
                            randm.nextInt(1000) % 26));
        }
        return str;
    }

    // make powerful String
    static StringBuilder suggester(int l, int u, int d,
                              int s, StringBuilder str)
    {
        Random randm = new Random();

        // all digits
        String num = "0123456789";

        // all lower case, uppercase and special
        // characters
        String low_case = "abcdefghijklmnopqrstuvwxyz";
        String up_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String spl_char = "@#$_()!";

        // position at which place a character
        int pos = 0;

        // if there is no lowercase char in input
        // String, add it
        if (l == 0) {

            // generate random integer under
            // String length()
            pos = randm.nextInt(1000) % str.length();

            // generate random integer under 26 for
            // indexing of a to z
            str.setCharAt(pos,low_case.charAt(randm.nextInt(1000)
                                        % 26));
        }

        // if there is no upper case char in input
        // String, add it
        if (u == 0) {
            pos = randm.nextInt(1000) % str.length();
            str.setCharAt(pos,low_case.charAt(randm.nextInt(1000)
                                        % 26));
        }

        // if there is no digit in input String, add it
        if (d == 0) {
            pos = randm.nextInt(1000) % str.length();
            str.setCharAt(pos,low_case.charAt(randm.nextInt(1000)
                                        % 10));
        }

        // if there is no special character in input
        // String, add it
        if (s == 0) {
            pos = randm.nextInt(1000) % str.length();
            str.setCharAt(pos,low_case.charAt(randm.nextInt(1000)
                                        % 7));
        }

        return str;
    }

    /* make_password function :This function is used
    to check strongness and if input String is not
    strong, it will suggest*/
    static void generate_password(int n, StringBuilder p)
    {

        // flag for lower case, upper case, special
        // characters and need of more characters
        int l = 0, u = 0, d = 0, s = 0, need = 0;

        // password suggestions.
        StringBuilder suggest;

        for (int i = 0; i < n; i++) {

            // password suggestions.
            if (p.charAt(i) >= 97 && p.charAt(i) <= 122)
                l = 1;
            else if (p.charAt(i) >= 65 && p.charAt(i) <= 90)
                u = 1;
            else if (p.charAt(i) >= 48 && p.charAt(i) <= 57)
                d = 1;
            else
                s = 1;
        }

        // Check if input String is strong that
        // means all flag are active.
        if ((l + u + d + s) == 4) {
            System.out.println("Your Password is Strong");
            return;
        }
        else
            System.out.println("Suggested password ");

        /*suggest 10 strong Strings */
        for (int i = 0; i < 10; i++) {
            suggest = suggester(l, u, d, s, p);
            need = 8 - suggest.length();
            if (need > 0)
                suggest = add_more_char(suggest, need);
            System.out.println(suggest);;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        StringBuilder input_String = new StringBuilder("geek@2018");
        generate_password(input_String.length(), input_String);
    }
}

// This code is contributed by Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python code to suggest strong password

import random

# Function to insert character in a string
# Because string is immutable in python
def insert(s, pos, ch):
        return(s[:pos] + ch + s[pos:])

# adding more characters to
# suggest strong password
def add_more_char(s, need):
        pos = 0

        # add 26 letters
        low_case = "abcdefghijklmnopqrstuvwxyz"

        for i in range(need):
                pos = random.randint(0, len(s)-1)
                s = insert(s, pos, low_case[random.randint(0,25)])

        return(s)

# Make powerful string
def suggester(l, u, d, s, st):

        # all digits
        num = '0123456789'

        # all lower case, upper case and special characters
        low_case = "abcdefghijklmnopqrstuvwxyz"
        up_case = low_case.upper()
        spl_char = '@#$_()!'

        # Position at which place a character
        pos = 0

        # If there is no lowercase char
        # in input string, add it
        if( l == 0 ):

                # Generate random integer under string length
                pos = random.randint(0,len(st)-1)

                # Generate random integer under 26 for indexing of a to z
                st = insert(st, pos, low_case[random.randint(0,25)])

        # If there is no upper case char in input string, add it
        if( u == 0 ):

                # Generate random integer under string length
                pos = random.randint(0,len(st)-1)

                # Generate random integer under 26 for indexing of A to Z
                st = insert(st, pos, up_case[random.randint(0,25)])

        # If there is no digit in input string, add it
        if( d == 0 ):

                # Generate random integer under string length
                pos = random.randint(0,len(st)-1)

                # Generate random integer under 10 for indexing of 0 to 9
                st = insert(st, pos, num[random.randint(0,9)])

        # If there is no special character
        # in input string, add it
        if( s == 0 ):

                # Generate random integer under string length
                pos = random.randint(0,len(st)-1)

                # Generate random integer under 7 for
                # indexing of special characters
                st = insert(st, pos, low_case[random.randint(0,6)])

        return st

# generate_password function : This function is used to check
# strength and if input string is not strong, It will suggest
def generate_password(n, p):

        # flag for lower case, upper case, special
        # characters and need of more characters
        l = 0; u = 0; d = 0; s = 0; need = 0

        # Password suggestions
        suggest = ''

        for i in range(n):

                # Password suggestion
                if( p[i].islower() ):
                        l = 1
                elif( p[i].isupper() ):
                        u = 1
                elif( p[i].isdigit() ):
                        d = 1
                else:
                        s = 1

        # Check if input string is strong that
        # means all flags are active
        if( (l + u + d + s) == 4):
                print("Your Password is Strong")
                return
        else:
                print("Suggested Passwords")

        # Suggest 10 strong strings
        for i in range(10):
                suggest = suggester(l, u, d, s, p)
                need = 8 - len(suggest)

                if(need > 0):
                        suggest = add_more_char(suggest, need)
                print(suggest)

# Driver Code
input_string = 'geek@2018'

generate_password( len(input_string), input_string)

# This code is contributed by Arjun Saini
```

## C#

```
// C# code to suggest strong password
using System;
using System.Collections.Generic;

class GFG {

    // adding more characters to suggest
    // strong password
    static string add_more_char(string str, int need)
    {
        int pos = 0;
        Random randm = new Random();

        // all 26 letters
        string low_case = "abcdefghijklmnopqrstuvwxyz";

        for (int i = 0; i < need; i++) {
            pos = randm.Next(1,1000) % str.Length;
            str = str.Insert(pos,low_case[randm.Next(1000)
                                        % 26].ToString());
        }
        return str;
    }

    // make powerful string
    static string suggester(int l, int u, int d, int s,
                                             string str)
    {
        Random randm = new Random();

        // all digits
        string num = "0123456789";

        // all lower case, uppercase and special
        // characters
        string low_case = "abcdefghijklmnopqrstuvwxyz";
        string up_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        string spl_char = "@#$_()!";

        // position at which place a character
        int pos = 0;

        // if there is no lowercase char in input
        // string, add it
        if (l == 0) {

            // generate random integer under
            // string length
            pos = randm.Next(1,1000) % str.Length;

            // generate random integer under 26 for
            // indexing of a to z
            str = str.Insert(pos,low_case[randm.Next(1,
                                 1000) % 26].ToString());
        }

        // if there is no upper case char in input
        // string, add it
        if (u == 0) {
            pos = randm.Next(1,1000) % str.Length;
            str = str.Insert(pos,up_case[randm.Next(
                              1,1000) % 26].ToString());
        }

        // if there is no digit in input string, add it
        if (d == 0) {
            pos = randm.Next(1,1000) % str.Length;
            str = str.Insert(pos,num[randm.Next(1,1000)
                                      % 10].ToString());
        }

        // if there is no special character in input
        // string, add it
        if (s == 0) {
            pos = randm.Next(1,1000) % str.Length;
            str = str.Insert(pos,spl_char[randm.Next(
                              1,1000) % 7].ToString());
        }

        return str;
    }

    /* make_password function :This function is used
    to check strongness and if input string is not
    strong, it will suggest*/
    static void generate_password(int n, string p)
    {

        // flag for lower case, upper case, special
        // characters and need of more characters
        int l = 0, u = 0, d = 0, s = 0, need = 0;

        // password suggestions.
        string suggest;

        for (int i = 0; i < n; i++) {

            // password suggestions.
            if (p[i] >= 97 && p[i] <= 122)
                l = 1;
            else if (p[i] >= 65 && p[i] <= 90)
                u = 1;
            else if (p[i] >= 48 && p[i] <= 57)
                d = 1;
            else
                s = 1;
        }

        // Check if input string is strong that
        // means all flag are active.
        if ((l + u + d + s) == 4) {
            Console.WriteLine("Your Password is Strong\n");
            return;
        }
        else
            Console.WriteLine("Suggested password\n ");

        /*suggest 10 strong strings */
        for (int i = 0; i < 10; i++) {
            suggest = suggester(l, u, d, s, p);
            need = 8 - suggest.Length;
            if (need > 0)
                suggest = add_more_char(suggest, need);
            Console.WriteLine(suggest + "\n");;
        }
    }

    // Driver code
    public static void Main()
    {
        string input_string = "geek@2018";
        generate_password(input_string.Length, input_string);
    }
}

// This code is contributed by Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php code to suggest
// strong password

// adding more characters to
// suggest strong password
function add_more_char( $str, $need)
{
    $pos = 0;

    // all 26 letters
    $low_case = "abcdefghijklmnopqrstuvwxyz";

    for ($i = 0; $i < $need; $i++)
    {
        $pos = rand() % strlen($str);
        $str[$pos]=$low_case[rand() % 26];
    }
    return $str;
}

// make powerful string
function suggester($l, $u, $d, $s, $str)
{

    // all digits
    $num = "0123456789";

    // all lower case, uppercase and
    // special characters
    $low_case = "abcdefghijklmnopqrstuvwxyz";
    $up_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    // $spl_char1 = "@#$_()!";
    // position at which place
    // a character
    $pos = 0;

    // if there is no lowercase char
    // in input string, add it
    if ($l == 0)
    {

        // generate random integer
        // under string length
        $pos = rand() % strlen($str);

        // generate random integer under
        // 26 for indexing of a to z
        $str[$pos]=$low_case[rand() % 26];
    }

    // if there is no upper case
    // char in input string, add it
    if ($u == 0)
    {
        $pos = rand() % strlen($str);
        $str[$pos]=$up_case[rand() % 26];
    }

    // if there is no digit
    // in input string, add it
    if ($d == 0) {
        $pos = rand() % strlen($str);
        $str[$pos]=$num[rand() % 10];
    }

    // if there is no special character
    // in input string, add it
    if ($s == 0)
    {
        $pos = rand() % strlen($str);
        $str[$pos]=$spl_char1[rand() % 7];
    }

    return $str;
}

// Make_password function : This
// function is used to check
// strongness and if input string
// is not strong, it will suggest
function generate_password($n, $p)
{

    // flag for lower case, upper case,
    // special characters and need
    // of more characters
    $l = 0;
    $u = 0;
    $d = 0;
    $s = 0;
    $need = 0;

    // password suggestions.
    $suggest;

    for ($i = 0; $i < $n; $i++)
    {
        // password suggestions.
        if ($p[$i] >= 97 && $p[$i] <= 122)
            $l = 1;
        else if ($p[$i] >= 65 && $p[$i] <= 90)
            $u = 1;
        else if ($p[$i] >= 48 && $p[$i] <= 57)
            $d = 1;
        else
            $s = 1;
    }

    // Check if input string is strong
    // that means all flag are active.
    if (($l + $u + $d + $s) == 4)
    {
        echo "Your Password is Strong.\n";
        return;
    }
    else
        echo "Suggested password";

    // suggest 10 strong strings
    for ($i = 0; $i < 10; $i++)
    {
        $suggest = suggester($l, $u, $d, $s, $p);
        $need = 8 - strlen($suggest);
        if ($need > 0)
            $suggest = add_more_char($suggest, $need);
        echo "\n".$suggest;
    }
}

    // Driver code
    $input_string = "geek@2018";
    srand(mktime(NULL));

    // srand function set Seed for rand().
    generate_password(strlen($input_string),
                      $input_string);

// This code is contributed by mits
?>
```

**Output:** 

```
Suggested password 
geek@201K8
geek@201S8
gOeek@2018
geek@201N8
geek@2P018
geek@D2018
geUek@2018
geek@2Q018
geek@2F018
geekZ@2018
```

**时间复杂度:O(n)。**