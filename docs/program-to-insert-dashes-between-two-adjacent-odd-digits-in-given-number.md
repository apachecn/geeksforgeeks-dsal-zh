# 程序在给定数字

的两个相邻奇数位之间插入破折号

> 原文:[https://www . geesforgeks . org/program-to-insert-破折号-两个相邻奇数位之间-给定数字/](https://www.geeksforgeeks.org/program-to-insert-dashes-between-two-adjacent-odd-digits-in-given-number/)

给定一个字符串形式的大数 **N** ，任务是以字符串形式在给定数中相邻的两个奇数位之间插入一个破折号。

**示例:**

> **输入:** N = 1745389
> **输出:** 1-745-389
> **说明:**
> 在字符串 str 中，str[0]和 str[1]都是连续的奇数，所以在它们之间插入一个破折号。
> **输入:** N = 34657323128437
> **输出:** 3465-7-323-12843-7

**逐位逼近:**

1.  逐个字符遍历整个数字串。
2.  使用逻辑[按位“或”和“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)运算符比较每个连续字符。
3.  如果字符串的两个连续字符是奇数，请在其中插入破折号(-)并检查接下来的两个连续字符。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <string>
using namespace std;

// Function to check if char ch is
// odd or not
bool checkOdd(char ch)
{
    return ((ch - '0') & 1);
}

// Function to insert dash - between
// any 2 consecutive digit in string str
string Insert_dash(string num_str)
{

    string result_str = num_str;

    // Traverse the string character
    // by character
    for (int x = 0;
         x < num_str.length() - 1; x++) {

        // Compare every consecutive
        // character with the odd value
        if (checkOdd(num_str[x])
            && checkOdd(num_str[x + 1])) {

            result_str.insert(x + 1, "-");
            num_str = result_str;
            x++;
        }
    }

    // Print the resultant string
    return result_str;
}

// Driver Code
int main()
{

    // Given number in form of string
    string str = "1745389";

    // Function Call
    cout << Insert_dash(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if char ch is
// odd or not
static boolean checkOdd(char ch)
{
    return ((ch - '0') & 1) != 0 ?
            true : false;
}

// Function to insert dash - between
// any 2 consecutive digit in string str
static String Insert_dash(String num_str)
{
    StringBuilder result_str = new StringBuilder(num_str);

    // Traverse the string character
    // by character
    for(int x = 0; x < num_str.length() - 1; x++)
    {

        // Compare every consecutive
        // character with the odd value
        if (checkOdd(num_str.charAt(x)) &&
            checkOdd(num_str.charAt(x + 1)))
        {
            result_str.insert(x + 1, "-");
            num_str = result_str.toString();
            x++;
        }
    }

    // Print the resultant string
    return result_str.toString();
}

// Driver Code
public static void main(String[] args)
{

    // Given number in form of string
    String str = "1745389";

    // Function call
    System.out.println(Insert_dash(str));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if char ch is
# odd or not
def checkOdd(ch):

    return ((ord(ch) - 48) & 1)

# Function to insert dash - between
# any 2 consecutive digit in string str
def Insert_dash(num_str):

    result_str = num_str

    # Traverse the string character
    # by character
    x = 0
    while(x < len(num_str) - 1):

        # Compare every consecutive
        # character with the odd value
        if (checkOdd(num_str[x]) and
            checkOdd(num_str[x + 1])):

            result_str = (result_str[:x + 1] + '-' +
                          result_str[x + 1:])
            num_str = result_str
            x += 1
        x += 1

    # Print the resultant string
    return result_str

# Driver Code

# Given number in form of string
str = "1745389"

# Function call
print(Insert_dash(str))

# This code is contributed by vishu2908
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Text;
class GFG{

// Function to check if char ch is
// odd or not
static bool checkOdd(char ch)
{
    return ((ch - '0') & 1) != 0 ?
            true : false;
}

// Function to insert dash - between
// any 2 consecutive digit in string str
static String Insert_dash(String num_str)
{
    StringBuilder result_str = new StringBuilder(num_str);

    // Traverse the string character
    // by character
    for(int x = 0; x < num_str.Length - 1; x++)
    {

        // Compare every consecutive
        // character with the odd value
        if (checkOdd(num_str[x]) &&
            checkOdd(num_str[x + 1]))
        {
            result_str.Insert(x + 1, "-");
            num_str = result_str.ToString();
            x++;
        }
    }

    // Print the resultant string
    return result_str.ToString();
}

// Driver Code
public static void Main(String[] args)
{

    // Given number in form of string
    String str = "1745389";

    // Function call
    Console.WriteLine(Insert_dash(str));
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
1-745-389
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**正则表达式方法:**

给定的问题可以使用[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)来解决。这个问题的答案是:

> **(？<=【13579】)(？=[13579])**
> 给定的 RE 在奇数之间匹配。我们可以用破折号替换零宽度的匹配部分，即
> **str = str.replaceAll((？< =[13579])(？=[13579])", "-");**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
#include <regex>
using namespace std;

// Function to insert dash - between
// any 2 consecutive odd digit
string Insert_dash(string str)
{

  // Get the regex to be checked
  const regex pattern("([13579])([13579])");

  // Replaces the matched value
  // (here dash) with given string
  return regex_replace(str, pattern, "$1-$2");;
}

// Driver Code
int main()
{
  string str = "1745389";
  cout << Insert_dash(str);
  return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.regex.*;

public class GFG {

    // Function to insert dash - between
    // any 2 consecutive odd digit
    public static String Insert_dash(String str)
    {

        // Get the regex to be checked
        String regex = "(?<=[13579])(?=[13579])";

        // Create a pattern from regex
        Pattern pattern = Pattern.compile(regex);

        // Create a matcher for the input String
        Matcher matcher
            = pattern.matcher(str);

        // Get the String to be replaced,
        // i.e. here dash
        String stringToBeReplaced = "-";
        StringBuilder builder
            = new StringBuilder();

        // Replace every matched pattern
        // with the target String
        // using replaceAll() method
        return (matcher
                    .replaceAll(stringToBeReplaced));
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given number in form of string
        String str = "1745389";

        // Function Call
        System.out.println(Insert_dash(str));
    }
}
```

## 计算机编程语言

```
# Python program for the above approach
import re

# Function to insert dash - between
# any 2 consecutive odd digit
def Insert_dash(str):

    # Get the regex to be checked
    regex = "(?<=[13579])(?=[13579])"

    return re.sub(regex,'\1-\2', str)

# Driver Code

# Given number in form of string
str = "1745389"

# Function Call
print(Insert_dash(str))

# This code is contributed by yuvraj_chandra
```

**Output:** 

```
1-745-389
```