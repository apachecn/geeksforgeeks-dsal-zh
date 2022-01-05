# 打印重复字符的所有排列

> 原文:[https://www . geesforgeks . org/print-所有字符重复排列/](https://www.geeksforgeeks.org/print-all-permutations-with-repetition-of-characters/)

给定长度为 n 的字符串，打印给定字符串的所有排列。允许重复字符。按照字典顺序打印这些排列

**示例:**

```
Input: AB
Output: All permutations of AB with repetition are:
      AA
      AB
      BA
      BB

Input: ABC
Output: All permutations of ABC with repetition are:
       AAA
       AAB
       AAC
       ABA
       ...
       ...
       CCB
       CCC
```

对于大小为 n 的输入字符串，将存在允许重复的 n^n 排列。其思想是在第一个索引处固定第一个字符，并递归调用其他后续索引。一旦从第一个字符开始的所有排列都被打印出来，将第二个字符固定在第一个索引处。继续这些步骤，直到最后一个字符。感谢心理编码器提供以下 C 实现。

## C++

```
// C++ program to print all permutations
// with repetition of characters
#include <bits/stdc++.h>
#include<string.h>
using namespace std;

/* Following function is used by
the library qsort() function
to sort an array of chars */
int compare (const void * a, const void * b);

/* The main function that recursively
prints all repeated permutations of
the given string. It uses data[] to store all
permutations one by one */
void allLexicographicRecur (char *str, char* data,
                            int last, int index)
{
    int i, len = strlen(str);

    // One by one fix all characters at
    // the given index and recur for
    // the/ subsequent indexes
    for ( i = 0; i < len; i++ )
    {
        // Fix the ith character at index
        // and if this is not the last
        // index then recursively call
        // for higher indexes
        data[index] = str[i] ;

        // If this is the last index then
        // print the string stored in
        // data[]
        if (index == last)
            cout << data << endl;
        else // Recur for higher indexes
            allLexicographicRecur (str, data, last, index+1);
    }
}

/* This function sorts input string,
allocate memory for data (needed
for allLexicographicRecur()) and
calls allLexicographicRecur() for
printing all permutations */
void allLexicographic(char *str)
{
    int len = strlen (str) ;

    // Create a temp array that will
    // be used by allLexicographicRecur()
    char *data = (char *) malloc (sizeof(char) * (len + 1)) ;
    data[len] = '\0';

    // Sort the input string so that
    // we get all output strings in
    // lexicographically sorted order
    qsort(str, len, sizeof(char), compare);

    // Now print all permutations
    allLexicographicRecur (str, data, len-1, 0);

    // Free data to avoid memory leak
    free(data);
}

// Needed for library function qsort()
int compare (const void * a, const void * b)
{
    return ( *(char *)a - *(char *)b );
}

// Driver code
int main()
{
    char str[] = "ABC";
    cout << "All permutations with repetition of "<<
                                str <<" are: "<<endl ;
    allLexicographic(str);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to print all permutations with repetition
// of characters
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

/* Following function is used by the library qsort() function
  to sort an array of chars */
int compare (const void * a, const void * b);

/* The main function that recursively prints all repeated
   permutations of  the given string. It uses data[] to store all
   permutations one by one */
void allLexicographicRecur (char *str, char* data, int last, int index)
{
    int i, len = strlen(str);

    // One by one fix all characters at the given index and recur for
    // the/ subsequent indexes
    for ( i=0; i<len; i++ )
    {
        // Fix the ith character at index and if this is not the last
        // index then recursively call for higher indexes
        data[index] = str[i] ;

        // If this is the last index then print the string stored in
        // data[]
        if (index == last)
            printf("%s\n", data);
        else // Recur for higher indexes
            allLexicographicRecur (str, data, last, index+1);
    }
}

/* This function sorts input string, allocate memory for data (needed
   for allLexicographicRecur()) and calls allLexicographicRecur() for
   printing all  permutations */
void allLexicographic(char *str)
{
    int len = strlen (str) ;

    // Create a temp array that will be used by allLexicographicRecur()
    char *data = (char *) malloc (sizeof(char) * (len + 1)) ;
    data[len] = '\0';

    // Sort the input string so that we get all output strings in
    // lexicographically sorted order
    qsort(str, len, sizeof(char), compare);

    // Now print all permutations
    allLexicographicRecur (str, data, len-1, 0);

    // Free data to avoid memory leak
    free(data);
}

// Needed for library function qsort()
int compare (const void * a, const void * b)
{
    return ( *(char *)a - *(char *)b );
}

// Driver program to test above functions
int main()
{
    char str[] = "ABC";
    printf("All permutations with repetition of %s are: \n",
            str);
    allLexicographic(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all permutations
// with repetition of characters
import java.util.Arrays;

class GFG
{

    // The main function that recursively prints
    // all repeated permutations of the given string.
    // It uses data[] to store all permutations one by one
    static void allLexicographicRecur(String str, char[] data,
                                      int last, int index)
    {
        int length = str.length();

        // One by one fix all characters at the given index
        // and recur for the subsequent indexes
        for (int i = 0; i < length; i++)
        {

            // Fix the ith character at index and if
            // this is not the last index then
            // recursively call for higher indexes
            data[index] = str.charAt(i);

            // If this is the last index then print
            // the string stored in data[]
            if (index == last)
                System.out.println(new String(data));
            else
                allLexicographicRecur(str, data, last,
                                           index + 1);
        }
    }

    // This function sorts input string, allocate memory
    // for data(needed for allLexicographicRecur()) and calls
    // allLexicographicRecur() for printing all permutations
    static void allLexicographic(String str)
    {
        int length = str.length();

        // Create a temp array that will be used by
        // allLexicographicRecur()
        char[] data = new char[length + 1];
        char[] temp = str.toCharArray();

        // Sort the input string so that we get all
        // output strings in lexicographically sorted order
        Arrays.sort(temp);
        str = new String(temp);

        // Now print all permutations
        allLexicographicRecur(str, data, length - 1, 0);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "ABC";
        System.out.printf("All permutations with " +
                   "repetition of %s are: \n", str);
        allLexicographic(str);
    }
}

// This code is contributed by
// sanjeev2552
```

## 计算机编程语言

```
# Python program to print all permutations with repetition
# of characters

def toString(List):
    return ''.join(List)

# The main function that recursively prints all repeated
# permutations of the given string. It uses data[] to store
# all permutations one by one
def allLexicographicRecur (string, data, last, index):
    length = len(string)

    # One by one fix all characters at the given index and
    # recur for the subsequent indexes
    for i in xrange(length):

        # Fix the ith character at index and if this is not
        # the last index then recursively call for higher
        # indexes
        data[index] = string[i]

        # If this is the last index then print the string
        # stored in data[]
        if index==last:
            print toString(data)
        else:
            allLexicographicRecur(string, data, last, index+1)

# This function sorts input string, allocate memory for data
# (needed for allLexicographicRecur()) and calls
# allLexicographicRecur() for printing all permutations
def allLexicographic(string):
    length = len(string)

    # Create a temp array that will be used by
    # allLexicographicRecur()
    data = [""] * (length+1)

    # Sort the input string so that we get all output strings in
    # lexicographically sorted order
    string = sorted(string)

    # Now print all permutations
    allLexicographicRecur(string, data, length-1, 0)

# Driver program to test the above functions
string = "ABC"
print "All permutations with repetition of " + string + " are:"
allLexicographic(string)

# This code is contributed to Bhavya Jain
```

## C#

```

// C# program to print all permutations
// with repetition of characters
using System;

public class GFG
{

    // The main function that recursively prints
    // all repeated permutations of the given string.
    // It uses data[] to store all permutations one by one
    static void allLexicographicRecur(String str, char[] data,
                                      int last, int index)
    {
        int length = str.Length;

        // One by one fix all characters at the given index
        // and recur for the subsequent indexes
        for (int i = 0; i < length; i++)
        {

            // Fix the ith character at index and if
            // this is not the last index then
            // recursively call for higher indexes
            data[index] = str[i];

            // If this is the last index then print
            // the string stored in data[]
            if (index == last)
                Console.WriteLine(new String(data));
            else
                allLexicographicRecur(str, data, last,
                                           index + 1);
        }
    }

    // This function sorts input string, allocate memory
    // for data(needed for allLexicographicRecur()) and calls
    // allLexicographicRecur() for printing all permutations
    static void allLexicographic(String str)
    {
        int length = str.Length;

        // Create a temp array that will be used by
        // allLexicographicRecur()
        char[] data = new char[length + 1];
        char[] temp = str.ToCharArray();

        // Sort the input string so that we get all
        // output strings in lexicographically sorted order
        Array.Sort(temp);
        str = new String(temp);

        // Now print all permutations
        allLexicographicRecur(str, data, length - 1, 0);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "ABC";
        Console.Write("All permutations with " +
                   "repetition of {0} are: \n", str);
        allLexicographic(str);
    }
}

// This code is contributed by PrinciRaj1992
```

**输出:**

```
All permutations with repetition of ABC are: 
AAA
AAB
AAC
ABA
ABB
ABC
ACA
ACB
ACC
BAA
BAB
BAC
BBA
BBB
BBC
BCA
BCB
BCC
CAA
CAB
CAC
CBA
CBB
CBC
CCA
CCB
CCC
```

C 语言编程基础
极客免费在线课程
下面是输入字符串“AB”的递归树。递归树的目的是帮助理解上面的实现，因为它显示了不同变量的值。

```
                              data="" 
                          /         \
                         /           \ 
                   index=0           index=0
                    i=0               i=1 
                  data="A"           data="B"
                   /   \              /    \
                 /      \            /      \
              index=1  index=1    index=1    index=1 
               i=0      i=1        i=0        i=1 
            data="AA"  data="AB"  data="BA"  data="BB"
```

在上面的实现中，假设输入字符串的所有字符都不同。实现可以很容易地修改，以处理重复的字符。我们必须添加一个预处理步骤来查找唯一的字符(在调用 all dictionary graphics crecur()之前)。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。