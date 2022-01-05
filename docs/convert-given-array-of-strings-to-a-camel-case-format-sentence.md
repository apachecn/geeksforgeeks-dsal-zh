# 将给定的字符串数组转换为驼色格式句子

> 原文:[https://www . geesforgeks . org/convert-given-array-of-string-to-a-camel-case-format-句子/](https://www.geeksforgeeks.org/convert-given-array-of-strings-to-a-camel-case-format-sentence/)

给定一个由 **N** [字符串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，每个字符串包含带有[大写或小写](https://www.geeksforgeeks.org/case-conversion-lower-upper-vice-versa-string-using-bitwise-operators-cc/)英文字母的单词，任务是使用它们创建一个[骆驼格格式的句子](https://www.geeksforgeeks.org/camel-case-given-sentence/)。

**示例:**

> **输入:**arr[]= {“AnNiruddHA Routh”、“LOVES”、“to”、“COdE daily”}
> **输出:**aniruddhadrouth LOVES To COdE daily
> **解释:**以上句子是 Camel Case 中所有给定顺序的单词的合并句子。
> 
> **输入:** arr[] = {“我”、“GOT”、“实习生”、“在极客公司实习”}
> **输出:**我在极客公司实习

**方法:**给定的问题可以通过逐个遍历每个单词并将 Camel 大小写格式中的每个字符插入结果字符串来解决，如下步骤所示:

*   创建一个空字符串来存储结果字符串
*   逐字遍历字符串数组，对于每个单词:
    *   如果字符位于第一个索引处，则以大写格式插入当前字符
    *   否则以小写格式插入所有其他字符
    *   每当一个单词结束时，在字符串中添加一个空格，除了最后一个单词(在这种情况下插入一个句号)。
*   在末尾返回结果字符串。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to convert the given array
// of strings into a sentence in the
// Camel Case formatting
string convertCase(vector<string> arr, int N)
{
    // Stores the final sentence
    string ans = "";

    // Loop to iterate over the array
    for (int i = 0; i < N; i++) {

        // If the current word is not the 1st
        // word, insert space
        if (ans.size() > 0) {
            ans += ' ';
        }

        // Insert the first character of arr[i]
        ans += toupper(arr[i][0]);

        // Loop to iterate over current array element
        for (int j = 1; j < arr[i].size(); j++) {

            // If a space is found,
            // the next character
            // should be in upper case
            if (arr[i][j] == ' ') {
                ans += ' ';
                ans += toupper(arr[i][j + 1]);
                j++;
            }

            // Otherwise the characters
            // must be in the lower case
            else {
                ans += tolower(arr[i][j]);
            }
        }
    }

    // Return Answer
    return ans;
}

// Driver program
int main()
{
    vector<string> arr{
        "AnNiruddHA Routh",
        "LOVES", "to",
        "COdE everyDAY"
    };
    int N = arr.size();

    cout << convertCase(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to convert the given array
// of strings into a sentence in the
// Camel Case formatting
static String convertCase(String[] arr, int N)
{

    // Stores the final sentence
    String ans = "";

    // Loop to iterate over the array
    for(int i = 0; i < N; i++)
    {

        // If the current word is not the 1st
        // word, insert space
        if (ans.length() > 0)
        {
            ans += ' ';
        }

        // Insert the first character of arr[i]
        ans += Character.toUpperCase(arr[i].charAt(0));

        // Loop to iterate over current array element
        for(int j = 1; j < arr[i].length(); j++)
        {

            // If a space is found,
            // the next character
            // should be in upper case
            if (arr[i].charAt(j) == ' ')
            {
                ans += ' ';
                char t = Character.toUpperCase(
                    arr[i].charAt(j + 1));
                ans += t;
                j++;
            }

            // Otherwise the characters
            // must be in the lower case
            else
            {
                ans += Character.toLowerCase(
                    arr[i].charAt(j));
            }
        }
    }

    // Return Answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String[] arr = { "AnNiruddHA Routh", "LOVES", "to",
                     "COdE everyDAY" };
    int N = arr.length;

    System.out.println(convertCase(arr, N));
}
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Function to convert the given array
# of strings into a sentence in the
# Camel Case formatting
def convertCase(arr, N) :

    # Stores the final sentence
    ans = "";

    # Loop to iterate over the array
    for i in range(N) :

        # If the current word is not the 1st
        # word, insert space
        if (len(ans) > 0) :
            ans += ' ';

        # Insert the first character of arr[i]
        ans += arr[i][0].upper();

        j = 1

        # Loop to iterate over current array element
        while j < len(arr[i]) :

            # If a space is found,
            # the next character
            # should be in upper case
            if (arr[i][j] == ' ') :
                ans += ' ';
                ans += arr[i][j + 1].upper();
                j += 1;

            # Otherwise the characters
            # must be in the lower case
            else :
                ans += arr[i][j].lower();

            j += 1;

    # Return Answer
    return ans;

# Driver program
if __name__ == "__main__" :

    arr = ["AnNiruddHA Routh","LOVES", "to","COdE everyDAY"]
    N = len(arr);
    print(convertCase(arr, N));

    # This code is contributed by AnkThon
```

## C#

```
// C# code for the above approach
using System;

class GFG
{

    // Function to convert the given array
    // of strings into a sentence in the
    // Camel Case formatting
    static String convertCase(String[] arr, int N)
    {

        // Stores the final sentence
        String ans = "";

        // Loop to iterate over the array
        for (int i = 0; i < N; i++)
        {

            // If the current word is not the 1st
            // word, insert space
            if (ans.Length > 0)
            {
                ans += ' ';
            }

            // Insert the first character of arr[i]
            ans += char.ToUpper(arr[i][0]);

            // Loop to iterate over current array element
            for (int j = 1; j < arr[i].Length; j++)
            {

                // If a space is found,
                // the next character
                // should be in upper case
                if (arr[i][j] == ' ')
                {
                    ans += ' ';
                    char t = char.ToUpper(arr[i][j + 1]);
                    ans += t;
                    j++;
                }

                // Otherwise the characters
                // must be in the lower case
                else
                {
                    ans += char.ToLower(arr[i][j]);
                }
            }
        }

        // Return Answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        String[] arr = { "AnNiruddHA Routh", "LOVES", "to",
                     "COdE everyDAY" };
        int N = arr.Length;

        Console.Write(convertCase(arr, N));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
    // JavaScript program of the above approach

    // Function to convert the given array
    // of strings into a sentence in the
    // Camel Case formatting
    const convertCase = (arr, N) => {
        // Stores the final sentence
        let ans = "";

        // Loop to iterate over the array
        for (let i = 0; i < N; i++) {

            // If the current word is not the 1st
            // word, insert space
            if (ans.length > 0) {
                ans += ' ';
            }

            // Insert the first character of arr[i]
            ans += (arr[i][0]).toUpperCase();

            // Loop to iterate over current array element
            for (let j = 1; j < arr[i].length; j++) {

                // If a space is found,
                // the next character
                // should be in upper case
                if (arr[i][j] == ' ') {
                    ans += ' ';
                    ans += (arr[i][j + 1]).toUpperCase();
                    j++;
                }

                // Otherwise the characters
                // must be in the lower case
                else {
                    ans += (arr[i][j]).toLowerCase();
                }
            }
        }

        // Return Answer
        return ans;
    }

    // Driver program

    let arr = [
        "AnNiruddHA Routh",
        "LOVES", "to",
        "COdE everyDAY"
    ];
    let N = arr.length;

    document.write(convertCase(arr, N));

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
Anniruddha Routh Loves To Code Everyday
```

***时间** **复杂度:** O(N*M)，其中 M 是所有给定字符串的平均长度*
***辅助空间:** O(N*M)*