# 拆分数字字符串

> 原文:[https://www.geeksforgeeks.org/splitting-numeric-string/](https://www.geeksforgeeks.org/splitting-numeric-string/)

给定一个数字字符串(长度<= 32), split it into two or more integers( if possible), such that 
1)，当前数字和前一个数字的差值为 1。
2)没有数字包含前导零
如果可以分隔给定的数字串，则打印“**可能的**”后跟递增序列的第一个数字，否则打印“**不可能的**”。
**示例:**

```
Input : 1234
Output : Possible 1
Explanation: String can be split as "1", "2", 
"3", "4"

Input : 99100
Output :Possible 99
Explanation: String can be split as "99",
"100"

Input : 101103
Output : Not Possible
Explanation: It is not possible to split this 
string under given constraint.
```

**方法:**想法是从索引 0 到数值字符串的任何索引 i (i 从 1 开始)取一个子字符串，并将其转换为长数据类型。加 1，将增加的数字转换回字符串。检查下一个出现的子串是否等于增加的子串。如果是，则继续程序，否则增加 I 值并重复这些步骤。

## C++

```
// C++ program to split a numeric
// string in an Increasing
// sequence if possible
#include <bits/stdc++.h>
using namespace std;

// Function accepts a string and
// checks if string can be split.
void split(string str)
{
    int len = str.length();

    // if there is only 1 number
    // in the string then
    // it is not possible to split it
    if (len == 1) {
        cout << ("Not Possible");
        return;
    }

    string s1 = "", s2 = "";
    long num1, num2;

    for (int i = 0; i <= len / 2; i++) {

        int flag = 0;

        // storing the substring from
        // 0 to i+1 to form initial
        // number of the increasing sequence
        s1 = str.substr(0, i + 1);
        num1 = stoi((s1));
        num2 = num1 + 1;

        // convert string to integer
        // and add 1 and again convert
        // back to string s2
        s2 = to_string(num2);
        int k = i + 1;
        while (flag == 0) {
            int l = s2.length();

            // if s2 is not a substring
            // of number than not possible
            if (k + l > len) {
                flag = 1;
                break;
            }

            // if s2 is the next substring
            // of the numeric string
            if ((str.substr(k, k + l) == s2)) {
                flag = 0;

                // Increase num2 by 1 i.e the
                // next number to be looked for
                num2++;
                k = k + l;

                // check if string is fully
                // traversed then break
                if (k == len)
                    break;
                s2 = to_string(num2);
                l = s2.length();
                if (k + 1 > len) {

                    // If next string doesnot occurs
                    // in a given numeric string
                    // then it is not possible
                    flag = 1;
                    break;
                }
            }

            else
                flag = 1;
        }

        // if the string was fully traversed
        // and conditions were satisfied
        if (flag == 0) {
            cout << "Possible " << s1 << endl;
            break;
        }

        // if conditions failed to hold
        else if (flag == 1 && i > len / 2 - 1) {
            cout << "Not Possible" << endl;
            break;
        }
    }
}

// Driver code
int main()
{
    string str = "99100";

    // Call the split function
    // for splitting the string
    split(str);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split a numeric
// string in an Increasing
// sequence if possible
import java.io.*;
import java.util.*;

class GFG {

    // Function accepts a string and
    // checks if string can be split.
    public static void split(String str)
    {
        int len = str.length();

        // if there is only 1 number
        // in the string then
        // it is not possible to split it
        if (len == 1) {
            System.out.println("Not Possible");
            return;
        }

        String s1 = "", s2 = "";
        long num1, num2;

        for (int i = 0; i <= len / 2; i++) {

            int flag = 0;

            // storing the substring from
            // 0 to i+1 to form initial
            // number of the increasing sequence
            s1 = str.substring(0, i + 1);
            num1 = Long.parseLong((s1));
            num2 = num1 + 1;

            // convert string to integer
            // and add 1 and again convert
            // back to string s2
            s2 = Long.toString(num2);
            int k = i + 1;
            while (flag == 0) {
                int l = s2.length();

                // if s2 is not a substring
                // of number than not possible
                if (k + l > len) {
                    flag = 1;
                    break;
                }

                // if s2 is the next substring
                // of the numeric string
                if ((str.substring(k, k + l).equals(s2))) {
                    flag = 0;

                    // Increase num2 by 1 i.e the
                    // next number to be looked for
                    num2++;
                    k = k + l;

                    // check if string is fully
                    // traversed then break
                    if (k == len)
                        break;
                    s2 = Long.toString(num2);
                    l = s2.length();
                    if (k + 1 > len) {

                        // If next string doesnot occurs
                        // in a given numeric string
                        // then it is not possible
                        flag = 1;
                        break;
                    }
                }

                else
                    flag = 1;
            }

            // if the string was fully traversed
            // and conditions were satisfied
            if (flag == 0) {
                System.out.println("Possible"
                                   + " " + s1);
                break;
            }

            // if conditions failed to hold
            else if (flag == 1 && i > len / 2 - 1) {
                System.out.println("Not Possible");
                break;
            }
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        Scanner in = new Scanner(System.in);
        String str = "99100";

        // Call the split function
        // for splitting the string
        split(str);
    }
}
```

## 蟒蛇 3

```
# Python3 program to split a numeric
# string in an Increasing
# sequence if possible

# Function accepts a string and
# checks if string can be split.
def split(Str) :
    Len = len(Str)

    # if there is only 1 number
    # in the string then
    # it is not possible to split it
    if (Len == 1) :
        print("Not Possible")
        return

    s1, s2 = "", ""
    for i in range((Len // 2) + 1) :
        flag = 0

        # storing the substring from
        # 0 to i+1 to form initial
        # number of the increasing sequence
        s1 = Str[0 : i + 1]
        num1 = int(s1)
        num2 = num1 + 1

        # convert string to integer
        # and add 1 and again convert
        # back to string s2
        s2 = str(num2)
        k = i + 1
        while (flag == 0) :
            l = len(s2)

            # if s2 is not a substring
            # of number than not possible
            if (k + l > Len) :
                flag = 1
                break

            # if s2 is the next substring
            # of the numeric string
            if ((Str[k : k + l] == s2)) :
                flag = 0

                # Increase num2 by 1 i.e the
                # next number to be looked for
                num2 += 1
                k = k + l

                # check if string is fully
                # traversed then break
                if (k == Len) :
                    break
                s2 = str(num2)
                l = len(s2)
                if (k + 1 > len) :

                    # If next string doesnot occurs
                    # in a given numeric string
                    # then it is not possible
                    flag = 1
                    break
            else :
                flag = 1

        # if the string was fully traversed
        # and conditions were satisfied
        if (flag == 0) :
            print("Possible",  s1)
            break

        # if conditions failed to hold
        elif (flag == 1 and i > (Len // 2) - 1) :
            print("Not Possible")
            break

# Driver code       
Str = "99100"

# Call the split function
# for splitting the string
split(Str)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to split a numeric
// string in an Increasing
// sequence if possible
using System;

class GFG
{

// Function accepts a
// string and checks if
// string can be split.
static void split(string str)
{
    int len = str.Length;

    // if there is only 1
    // number in the string
    // then it is not possible
    // to split it
    if (len == 1)
    {
        Console.WriteLine("Not Possible");
        return;
    }

    string s1 = "", s2 = "";
    long num1, num2;

    for (int i = 0; i < len / 2; i++)
    {

        int flag = 0;

        // storing the substring
        // from 0 to i+1 to form
        // initial number of the
        // increasing sequence
        s1 = str.Substring(0, i + 1);
        num1 = Convert.ToInt64((s1));
        num2 = num1 + 1;

        // convert string to integer
        // and add 1 and again convert
        // back to string s2
        s2 = num2.ToString();
        int k = i + 1;
        while (flag == 0)
        {
            int l = s2.Length;

            // if s2 is not a substring
            // of number than not possible
            if (k + l > len)
            {
                flag = 1;
                break;
            }

            // if s2 is the next
            // substring of the
            // numeric string
            if ((str.Substring(k, l).Equals(s2)))
            {
                flag = 0;

                // Increase num2 by 1 i.e
                // the next number to be
                // looked for
                num2++;
                k = k + l;

                // check if string is fully
                // traversed then break
                if (k == len)
                    break;
                s2 = num2.ToString();
                l = s2.Length;
                if (k + 1 > len)
                {

                    // If next string doesnot
                    // occurs in a given numeric
                    // string then it is not
                    // possible
                    flag = 1;
                    break;
                }
            }

            else
                flag = 1;
        }

        // if the string was fully
        // traversed and conditions
        // were satisfied
        if (flag == 0)
        {
            Console.WriteLine("Possible" +
                                " " + s1);
            break;
        }

        // if conditions
        // failed to hold
        else if (flag == 1 &&
                 i > len / 2 - 1)
        {
            Console.WriteLine("Not Possible");
            break;
        }
    }
}

// Driver Code
static void Main()
{
    string str = "99100";

    // Call the split function
    // for splitting the string
    split(str);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

**输出:**

```
Possible 99
```