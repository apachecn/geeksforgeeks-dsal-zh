# 替换最少数量的字符，使所有字符成对出现

> 原文:[https://www . geesforgeks . org/replace-最小字符数-使所有字符成对区分/](https://www.geeksforgeeks.org/replace-minimal-number-of-characters-to-make-all-characters-pair-wise-distinct/)

给定一个仅由小写英文字母组成的字符串。任务是在给定的字符串中找到最小数量的字符并用任何小写字符替换，以便由该字符串形成的所有字符对都是不同的。如果做不到，打印“不可能”。
**注**:如果可能的答案不止一个，打印字典最小的字符串。

**示例**:

> **输入** : str = "xxxxyyyy"
> **输出**:abcxdefe
> 在上面的例子中，x 出现了 4 次，y 出现了 4 次，所以我们可以把 x 的 3 次改为 a、b 和 c，再把 y 的 3 次改为 d、e、f，这样所有的字符就成对区分了。
> 
> **输入** : str =“无答案的历史最有可能”
> **输出**:不可能
> 改变字符使所有字符成对清晰是不可能的。

**方法:**问题基于字符串中每个字符出现的频率。如果字符串的长度大于 26，那么总是不可能使字符成对区分，因为英语字母表中只有 26 个小写字符。
如果字符串的长度小于或等于 26，

1.  创建一个哈希数组来存储字符串中所有字符的频率。
2.  开始解开绳子。
3.  检查字符串中当前字符的频率是否大于 1。
4.  如果是，则遍历哈希并找到从“a”开始的第一个字符，该字符尚未出现在字符串中。
5.  降低字符串中当前字符的频率，并用哈希中的当前字符替换字符串中的当前字符。

下面是上述方法的实现:

## C++

```
// C++ program to replace minimal number of
// characters to make all characters
// pair wise distinct

#include <iostream>
#include <string>

using namespace std;

// Function to replace minimal number of
// characters to make all characters
// pair wise distinct
void minReplacement(string str)
{
    // If length of string is greater than 26,
    // it is impossible to make characters
    // pair wise distinct
    if (str.length() > 26)
        cout << "IMPOSSIBLE";
    else {
        // Array to store frequency of each
        // character
        int hash[26] = { 0 };

        // Store frequency of each character
        for (int i = 0; i < str.length(); i++)
            hash[str[i] - 'a']++;

        int count = 0;

        // Start traversing the string
        for (int i = 0; i < str.length(); i++) {

            // Check if frequency of current character
            // is greater than 1
            if (hash[str[i] - 'a'] > 1) {

                // Traverse the hash
                for (int j = 0; j < 26; j++) {

                    // Find the first character starting from 'a'
                    // which have not appeared in the string yet
                    if (hash[j] == 0) {

                        // Reduce the frequency of current
                        // character in the string
                        hash[str[i] - 'a']--;

                        // Replace the current character in string
                        // by current character in hash
                        str[i] = (char)(j + 'a');

                        // Increment the frequency of
                        // this char in hash
                        hash[j]++;

                        break;
                    }
                }
            }
        }

        // Print the modified string
        cout << str;
    }
}

// Driver code
int main()
{
    string str = "xxxxyyyy";

    minReplacement(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace minimal number of
// characters to make all characters
// pair wise distinct 

class GFG {

// Function to replace minimal number of
// characters to make all characters
// pair wise distinct
    static void minReplacement(String str) {
        // If length of String is greater than 26,
        // it is impossible to make characters
        // pair wise distinct
        if (str.length() > 26) {
            System.out.println("IMPOSSIBLE");
        } else {
            // Array to store frequency of each
            // character
            int hash[] = new int[26];

            // Store frequency of each character
            for (int i = 0; i < str.length(); i++) {
                hash[str.charAt(i) - 'a']++;
            }

            int count = 0;

            // Start traversing the String
            for (int i = 0; i < str.length(); i++) {

                // Check if frequency of current character
                // is greater than 1
                if (hash[str.charAt(i) - 'a'] > 1) {

                    // Traverse the hash
                    for (int j = 0; j < 26; j++) {

                        // Find the first character starting from 'a'
                        // which have not appeared in the String yet
                        if (hash[j] == 0) {

                            // Reduce the frequency of current
                            // character in the String
                            hash[str.charAt(i) - 'a']--;

                            // Replace the current character in String
                            // by current character in hash
                            str = str.substring(0, i) + (char) (j + 'a') + str.substring(i + 1);
                            //str[i] = (char)(j + 'a');

                            // Increment the frequency of
                            // this char in hash
                            hash[j]++;

                            break;
                        }
                    }
                }
            }

            // Print the modified String
            System.out.println(str);
        }
    }
// Driver code

    public static void main(String[] args) {
        String str = "xxxxyyyy";

        minReplacement(str);
    }
}

/* This Java code is contributed by Rajput-Ji*/
```

## 蟒蛇 3

```
# Python3 program to replace minimal
# number of characters to make all
# characters pair wise distinct

# Function to replace minimal
# number of characters to make all
# characters pair wise distinct
def minReplacement(string):

    # If length of string is greater
    # than 26, it is impossible to make
    # characters pair wise distinct
    if len(string) > 26:
        print("IMPOSSIBLE")
    else:

        # Array to store frequency of each
        # character
        Hash = [0] * 26

        # Store frequency of each character
        for i in range(0, len(string)):
            Hash[ord(string[i]) - ord('a')] += 1

        count = 0

        # Start traversing the string
        for i in range(0, len(string)):

            # Check if frequency of current
            # character is greater than 1
            if Hash[ord(string[i]) - ord('a')] > 1:

                # Traverse the hash
                for j in range(0, 26):

                    # Find the first character starting from 'a'
                    # which have not appeared in the string yet
                    if Hash[j] == 0:

                        # Reduce the frequency of current
                        # character in the string
                        Hash[ord(string[i]) - ord('a')] -= 1

                        # Replace the current character in
                        # string by current character in hash
                        string[i] = chr(j + ord('a'))

                        # Increment the frequency
                        # of this char in hash
                        Hash[j] += 1

                        break

        # Print the modified string
        print(''.join(string))

# Driver code
if __name__ == "__main__":

    string = "xxxxyyyy"

    minReplacement(list(string))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to replace minimal
// number of characters to make
// all characters pair wise distinct
using System;

class GFG
{

// Function to replace minimal number 
// of characters to make all characters
// pair wise distinct
static void minReplacement(String str)
{
    // If length of String is greater 
    // than 26, it is impossible to
    // make characters pair wise distinct
    if (str.Length > 26)
    {
        Console.WriteLine("IMPOSSIBLE");
    }
    else
    {
        // Array to store frequency
        // of each character
        int []hash = new int[26];

        // Store frequency of each character
        for (int i = 0; i < str.Length; i++)
        {
            hash[str[i] - 'a']++;
        }
        // Start traversing the String
        for (int i = 0; i < str.Length; i++)
        {

            // Check if frequency of current
            // character is greater than 1
            if (hash[str[i] - 'a'] > 1)
            {

                // Traverse the hash
                for (int j = 0; j < 26; j++)
                {

                    // Find the first character
                    // starting from 'a' which
                    // have not appeared in the
                    // String yet
                    if (hash[j] == 0)
                    {

                        // Reduce the frequency of current
                        // character in the String
                        hash[str[i] - 'a']--;

                        // Replace the current character in
                        // String by current character in hash
                        str = str.Substring(0, i) +
                                 (char) (j + 'a') +
                              str.Substring(i + 1);
                        //str[i] = (char)(j + 'a');

                        // Increment the frequency of
                        // this char in hash
                        hash[j]++;

                        break;
                    }
                }
            }
        }

        // Print the modified String
        Console.WriteLine(str);
    }
}

// Driver code
public static void Main()
{
    String str = "xxxxyyyy";

    minReplacement(str);
}
}

// This code is contributed
// by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to replace minimal number
// of characters to make all characters
// pair wise distinct

// Function to replace minimal number
// of characters to make all characters
// pair wise distinct
function minReplacement($str)
{
    // If length of string is greater than 26,
    // it is impossible to make characters
    // pair wise distinct
    if (strlen($str) > 26)
        echo "IMPOSSIBLE";
    else
    {
        // Array to store frequency of
        // each character
        $hash = array_fill(0, 26, NULL);

        // Store frequency of each character
        for ($i = 0; $i < strlen($str); $i++)
            $hash[ord($str[$i]) - ord('a')]++;

        $count = 0;

        // Start traversing the string
        for ($i = 0; $i < strlen($str); $i++)
        {

            // Check if frequency of current
            // character is greater than 1
            if ($hash[ord($str[$i]) - ord('a')] > 1)
            {

                // Traverse the hash
                for ($j = 0; $j < 26; $j++)
                {

                    // Find the first character starting from 'a'
                    // which have not appeared in the string yet
                    if ($hash[$j] == 0)
                    {

                        // Reduce the frequency of current
                        // character in the string
                        $hash[ord($str[$i]) - ord('a')]--;

                        // Replace the current character in
                        // string by current character in hash
                        $str[$i] = chr($j + ord('a'));

                        // Increment the frequency of
                        // this char in hash
                        $hash[$j]++;

                        break;
                    }
                }
            }
        }

        // Print the modified string
        echo $str;
    }
}

// Driver code
$str = "xxxxyyyy";
minReplacement($str);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to replace minimal number of
// characters to make all characters
// pair wise distinct 

// Function to replace minimal number of
// characters to make all characters
// pair wise distinct
    function minReplacement(str)
    {
        // If length of String is greater than 26,
        // it is impossible to make characters
        // pair wise distinct
        if (str.length > 26) {
            document.write("IMPOSSIBLE<br>");
        }
        else {
            // Array to store frequency of each
            // character
            let hash = new Array(26);
            for(let i=0;i<26;i++)
            {
                hash[i]=0;
            }

            // Store frequency of each character
            for (let i = 0; i < str.length; i++) {
                hash[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;
            }

            let count = 0;

            // Start traversing the String
            for (let i = 0; i < str.length; i++) {

                // Check if frequency of current character
                // is greater than 1
                if (hash[str[i].charCodeAt(0) - 'a'.charCodeAt(0)] > 1) {

                    // Traverse the hash
                    for (let j = 0; j < 26; j++) {

                        // Find the first character starting from 'a'
                        // which have not appeared in the String yet
                        if (hash[j] == 0) {

                            // Reduce the frequency of current
                            // character in the String
                            hash[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]--;

                            // Replace the current character in String
                            // by current character in hash
                            str = str.substring(0, i) +
                              String.fromCharCode(j + 'a'.charCodeAt(0)) +
                              str.substring(i + 1);
                            //str[i] = (char)(j + 'a');

                            // Increment the frequency of
                            // this char in hash
                            hash[j]++;

                            break;
                        }
                    }
                }
            }

            // Print the modified String
            document.write(str);
        }
    }

    // Driver code
    let str = "xxxxyyyy";
    minReplacement(str);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
abcxdefy
```

**时间复杂度:** O(N)，其中 N 为字符串的长度

**辅助空间:** O(1)