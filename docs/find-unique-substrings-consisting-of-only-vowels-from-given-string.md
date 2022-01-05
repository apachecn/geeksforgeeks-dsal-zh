# 从给定的字符串中找到仅由元音组成的唯一子字符串

> 原文:[https://www . geesforgeks . org/find-unique-substrings-仅由给定字符串中的元音组成/](https://www.geeksforgeeks.org/find-unique-substrings-consisting-of-only-vowels-from-given-string/)

给定一个由大写和小写英文字母组成的大小为 **N** 的字符串 **str** 。任务是找到所有只包含元音的唯一子串。

**示例:**

> **输入:** str = "GeeksforGeeks"
> **输出:**【ee】【e】【o】
> **解释:**像“ee”这样的子串有多次出现，但这些是唯一的唯一子串。
> 
> **输入:** str = "TRAnsmission"
> **输出:**“A”、“io”、“I”、“o”
> 
> **输入:**【str = " AiraecvbcUoee】
> **输出:**【aiou】、【Aio】、【ai】、【iou】、【io】、【io】、【io】、【o】、【u】、【ae】、
> 【a】、【e】、【uoe】、【uoe】、【uou】、【oee】、【oe】、【ee】

**天真方法:** *最简单的方法是生成所有子串，检查每个子串是否只包含元音，是否唯一。使用以下步骤:*

*   *生成字符串的所有子串。*
*   *使用**映射**来跟踪唯一的子串。*
*   *如果子串仅由元音组成，且不在地图中，则将其添加到地图中，并将其存储为答案。*
*   *打印所有答案*

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a character is vowel
bool isvowel(char ch)
{
    return (ch == 'a' or ch == 'A' or
            ch == 'e' or ch == 'E'
            or ch == 'i' or ch == 'I'
            or ch == 'o' or ch == 'O' or
            ch == 'u' or ch == 'U');
}

// Function to check whether
// string contains only vowel
bool isvalid(string& s)
{
    int n = s.length();

    for (int i = 0; i < n; i++) {

        // Check if the character is
        // not vowel then invalid
        if (!isvowel(s[i]))
            return false;
    }

    return true;
}

// Function for generating
// all unique substrings of only vowels.
void generateVowelSubstrings(string params)
{
    int ans = 0;
    unordered_map<string, bool> map;

    // Generate all substring of string
    for (int i = 0; i < params.length();
         i++) {
        string temp = "";
        for (int j = i; j < params.length();
             j++) {
            temp += params[j];

            // If temp contains only vowels
            if (isvalid(temp)) {
                map[temp] = true;
            }
        }
    }

    unordered_map<string, bool>::iterator itr;
    for (itr = map.begin(); itr != map.end();
         ++itr) {

        // Printing all unique substrings.
        cout << itr->first << '\n';
    }
}

// Driver code
int main()
{
    string str = "GeeksForGeeks";
    generateVowelSubstrings(str);
    return 0;
}
```

## java 描述语言

```
<script>

// JavaScript code for the above approach

// Function to check if a character is vowel
function isvowel(ch)
{
    return (ch == 'a' || ch == 'A' || ch == 'e' ||
            ch == 'E' || ch == 'i' || ch == 'I' ||
            ch == 'o' || ch == 'O' || ch == 'u' ||
            ch == 'U');
}

// Function to check whether
// string contains only vowel
function isvalid(s)
{
    let n = s.length;

    for(let i = 0; i < n; i++)
    {

        // Check if the character is
        // not vowel then invalid
        if (!isvowel(s[i]))
            return false;
    }
    return true;
}

// Function for generating all unique
// substrings of only vowels.
function generateVowelSubstrings(params)
{
    let ans = 0;
    let map = {};

    // Generate all substring of string
    for(let i = 0; i < params.length; i++)
    {
        let temp = "";
        for(let j = i; j < params.length; j++)
        {
            temp += params[j];

            // If temp contains only vowels
            if (isvalid(temp))
            {
                map[temp] = true;
            }
        }
    }
    Object.keys(map).forEach(function (key)
    {
        document.write(key + '<br>');
    });
}

// Driver code
let str = "GeeksForGeeks";

generateVowelSubstrings(str);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
o
e
ee
```

***时间复杂度:**T3】O(N<sup>3</sup>)
*T8】辅助空间:T10】O(N)**

**高效方法:**解决这个问题更好的方法是提取所有只包含元音的最大长度子串。现在分别为所有这些子串，在 map 的帮助下生成只包含元音的唯一子串。遵循以下步骤:

*   存储所有只包含元音的最大长度子字符串(例如，对于“极客”最大长度，一个是“ee”和“aioe”)。
*   使用这些子串并从这些子串中生成更小的段，并使用**映射**来找到唯一的段。
*   打印所有唯一的字符串。

下面是上述方法的实现:

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a character is vowel
bool isVowel(string c)
{
    // Checking for vowels.
    return ((c == "a") || (c == "A") ||
            (c == "e") || (c == "E") ||
            (c == "i") || (c == "I") ||
            (c == "o") || (c == "O") ||
            (c == "u") || (c == "U"));
}

// Extracting all the maximum length
// sub-strings that contain only vowels.
unordered_map<string, bool> vowelSubstrings(
    string params)
{
    string str;

    // Using map to remove identicals
    // substrings. e.g. AiotrfAio has 2 "Aio".
    unordered_map<string, bool> map;
    for (int i = 0; i < params.length();
         i++) {
        string subString = params.substr(i, 1);
        if (isVowel(subString)) {
            str += subString;
        }
        else {

            // Storing a substring only if
            // it is not empty.
            if (!str.empty())
                map[str] = true;
            str = "";
        }
    }
    if (!str.empty())
        map[str] = true;
    return map;
}

// Function to generate all unique substrings
// containing only vowels
void generateVowelSubstrings(string params)
{
    unordered_map<string, bool> substringMap
        = vowelSubstrings(params);
    unordered_map<string, bool> map;
    // map iterator.
    unordered_map<string, bool>::iterator itr;
    for (itr = substringMap.begin();
         itr != substringMap.end(); ++itr) {
        string x = itr->first;

        // For each substring stored in map
        // generate all possible substrings.
        for (int i = 0; i < x.length(); i++) {
            for (int len = 1; len <=
                 x.length() - i; len++)
            {
                // Storing the generated
                // substring if it is
                // absent in the map.
                map[x.substr(i, len)] = true;
            }
        }
    }
    for (itr = map.begin(); itr != map.end();
         ++itr) {
        // Printing all values in map.
        cout << itr->first << '\n';
    }
}

// Driver code
int main()
{
    string str = "GeeksForGeeks";
    generateVowelSubstrings(str);
    return 0;
}
```

## java 描述语言

```
<script>
    // JavaScript code to implement above approach

    // Function to check if a character is vowel
    const isVowel = (c) => {

        // Checking for vowels.
        return ((c == "a") || (c == "A") ||
            (c == "e") || (c == "E") ||
            (c == "i") || (c == "I") ||
            (c == "o") || (c == "O") ||
            (c == "u") || (c == "U"));
    }

    // Extracting all the maximum length
    // sub-strings that contain only vowels.
    const vowelSubstrings = (params) => {
        let str = "";

        // Using map to remove identicals
        // substrings. e.g. AiotrfAio has 2 "Aio".
        let map = {};
        for (let i = 0; i < params.length; i++) {
            let subString = params.substring(i, i + 1);
            if (isVowel(subString)) {
                str += subString;
            }
            else {

                // Storing a substring only if
                // it is not empty.
                if (str.length !== 0)
                    map[str] = true;
                str = "";
            }
        }
        if (str.length !== 0)
            map[str] = true;
        return map;
    }

    // Function to generate all unique substrings
    // containing only vowels
    const generateVowelSubstrings = (params) => {
        let substringMap = vowelSubstrings(params);
        let map = {};

        // map iterator.
        for (let itr in substringMap) {
            let x = itr;

            // For each substring stored in map
            // generate all possible substrings.
            for (let i = 0; i < x.length; i++)
            {
                for (let len = 1; len <= x.length - i; len++)
                {

                    // Storing the generated
                    // substring if it is
                    // absent in the map.
                    map[x.substring(i, i + len)] = true;
                }
            }
        }
        for (let itr in map)
        {

            // Printing all values in map.
            document.write(`${itr}<br/>`);
        }
    }

    // Driver code
    let str = "GeeksForGeeks";
    generateVowelSubstrings(str);

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
o
ee
e
```

***时间复杂度:*****O(N<sup>2</sup>)
***辅助空间:*** O(N)**