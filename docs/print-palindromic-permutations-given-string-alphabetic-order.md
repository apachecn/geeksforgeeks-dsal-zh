# 按字母顺序打印给定字符串的所有回文排列

> 原文:[https://www . geesforgeks . org/print-回文-排列-给定-字符串-字母顺序/](https://www.geeksforgeeks.org/print-palindromic-permutations-given-string-alphabetic-order/)

给定一根大小为 **n** 的绳子**绳子**。问题是按字母顺序打印**串**的所有回文排列，如果可能的话打印“-1”。
**举例:**

```
Input : str = "aabb"
Output :
abba
baab

Input : malayalam
Output :
aalmymlaa
aamlylmaa
alamymala
almayamla
amalylama
amlayalma
laamymaal
lamayamal
lmaayaaml
maalylaam
malayalam
mlaayaalm
```

**先决条件:** [词典第一个回文串](https://www.geeksforgeeks.org/lexicographically-first-palindromic-string/)和[下一个更高的回文号使用同一组数字。](https://www.geeksforgeeks.org/next-higher-palindromic-number-using-set-digits/)
**进场:**以下为步骤:

1.  如果可能，使用**字符串**的字符找到[词典第一个回文字符串](https://www.geeksforgeeks.org/lexicographically-first-palindromic-string/)，否则打印“-1”并返回。
2.  如果从词典学的角度来看，第一个回文字符串被获得，那么打印它。
3.  现在，使用**字符串**的相同字符集找到下一个更高的回文字符串。参考[这篇](https://www.geeksforgeeks.org/next-higher-palindromic-number-using-set-digits/)帖子。
    这两个帖子唯一的区别是，一个数字在排列，另一个小写字母在排列。
4.  如果获得下一个更高的回文字符串，则打印它并转到步骤 3，否则返回。

请注意，字符串**字符串**总是被操纵，以便使用上述步骤获得回文字符串。

## C++

```
// C++ implementation to print all the palindromic
// permutations alphabetically
#include <bits/stdc++.h>
using namespace std;

const char MAX_CHAR = 26;

// Function to count frequency of each char in the
// string. freq[0] for 'a', ...., freq[25] for 'z'
void countFreq(char str[], int freq[], int n)
{
    for (int i = 0; i < n; i++)
        freq[str[i] - 'a']++;
}

// Cases to check whether a palindromic
// string can be formed or not
bool canMakePalindrome(int freq[], int n)
{
    // count_odd to count no of
    // chars with odd frequency
    int count_odd = 0;
    for (int i = 0; i < MAX_CHAR; i++)
        if (freq[i] % 2 != 0)
            count_odd++;

    // For even length string
    // no odd freq character
    if (n % 2 == 0) {
        if (count_odd > 0)
            return false;
        else
            return true;
    }

    // For odd length string
    // one odd freq character
    if (count_odd != 1)
        return false;

    return true;
}

// Function to find odd freq char and reducing its
// freq by 1, returns garbage value if odd freq
// char is not present
char findOddAndRemoveItsFreq(int freq[])
{
    char odd_char;

    for (int i = 0; i < MAX_CHAR; i++) {
        if (freq[i] % 2 != 0) {
            freq[i]--;
            odd_char = (char)(i + 'a');
            break;
        }
    }

    return odd_char;
}

// To find lexicographically first palindromic
// string.
bool findPalindromicString(char str[], int n)
{
    int freq[MAX_CHAR] = { 0 };
    countFreq(str, freq, n);

    // check whether a palindromic string
    // can be formed or not with the
    // characters of 'str'
    if (!canMakePalindrome(freq, n))
        // cannot be formed
        return false;

    // Assigning odd freq character if present
    // else some garbage value
    char odd_char = findOddAndRemoveItsFreq(freq);

    // indexes to store characters from the front
    // and end
    int front_index = 0, rear_index = n - 1;

    // Traverse characters in alphabetical order
    for (int i = 0; i < MAX_CHAR; i++) {
        if (freq[i] != 0) {
            char ch = (char)(i + 'a');

            // store 'ch' to half its frequency times
            // from the front and rear end. Note that
            // odd character is removed by
            // findOddAndRemoveItsFreq()
            for (int j = 1; j <= freq[i] / 2; j++) {
                str[front_index++] = ch;
                str[rear_index--] = ch;
            }
        }
    }

    // if true then odd frequency char exists
    // store it to its corresponding index
    if (front_index == rear_index)
        str[front_index] = odd_char;

    // palindromic string can be formed
    return true;
}

// function to reverse the characters in the
// range i to j in 'str'
void reverse(char str[], int i, int j)
{
    while (i < j) {
        swap(str[i], str[j]);
        i++;
        j--;
    }
}

// function to find next higher palindromic
// string using the same set of characters
bool nextPalin(char str[], int n)
{
    // if length of 'str' is less than '3'
    // then no higher palindromic string
    // can be formed
    if (n <= 3)
        return false;

    // find the index of last character
    // in the 1st half of 'str'
    int mid = n / 2 - 1;
    int i, j;

    // Start from the (mid-1)th character and
    // find the first character that is
    // alphabetically smaller than the
    // character next to it.
    for (i = mid - 1; i >= 0; i--)
        if (str[i] < str[i + 1])
            break;

    // If no such character is found, then all characters
    // are in descending order (alphabetically) which
    // means there cannot be a higher palindromic string
    // with same set of characters
    if (i < 0)
        return false;

    // Find the alphabetically smallest character on
    // right side of ith character which is greater
    // than str[i] up to index 'mid'
    int smallest = i + 1;
    for (j = i + 2; j <= mid; j++)
        if (str[j] > str[i] && str[j] < str[smallest])
            smallest = j;

    // swap str[i] with str[smallest]
    swap(str[i], str[smallest]);

    // as the string is a palindrome, the same
    // swap of characters should be performed
    // in the 2nd half of 'str'
    swap(str[n - i - 1], str[n - smallest - 1]);

    // reverse characters in the range (i+1) to mid
    reverse(str, i + 1, mid);

    // if n is even, then reverse characters in the
    // range mid+1 to n-i-2
    if (n % 2 == 0)
        reverse(str, mid + 1, n - i - 2);

    // else if n is odd, then reverse characters
    // in the range mid+2 to n-i-2
    else
        reverse(str, mid + 2, n - i - 2);

    // next alphabetically higher palindromic
    // string can be formed
    return true;
}

// function to print all the palindromic permutations
// alphabetically
void printAllPalinPermutations(char str[], int n)
{
    // check if lexicographically first palindromic string
    // can be formed or not using the characters of 'str'
    if (!(findPalindromicString(str, n))) {
        // cannot be formed
        cout << "-1";
        return;
    }

    // print all palindromic permutations
    do {
        cout << str << endl;
    } while (nextPalin(str, n));
}

// Driver program to test above
int main()
{
    char str[] = "malayalam";
    int n = strlen(str);
    printAllPalinPermutations(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print all the
// palindromic permutations alphabetically
import java.util.*;

class GFG {

static int MAX_CHAR = 26;

// Function to count frequency
// of each char in the string.
// freq[0] for 'a', ...., freq[25] for 'z'
static void countFreq(char str[],
                    int freq[], int n){

    for (int i = 0; i < n; i++)
        freq[str[i] - 'a']++;
}

// Cases to check whether a palindromic
// string can be formed or not
static Boolean canMakePalindrome
            (int freq[], int n){

    // count_odd to count no of
    // chars with odd frequency
    int count_odd = 0;

    for (int i = 0; i < MAX_CHAR; i++)
        if (freq[i] % 2 != 0)
            count_odd++;

    // For even length string
    // no odd freq character
    if (n % 2 == 0) {
        if (count_odd > 0)
            return false;
        else
            return true;
    }

    // For odd length string
    // one odd freq character
    if (count_odd != 1)
        return false;

    return true;
}

// Function for odd freq char and
// reducing its freq by 1, returns
// garbage value if odd freq
// char is not present
static char findOddAndRemoveItsFreq
                    (int freq[])
{

    char odd_char = 'a';

    for (int i = 0; i < MAX_CHAR; i++)
    {
        if (freq[i] % 2 != 0) {
            freq[i]--;
            odd_char = (char)(i + 'a');
            break;
        }
    }

    return odd_char;
}

// To find lexicographically
// first palindromic string.
static boolean findPalindromicString
            (char[] str, int n)
{
    int[] freq = new int[MAX_CHAR] ;
    countFreq(str, freq, n);

    // check whether a palindromic
    // string can be formed or not
    // with the characters of 'str'
    if (!canMakePalindrome(freq, n))
        return false;

    // Assigning odd freq character if
    // present else some garbage value
    char odd_char =
        findOddAndRemoveItsFreq(freq);

    // indexes to store characters
    // from the front and end
    int front_index = 0,
        rear_index = n - 1;

    // Traverse characters
    // in alphabetical order
    for (int i = 0; i < MAX_CHAR; i++)
    {
        if (freq[i] != 0) {
            char ch = (char)(i + 'a');

            // store 'ch' to half its frequency
            // times from the front and rear
            // end. Note that odd character is
            // removed by findOddAndRemoveItsFreq()
            for (int j = 1; j <= freq[i] / 2; j++){
                str[front_index++] = ch;
                str[rear_index--] = ch;
            }
        }
    }

    // if true then odd frequency char exists
    // store it to its corresponding index
    if (front_index == rear_index)
        str[front_index] = odd_char;

    // palindromic string can be formed
    return true;
}

// function to reverse the characters
// in the range i to j in 'str'
static void reverse(char[] str, int i, int j)
{
    char temp;
    while (i < j) {
        temp = str[i];
        str[i] = str[j];
        str[j] = temp;

        i++;
        j--;
    }
}

// function to find next higher
// palindromic string using the
// same set of characters
static Boolean nextPalin(char[] str, int n)
{
    // if length of 'str' is less
    // than '3' then no higher
    // palindromic string can be formed
    if (n <= 3)
        return false;

    // find the index of last character
    // in the 1st half of 'str'
    int mid = n / 2 - 1;
    int i, j;

    // Start from the (mid-1)th character
    // and find the first character
    // that is alphabetically smaller
    // than the character next to it.
    for (i = mid - 1; i >= 0; i--)
        if (str[i] < str[i + 1])
            break;

    // If no such character is found,
    // then all characters are in
    // descending order (alphabetically)
    // which means there cannot be a
    // higher palindromic string
    // with same set of characters
    if (i < 0)
        return false;

    // Find the alphabetically smallest
    // character on right side of ith
    // character which is greater than
    // str[i] up to index 'mid'
    int smallest = i + 1;
    for (j = i + 2; j <= mid; j++)
        if (str[j] > str[i] && str[j]
                     < str[smallest])
            smallest = j;

char temp;

    // swap str[i] with str[smallest]
    temp = str[i];
    str[i] = str[smallest];
    str[smallest] = temp;

    // as the string is a palindrome,
    // the same swap of characters
    // should be performed in the
    // 2nd half of 'str'
    temp = str[n - i - 1];
    str[n - i - 1] = str[n - smallest - 1];
    str[n - smallest - 1] = temp;

    // reverse characters in the
    // range (i+1) to mid
    reverse(str, i + 1, mid);

    // if n is even, then reverse
    // characters in the range
    // mid+1 to n-i-2
    if (n % 2 == 0)
        reverse(str, mid + 1, n - i - 2);

    // else if n is odd, then
    // reverse characters in
    // the range mid+2 to n-i-2
    else
        reverse(str, mid + 2, n - i - 2);

    // next alphabetically higher
    // palindromic string can be formed
    return true;
}

// function to print all palindromic
// permutations alphabetically
static void printAllPalinPermutations
            (char[] str, int n) {

    // check if lexicographically
    // first palindromic string can
    // be formed or not using the
    // characters of 'str'
    if (!(findPalindromicString(str, n)))
    {
        // cannot be formed
        System.out.print("-1");
        return;
    }

    // print all palindromic permutations
    do {
        System.out.println(str);
    } while (nextPalin(str, n));
}

// Driver program
public static void main(String[] args)
{

    char[] str = ("malayalam").toCharArray();
    int n = str.length;

    printAllPalinPermutations(str, n);
}
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 implementation to print all the
# palindromic permutations alphabetically

# import library
import numpy as np

MAX_CHAR = 26

# Function to count frequency of each in the
# string. freq[0] for 'a', ...., freq[25] for 'z'
def countFreq(str, freq, n) :
    for i in range(0, n) :
        freq[ord(str[i]) - ord('a')] += 1

# Cases to check whether a palindromic
# string can be formed or not
def canMakePalindrome(freq, n) :

    # count_odd to count no of
    # s with odd frequency
    count_odd = 0
    for i in range(0, MAX_CHAR) :

        if (freq[i] % 2 != 0):
            count_odd += 1

    # For even length string
    # no odd freq character
    if (n % 2 == 0):
        if (count_odd > 0):
            return False
        else:
            return True

    # For odd length string
    # one odd freq character
    if (count_odd != 1):
        return False

    return True

# Function to find odd freq and reducing
# its freq by 1, returns garbage
# value if odd freq is not present
def findOddAndRemoveItsFreq(freq) :

    odd_char = 0

    for i in range(0, MAX_CHAR) :
        if (freq[i] % 2 != 0):
            freq[i] = freq[i] - 1
            odd_char = (chr)(i + ord('a'))
            break

    return odd_char

# To find lexicographically first
# palindromic string.
def findPalindromicString(str, n) :

    freq = np.zeros(26, dtype = np.int)
    countFreq(str, freq, n)

    # Check whether a palindromic string
    # can be formed or not with the
    # characters of 'str'
    if (not(canMakePalindrome(freq, n))):
        # cannot be formed
        return False

    # Assigning odd freq character if
    # present else some garbage value
    odd_char = findOddAndRemoveItsFreq(freq)

    # indexes to store acters from
    # the front and end
    front_index = 0; rear_index = n - 1

    # Traverse acters in alphabetical order
    for i in range(0, MAX_CHAR) :
        if (freq[i] != 0) :
            ch = (chr)(i + ord('a'))

            # Store 'ch' to half its frequency times
            # from the front and rear end. Note that
            # odd character is removed by
            # findOddAndRemoveItsFreq()

            for j in range(1, int(freq[i]/2) + 1):
                str[front_index] = ch
                front_index += 1

                str[rear_index] = ch
                rear_index -= 1

    # if True then odd frequency exists
    # store it to its corresponding index
    if (front_index == rear_index):
        str[front_index] = odd_char

    # palindromic string can be formed
    return True

# Function to reverse the acters in the
# range i to j in 'str'
def reverse( str, i, j):

    while (i < j):
        str[i], str[j] = str[j], str[i]
        i += 1
        j -= 1

# Function to find next higher palindromic
# string using the same set of acters
def nextPalin(str, n) :

    # If length of 'str' is less than '3'
    # then no higher palindromic string
    # can be formed
    if (n <= 3):
        return False

    # Find the index of last acter
    # in the 1st half of 'str'
    mid = int (n / 2) - 1

    # Start from the (mid-1)th acter and
    # find the first acter that is
    # alphabetically smaller than the
    # acter next to it
    i = mid -1
    while(i >= 0) :
        if (str[i] < str[i + 1]):
            break
        i -= 1

    # If no such character is found, then
    # all characters are in descending order
    # (alphabetically) which means there cannot
    # be a higher palindromic string with same
    # set of characters
    if (i < 0):
        return False

    # Find the alphabetically smallest character
    # on right side of ith character which is
    # greater than str[i] up to index 'mid'
    smallest = i + 1;
    for j in range(i + 2, mid + 1):
        if (str[j] > str[i] and str[j] < str[smallest]):
            smallest = j

    # Swap str[i] with str[smallest]
    str[i], str[smallest] = str[smallest], str[i]

    # As the string is a palindrome, the same
    # swap of characters should be performed
    # in the 2nd half of 'str'
    str[n - i - 1], str[n - smallest - 1] = str[n - smallest - 1], str[n - i - 1]

    # Reverse characters in the range (i+1) to mid
    reverse(str, i + 1, mid)

    # If n is even, then reverse characters in the
    # range mid+1 to n-i-2
    if (n % 2 == 0):
        reverse(str, mid + 1, n - i - 2)

    # else if n is odd, then reverse acters
    # in the range mid+2 to n-i-2
    else:
        reverse(str, mid + 2, n - i - 2)

    # Next alphabetically higher palindromic
    # string can be formed
    return True

# Function to print all the palindromic
# permutations alphabetically
def printAllPalinPermutations(str, n) :

    # Check if lexicographically first
    # palindromic string can be formed
    # or not using the acters of 'str'
    if (not(findPalindromicString(str, n))):
           # cannot be formed
        print ("-1")
        return

    # Converting list into string
    print ( "".join(str))

    # print all palindromic permutations
    while (nextPalin(str, n)):

        # converting list into string
        print ("".join(str))

# Driver Code
str= "malayalam"
n = len(str)

# Convertnig string into list so that
# replacement of characters would be easy
str = list(str)

printAllPalinPermutations(str, n)

# This article is contributed by 'saloni1297'
```

## C#

```
// C# code to print all the palindromic
// permutations alphabetically
using System;

class GFG {

static int MAX_CHAR = 26;

// Function to count frequency
// of each char in the string.
// freq[0] for 'a', ...., freq[25] for 'z'
static void countFreq(char []str, int []freq, int n)
{
    for (int i = 0; i < n; i++)
        freq[str[i] - 'a']++;
}

// Cases to check whether a palindromic
// string can be formed or not
static Boolean canMakePalindrome(int []freq, int n)
{
    // count_odd to count no of
    // chars with odd frequency
    int count_odd = 0;

    for (int i = 0; i < MAX_CHAR; i++)
        if (freq[i] % 2 != 0)
            count_odd++;

    // For even length string
    // no odd freq character
    if (n % 2 == 0) {
        if (count_odd > 0)
            return false;
        else
            return true;
    }

    // For odd length string
    // one odd freq character
    if (count_odd != 1)
        return false;

    return true;
}

// Function for odd freq char and
// reducing its freq by 1, returns
// garbage value if odd freq
// char is not present
static char findOddAndRemoveItsFreq(int []freq)
{
    char odd_char = 'a';

    for (int i = 0; i < MAX_CHAR; i++)
    {
        if (freq[i] % 2 != 0) {
            freq[i]--;
            odd_char = (char)(i + 'a');
            break;
        }
    }

    return odd_char;
}

// To find lexicographically
// first palindromic string.
static Boolean findPalindromicString(char[] str, int n)
{
    int[] freq = new int[MAX_CHAR] ;
    countFreq(str, freq, n);

    // check whether a palindromic
    // string can be formed or not
    // with the characters of 'str'
    if (!canMakePalindrome(freq, n))
        return false;

    // Assigning odd freq character if
    // present else some garbage value
    char odd_char =
        findOddAndRemoveItsFreq(freq);

    // indexes to store characters
    // from the front and end
    int front_index = 0,
        rear_index = n - 1;

    // Traverse characters
    // in alphabetical order
    for (int i = 0; i < MAX_CHAR; i++)
    {
        if (freq[i] != 0) {
            char ch = (char)(i + 'a');

            // store 'ch' to half its frequency
            // times from the front and rear
            // end. Note that odd character is
            // removed by findOddAndRemoveItsFreq()
            for (int j = 1; j <= freq[i] / 2; j++){
                str[front_index++] = ch;
                str[rear_index--] = ch;
            }
        }
    }

    // if true then odd frequency char exists
    // store it to its corresponding index
    if (front_index == rear_index)
        str[front_index] = odd_char;

    // palindromic string can be formed
    return true;
}

// function to reverse the characters
// in the range i to j in 'str'
static void reverse(char[] str, int i, int j)
{
    char temp;
    while (i < j) {
        temp = str[i];
        str[i] = str[j];
        str[j] = temp;

        i++;
        j--;
    }
}

// function to find next higher
// palindromic string using the
// same set of characters
static Boolean nextPalin(char[] str, int n)
{
    // if length of 'str' is less
    // than '3' then no higher
    // palindromic string can be formed
    if (n <= 3)
        return false;

    // find the index of last character
    // in the 1st half of 'str'
    int mid = n / 2 - 1;
    int i, j;

    // Start from the (mid-1)th character
    // and find the first character
    // that is alphabetically smaller
    // than the character next to it.
    for (i = mid - 1; i >= 0; i--)
        if (str[i] < str[i + 1])
            break;

    // If no such character is found,
    // then all characters are in
    // descending order (alphabetically)
    // which means there cannot be a
    // higher palindromic string
    // with same set of characters
    if (i < 0)
        return false;

    // Find the alphabetically smallest
    // character on right side of ith
    // character which is greater than
    // str[i] up to index 'mid'
    int smallest = i + 1;
    for (j = i + 2; j <= mid; j++)
        if (str[j] > str[i] && str[j]
                    < str[smallest])
            smallest = j;

char temp;

    // swap str[i] with str[smallest]
    temp = str[i];
    str[i] = str[smallest];
    str[smallest] = temp;

    // as the string is a palindrome,
    // the same swap of characters
    // should be performed in the
    // 2nd half of 'str'
    temp = str[n - i - 1];
    str[n - i - 1] = str[n - smallest - 1];
    str[n - smallest - 1] = temp;

    // reverse characters in the
    // range (i+1) to mid
    reverse(str, i + 1, mid);

    // if n is even, then reverse
    // characters in the range
    // mid+1 to n-i-2
    if (n % 2 == 0)
        reverse(str, mid + 1, n - i - 2);

    // else if n is odd, then
    // reverse characters in
    // the range mid+2 to n-i-2
    else
        reverse(str, mid + 2, n - i - 2);

    // next alphabetically higher
    // palindromic string can be formed
    return true;
}

// function to print all palindromic
// permutations alphabetically
static void printAllPalinPermutations(char[] str, int n)
{
    // check if lexicographically
    // first palindromic string can
    // be formed or not using the
    // characters of 'str'
    if (!(findPalindromicString(str, n)))
    {
        // cannot be formed
        Console.WriteLine("-1");
        return;
    }

    // print all palindromic permutations
    do {
    Console.WriteLine(str);
    } while (nextPalin(str, n));
}

// Driver program
public static void Main(String[] args)
{
    char[] str = ("malayalam").ToCharArray();
    int n = str.Length;

    printAllPalinPermutations(str, n);
}
}

// This code is contributed by parashar.
```

输出:

```
aalmymlaa
aamlylmaa
alamymala
almayamla
amalylama
amlayalma
laamymaal
lamayamal
lmaayaaml
maalylaam
malayalam
mlaayaalm
```

时间复杂度:O(m*n)，其中 **m** 是**串**的回文排列数。