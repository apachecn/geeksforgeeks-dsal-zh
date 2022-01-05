# Sudo 放置|回文族

> 原文:[https://www . geesforgeks . org/sudo-placement-回文-family/](https://www.geeksforgeeks.org/sudo-placement-palindrome-family/)

给定一串小写字符，任务是检测字符串族，其中字符串族描述如下。

*   **奇数回文**:奇数索引(基于 1 的索引)的字符构成回文的字符串。
*   **偶数回文**:偶数索引(基于 1 的索引)的字符串组成回文。
*   **TWIN 回文**:同时具有上述两种属性的字符串。
*   **PARENT 回文**:如果字符串本身就是回文。

**示例**:

> **输入** : geeksforskeeg
> **输出** : ODD 回文
> **解释**:奇数索引处的字符组成的字符串(遵循 1-based indexing)为“ **gesoseg** ，为回文，偶数索引处的字符组成的字符串不构成回文。因此，给定的字符串属于“**奇数**族。
> 
> **输入** : aibohobia
> **输出** : PARENT 回文
> **解释**:字符串本身就是回文，因此属于 **PARENT** 家族。

**逼近**:定义 2 个空字符串，oddString 和 evenString。

*   在 evenString 中的偶数索引处追加所有字符。
*   在 oddString 中的奇数索引处追加所有字符。

现在，检查以下情况:

1.  检查给定的字符串是否是回文，如果是打印“父回文”。
2.  如果第一种情况不成立，检查 evenString 和 oddString 是否都是回文，如果是，则打印“TWIN 回文”
3.  如果第二种情况不成立，那么如果偶数字符串是回文，则打印“偶数回文”，否则如果奇数字符串是回文，则打印“奇数回文”。
4.  如果以上条件都不满足，则打印“异形回文”。

下面是上述方法的实现:

## C++

```
// CPP program to print the Palindrome Family
// corresponding to a given string
#include <bits/stdc++.h>

using namespace std;

// Checks if the given string is a Palindrome
bool isPalindrome(string str)
{
    // Find the reverse of the given string
    string reverse_str = str;
    reverse(reverse_str.begin(), reverse_str.end());

    // Check if the reverse and the string are equal
    if (str == reverse_str)
        return true;
    return false;
}

// Prints the Palindrome Family corresponding to a given string
void printPalindromeFamily(string str)
{

    // Check if the given string is a palindrome
    if (isPalindrome(str)) {
        cout << "PARENT Palindrome" << endl;
        return;
    }

    string oddString = "";
    string evenString = "";

    int n = str.length();

    // append characters at odd indices(1 based) to oddString
    for (int i = 0; i < n; i += 2)
        oddString += str[i];

    // append characters at even indices(1 based indexing) to evenString
    for (int i = 1; i < n; i += 2)
        evenString += str[i];

    // Check if the individual evenString and oddString are palindrome
    bool isEvenPalindrome = isPalindrome(evenString);
    bool isOddPalindrome = isPalindrome(oddString);

    // Check if both oddString and evenString are palindromes
    // If so, it is a TWIN palindrome
    if (isEvenPalindrome && isOddPalindrome)
        cout << "TWIN Palindrome" << endl;

    // Else check if even indices form a palindrome
    else if (isEvenPalindrome)
        cout << "EVEN Palindrome" << endl;

    // Else check if odd indices form a palindrome
    else if (isOddPalindrome)
        cout << "ODD Palindrome" << endl;

    // If none of the cases satisfy, then it is an ALIEN Palindrome
    else
        cout << "Alien Palindrome" << endl;
}

// Driver Code
int main()
{

    string s = "geeksforskeeg";
    printPalindromeFamily(s);

    s = "aibohobia";
    printPalindromeFamily(s);

    s = "geeks";
    printPalindromeFamily(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the Palindrome Family
// corresponding to a given string
import java.util.*;
import java.io.*;

public class PalindromeFamily {

    // Checks if the given string is a Palindrome
    public static boolean isPalindrome(String str){

        //Set two pointers, one at the last character of the string and
        // other the first character. If both of them don't match, then
        // it is not a palindrome. Keep incrementing start pointer,
        // and decreasing end pointer by one, until they check the middle character.
        int start = 0, end = str.length() -1;
        while(start <= end){
            if(str.charAt(start) != str.charAt(end)){
                return false;
            }
            start++;
            end--;
        }
        return true;
    }

    // Prints the Palindrome Family corresponding to a given string
    public static void palindromeFamily(String str){

        //Check for parent palindrome
        if(isPalindrome(str)){
            System.out.println("PARENT Palindrome");
            return;
        }

        //Check for odd and even palindromes
        String oddString = "";
        String evenString = "";

        // append characters at odd indices(1 based) to oddString
        for(int i=0; i<str.length(); i+=2){
            oddString += str.charAt(i);
        }

        // append characters at even indices(1 based indexing) to evenString
        for(int i=1; i<str.length(); i+=2){
            evenString += str.charAt(i);
        }

         // Check if the individual evenString and oddString are palindrome
        boolean isEvenPalindrome = isPalindrome(evenString);
        boolean isOddPalindrome = isPalindrome(oddString);

        //Check if both oddString and evenString are palindromes
        //If yes, then it is a twin palindrome
        if(isOddPalindrome && isEvenPalindrome){
            System.out.println("TWIN Palindrome");
        }
        //Else, check if odd indices form a palindrome
        else if (isOddPalindrome){
            System.out.println("ODD Palindrome");
        }
        //Else, check if even indices form a palindrome
        else if (isEvenPalindrome){
            System.out.println("EVEN Palindrome");
        }
        //If none of the cases satisfy, then it is an ALIEN palindrome
        else
            System.out.println("ALIEN Palindrome");

    }

    public static void main(String[] args){
        String s = "geeksforskeeg";
        palindromeFamily(s);

        s = "aibohobia";
        palindromeFamily(s);

        s = "geeks";
        palindromeFamily(s);
    }

}
```

## 蟒蛇 3

```
# Python3 Program to print the Palindrome Family
# corresponding to a given string 
# check if the given string is a Palindrome 
def isPalindrome(str1):

    # Find the reverse of the given string
    reverse_str = str1[::-1]

    # Check if the reverse and the string are equal
    if(str1 == reverse_str):
        return True
    return False

# Prints the palindrome family corresponding to a given string
def printPalindromeFamily(str1):

    # Check if the given string is a palindrome
    if(isPalindrome(str1)):
        print("PARENT Palindrome")
        return False
    oddString = ""
    evenString = ""
    n = len(str1)

    # append characters at odd 
    # indices(1 based) to oddString
    for i in range(0, n, 2):
        oddString += str1[i]

    # append characters at even 
    # indices(1 based) to evenString
    for i in range(1, n, 2):
        evenString += str1[i]

    # check if the indivisual evenString and 
    # OddString are palindromes
    isEvenPalindrome = isPalindrome(evenString)
    isOddPalindrome = isPalindrome(oddString)

    # Check if both oddString and evenString are palindromes
    # If so, it is a twin palindrome
    if(isEvenPalindrome and isOddPalindrome):
        print("TWIN Palindrome")
    elif(isEvenPalindrome):
        print("EVEN Palindrome")
    elif(isOddPalindrome):
        print("ODD Palindrome")
    else:
        print("Alien Palindrome")

# Driver code 
s = "geeksforskeeg"
printPalindromeFamily(s)
s = "aibohobia"
printPalindromeFamily(s)
s = "geeks"
printPalindromeFamily(s)

# This code is contributed by simranjenny84
```

**Output:**

```
ODD Palindrome
PARENT Palindrome
Alien Palindrome

```