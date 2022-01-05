# 制作一串 Panagram 的成本

> 原文:[https://www . geesforgeks . org/字符串制作成本-panagram/](https://www.geeksforgeeks.org/cost-to-make-a-string-panagram/)

给定一个数组**arr【】**包含添加来自**(a–z)**的每个字母表的成本，以及一个字符串 **str** ，它可能是也可能不是一个 [Panagram](https://www.geeksforgeeks.org/pangram-checking/) 。任务是找到制作字符串 Panagram 的总成本。

**示例:**

> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10，11，12，13，14，15，16，17，18，19，20，21，22，23，24，25，26}，
> str = " abcdefghijklmopsutvwz "
> T4】输出: 63
> n，x 和 y 是唯一缺少的字符
> 它们的成本分别是 14、24、25。
> 因此，总成本= 14 + 24 + 25 = 63
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10，11，12，13，14，15，16，17，18，19，20，21，22，23，24，25，26}，
> str = " The quickbrownfoxpjumpershiphelazydog "
> **输出:** 0
> 该字符串已经是一个 Pangram，因为它包含了所有

**方法:**标记所有出现在**字符串**中的**(a–z)**的字母，然后找到字符串中缺失的字母。将这些缺失字母的成本相加，得到制作字符串 Pangram 所需的总成本。

下面是上述方法的实现:

## C++

```
// C++ program to find the cost to make a string Panagram
#include <bits/stdc++.h>
using namespace std;

// Function to return the total cost required
// to make the string Pangram
int pangramCost(int arr[], string str)
{
    int cost = 0;
    bool occurred[26] = { false };

    // Mark all the alphabets that occurred in the string
    for (int i = 0; i < str.size(); i++)
        occurred[str[i] - 'a'] = true;

    // Calculate the total cost for the missing alphabets
    for (int i = 0; i < 26; i++) {
        if (!occurred[i])
            cost += arr[i];
    }

    return cost;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15,
                  16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26 };
    string str = "abcdefghijklmopqrstuvwz";

    cout << pangramCost(arr, str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the cost to make a string Panagram

class GFG
{
        // Function to return the total cost required
        // to make the string Pangram
        static  int pangramCost(int arr[], String str)
        {
            int cost = 0;
            boolean []occurred=new boolean[26];

            for(int i=0;i<26;i++)
             occurred[i]=false;

            // Mark all the alphabets that occurred in the string
            for (int i = 0; i < str.length(); i++)
                occurred[str.charAt(i) - 'a'] = true;

            // Calculate the total cost for the missing alphabets
            for (int i = 0; i < 26; i++) {
                if (occurred[i]==false)
                    cost += arr[i];
            }

            return cost;
        }

        // Driver Code
        public static void main(String []args)
        {
            int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15,
                        16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26 };
            String str = "abcdefghijklmopqrstuvwz";

            System.out.println(pangramCost(arr, str));

    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to find the cost
# to make a string Panagram

# Function to return the total cost
# required to make the string Pangram
def pangramCost(arr, string) :

    cost = 0
    occurred = [False] * 26

    # Mark all the alphabets that
    # occurred in the string
    for i in range(len(string)) :
        occurred[ord(string[i]) - ord('a')] = True

    # Calculate the total cost for
    # the missing alphabets
    for i in range(26) :
        if (not occurred[i]) :
            cost += arr[i]

    return cost

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9,
            10, 11, 12, 13, 14, 15, 16,
            17, 18, 19, 20, 21, 22, 23,
            24, 25, 26 ]
    string = "abcdefghijklmopqrstuvwz"

    print(pangramCost(arr, string))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the cost to make a string Panagram

using System;
class GFG
{
        // Function to return the total cost required
        // to make the string Pangram
        static  int pangramCost(int []arr, string str)
        {
            int cost = 0;
            bool []occurred=new bool[26];

            for(int i=0;i<26;i++)
             occurred[i]=false;

            // Mark all the alphabets that occurred in the string
            for (int i = 0; i < str.Length; i++)
                occurred[str[i] - 'a'] = true;

            // Calculate the total cost for the missing alphabets
            for (int i = 0; i < 26; i++) {
                if (occurred[i]==false)
                    cost += arr[i];
            }

            return cost;
        }

        // Driver Code
        public static void Main(string []args)
        {
            int []arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15,
                        16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26 };
            string str = "abcdefghijklmopqrstuvwz";

            Console.WriteLine(pangramCost(arr, str));

    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the cost to make
// a string Panagram

// Function to return the total cost
// required to make the string Pangram
function pangramCost($arr, $str)
{
    $cost = 0;
    $occurred = array();

    for($i = 0; $i < 26; $i++)
        $occurred[$i] = false;

    // Mark all the alphabets that occurred
    // in the string
    for($i = 0; $i < strlen($str); $i++)
    {

        $idx = ord($str[$i]) - 97;
        $occurred[$idx] = true;
    }

    // Calculate the total cost for the
    // missing alphabets
    for($i = 0; $i < 26; $i++)
    {
        if ($occurred[$i] == false)
            $cost += $arr[$i];
    }

    return $cost;
}

// Driver Code
$arr = array( 1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
             11, 12, 13, 14, 15, 16, 17, 18,
             19, 20, 21, 22, 23, 24, 25, 26 );
$str = "abcdefghijklmopqrstuvwz";

echo pangramCost($arr, $str);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>

// Javascript program to find the cost to
// make a string Panagram

// Function to return the total cost required
// to make the string Pangram
function pangramCost(arr, str)
{
    var cost = 0;
    var occurred = new Array(26);

    for(let i = 0; i < 26; i++)
        occurred[i] = false;

    // Mark all the alphabets that occurred
    // in the string
    for(let i = 0; i < str.length; i++)
        occurred[str[i].charCodeAt() -
                    'a'.charCodeAt()] = true;

    // Calculate the total cost for
    // the missing alphabets
    for(let i = 0; i < 26; i++)
    {
        if (occurred[i] == false)
            cost += arr[i];
    }
    return cost;
}

// Driver Code
var arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
            11, 12, 13, 14, 15, 16, 17, 18,
            19, 20, 21, 22, 23, 24, 25, 26 ];
var str = "abcdefghijklmopqrstuvwz";

document.write(pangramCost(arr, str));

// This code is contributed by bunnyram19

</script>
```

**Output:** 

```
63
```