# 只交换一个字符的回文

> 原文:[https://www . geesforgeks . org/仅交换一个字符的回文/](https://www.geeksforgeeks.org/palindrome-by-swapping-only-one-character/)

给定一个字符串，任务是检查该字符串是否可以通过只交换一次字符而变成回文。
【注意:只能交换一个字符，且只能有一个字符与另一个字符交换】

**示例:**

```
Input : bbg
Output : true
Explanation: Swap b(1st index) with g.

Input : bdababd
Output : true
Explanation: Swap b(0th index) with d(last index) or
             Swap d(1st index) with b(second index)

Input : gcagac
Output : false

```

**进场:**

> 该算法基于对形成字符串回文的行为和可能性的彻底分析。通过这样的分析，我得到了以下结论:
> 1。首先，我们将找到字符串中的差异，这些差异实际上阻止了它成为回文。
> …..a)为了做到这一点，我们将从两端开始，每次从两端比较一个元素，只要它匹配，我们就将值存储在一个单独的数组中，与此同时，我们对不匹配的项目的数量进行计数。
> T3】2。如果不匹配项的数量超过 2，则永远不可能通过仅交换一个字符来使其成为回文字符串。
> 
> 3。如果(不匹配项目数= 2)–如果第一个不匹配集合中出现的字符与第二个不匹配集合中出现的字符相同，则有可能使字符串成为回文。(例如:试试这个“bdababd”)。
> 
> 4。If(不匹配项目数= 1)
> …..a) if(字符串长度为偶数)–不可能用它来制作回文字符串。
> …..b)如果(字符串长度为奇数)–如果有一个不匹配的字符与中间字符匹配，则可以用这个**组成回文字符串。
> 
> 5。如果(不匹配项的数量= 0)–如果我们交换任何相同字符的位置，回文是可能的。**

## C++

```
// C++ program palindrome by swapping
// only one character
#include <bits/stdc++.h>
using namespace std;

bool isPalindromePossible(string input)
{
    int len = input.length();

    // counts the number of differences 
    // which prevents the string from
    // being palindrome.
    int diffCount = 0, i;

    // keeps a record of the characters 
    // that prevents the string from 
    // being palindrome.
    char diff[2][2];

    // loops from the start of a string 
    // till the midpoint of the string
    for (i = 0; i < len / 2; i++)
    {

        // difference is encountered preventing 
        // the string from being palindrome
        if (input[i] != input[len - i - 1]) 
        {

            // 3rd differences encountered and 
            // its no longer possible to make 
            // is palindrome by one swap
            if (diffCount == 2) return false;

            // record the different character
            diff[diffCount][0] = input[i];

            // store the different characters
            diff[diffCount++][1] = input[len - i - 1];
        }
    }

    switch (diffCount)
    {
        // its already palindrome
        case 0:
            return true;

        // only one difference is found
        case 1: 
        {
            char midChar = input[i];

            // if the middleChar matches either of
            // the difference producing characters,
            // return true
            if (len % 2 != 0 and
               (diff[0][0] == midChar or
                diff[0][1] == midChar))
                return true;
        }

        // two differences are found
        case 2:

            // if the characters contained in 
            // the two sets are same, return true
            if ((diff[0][0] == diff[1][0] and 
                 diff[0][1] == diff[1][1]) or
                (diff[0][0] == diff[1][1] and 
                 diff[0][1] == diff[1][0]))
                return true;
    }
    return false;
}

// Driver Code
int main() 
{
    cout << boolalpha 
         << isPalindromePossible("bbg") << endl;
    cout << boolalpha
         << isPalindromePossible("bdababd") << endl;
    cout << boolalpha 
         << isPalindromePossible("gcagac") << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program palindrome by swapping
// only one character
class GFG
 {

    public static boolean isPalindromePossible(String input)
    {

        // convert the string to character array
        char[] charStr = input.toCharArray();
        int len = input.length(), i;

        // counts the number of differences which prevents
        // the string from being palindrome.
        int diffCount = 0;

        // keeps a record of the characters that prevents
        // the string from being palindrome.
        char[][] diff = new char[2][2];

        // loops from the start of a string till the midpoint
        // of the string
        for (i = 0; i < len / 2; i++) {

            // difference is encountered preventing the string
            // from being palindrome
            if (charStr[i] != charStr[len - i - 1]) {

                // 3rd differences encountered and its no longer
                // possible to make is palindrome by one swap
                if (diffCount == 2)
                    return false;

                // record the different character
                diff[diffCount][0] = charStr[i];

                // store the different characters
                diff[diffCount++][1] = charStr[len - i - 1];
            }
        }

        switch (diffCount) {

        // its already palindrome
        case 0:
            return true;

        // only one difference is found
        case 1:
            char midChar = charStr[i];

            // if the middleChar matches either of the
            // difference producing characters, return true
            if (len % 2 != 0 && (diff[0][0] == midChar
                                 || diff[0][1] == midChar))
                return true;

        // two differences are found
        case 2:

            // if the characters contained in the two sets are same,
            // return true
            if ((diff[0][0] == diff[1][0] && diff[0][1] == diff[1][1])
                || (diff[0][0] == diff[1][1] && diff[0][1] == diff[1][0]))
                return true;
        }
        return false;
    }

    public static void main(String[] args)
    {
        System.out.println(isPalindromePossible("bbg"));
        System.out.println(isPalindromePossible("bdababd"));
        System.out.println(isPalindromePossible("gcagac"));
    }
}
```

## 蟒蛇 3

```
# Python3 program palindrome by swapping
# only one character

def isPalindromePossible(input: str) -> bool:
    length = len(input)

    # counts the number of differences
    # which prevents the string from
    # being palindrome.
    diffCount = 0
    i = 0

    # keeps a record of the characters
    # that prevents the string from
    # being palindrome.
    diff = [['0'] * 2] * 2

    # loops from the start of a string
    # till the midpoint of the string
    while i < length // 2:

        # difference is encountered preventing
        # the string from being palindrome
        if input[i] != input[length - i - 1]:

            # 3rd differences encountered and
            # its no longer possible to make
            # is palindrome by one swap
            if diffCount == 2:
                return False

            # record the different character
            diff[diffCount][0] = input[i]

            # store the different characters
            diff[diffCount][1] = input[length - i - 1]
            diffCount += 1
        i += 1

    # its already palindrome
    if diffCount == 0:
        return True

    # only one difference is found
    elif diffCount == 1:
        midChar = input[i]

        # if the middleChar matches either of
        # the difference producing characters,
        # return true
        if length % 2 != 0 and (diff[0][0] == midChar
                                or diff[0][1] == midChar):
            return True

    # two differences are found
    elif diffCount == 2:

        # if the characters contained in
        # the two sets are same, return true
        if (diff[0][0] == diff[1][0] and diff[0][1] == diff[1][1]) or (
                diff[0][0] == diff[1][1] and diff[0][1] == diff[1][0]):
            return True
    return False

# Driver Code
if __name__ == "__main__":

    print(isPalindromePossible("bbg"))
    print(isPalindromePossible("bdababd"))
    print(isPalindromePossible("gcagac"))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program palindrome by swapping
// only one character
using System;

class GFG 
{ 

    public static bool isPalindromePossible(String input) 
    { 

        // convert the string to character array 
        char[] charStr = input.ToCharArray(); 
        int len = input.Length, i; 

        // counts the number of differences 
        // which prevents the string
        // from being palindrome. 
        int diffCount = 0; 

        // keeps a record of the 
        // characters that prevents 
        // the string from being palindrome. 
        char[,] diff = new char[2, 2]; 

        // loops from the start of a string 
        // till the midpoint of the string 
        for (i = 0; i < len / 2; i++)
        { 

            // difference is encountered preventing 
            // the string from being palindrome 
            if (charStr[i] != charStr[len - i - 1]) 
            { 

                // 3rd differences encountered 
                // and its no longer possible to
                // make is palindrome by one swap 
                if (diffCount == 2) 
                    return false; 

                // record the different character 
                diff[diffCount, 0] = charStr[i]; 

                // store the different characters 
                diff[diffCount++, 1] = charStr[len - i - 1]; 
            } 
        } 

        switch (diffCount) 
        { 

            // its already palindrome 
            case 0: 
                return true; 

            // only one difference is found 
            case 1: 
                char midChar = charStr[i]; 

            // if the middleChar matches either of the 
            // difference producing characters, return true 
            if (len % 2 != 0 && 
                (diff[0,0] == midChar || 
                diff[0,1] == midChar)) 
                return true; 
            break;

            // two differences are found 
            case 2: 

            // if the characters contained in 
            // the two sets are same, return true 
            if ((diff[0,0] == diff[1,0] && 
                 diff[0,1] == diff[1,1]) ||
                 (diff[0,0] == diff[1,1] && 
                 diff[0,1] == diff[1,0])) 
                return true; 
            break;
        } 
        return false; 
    } 

    // Driver code
    public static void Main(String[] args) 
    { 
        Console.WriteLine(isPalindromePossible("bbg")); 
        Console.WriteLine(isPalindromePossible("bdababd")); 
        Console.WriteLine(isPalindromePossible("gcagac")); 
    } 
} 

// This code is contributed by PrinciRaj1992
```

**Output:**

```
true
true
false

```

**时间复杂度:**O(n)
T3】辅助空间: O(1)