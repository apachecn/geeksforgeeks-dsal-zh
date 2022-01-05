# 检查弦是否相互旋转的程序

> 原文:[https://www . geesforgeks . org/a-program-to-check-如果字符串是相互旋转的/](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)

给定一个字符串 s1 和一个字符串 s2，写一个片段来说明 s2 是否是 s1 的旋转？
(如给定 s1 = ABCD，s2 = CDAB，返回真，给定 s1 = ABCD，s2 = ACBD，返回假)

**算法:**旋转(str1，str2)

```
    1\. Create a temp string and store concatenation of str1 to
       str1 in temp.
                          temp = str1.str1
    2\. If str2 is a substring of temp then str1 and str2 are 
       rotations of each other.

    Example:                 
                     str1 = "ABACD"
                     str2 = "CDABA"

     temp = str1.str1 = "ABACDABACD"
     Since str2 is a substring of temp, str1 and str2 are 
     rotations of each other.
```

## C++

```
// C++ program to check if two given strings
// are rotations of  each other
# include <bits/stdc++.h>
using namespace std;

/* Function checks if passed strings (str1
   and str2) are rotations of each other */
bool areRotations(string str1, string str2)
{
   /* Check if sizes of two strings are same */
   if (str1.length() != str2.length())
        return false;

   string temp = str1 + str1;
  return (temp.find(str2) != string::npos);
}

/* Driver program to test areRotations */
int main()
{
   string str1 = "AACD", str2 = "ACDA";
   if (areRotations(str1, str2))
     printf("Strings are rotations of each other");
   else
      printf("Strings are not rotations of each other");
   return 0;
}
```

## C

```
// C program to check if two given strings are rotations of
// each other
# include <stdio.h>
# include <string.h>
# include <stdlib.h>

/* Function checks if passed strings (str1 and str2)
   are rotations of each other */
int areRotations(char *str1, char *str2)
{
  int size1   = strlen(str1);
  int size2   = strlen(str2);
  char *temp;
  void *ptr;

  /* Check if sizes of two strings are same */
  if (size1 != size2)
     return 0;

  /* Create a temp string with value str1.str1 */
  temp   = (char *)malloc(sizeof(char)*(size1*2 + 1));
  temp[0] = '';
  strcat(temp, str1);
  strcat(temp, str1);

  /* Now check if str2 is a substring of temp */
  ptr = strstr(temp, str2);

  free(temp); // Free dynamically allocated memory

  /* strstr returns NULL if the second string is NOT a
    substring of first string */
  if (ptr != NULL)
    return 1;
  else
    return 0;
}

/* Driver program to test areRotations */
int main()
{
    char *str1 = "AACD";
    char *str2 = "ACDA";

    if (areRotations(str1, str2))
       printf("Strings are rotations of each other");
    else
       printf("Strings are not rotations of each other");

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two given strings are rotations of
// each other

class StringRotation
{
    /* Function checks if passed strings (str1 and str2)
       are rotations of each other */
    static boolean areRotations(String str1, String str2)
    {
        // There lengths must be same and str2 must be
        // a substring of str1 concatenated with str1. 
        return (str1.length() == str2.length()) &&
               ((str1 + str1).indexOf(str2) != -1);
    }

    // Driver method
    public static void main (String[] args)
    {
        String str1 = "AACD";
        String str2 = "ACDA";

        if (areRotations(str1, str2))
            System.out.println("Strings are rotations of each other");
        else
            System.out.printf("Strings are not rotations of each other");
    }
}
// This code is contributed by  munjal
```

## 计算机编程语言

```
# Python program to check if strings are rotations of
# each other or not

# Function checks if passed strings (str1 and str2)
# are rotations of each other
def areRotations(string1, string2):
    size1 = len(string1)
    size2 = len(string2)
    temp = ''

    # Check if sizes of two strings are same
    if size1 != size2:
        return 0

    # Create a temp string with value str1.str1
    temp = string1 + string1

    # Now check if str2 is a substring of temp
    # string.count returns the number of occurrences of
    # the second string in temp
    if (temp.count(string2)> 0):
        return 1
    else:
        return 0

# Driver program to test the above function
string1 = "AACD"
string2 = "ACDA"

if areRotations(string1, string2):
    print "Strings are rotations of each other"
else:
    print "Strings are not rotations of each other"

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to check if two given strings
// are rotations of each other
using System;

class GFG {

    /* Function checks if passed strings
    (str1 and str2) are rotations of
    each other */
    static bool areRotations(String str1,
                                 String str2)
    {

        // There lengths must be same and
        // str2 must be a substring of
        // str1 concatenated with str1.
        return (str1.Length == str2.Length )
             && ((str1 + str1).IndexOf(str2)
                                     != -1);
    }

    // Driver method
    public static void Main ()
    {
        String str1 = "FGABCDE";
        String str2 = "ABCDEFG";

        if (areRotations(str1, str2))
            Console.Write("Strings are"
            + " rotation s of each other");
        else
            Console.Write("Strings are "
           + "not rotations of each other");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to check if
// two given strings are
// rotations of each other

/* Function checks if passed
strings (str1 and str2) are
rotations of each other */
function areRotations($str1, $str2)
{
/* Check if sizes of two
   strings are same */
if (strlen($str1) != strlen($str2))
{
        return false;
}

$temp = $str1 + $str1;
if ($temp.count($str2)> 0)
{
        return true;
}
else
{
    return false;
}
}

// Driver code
$str1 = "AACD";
$str2 = "ACDA";
if (areRotations($str1, $str2))
{
    echo "Strings are rotations ".
                  "of each other";
}
else
{
    echo "Strings are not " .
         "rotations of each other" ;
}

// This code is contributed
// by Shivi_Aggarwal.
?>
```

## java 描述语言

```
<script>
// javascript program to check if two given strings are rotations of
// each other

    /* Function checks if passed strings (str1 and str2)
       are rotations of each other */
    function areRotations( str1,  str2)
    {
        // There lengths must be same and str2 must be
        // a substring of str1 concatenated with str1. 
        return (str1.length == str2.length) &&
               ((str1 + str1).indexOf(str2) != -1);
    }

    // Driver method

        var str1 = "AACD";
        var str2 = "ACDA";

        if (areRotations(str1, str2))
            document.write("Strings are rotations of each other");
        else
            document.write("Strings are not rotations of each other");

// This code is contributed by umadevi9616
</script>
```

**Output**

```
Strings are rotations of each other
```

**方法 2(使用 STL):**

**算法:**

1.如果两个字符串的大小不相等，那么就永远不可能。

2.将原字符串推入队列 **q1** 。

3.将待检查的字符串推入另一个队列 **q2** 。

4.继续弹出 **q2** ，并将其推回其中，直到此类操作的次数小于管柱的大小。

5.如果 **q2** 在这些操作中的任何一点变得等于 **q1** ，这是可能的。否则不行。

## C++

```
#include <bits/stdc++.h>
using namespace std;
bool check_rotation(string s, string goal)
{
    if (s.size() != goal.size())
        ;
    queue<char> q1;
    for (int i = 0; i < s.size(); i++) {
        q1.push(s[i]);
    }
    queue<char> q2;
    for (int i = 0; i < goal.size(); i++) {
        q2.push(goal[i]);
    }
    int k = goal.size();
    while (k--) {
        char ch = q2.front();
        q2.pop();
        q2.push(ch);
        if (q2 == q1)
            return true;
    }
    return false;
}
int main()
{
    string s1 = "ABCD";
    string s2 = "CDAB";
    if (check_rotation(s1, s2))
        cout << s2 << " is a rotated form of " << s1
             << endl;
    else
        cout << s2 << " is not a rotated form of " << s1
             << endl;
    string s3 = "ACBD";
    if (check_rotation(s1, s3))
        cout << s3 << " is a rotated form of " << s1
             << endl;
    else
        cout << s3 << " is not a rotated form of " << s1
             << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{
static boolean check_rotation(String s, String goal)
{
    if (s.length() != goal.length())
        ;
    Queue<Character> q1 = new LinkedList<>();
    for (int i = 0; i < s.length(); i++) {
        q1.add(s.charAt(i));
    }
    Queue<Character> q2 = new LinkedList<>();
    for (int i = 0; i < goal.length(); i++) {
        q2.add(goal.charAt(i));
    }
    int k = goal.length();
    while (k>0) {
        k--;
        char ch = q2.peek();
        q2.remove();
        q2.add(ch);
        if (q2.equals(q1))
            return true;
    }
    return false;
}
public static void main(String[] args)
{
    String s1 = "ABCD";
    String s2 = "CDAB";
    if (check_rotation(s1, s2))
        System.out.print(s2+ " is a rotated form of " +  s1
             +"\n");
    else
        System.out.print(s2+ " is not a rotated form of " +  s1
             +"\n");
    String s3 = "ACBD";
    if (check_rotation(s1, s3))
        System.out.print(s3+ " is a rotated form of " +  s1
             +"\n");
    else
        System.out.print(s3+ " is not a rotated form of " +  s1
             +"\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
def check_rotation(s, goal):

    if (len(s) != len(goal)):
        skip

    q1 = []
    for i in range(len(s)):
        q1.insert(0, s[i])

    q2 = []
    for i in range(len(goal)):
        q2.insert(0, goal[i])

    k = len(goal)
    while (k > 0):
        ch = q2[0]
        q2.pop(0)
        q2.insert(0, ch)
        if (q2 == q1):
            return True

        k -= 1

    return False

if __name__ == "__main__":

    s1 = "ABCD"
    s2 = "CDAB"
    if (check_rotation(s1, s2)):
        print(s2, " is a rotated form of ", s1)

    else:
        print(s2, " is not a rotated form of ", s1)

    s3 = "ACBD"
    if (check_rotation(s1, s3)):
        print(s3, " is a rotated form of ", s1)

    else:
        print(s3, " is not a rotated form of ", s1)

        # This code is contributed by ukasp.
```

**Output**

```
CDAB is a rotated form of ABCD
ACBD is not a rotated form of ABCD
```

**使用的库函数:**
strtr:
strtr 在字符串中查找子字符串。
原型:char * strtr(const char * S1，const char * S2)；
见[http://www.lix.polytechnique.fr/Labo/Leo.liberti/public/computing/Prog/C/C/MAN/strtr . htm](http://www.lix.polytechnique.fr/Labo/Leo.Liberti/public/computing/prog/c/C/MAN/strstr.htm)了解更多详情
strcat:
strcat 串联两个字符串
原型:char *strcat(char *dest，const char * src)；
见[http://www.lix.polytechnique.fr/Labo/Leo.liberti/public/computing/Prog/C/C/MAN/strcat . htm](http://www.lix.polytechnique.fr/Labo/Leo.Liberti/public/computing/prog/c/C/MAN/strcat.htm)了解更多详情

**时间复杂度:**这个问题的时间复杂度取决于 strstr 函数的实现。
如果 strstr 的实现是使用 KMP 匹配器完成的，那么上述程序的复杂性是(-)(n1 + n2)，其中 n1 和 n2 是字符串的长度。KMP 匹配器花费(-)(n)时间在长度为 n 的字符串中查找子字符串，其中假设子字符串的长度小于该字符串。

**方法 3:**

**算法:**

1.查找要检查的字符串中原始字符串的第一个字符的所有位置。

2.对于找到的每个位置，将其视为要检查的字符串的起始索引。

3.从新的起始索引开始，比较两个字符串并检查它们是否相等。

(假设原字符串为 **s1** ，待检字符串为 **s2，n** 为字符串长度， **j** 为 s2 中 s1 第一个字符的位置，

然后对于 I

4.对找到的所有位置重复第三步。

## C++

```
#include <iostream>
#include <vector>
using namespace std;

bool checkString(string &s1, string &s2, int indexFound, int Size)
{
    for(int i=0;i<Size;i++){
       //check whether the character is equal or not
        if(s1[i]!=s2[(indexFound+i)%Size])return false;
      // %Size keeps (indexFound+i) in bounds, since it ensures it's value is always less than Size
    }

     return true;
}

int main() {

  string s1="abcd";
  string s2="cdab";

  if(s1.length()!=s2.length()){
      cout<<"s2 is not a rotation on s1"<<endl;
  }
  else{

      vector<int> indexes; //store occurences of the first character of s1

      int Size = s1.length();

      char firstChar = s1[0];

      for(int i=0;i<Size;i++)
      {
          if(s2[i]==firstChar)
          {
            indexes.push_back(i);
          }
      }

      bool isRotation=false;

     // check if the strings are rotation of each other for every occurence of firstChar in s2 
      for(int idx: indexes)
      {
          isRotation = checkString( s1, s2, idx, Size);

          if(isRotation)
            break;
      }

      if(isRotation)cout<<"s2 is rotation of s1"<<endl;
      else cout<<"s2 is not a rotation of s1"<<endl;

    }

    return 0;
}
```

**Output**

```
s2 is rotation of s1
```

**时间复杂度:**

在最坏的情况下，时间复杂度为 n*n，其中 n 是字符串的长度。