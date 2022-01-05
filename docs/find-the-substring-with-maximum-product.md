# 找到乘积最大的子串

> 原文:[https://www . geesforgeks . org/find-the-substring-with-max-product/](https://www.geeksforgeeks.org/find-the-substring-with-maximum-product/)

给定只包含大小为 **N** 的小写英文字母的字符串 **str** ，任务是找到具有最大乘积的子字符串。

> 每个英文字母都有一个值，使得 **val('a') = 0，val('b') = 1，val('c') = 2，…，val('z') = 25** 。

**例:**

> **输入:** str = "sdtfakdhdahdzz"
> **输出:** hdzz
> 这里，最大乘积为子串“hdzz”。
> 产品= 7 * 3 * 25 * 25 = 13125
> **输入:**str = " geeksforgeeks "
> **输出:** geeksforgeeks

**进场:**

*   首先，遍历给定的字符串，同时保持最大乘积值。
*   除非我们遇到一个**‘a’**，否则产品将一直增加或保持不变。因此，在每次出现**‘a’**后，开始一个新的子字符串。
*   此外，除了最大乘积值，我们还将维护最大乘积对应的子串。
*   遍历整个字符串后，打印对应于最大乘积的子字符串。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum product substring

#include <bits/stdc++.h>
using namespace std;

// Function to return the value of a character
int value(char x)
{
    return (int)(x - 'a');
}

// Function to find the maximum product substring
string maximumProduct(string str, int n)
{
    // To store substrings
    string answer = "", curr = "";
    long long maxProduct = 0, product = 1;

    for (int i = 0; i < n; i++) {
        product *= 1LL * value(str[i]);

        curr += str[i];

        // Check if current product is maximum
        // possible or not
        if (product >= maxProduct) {
            maxProduct = product;
            answer = curr;
        }

        // If product is 0
        if (product == 0) {
            product = 1;
            curr = "";
        }
    }

    // Return the substring with maximum product
    return answer;
}

// Driver code
int main()
{
    string str = "sdtfakdhdahdzz";

    int n = str.size();

    // Function call
    cout << maximumProduct(str, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum product subString

class GFG{

// Function to return the value of a character
static int value(char x)
{
    return (int)(x - 'a');
}

// Function to find the maximum product subString
static String maximumProduct(String str, int n)
{
    // To store subStrings
    String answer = "", curr = "";
    long maxProduct = 0, product = 1;

    for (int i = 0; i < n; i++) {
        product *= 1L * value(str.charAt(i));

        curr += str.charAt(i);

        // Check if current product is maximum
        // possible or not
        if (product >= maxProduct) {
            maxProduct = product;
            answer = curr;
        }

        // If product is 0
        if (product == 0) {
            product = 1;
            curr = "";
        }
    }

    // Return the subString with maximum product
    return answer;
}

// Driver code
public static void main(String[] args)
{
    String str = "sdtfakdhdahdzz";

    int n = str.length();

    // Function call
    System.out.print(maximumProduct(str, n) +"\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the maximum product sub

# Function to return the value of a character
def value(x):
    return (ord(x) - ord('a'))

# Function to find the maximum product sub
def maximumProduct(strr, n):

    # To store subs
    answer = ""
    curr = ""
    maxProduct = 0
    product = 1

    for i in range(n):
        product *=value(strr[i])

        curr += strr[i]

        # Check if current product is maximum
        # possible or not
        if (product >= maxProduct):
            maxProduct = product
            answer = curr

        # If product is 0
        if (product == 0):
            product = 1
            curr = ""

    # Return the sub with maximum product
    return answer

# Driver code
if __name__ == '__main__':
    strr = "sdtfakdhdahdzz"

    n = len(strr)

    # Function call
    print(maximumProduct(strr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the maximum product subString

using System;

public class GFG{

// Function to return the value of a character
static int value(char x)
{
    return (int)(x - 'a');
}

// Function to find the maximum product subString
static String maximumProduct(String str, int n)
{
    // To store subStrings
    String answer = "", curr = "";
    long maxProduct = 0, product = 1;

    for (int i = 0; i < n; i++) {
        product *= 1L * value(str[i]);

        curr += str[i];

        // Check if current product is maximum
        // possible or not
        if (product >= maxProduct) {
            maxProduct = product;
            answer = curr;
        }

        // If product is 0
        if (product == 0) {
            product = 1;
            curr = "";
        }
    }

    // Return the subString with maximum product
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    String str = "sdtfakdhdahdzz";

    int n = str.Length;

    // Function call
    Console.Write(maximumProduct(str, n) +"\n");

}
}
// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find the
// maximum product subString

// Function to return the value of a character
function value(x)
{
    return (x.charCodeAt() - 'a'.charCodeAt());
}

// Function to find the maximum product subString
function maximumProduct(str, n)
{
    // To store subStrings
    let answer = "", curr = "";
    let maxProduct = 0, product = 1;

    for (let i = 0; i < n; i++) {
        product *= (1 * value(str[i]));

        curr += str[i];

        // Check if current product is maximum
        // possible or not
        if (product >= maxProduct) {
            maxProduct = product;
            answer = curr;
        }

        // If product is 0
        if (product == 0) {
            product = 1;
            curr = "";
        }
    }

    // Return the subString with maximum product
    return answer;
}

// Driver Code

     let str = "sdtfakdhdahdzz";

    let n = str.length;

    // Function call
    document.write(maximumProduct(str, n) +"<br/>");

</script>
```

**Output:** 

```
hdzz
```

时间复杂度:0(N)

辅助空间:0(1)