# 打印给定两个字符串的所有插页

> 原文:[https://www . geeksforgeeks . org/print-all-interleaves-of-given-two-string/](https://www.geeksforgeeks.org/print-all-interleavings-of-given-two-strings/)

给定两个字符串 str1 和 str2，编写一个函数，打印给定两个字符串的所有交错。您可以假设两个字符串中的所有字符都不同
示例:

```
Input: str1 = "AB",  str2 = "CD"
Output:
    ABCD
    ACBD
    ACDB
    CABD
    CADB
    CDAB

Input: str1 = "AB",  str2 = "C"
Output:
    ABC
    ACB
    CAB
```

给定两个字符串的交错字符串保持了单个字符串中字符的顺序。例如，在上面第一个例子的所有插页中，“A”在“B”之前，“C”在“D”之前。

设 str1 的长度为 m，str2 的长度为 n，假设 str1 和 str2 中的所有字符都不同。让 count(m，n)为这些串中所有交错串的计数。计数(m，n)的值可以写成如下形式。

```
     count(m, n) = count(m-1, n) + count(m, n-1)
     count(1, 0) = 1 and count(0, 1) = 1
```

要打印所有插页，我们可以首先修复 str1[0..输出字符串中的 m-1]，并递归调用 str1[ **1** ..m-1]和 str2[0..n-1]。然后我们可以修复 str 2[0]的第一个字符..n-1]并递归调用 str1[0..m-1]和 str2[ **1** ..n-1]。感谢 akash01 提供以下 C 实现。

## C

```
// C program to print all interleavings of given two strings
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// The main function that recursively prints all interleavings.
// The variable iStr is used to store all interleavings (or
// output strings) one by one. 
// i is used to pass next available place in iStr
void printIlsRecur (char *str1, char *str2, char *iStr, int m,
                    int n, int i)
{
    // Base case: If all characters of str1 and str2 have been
    // included in output string, then print the output string
    if (m==0 && n==0)
        printf("%s\n", iStr) ;

    // If some characters of str1 are left to be included, then
    // include the  first character from the remaining characters
    // and recur for rest
    if (m != 0)
    {
        iStr[i] = str1[0];
        printIlsRecur (str1 + 1, str2, iStr, m-1, n, i+1);
    }

    // If some characters of str2 are left to be included, then
    // include the  first character from the remaining characters
    // and recur for rest
    if (n != 0)
    {
        iStr[i] = str2[0];
        printIlsRecur(str1, str2+1, iStr, m, n-1, i+1);
    }
}

// Allocates memory for output string and uses printIlsRecur()
// for printing all interleavings
void printIls (char *str1, char *str2, int m, int n)
{
   // allocate memory for the output string
   char *iStr= (char*)malloc((m+n+1)*sizeof(char));

   // Set the terminator for the output string
   iStr[m+n] = '\0';

   // print all interleavings using printIlsRecur()
   printIlsRecur (str1, str2, iStr, m, n, 0);

   // free memory to avoid memory leak
   free(iStr);
}

// Driver program to test above functions
int main()
{
    char str1[] = "AB";
    char str2[] = "CD";
    printIls (str1, str2, strlen(str1), strlen(str2));
    return 0;
}
```

## C++

```
// C++ program to print all interleavings of given two strings
#include <bits/stdc++.h>
using namespace std;

// The main function that recursively prints all interleavings.
// The variable iStr is used to store all interleavings (or
// output strings) one by one.
// i is used to pass next available place in iStr
void printIlsRecur (char *str1, char *str2, char *iStr, int m,
                    int n, int i)
{
    // Base case: If all characters of str1 and str2 have been
    // included in output string, then print the output string
    if (m == 0 && n == 0)
        cout << iStr << endl ;

    // If some characters of str1 are left to be included, then
    // include the first character from the remaining characters
    // and recur for rest
    if (m != 0)
    {
        iStr[i] = str1[0];
        printIlsRecur (str1 + 1, str2, iStr, m - 1, n, i + 1);
    }

    // If some characters of str2 are left to be included, then
    // include the first character from the remaining characters
    // and recur for rest
    if (n != 0)
    {
        iStr[i] = str2[0];
        printIlsRecur(str1, str2 + 1, iStr, m, n - 1, i + 1);
    }
}

// Allocates memory for output string and uses printIlsRecur()
// for printing all interleavings
void printIls (char *str1, char *str2, int m, int n)
{
    // allocate memory for the output string
    char *iStr= new char[((m + n + 1)*sizeof(char))];

    // Set the terminator for the output string
    iStr[m + n] = '\0';

    // print all interleavings using printIlsRecur()
    printIlsRecur (str1, str2, iStr, m, n, 0);

    // free memory to avoid memory leak
    free(iStr);
}

// Driver code
int main()
{
    char str1[] = "AB";
    char str2[] = "CD";
    printIls (str1, str2, strlen(str1), strlen(str2));
    return 0;
}

// This is code is contributed by rathbhupendra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    /*
     * This methods prints interleaving string of two
     * strings
     * @param s1  String 1
     * @param i   current index of s1
     * @param s2  String 2
     * @param j  Current index of s2
     * @param asf String containing interleaving string of
     *     s1 and s2
     *
     */
    static void printInterLeaving(String s1, int i,
                                  String s2, int j,
                                  String asf)
    {
        if (i == s1.length() && j == s2.length()) {
            System.out.println(asf);
        }

        // Either we will start with string 1
        if (i < s1.length())
            printInterLeaving(s1, i + 1, s2, j,
                              asf + s1.charAt(i));
        // Or with string 2
        if (j < s2.length())
            printInterLeaving(s1, i, s2, j + 1,
                              asf + s2.charAt(j));
    }

    /*
     * Main function executed by JVM
     * @param args String array
     */
    public static void main(String[] args)
    {
        // TODO Auto-generated method stub

        String s1 = "AB"; // String 1
        String s2 = "CD"; // String 2

        printInterLeaving(s1, 0, s2, 0, "");
    }
}

/* Code by mahi_07 */
```

## 计算机编程语言

```
# Python program to print all interleavings of given two strings

# Utility function
def toString(List):
    return "".join(List)

# The main function that recursively prints all interleavings.
# The variable iStr is used to store all interleavings (or output
# strings) one by one.
# i is used to pass next available place in iStr
def printIlsRecur(str1, str2, iStr, m, n, i):

    # Base case: If all characters of str1 and str2 have been
    # included in output string, then print the output string
    if m==0 and n==0:
        print toString(iStr)

    # If some characters of str1 are left to be included, then
    # include the first character from the remaining characters
    # and recur for rest
    if m != 0:
        iStr[i] = str1[0]
        printIlsRecur(str1[1:], str2, iStr, m-1, n, i+1)

    # If some characters of str2 are left to be included, then
    # include the first character from the remaining characters
    # and recur for rest
    if n != 0:
        iStr[i] = str2[0]
        printIlsRecur(str1, str2[1:], iStr, m, n-1, i+1)

# Allocates memory for output string and uses printIlsRecur()
# for printing all interleavings
def printIls(str1, str2, m, n):
    iStr = [''] * (m+n)

    # print all interleavings using printIlsRecur()
    printIlsRecur(str1, str2, iStr, m, n, 0)

# Driver program to test the above function
str1 = "AB"
str2 = "CD"
printIls(str1, str2, len(str1), len(str2))

# This code is contributed by Bhavya Jain
```

**输出:**

```
ABCD
ACBD
ACDB
CABD
CADB
CDAB
```

**时间复杂度:** O(2 ^ (m+n))

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。