# 从给定的字符串中找出最大可能的二进制数

> 原文:[https://www . geeksforgeeks . org/从给定字符串中找到最大可能的二进制数/](https://www.geeksforgeeks.org/find-the-maximum-possible-binary-number-from-given-string/)

给定由集合 **{'o '，' n '，' e '，' z '，' r'}** 中的字符组成的字符串 **str** ，任务是通过重新排列给定字符串的字符来找到最大可能的二进制数。请注意，该字符串将至少形成一个有效的数字。

**示例:**

> **输入:**str = " roeenzooe "
> **输出:**110
> “one zero”为必输字符串。
> 
> **输入:**str = " zero zerone "
> T3】输出: 1000

**方法:**创建一个地图，并在其中存储**【z】**和**【n】**的频率，因为这些是唯一只会出现在 0 或 1 中而不会同时出现在 0 和 1 中的字符。字符串中 1 的数量将等于 **'n'** 的频率，字符串中 0 的数量将等于地图中 **'z'** 的频率。现在要找到最大的数字，打印所有的 1，然后是所有的 0。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum number
// that can be formed from the string
string maxNumber(string str, int n)
{
    // To store the frequency of 'z' and 'n'
    // in the given string
    int freq[2] = { 0 };

    for (int i = 0; i < n; i++) {
        if (str[i] == 'z') {

            // Number of zeroes
            freq[0]++;
        }
        else if (str[i] == 'n') {

            // Number of ones
            freq[1]++;
        }
    }

    // To store the required number
    string num = "";

    // Add all the ones
    for (int i = 0; i < freq[1]; i++)
        num += '1';

    // Add all the zeroes
    for (int i = 0; i < freq[0]; i++)
        num += '0';

    return num;
}

// Driver code
int main()
{
    string str = "roenenzooe";
    int n = str.length();

    cout << maxNumber(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return maximum number
    // that can be formed from the string
    static String maxNumber(String str, int n)
    {

        // To store the frequency of 'z' and 'n'
        // in the given string
        int[] freq = new int[2];

        for (int i = 0; i < n; i++)
        {
            if (str.charAt(i) == 'z')

                // Number of zeroes
                freq[0]++;

            else if (str.charAt(i) == 'n')

                // Number of ones
                freq[1]++;
        }

        // To store the required number
        String num = "";

        // Add all the ones
        for (int i = 0; i < freq[1]; i++)
            num += '1';

        // Add all the zeroes
        for (int i = 0; i < freq[0]; i++)
            num += '0';

        return num;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "roenenzooe";
        int n = str.length();

        System.out.println(maxNumber(str, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return maximum number
# that can be formed from the string
def maxNumber(string , n) :

    # To store the frequency of 'z' and 'n'
    # in the given string
    freq = [0, 0]

    for i in range(n) :
        if (string[i] == 'z') :

            # Number of zeroes
            freq[0] += 1;

        elif (string[i] == 'n') :

            # Number of ones
            freq[1] += 1;

    # To store the required number
    num = "";

    # Add all the ones
    for i in range(freq[1]) :
        num += '1';

    # Add all the zeroes
    for i in range(freq[0]) :
        num += '0';

    return num;

# Driver code
if __name__ == "__main__" :

    string = "roenenzooe";
    n = len(string);

    print(maxNumber(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return maximum number
    // that can be formed from the string
    static string maxNumber(string str, int n)
    {
        // To store the frequency of 'z' and 'n'
        // in the given string
        int [] freq = new int[2];

        for (int i = 0; i < n; i++)
        {
            if (str[i] == 'z')
            {

                // Number of zeroes
                freq[0]++;
            }
            else if (str[i] == 'n')
            {

                // Number of ones
                freq[1]++;
            }
        }

        // To store the required number
        string num = "";

        // Add all the ones
        for (int i = 0; i < freq[1]; i++)
            num += '1';

        // Add all the zeroes
        for (int i = 0; i < freq[0]; i++)
            num += '0';

        return num;
    }

    // Driver code
    public static void Main()
    {
        string str = "roenenzooe";
        int n = str.Length;
        Console.Write(maxNumber(str, n));
    }
}

// This code is contributed by Sanjit Prasad
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return maximum number
// that can be formed from the string
function maxNumber(str, n)
{
    // To store the frequency of 'z' and 'n'
    // in the given string
    var freq = Array(2).fill(0);

    for (var i = 0; i < n; i++) {
        if (str[i] == 'z') {

            // Number of zeroes
            freq[0]++;
        }
        else if (str[i] == 'n') {

            // Number of ones
            freq[1]++;
        }
    }

    // To store the required number
    var num = "";

    // Add all the ones
    for (var i = 0; i < freq[1]; i++)
        num += '1';

    // Add all the zeroes
    for (var i = 0; i < freq[0]; i++)
        num += '0';

    return num;
}

// Driver code
var str = "roenenzooe";
var n = str.length;
document.write( maxNumber(str, n));

</script>
```

**Output:** 

```
110
```

**时间复杂度:** O(N)