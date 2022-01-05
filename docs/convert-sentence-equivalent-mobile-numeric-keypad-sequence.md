# 将一个句子转换成其等效的移动数字键盘序列

> 原文:[https://www . geesforgeks . org/convert-句子-等效-移动-数字-键盘-序列/](https://www.geeksforgeeks.org/convert-sentence-equivalent-mobile-numeric-keypad-sequence/)

给定一个字符串形式的句子，将其转换为等效的移动数字键盘序列。

![Mobile-keypad](img/7e82a5f8eea3ad5277c67de46daa9a8e.png)

**例:**

```
Input : GEEKSFORGEEKS
Output : 4333355777733366677743333557777
For obtaining a number, we need to press a
number corresponding to that character for 
number of times equal to position of the 
character. For example, for character C, 
we press number 2 three times and accordingly.

Input : HELLO WORLD
Output : 4433555555666096667775553
```

[推荐:请先在{IDE}上尝试您的方法，然后再继续解决方案。](https://practice.geeksforgeeks.org/problems/convert-a-sentence-into-its-equivalent-mobile-numeric-keypad-sequence0547/1)

按照下面给出的步骤将一个句子转换成它的等效移动数字键盘序列。

*   对于每个字符，存储应该在数组中相应位置获得的序列，即对于 Z，存储 9999。Y 的话，999 店。对于 K，存储 55 等等。
*   对于每个字符，减去 ASCII 值“A”，获得该字符在数组中指向的位置
    ，并将存储在该数组中的序列添加到字符串中。
*   如果字符是空格，存储 0
*   打印整个序列。

以下是上述方法的实现:

## C++

```
// C++ implementation to convert a
// sentence into its equivalent
// mobile numeric keypad sequence
#include <bits/stdc++.h>
using namespace std;

// Function which computes the sequence
string printSequence(string arr[],
                       string input)
{
    string output = "";

    // length of input string
    int n = input.length();
    for (int i=0; i<n; i++)
    {
        // Checking for space
        if (input[i] == ' ')
            output = output + "0";

        else
        {
            // Calculating index for each
            // character
            int position = input[i]-'A';
            output = output + arr[position];
        }
    }

    // Output sequence
    return output;
}

// Driver function
int main()
{
    // storing the sequence in array
    string str[] = {"2","22","222",
                    "3","33","333",
                    "4","44","444",
                    "5","55","555",
                    "6","66","666",
                    "7","77","777","7777",
                    "8","88","888",
                    "9","99","999","9999"
                   };

    string input = "GEEKSFORGEEKS";
    cout << printSequence(str, input);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to convert a
// sentence into its equivalent
// mobile numeric keypad sequence
import java.util.*;

class GFG
{

    // Function which computes the sequence
    static String printSequence(String arr[],
                               String input)
    {
        String output = "";

        // length of input string
        int n = input.length();
        for (int i = 0; i < n; i++)
        {
            // Checking for space
            if (input.charAt(i) == ' ')
                output = output + "0";

            else
            {
                // Calculating index for each
                // character
                int position = input.charAt(i) - 'A';
                output = output + arr[position];
            }
        }

        // Output sequence
        return output;
    }

    // Driver Function
    public static void main(String[] args)
    {
        // storing the sequence in array
        String str[] = {"2","22","222",
                        "3","33","333",
                        "4","44","444",
                        "5","55","555",
                        "6","66","666",
                        "7","77","777","7777",
                        "8","88","888",
                        "9","99","999","9999"
                    };

        String input = "GEEKSFORGEEKS";
        System.out.println(printSequence(str, input));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 implementation to convert
# a sentence into its equivalent
# mobile numeric keypad sequence

# Function which computes the
# sequence
def printSequence(arr, input):

# length of input string
    n = len(input)
    output = ""

    for i in range(n):

        # checking for space
        if(input[i] == ' '):
            output = output + "0"
        else:
            # calculating index for each
            # character        
            position = ord(input[i]) - ord('A')
            output = output + arr[position]
    # output sequence    
    return output

# Driver code
str = ["2", "22", "222",
       "3", "33", "333",
       "4", "44", "444",
       "5", "55", "555",
       "6", "66", "666",
       "7", "77", "777", "7777",
       "8", "88", "888",
       "9", "99", "999", "9999" ]

input = "GEEKSFORGEEKS";
print( printSequence(str, input))

# This code is contributed by upendra bartwal
```

## C#

```
// C# implementation to convert a
// sentence into its equivalent
// mobile numeric keypad sequence
using System;

class GFG
{

    // Function which computes the sequence
    static String printSequence(string []arr,
                            string input)
    {
        string output = "";

        // length of input string
        int n = input.Length;
        for (int i = 0; i < n; i++)
        {
            // Checking for space
            if (input[i] == ' ')
                output = output + "0";

            else
            {
                // Calculating index for each
                // character
                int position = input[i] - 'A';
                output = output + arr[position];
            }
        }

        // Output sequence
        return output;
    }

    // Driver Function
    public static void Main()
    {
        // storing the sequence in array
        string []str = {"2","22","222",
                        "3","33","333",
                        "4","44","444",
                        "5","55","555",
                        "6","66","666",
                        "7","77","777","7777",
                        "8","88","888",
                        "9","99","999","9999"
                    };

        string input = "GEEKSFORGEEKS";
        Console.WriteLine(printSequence(str, input));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to convert a
// sentence into its equivalent
// mobile numeric keypad sequence

// Function which computes the sequence
function printSequence(&$arr, $input)
{
    $output = "";

    // length of input string
    $n = strlen($input);
    for ($i = 0; $i < $n; $i++)
    {
        // Checking for space
        if ($input[$i] == ' ')
            $output = $output + "0";

        else
        {
            // Calculating index for each
            // character
            $position = ord($input[$i]) - ord('A');
            $output = $output . $arr[$position];
        }
    }

    // Output sequence
    return $output;
}

// Driver Code

// storing the sequence in array
$str = array("2","22","222", "3","33","333",
             "4","44","444", "5","55","555",
             "6","66","666", "7","77","777","7777",
             "8","88","888", "9","99","999","9999");

$input = "GEEKSFORGEEKS";
echo printSequence($str, $input);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation to convert a
// sentence into its equivalent
// mobile numeric keypad sequence

    // Function which computes the sequence
    function printSequence(arr,input)
    {
        let output = "";

        // length of input string
        let n = input.length;
        for (let i = 0; i < n; i++)
        {
            // Checking for space
            if (input[i] == ' ')
                output = output + "0".charCodeAt(0);

            else
            {
                // Calculating index for each
                // character
                let position = input[i].charCodeAt(0) - 'A'.charCodeAt(0);
                output = output + arr[position];
            }
        }

        // Output sequence
        return output;
    }

    // Driver Function
    let str = ["2", "22", "222",
       "3", "33", "333",
       "4", "44", "444",
       "5", "55", "555",
       "6", "66", "666",
       "7", "77", "777", "7777",
       "8", "88", "888",
       "9", "99", "999", "9999" ]

    let input = "GEEKSFORGEEKS";
    document.write(printSequence(str, input));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
4333355777733366677743333557777
```

**时间复杂度:** O(n)