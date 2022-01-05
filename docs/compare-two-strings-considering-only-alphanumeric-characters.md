# 仅考虑字母数字字符比较两个字符串

> 原文:[https://www . geesforgeks . org/compare-two-string-仅考虑字母数字字符/](https://www.geeksforgeeks.org/compare-two-strings-considering-only-alphanumeric-characters/)

给定两个字符串，可以包含小写字母、数字和特殊字符，如点、空格、逗号等。如果两个字符串相等或不相等，请仅考虑字母数字字符([a-b]、[A-B]和[0-9])。例如，字符串“Ram，Shyam”和“Ram-Shyam”都是相同的，也是“/”。；[]”和“@# >”相同。

**示例:**

```
Input: str1 = "Ram, Shyam", str2 = " Ram - Shyam."
Output: Equal
Explanation: 
if we ignore all characters 
except alphanumeric characters 
then strings will be, 
str1 = "RamShyam" and str2 = "RamShyam". 
Therefore both strings are equal.

Input : str1 = "aaa123", str2 = "@aaa-12-3"
Output : Equal

Input : str1 = "abc123", str2 = "123abc"
Output : Unequal
Explanation: 
In this, str1 = "abc123" and str2 = "123abc". 
Therefore both strings are not equal.
```

因为我们必须只比较字母数字字符，所以只要发现任何其他字符，只需通过增加迭代器指针来忽略它。简单地取两个整数变量 I 和 j，用 0 初始化它们。现在运行一个循环来比较两个字符串的每个字符。如果字符是字母数字，则逐个比较，否则将 I 或 j 的值增加 1。

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

// Function to check alphanumeric equality of both strings
bool CompareAlphanumeric(string& str1, string& str2)
{
    // variable declaration
    int i, j;
    i = 0;
    j = 0;

    // Length of first string
    int len1 = str1.size();

    // Length of second string
    int len2 = str2.size();

    // To check each and every characters of both string
    while (i <= len1 && j <= len2) {

        // If the current character of the first string is not an
        // alphanumeric character, increase the pointer i
        while (i < len1
               && (!((str1[i] >= 'a' && str1[i] <= 'z')
                     || (str1[i] >= 'A' && str1[i] <= 'Z')
                     || (str1[i] >= '0' && str1[i] <= '9')))) {
            i++;
        }

        // If the current character of the second string is not an
        // alphanumeric character, increase the pointer j
        while (j < len2
               && (!((str2[j] >= 'a' && str2[j] <= 'z')
                     || (str2[j] >= 'A' && str2[j] <= 'Z')
                     || (str2[j] >= '0' && str2[j] <= '9')))) {
            j++;
        }

        // if all alphanumeric characters of both strings are same
        // then return true
        if (i == len1 && j == len2)
            return true;

        // if any alphanumeric characters of both strings are not same
        // then return false
        else if (str1[i] != str2[j])
            return false;

        // If current character matched,
        // increase both pointers to check the next character
        else {
            i++;
            j++;
        }
    }

    // If not same, then return false
    return false;
}

// Function to print Equal or Unequal if strings are same or not
void CompareAlphanumericUtil(string str1, string str2)
{
    bool res;

    // check alphanumeric equality of both strings
    res = CompareAlphanumeric(str1, str2);

    // if both are alphanumeric equal, print Equal
    if (res == true)
        cout << "Equal" << endl;

    // otherwise print Unequal
    else
        cout << "Unequal" << endl;
}

// Driver code
int main()
{

    string str1, str2;

    str1 = "Ram, Shyam";
    str2 = " Ram - Shyam.";
    CompareAlphanumericUtil(str1, str2);

    str1 = "abc123";
    str2 = "123abc";
    CompareAlphanumericUtil(str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to check alphanumeric
// equality of both strings
static boolean CompareAlphanumeric(char[] str1,
                                   char[] str2)
{
    // variable declaration
    int i, j;
    i = 0;
    j = 0;

    // Length of first string
    int len1 = str1.length;

    // Length of second string
    int len2 = str2.length;

    // To check each and every characters
    // of both string
    while (i <= len1 && j <= len2)
    {

        // If the current character of the first string is not an
        // alphanumeric character, increase the pointer i
        while (i < len1 && (!((str1[i] >= 'a' && str1[i] <= 'z') ||
                              (str1[i] >= 'A' && str1[i] <= 'Z') ||
                              (str1[i] >= '0' && str1[i] <= '9'))))
        {
            i++;
        }

        // If the current character of the second string is not an
        // alphanumeric character, increase the pointer j
        while (j < len2 && (!((str2[j] >= 'a' && str2[j] <= 'z') ||
                              (str2[j] >= 'A' && str2[j] <= 'Z') ||
                              (str2[j] >= '0' && str2[j] <= '9'))))
        {
            j++;
        }

        // if all alphanumeric characters of
        // both strings are same then return true
        if (i == len1 && j == len2)
        {
            return true;
        }

        // if any alphanumeric characters of
        // both strings are not same then return false
        else if (str1[i] != str2[j])
        {
            return false;
        }

        // If current character matched,
        // increase both pointers to
        // check the next character
        else
        {
            i++;
            j++;
        }
    }

    // If not same, then return false
    return false;
}

// Function to print Equal or Unequal
// if strings are same or not
static void CompareAlphanumericUtil(String str1,
                                    String str2)
{
    boolean res;

    // check alphanumeric equality of both strings
    res = CompareAlphanumeric(str1.toCharArray(),
                              str2.toCharArray());

    // if both are alphanumeric equal,
    // print Equal
    if (res == true)
    {
        System.out.println("Equal");
    }

    // otherwise print Unequal
    else
    {
        System.out.println("Unequal");
    }
}

// Driver code
public static void main(String[] args)
{
    String str1, str2;

    str1 = "Ram, Shyam";
    str2 = " Ram - Shyam.";
    CompareAlphanumericUtil(str1, str2);

    str1 = "abc123";
    str2 = "123abc";
    CompareAlphanumericUtil(str1, str2);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Function to check alphanumeric equality
# of both strings
def CompareAlphanumeric(str1, str2):

    # variable declaration
    i = 0
    j = 0

    # Length of first string
    len1 = len(str1)

    # Length of second string
    len2 = len(str2)

    # To check each and every character of both string
    while (i <= len1 and j <= len2):

        # If the current character of the first string
        # is not an alphanumeric character,
        # increase the pointer i
        while (i < len1 and
              (((str1[i] >= 'a' and str1[i] <= 'z') or
                (str1[i] >= 'A' and str1[i] <= 'Z') or
                (str1[i] >= '0' and str1[i] <= '9')) == False)):
            i += 1

        # If the current character of the second string
        # is not an alphanumeric character,
        # increase the pointer j
        while (j < len2 and
              (((str2[j] >= 'a' and str2[j] <= 'z') or
                (str2[j] >= 'A' and str2[j] <= 'Z') or
                (str2[j] >= '0' and str2[j] <= '9')) == False)):
            j += 1

        # if all alphanumeric characters of
        # both strings are same, then return true
        if (i == len1 and j == len2):
            return True

        # if any alphanumeric characters of
        # both strings are not same, then return false
        elif (str1[i] != str2[j]):
            return False

        # If current character matched,
        # increase both pointers
        # to check the next character
        else:
            i += 1
            j += 1

    # If not same, then return false
    return False

# Function to print Equal or Unequal
# if strings are same or not
def CompareAlphanumericUtil(str1, str2):

    # check alphanumeric equality of both strings
    res = CompareAlphanumeric(str1, str2)

    # if both are alphanumeric equal, print Equal
    if (res == True):
        print("Equal")

    # otherwise print Unequal
    else:
        print("Unequal")

# Driver code
if __name__ == '__main__':
    str1 = "Ram, Shyam"
    str2 = " Ram - Shyam."
    CompareAlphanumericUtil(str1, str2)

    str1 = "abc123"
    str2 = "123abc"
    CompareAlphanumericUtil(str1, str2)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to check alphanumeric
    // equality of both strings
    static bool CompareAlphanumeric(char []str1,
                                    char []str2)
    {
        // variable declaration
        int i, j;
        i = 0;
        j = 0;

        // Length of first string
        int len1 = str1.Length;

        // Length of second string
        int len2 = str2.Length;

        // To check each and every characters
        // of both string
        while (i <= len1 && j <= len2)
        {

            // If the current character of the first
            // string is not an alphanumeric character,
            // increase the pointer i
            while (i < len1 && (!((str1[i] >= 'a' && str1[i] <= 'z') ||
                                  (str1[i] >= 'A' && str1[i] <= 'Z') ||
                                  (str1[i] >= '0' && str1[i] <= '9'))))
            {
                i++;
            }

            // If the current character of the second
            // string is not an alphanumeric character,
            // increase the pointer j
            while (j < len2 && (!((str2[j] >= 'a' && str2[j] <= 'z') ||
                                  (str2[j] >= 'A' && str2[j] <= 'Z') ||
                                  (str2[j] >= '0' && str2[j] <= '9'))))
            {
                j++;
            }

            // if all alphanumeric characters of
            // both strings are same then return true
            if (i == len1 && j == len2)
            {
                return true;
            }

            // if any alphanumeric characters of
            // both strings are not same then return false
            else if (str1[i] != str2[j])
            {
                return false;
            }

            // If current character matched,
            // increase both pointers to
            // check the next character
            else
            {
                i++;
                j++;
            }
        }

        // If not same, then return false
        return false;
    }

    // Function to print Equal or Unequal
    // if strings are same or not
    static void CompareAlphanumericUtil(string str1,
                                        string str2)
    {
        bool res;

        // check alphanumeric equality of both strings
        res = CompareAlphanumeric(str1.ToCharArray(),
                                  str2.ToCharArray());

        // if both are alphanumeric equal,
        // print Equal
        if (res == true)
        {
            Console.WriteLine("Equal");
        }

        // otherwise print Unequal
        else
        {
            Console.WriteLine("Unequal");
        }
    }

    // Driver code
    public static void Main()
    {
        string str1, str2;

        str1 = "Ram, Shyam";
        str2 = " Ram - Shyam.";
        CompareAlphanumericUtil(str1, str2);

        str1 = "abc123";
        str2 = "123abc";
        CompareAlphanumericUtil(str1, str2);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to check alphanumeric
    // equality of both strings
    function CompareAlphanumeric(str1, str2)
    {
        // variable declaration
        let i, j;
        i = 0;
        j = 0;

        // Length of first string
        let len1 = str1.length;

        // Length of second string
        let len2 = str2.length;

        // To check each and every characters
        // of both string
        while (i <= len1 && j <= len2)
        {

            // If the current character of the first
            // string is not an alphanumeric character,
            // increase the pointer i
            while (i < len1 &&
            (!((str1[i].charCodeAt() >= 'a'.charCodeAt() &&
            str1[i].charCodeAt() <= 'z'.charCodeAt()) ||
            (str1[i].charCodeAt() >= 'A'.charCodeAt() &&
            str1[i].charCodeAt() <= 'Z'.charCodeAt()) ||
            (str1[i].charCodeAt() >= '0'.charCodeAt() &&
            str1[i].charCodeAt() <= '9'.charCodeAt()))))
            {
                i++;
            }

            // If the current character of the second
            // string is not an alphanumeric character,
            // increase the pointer j
            while (j < len2 &&
            (!((str2[j].charCodeAt() >= 'a'.charCodeAt() &&
            str2[j].charCodeAt() <= 'z'.charCodeAt()) ||
            (str2[j].charCodeAt() >= 'A'.charCodeAt() &&
            str2[j].charCodeAt() <= 'Z'.charCodeAt()) ||
            (str2[j].charCodeAt() >= '0'.charCodeAt() &&
            str2[j].charCodeAt() <= '9'.charCodeAt()))))
            {
                j++;
            }

            // if all alphanumeric characters of
            // both strings are same then return true
            if (i == len1 && j == len2)
            {
                return true;
            }

            // if any alphanumeric characters of
            // both strings are not same then return false
            else if (str1[i] != str2[j])
            {
                return false;
            }

            // If current character matched,
            // increase both pointers to
            // check the next character
            else
            {
                i++;
                j++;
            }
        }

        // If not same, then return false
        return false;
    }

    // Function to print Equal or Unequal
    // if strings are same or not
    function CompareAlphanumericUtil(str1, str2)
    {
        let res;

        // check alphanumeric equality of both strings
        res = CompareAlphanumeric(str1.split(''),
                                  str2.split(''));

        // if both are alphanumeric equal,
        // print Equal
        if (res == true)
        {
            document.write("Equal" + "</br>");
        }

        // otherwise print Unequal
        else
        {
            document.write("Unequal");
        }
    }

    let str1, str2;

    str1 = "Ram, Shyam";
    str2 = " Ram - Shyam.";
    CompareAlphanumericUtil(str1, str2);

    str1 = "abc123";
    str2 = "123abc";
    CompareAlphanumericUtil(str1, str2);

</script>
```

**Output:** 

```
Equal
Unequal
```