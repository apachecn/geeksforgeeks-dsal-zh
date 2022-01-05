# 通过重新排列给定字符串的字符而可能出现的最大罗马数字

> 原文:[https://www . geeksforgeeks . org/最大罗马数字-通过重新排列给定字符串的可能字符/](https://www.geeksforgeeks.org/largest-roman-numeral-possible-by-rearranging-characters-of-a-given-string/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过重新排列给定字符串的字符来打印可能的最高罗马数字，如果给定字符串是有效的[罗马数字](https://en.wikipedia.org/wiki/Roman_numerals)。如果发现不可能，则打印**“无效”。**

**示例:**

> **输入:**S =**【MCMIV】
> **输出:** MMCVI
> **说明:**给定字符串 S 为有效罗马数字。重新排列字符以获得字符串“MMCVI”，使用给定的字符集生成可能的最高罗马数字。**
> 
> ****输入:**S = " XCYVM "
> T3】输出:无效**

****方式:**思路是使用[按第二元素](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)排序。按照以下步骤解决问题:**

*   **[迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。**
*   **检查字符串是否包含除 **{ 'I '，' V '，' X '，' L '，' C '，' D '，' M' }** 以外的任何字符。如发现属实，则打印“**作废”。****
*   **否则，[根据字符串字符的十进制值，对字符串进行降序排序](https://www.geeksforgeeks.org/program-sort-string-descending-order/)。**
*   **现在[将罗马值转换成等价的十进制](https://www.geeksforgeeks.org/converting-roman-numerals-decimal-lying-1-3999/)并将其存储在一个变量中，比如 **X.****
*   **现在[找到十进制数](https://www.geeksforgeeks.org/converting-decimal-number-lying-between-1-to-3999-to-roman-numerals/) **X** 的等价罗马值，并将其存储在一个变量中，比如 **Y.****
*   **如果发现 **S** 等于 **Y** ，现在打印字符串 **S** 。否则打印**“无效”。****

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find decimal
// value of a roman character
int charVal(char c)
{
    if (c == 'I')
        return 1;
    if (c == 'V')
        return 5;
    if (c == 'X')
        return 10;
    if (c == 'L')
        return 50;
    if (c == 'C')
        return 100;
    if (c == 'D')
        return 500;
    if (c == 'M')
        return 1000;

    return -1;
}

// Function to convert string representing
// roman number to equivalent decimal value
int romanToDec(string S)
{
    // Stores the decimal value
    // of the string S
    int res = 0;

    // Stores the size of the S
    int n = S.size();

    // Update res
    res = charVal(S[n - 1]);

    // Traverse the string
    for (int i = n - 2; i >= 0; i--) {

        if (charVal(S[i]) < charVal(S[i + 1]))
            res -= charVal(S[i]);
        else
            res += charVal(S[i]);
    }

    // Return res
    return res;
}

// Function to convert decimal
// to equivalent roman numeral
string DecToRoman(int number)
{
    // Stores the string
    string res = "";

    // Stores all the digit values of a roman digit
    int num[] = { 1, 4, 5, 9, 10, 40, 50,
                  90, 100, 400, 500, 900, 1000 };

    string sym[]
        = { "I", "IV", "V", "IX", "X", "XL", "L",
            "XC", "C", "CD", "D", "CM", "M" };

    int i = 12;

    // Iterate while number
    // is greater than 0
    while (number > 0) {

        int div = number / num[i];
        number = number % num[i];
        while (div--) {
            res += sym[i];
        }
        i--;
    }

    // Return res
    return res;
}

// Function to sort the string
// in descending order of values
// assigned to characters
bool compare(char x, char y)
{
    // Return character with
    // highest decimal value
    int val_x = charVal(x);
    int val_y = charVal(y);

    return (val_x > val_y);
}

// Function to find largest roman
// value possible by rearranging
// the characters of the string
string findLargest(string S)
{
    // Stores all roman characters
    set<char> st = { 'I', 'V', 'X', 'L', 'C', 'D', 'M' };

    // Traverse the string
    for (auto x : S) {

        // If X is not found
        if (st.find(x) == st.end())
            return "Invalid";
    }
    sort(S.begin(), S.end(), compare);

    // Stores the decimal value
    // of the roman number
    int N = romanToDec(S);

    // Find the roman value equivalent
    // to the decimal value of N
    string R = DecToRoman(N);

    if (S != R)
        return "Invalid";

    // Return result
    return S;
}

// Driver Code
int main()
{
    string S = "MCMIV";
    cout << findLargest(S);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find decimal
// value of a roman character
static int charVal(char c)
{
    if (c == 'I')
        return 1;
    if (c == 'V')
        return 5;
    if (c == 'X')
        return 10;
    if (c == 'L')
        return 50;
    if (c == 'C')
        return 100;
    if (c == 'D')
        return 500;
    if (c == 'M')
        return 1000;

    return -1;
}

// Function to convert string representing
// roman number to equivalent decimal value
static int romanToDec(String S)
{

    // Stores the decimal value
    // of the string S
    int res = 0;

    // Stores the size of the S
    int n = S.length();

    // Update res
    res = charVal(S.charAt(n - 1));

    // Traverse the string
    for(int i = n - 2; i >= 0; i--)
    {
        if (charVal(S.charAt(i)) <
            charVal(S.charAt(i + 1)))
            res -= charVal(S.charAt(i));
        else
            res += charVal(S.charAt(i));
    }

    // Return res
    return res;
}

// Function to convert decimal
// to equivalent roman numeral
static String DecToRoman(int number)
{

    // Stores the string
    String res = "";

    // Stores all the digit values of a roman digit
    int num[] = { 1,  4,   5,   9,   10,  40,  50,
                  90, 100, 400, 500, 900, 1000 };

    String sym[] = { "I",  "IV", "V",  "IX",
                     "X",  "XL", "L", "XC",
                     "C",  "CD", "D",  "CM", "M" };

    int i = 12;

    // Iterate while number
    // is greater than 0
    while (number > 0)
    {
        int div = number / num[i];
        number = number % num[i];

        while (div-- > 0)
        {
            res += sym[i];
        }
        i--;
    }

    // Return res
    return res;
}

// Function to find largest roman
// value possible by rearranging
// the characters of the string
static String findLargest(String S)
{
    char arr[] = { 'I', 'V', 'X', 'L', 'C', 'D', 'M' };

    // Stores all roman characters
    Set<Character> st = new HashSet<>();
    for(char x : arr)
        st.add(x);

    Character s[] = new Character[S.length()];
    for(int i = 0; i < S.length(); i++)
        s[i] = S.charAt(i);

    // Traverse the string
    for(char x : s)
    {

        // If X is not found
        if (!st.contains(x))
            return "Invalid";
    }

    Arrays.sort(s, new Comparator<Character>()
    {
        @Override
        public int compare(Character x, Character y)
        {
            return charVal(y) - charVal(x);
        }
    });

    String ss = "";
    for(char ch : s)
        ss += ch;

    // Stores the decimal value
    // of the roman number
    int N = romanToDec(ss);

    // Find the roman value equivalent
    // to the decimal value of N
    String R = DecToRoman(N);

    if (!ss.equals(R))
        return "Invalid";

    // Return result
    return ss;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String S = "MCMIV";
    int N = S.length();

    System.out.println(findLargest(S));
}
}

// This code is contributed by Kingash
```

****Output:** 

```
MMCVI
```** 

*****时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)***