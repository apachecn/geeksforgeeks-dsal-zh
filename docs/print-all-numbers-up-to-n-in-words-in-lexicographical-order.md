# 按照字典顺序打印单词中最多 N 个数字

> 原文:[https://www . geesforgeks . org/print-all-numbers-up-n-in-in-word-in-in-word-in-in-word-in-in-in-word-in-in-word-in-in-word-in-word-in-word-in-word-in-word-word-word-word-word-word](https://www.geeksforgeeks.org/print-all-numbers-up-to-n-in-words-in-lexicographical-order/)

给定一个整数 **N** ，任务是按照[字典顺序](https://en.wikipedia.org/wiki/Lexicographic_order)打印从 **1** 到 **N** ( N < 100000)的所有数字。

**示例:**

> **输入:** N = 11
> **输出:**八、十一、五、四、九、一、七、六、三、二
> **说明:**
> 从 1 到 N 的数字是 1、2、3、4、5、6、7、8、9、10、11。
> 它们各自的文字表述为{一、二、三、四、五、六、七、八、九、十、十一}。
> 它们正确的字典顺序是{八、十一、十一、五、四、九、一、七、六、三、二}。
> 
> **输入:** N = 5
> **输出:**五、四、一、三、二
> **说明:**
> 从 1 到 N 的数字是 1、2、3、4、5。
> 他们各自的文字表述是{一、二、三、四、五}。
> 它们正确的字典顺序是{五、四、一、三、二}。

**方法:**按照以下步骤解决问题:

1.  初始化一个大小为 **N + 1** 的数组 **arr[]** ，该数组在相应的索引处存储从 **1** 到 **N** 的每个索引的字符串表示。
2.  [将 **1** 到 **N** 的所有数字转换为文字](https://www.geeksforgeeks.org/convert-number-to-words/)并存储在相应的索引中。
3.  [按升序排列数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)**【arr】**。
4.  打印数组中的元素 **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert a number to words
string convert_to_words(int n)
{

    // Stores the digits
    char num[1000];
    string str = to_string(n);
    strcpy(num, str.c_str());
    char* arr_ptr = &num[0];
    int len = strlen(arr_ptr);
    string ans = "";

    // Base cases
    if (len == 0)
    {
        ans += "Empty String";
        return ans;
    }

    // Stores strings of unit place
    string single_digits[]
        = { "zero", "one", "two",   "three", "four",
            "five", "six", "seven", "eight", "nine" };

    // Stores strings for corner cases
    string two_digits[]
        = { "",          "ten",      "eleven",  "twelve",
            "thirteen",  "fourteen", "fifteen", "sixteen",
            "seventeen", "eighteen", "nineteen" };

    // Stores strings for ten's place digits
    string tens_multiple[] = {
        "",      "",      "twenty",  "thirty", "forty",
        "fifty", "sixty", "seventy", "eighty", "ninety"
    };

    // Stores strings for powers of 10
    string tens_power[] = { "hundred", "thousand" };

    // If given number contains a single digit
    if (len == 1)
    {
        ans += single_digits[num[0] - '0'];
        return ans;
    }

    // Iterate over all the digits
    int x = 0;
    while (x < len)
    {

        // Represent first 2 digits in words
        if (len >= 3)
        {
            if (num[x] - '0' != 0)
            {
                ans += single_digits[num[x] - '0'];
                ans += " ";
                ans += tens_power[len - 3];
                ans += " ";
            }
            --len;
        }

        // Represent last 2 digits in words
        else
        {

            // Explicitly handle corner cases [10, 19]
            if (num[x] - '0' == 1)
            {
                int sum = num[x] - '0' + num[x] - '0';
                ans += two_digits[sum];
                return ans;
            }

            // Explicitly handle corner case 20
            else if (num[x] - '0' == 2
                     && num[x + 1] - '0' == 0)
            {
                ans += "twenty";
                return ans;
            }

            // For rest of the two digit
            // numbers i.e., 21 to 99
            else
            {
                int i = (num[x] - '0');
                if (i > 0)
                {
                    ans += tens_multiple[i];
                    ans += " ";
                }
                else
                    ans += "";
                ++x;
                if (num[x] - '0' != 0)
                    ans += single_digits[num[x] - '0'];
            }
        }
        ++x;
    }
    return "";
}

// Function to print all the numbers
// up to n in lexicographical order
static void lexNumbers(int n)
{
    vector<string> s;

    // Convert all numbers in words
    for (int i = 1; i <= n; i++)
    {
        s.push_back(convert_to_words(i));
    }

    // Sort all strings
    sort(s.begin(), s.end());
    vector<string> ans;
    for (int i = 0; i < n; i++)
        ans.push_back(s[i]);

    // Print answer
    for (int i = 0; i < n - 1; i++)
        cout << ans[i] << ", ";
    cout << ans[n - 1];
}

// Driver Code
int main()
{
    int n = 5;
    lexNumbers(n);
    return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
class GFG {

    // Function to convert a number to words
    static String convert_to_words(int n)
    {
        // Stores the digits
        char num[] = String.valueOf(n)
                         .toCharArray();
        int len = num.length;
        String ans = "";

        // Base cases
        if (len == 0) {
            ans += "Empty String";
            return ans;
        }

        // Stores strings of unit place
        String[] single_digits = new String[] {
            "zero", "one", "two", "three", "four",
            "five", "six", "seven", "eight", "nine"
        };

        // Stores strings for corner cases
        String[] two_digits = new String[] {
            "", "ten", "eleven", "twelve",
            "thirteen", "fourteen", "fifteen", "sixteen",
            "seventeen", "eighteen", "nineteen"
        };

        // Stores strings for ten's place digits
        String[] tens_multiple = new String[] {
            "", "", "twenty", "thirty", "forty",
            "fifty", "sixty", "seventy", "eighty", "ninety"
        };

        // Stores strings for powers of 10
        String[] tens_power
            = new String[] { "hundred", "thousand" };

        // If given number contains a single digit
        if (len == 1) {
            ans += single_digits[num[0] - '0'];
            return ans;
        }

        // Iterate over all the digits
        int x = 0;
        while (x < num.length) {

            // Represent first 2 digits in words
            if (len >= 3) {
                if (num[x] - '0' != 0) {

                    ans += single_digits[num[x] - '0'];
                    ans += " ";
                    ans += tens_power[len - 3];
                    ans += " ";
                }

                --len;
            }

            // Represent last 2 digits in words
            else {

                // Explicitly handle corner cases [10, 19]
                if (num[x] - '0' == 1) {
                    int sum = num[x] - '0' + num[x] - '0';
                    ans += two_digits[sum];
                    return ans;
                }

                // Explicitly handle corner case 20
                else if (num[x] - '0' == 2
                         && num[x + 1] - '0' == 0) {
                    ans += "twenty";
                    return ans;
                }

                // For rest of the two digit
                // numbers i.e., 21 to 99
                else {
                    int i = (num[x] - '0');
                    if (i > 0) {
                        ans += tens_multiple[i];
                        ans += " ";
                    }
                    else
                        ans += "";
                    ++x;
                    if (num[x] - '0' != 0)
                        ans += single_digits[num[x] - '0'];
                }
            }
            ++x;
        }
        return "";
    }

    // Function to print all the numbers
    // up to n in lexicographical order
    static void lexNumbers(int n)
    {
        Vector<String> s = new Vector<String>();

        // Convert all numbers in words
        for (int i = 1; i <= n; i++) {
            s.add(convert_to_words(i));
        }

        // Sort all strings
        Collections.sort(s);
        Vector<String> ans
            = new Vector<String>();

        for (int i = 0; i < n; i++)
            ans.add(s.get(i));

        // Print answer
        for (int i = 0; i < n - 1; i++)
            System.out.print(
                ans.get(i) + ", ");

        System.out.print(ans.get(n - 1));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        lexNumbers(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to convert a number
# to words
def convert_to_words(n):

    # Stores the digits
    num = str(n)
    length = len(num)
    ans = ""

    # Base cases
    if (length == 0):
        ans += "Empty String"
        return ans

    # Stores strings of unit place
    single_digits = ["zero", "one", "two",
                     "three", "four", "five",
                     "six", "seven", "eight", "nine"]

    # Stores strings for corner cases
    two_digits = ["", "ten", "eleven",
                  "twelve", "thirteen",
                  "fourteen", "fifteen",
                  "sixteen", "seventeen",
                  "eighteen", "nineteen"]

    # Stores strings for ten's place digits
    tens_multiple = ["", "", "twenty",
                     "thirty", "forty",
                     "fifty", "sixty",
                     "seventy", "eighty",
                     "ninety"]

    # Stores strings for powers of 10
    tens_power = ["hundred", "thousand"]

    # If given number contains a
    # single digit
    if (length == 1):
        ans += single_digits[ord(num[0]) -
                             ord('0')]
        return ans

    # Iterate over all the digits
    x = 0

    while (x < len(num)):

        # Represent first 2 digits
        # in words
        if (length >= 3) :
            if (num[x] - '0' != 0):

                ans += single_digits[ord(num[x]) -
                                     ord('0')]
                ans += " "
                ans += tens_power[len - 3]
                ans += " "

            length -= 1

        # Represent last 2 digits in words
        else :

            # Explicitly handle corner
            # cases[10, 19]
            if (ord(num[x]) -
                ord('0') == 1):
                sum = (ord(num[x]) - ord('0' ) +
                       ord(num[x]) - ord('0'))
                ans += two_digits[sum]
                return ans

            # Explicitly handle corner
            # case 20
            elif (ord(num[x]) -
                  ord('0') == 2 and
                  ord(num[x + 1]) -
                  ord('0') == 0):
                ans += "twenty"
                return ans

            # For rest of the two digit
            # numbers i.e., 21 to 99
            else:
                i = (ord(num[x]) -
                     ord('0'))
                if (i > 0) :
                    ans += tens_multiple[i]
                    ans += " "

                else:
                  ans += ""
                  x += 1
                  if (ord(num[x]) -
                      ord('0') != 0):
                      ans += single_digits[ord(num[x]) -
                                         ord('0')]
        x += 1
    return ""

# Function to print all the numbers
# up to n in lexicographical order
def lexNumbers(n):

    s = []

    # Convert all numbers in
    # words
    for i in range(1, n + 1):
        s.append(convert_to_words(i))

    # Sort all strings
    s.sort()
    ans = []

    for i in range(n):
        ans.append(s[i])

    # Print answer
    for i in range(n - 1):
         print(ans[i], end = ", ")

    print(ans[n - 1], end = "")

# Driver Code
if __name__ == "__main__":

    n = 5
    lexNumbers(n)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to convert a number to words
static String convert_to_words(int n)
{

    // Stores the digits
    char []num = String.Join("", n).ToCharArray();
    int len = num.Length;
    String ans = "";

    // Base cases
    if (len == 0)
    {
        ans += "Empty String";
        return ans;
    }

    // Stores strings of unit place
    String[] single_digits = new String[]{
        "zero", "one", "two", "three", "four",
        "five", "six", "seven", "eight", "nine" };

    // Stores strings for corner cases
    String[] two_digits = new String[]{
        "", "ten", "eleven", "twelve",
        "thirteen", "fourteen", "fifteen", "sixteen",
        "seventeen", "eighteen", "nineteen" };

    // Stores strings for ten's place digits
    String[] tens_multiple = new String[]{
        "", "", "twenty", "thirty", "forty",
        "fifty", "sixty", "seventy", "eighty", "ninety" };

    // Stores strings for powers of 10
    String[] tens_power = new String[]{ "hundred",
                                        "thousand" };

    // If given number contains a single digit
    if (len == 1)
    {
        ans += single_digits[num[0] - '0'];
        return ans;
    }

    // Iterate over all the digits
    int x = 0;
    while (x < num.Length)
    {

        // Represent first 2 digits in words
        if (len >= 3)
        {
            if (num[x] - '0' != 0)
            {
                ans += single_digits[num[x] - '0'];
                ans += " ";
                ans += tens_power[len - 3];
                ans += " ";
            }
            --len;
        }

        // Represent last 2 digits in words
        else
        {

            // Explicitly handle corner cases [10, 19]
            if (num[x] - '0' == 1)
            {
                int sum = num[x] - '0' +
                          num[x] - '0';
                ans += two_digits[sum];
                return ans;
            }

            // Explicitly handle corner case 20
            else if (num[x] - '0' == 2 &&
                     num[x + 1] - '0' == 0)
            {
                ans += "twenty";
                return ans;
            }

            // For rest of the two digit
            // numbers i.e., 21 to 99
            else
            {
                int i = (num[x] - '0');
                if (i > 0)
                {
                    ans += tens_multiple[i];
                    ans += " ";
                }
                else
                    ans += "";

                ++x;

                if (num[x] - '0' != 0)
                    ans += single_digits[num[x] - '0'];
            }
        }
        ++x;
    }
    return "";
}

// Function to print all the numbers
// up to n in lexicographical order
static void lexNumbers(int n)
{
    List<String> s = new List<String>();

    // Convert all numbers in words
    for(int i = 1; i <= n; i++)
    {
        s.Add(convert_to_words(i));
    }

    // Sort all strings
    s.Sort();

    List<String> ans = new List<String>();

    for(int i = 0; i < n; i++)
        ans.Add(s[i]);

    // Print answer
    for(int i = 0; i < n - 1; i++)
        Console.Write(ans[i] + ", ");

    Console.Write(ans[n - 1]);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;

    lexNumbers(n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to convert a number to words
function convert_to_words(n)
{

    // Stores the digits
    let num = (n).toString().split("");

    let len = num.length;
    let ans = "";

    // Base cases
    if (len == 0)
    {
        ans += "Empty String";
        return ans;
    }

    // Stores strings of unit place
    let single_digits = [
        "zero", "one", "two", "three", "four",
        "five", "six", "seven", "eight", "nine" ];

    // Stores strings for corner cases
    let two_digits = [
        "", "ten", "eleven", "twelve",
        "thirteen", "fourteen", "fifteen", "sixteen",
        "seventeen", "eighteen", "nineteen" ];

    // Stores strings for ten's place digits
    let tens_multiple = [
        "", "", "twenty", "thirty", "forty",
        "fifty", "sixty", "seventy", "eighty", "ninety" ];

    // Stores strings for powers of 10
    let tens_power = [ "hundred", "thousand" ];

    // If given number contains a single digit
    if (len == 1)
    {
        ans += single_digits[num[0].charCodeAt(0) -
                                '0'.charCodeAt(0)];
        return ans;
    }

    // Iterate over all the digits
    let x = 0;

    while (x < num.length)
    {

        // Represent first 2 digits in words
        if (len >= 3)
        {
            if (num[x].charCodeAt(0) -
                   '0'.charCodeAt(0) != 0)
            {

                ans += single_digits[num[x].charCodeAt(0) -
                                        '0'.charCodeAt(0)];
                ans += " ";
                ans += tens_power[len - 3];
                ans += " ";
            }
            --len;
        }

        // Represent last 2 digits in words
        else
        {

            // Explicitly handle corner cases [10, 19]
            if (num[x].charCodeAt(0) -
                   '0'.charCodeAt(0) == 1)
            {
                let sum = num[x].charCodeAt(0) -
                             '0'.charCodeAt(0) +
                          num[x].charCodeAt(0) -
                             '0'.charCodeAt(0);
                ans += two_digits[sum];
                return ans;
            }

            // Explicitly handle corner case 20
            else if (num[x].charCodeAt(0) -
                        '0'.charCodeAt(0) == 2 &&
                 num[x + 1].charCodeAt(0) -
                        '0'.charCodeAt(0) == 0)
            {
                ans += "twenty";
                return ans;
            }

            // For rest of the two digit
            // numbers i.e., 21 to 99
            else
            {
                let i = (num[x].charCodeAt(0) -
                            '0'.charCodeAt(0));
                if (i > 0)
                {
                    ans += tens_multiple[i];
                    ans += " ";
                }
                else
                    ans += "";

                ++x;

                if (num[x].charCodeAt(0) -
                       '0'.charCodeAt(0) != 0)
                    ans += single_digits[num[x].charCodeAt(0) -
                                            '0'.charCodeAt(0)];
            }
        }
        ++x;
    }
    return "";
}

// Function to print all the numbers
// up to n in lexicographical order
function lexNumbers(n)
{
    let s = [];

    // Convert all numbers in words
    for(let i = 1; i <= n; i++)
    {
        s.push(convert_to_words(i));
    }

    // Sort all strings
    s.sort()
    let ans = [];

    for(let i = 0; i < n; i++)
        ans.push(s[i]);

    // Print answer
    for(let i = 0; i < n - 1; i++)
        document.write(ans[i] + ", ");

    document.write(ans[n - 1]);
}

// Driver Code
let n = 5;

lexNumbers(n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
five, four, one, three, two
```

***时间复杂度:** O(NlogN)，其中 N 是给定的整数。*
***辅助空间:** O(N)*