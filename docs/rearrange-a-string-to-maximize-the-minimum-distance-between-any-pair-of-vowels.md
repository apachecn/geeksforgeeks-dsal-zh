# 重新排列一个字符串，使任意一对元音之间的最小距离最大化

> 原文:[https://www . geesforgeks . org/重排字符串以最大化任意对元音之间的最小距离/](https://www.geeksforgeeks.org/rearrange-a-string-to-maximize-the-minimum-distance-between-any-pair-of-vowels/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是重新排列给定字符串的字符，使得任意一对元音之间的最小距离最大。

**示例:**

> **输入:** str = "aacbbc"
> **输出:**abbca
> **解释:**唯一一对元音之间最大化的距离是 **4** 。
> 
> **输入:**输出:阿巴巴克

**方法:**按照以下步骤解决问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，统计字符串 **str** 中存在的元音和辅音数量，分别说出**N<sub>v</sub>T7】和**N<sub>c</sub>T11】。****
*   现在，使用以下公式计算每对元音之间可以放入的辅音的最大数量:

> ***M =向下舍入【N<sub>c</sub>/(N<sub>v</sub>–1】***

*   现在，通过放置所有元音，然后在配对的每个相邻元音之间插入 **M** 辅音，来构建结果字符串。
*   构造结果字符串后，如果还有辅音，只需将它们插入字符串的末尾。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the string
// such that the minimum distance
// between any of vowels is maximum.
string solution(string s)
{

    // Store vowels and consonants
    vector<char> vowel, consonant;

    // Iterate over the characters
    // of string
    for (auto i : s) {

        // If current character is a vowel
        if (i == 'a' || i == 'e'
            || i == 'i' || i == 'o'
            || i == 'u') {

            vowel.push_back(i);
        }

        // If current character is
        // a consonant
        else {

            consonant.push_back(i);
        }
    }

    // Stores count of vowels and
    // consonants respectively
    int Nc, Nv;
    Nv = vowel.size();
    Nc = consonant.size();

    int M = Nc / (Nv - 1);

    // Stores the resultant string
    string ans = "";

    // Stores count of consonants
    // appended into ans
    int consotnant_till = 0;

    for (auto i : vowel) {

        // Append vowel to ans
        ans += i;
        int temp = 0;

        // Append consonants
        for (int j = consotnant_till;
             j < min(Nc, consotnant_till + M);
             j++) {

            // Append consonant to ans
            ans += consonant[j];

            // Update temp
            temp++;
        }

        // Remove the taken
        // elements of consonant
        consotnant_till += temp;
    }

    // Return final ans
    return ans;
}

// Driver Code
int main()
{
    string str = "aaaabbbcc";

    // Function Call
    cout << solution(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to rearrange the String
// such that the minimum distance
// between any of vowels is maximum.
static String solution(String s)
{

    // Store vowels and consonants
    Vector<Character> vowel = new Vector<Character>();
    Vector<Character> consonant = new Vector<Character>();

    // Iterate over the characters
    // of String
    for (char i : s.toCharArray())
    {

        // If current character is a vowel
        if (i == 'a' || i == 'e'
            || i == 'i' || i == 'o'
            || i == 'u')
        {

            vowel.add(i);
        }

        // If current character is
        // a consonant
        else
        {

            consonant.add(i);
        }
    }

    // Stores count of vowels and
    // consonants respectively
    int Nc, Nv;
    Nv = vowel.size();
    Nc = consonant.size();
    int M = Nc / (Nv - 1);

    // Stores the resultant String
    String ans = "";

    // Stores count of consonants
    // appended into ans
    int consotnant_till = 0;
    for (char i : vowel)
    {

        // Append vowel to ans
        ans += i;
        int temp = 0;

        // Append consonants
        for (int j = consotnant_till;
             j < Math.min(Nc, consotnant_till + M);
             j++) {

            // Append consonant to ans
            ans += consonant.get(j);

            // Update temp
            temp++;
        }

        // Remove the taken
        // elements of consonant
        consotnant_till += temp;
    }

    // Return final ans
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String str = "aaaabbbcc";

    // Function Call
    System.out.print(solution(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to rearrange the string
# such that the minimum distance
# between any of vowels is maximum.
def solution(S):

    # store vowels and consonants
    vowels = []
    consonants = []

    # Iterate over the
    # characters of string
    for i in S:

        # if current character is a vowel
        if (i == 'a' or i == 'e' or i == 'i' or i == 'o' or i == 'u'):
            vowels.append(i)

        # if current character is consonant
        else:
            consonants.append(i)

    # store count of vowels and
    # consonants respectively
    Nc = len(consonants)
    Nv = len(vowels)
    M = Nc // (Nv - 1)

    # store the resultant string
    ans = ""

    # store count of consonants
    # append into ans
    consonant_till = 0

    for i in vowels:
        # Append vowel to ans
        ans += i
        temp = 0

        # Append consonants
        for j in range(consonant_till, min(Nc, consonant_till + M)):

            # Appendconsonant to ans
            ans += consonants[j]

            # update temp
            temp += 1

        # Remove the taken
        # elements of consonant
        consonant_till += temp

    # return final answer
    return ans

# Driver code
S = "aaaabbbcc"
print(solution(S))

# This code is contributed by Virusbuddah
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to rearrange the String
// such that the minimum distance
// between any of vowels is maximum.
static String solution(string s)
{

    // Store vowels and consonants
    List<char> vowel = new List<char>();
    List<char> consonant = new List<char>();

    // Iterate over the characters
    // of String
    foreach (char i in s.ToCharArray())
    {

        // If current character is a vowel
        if (i == 'a' || i == 'e'
            || i == 'i' || i == 'o'
            || i == 'u')
        {

            vowel.Add(i);
        }

        // If current character is
        // a consonant
        else
        {

            consonant.Add(i);
        }
    }

    // Stores count of vowels and
    // consonants respectively
    int Nc, Nv;
    Nv = vowel.Count;
    Nc = consonant.Count;
    int M = Nc / (Nv - 1);

    // Stores the resultant String
    string ans = "";

    // Stores count of consonants
    // appended into ans
    int consotnant_till = 0;
    foreach (char i in vowel)
    {

        // Append vowel to ans
        ans += i;
        int temp = 0;

        // Append consonants
        for (int j = consotnant_till;
             j < Math.Min(Nc, consotnant_till + M);
             j++) {

            // Append consonant to ans
            ans += consonant[j];

            // Update temp
            temp++;
        }

        // Remove the taken
        // elements of consonant
        consotnant_till += temp;
    }

    // Return final ans
    return ans;
}

// Driver Code
static public void Main()
{
    String str = "aaaabbbcc";

    // Function Call
    Console.WriteLine(solution(str));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to rearrange the string
// such that the minimum distance
// between any of vowels is maximum.
function solution(s)
{

    // Store vowels and consonants
    var vowel = [], consonant = [];

    // Iterate over the characters
    // of string
    s.split('').forEach(i => {

        // If current character is a vowel
        if (i == 'a' || i == 'e'
            || i == 'i' || i == 'o'
            || i == 'u') {

            vowel.push(i);
        }

        // If current character is
        // a consonant
        else {

            consonant.push(i);
        }
    });

    // Stores count of vowels and
    // consonants respectively
    var Nc, Nv;
    Nv = vowel.length;
    Nc = consonant.length;

    var M = parseInt(Nc / (Nv - 1));

    // Stores the resultant string
    var ans = "";

    // Stores count of consonants
    // appended into ans
    var consotnant_till = 0;

    vowel.forEach(i => {

        // Append vowel to ans
        ans += i;
        var temp = 0;

        // Append consonants
        for (var j = consotnant_till;
             j < Math.min(Nc, consotnant_till + M);
             j++) {

            // Append consonant to ans
            ans += consonant[j];

            // Update temp
            temp++;
        }

        // Remove the taken
        // elements of consonant
        consotnant_till += temp;
    });

    // Return final ans
    return ans;
}

// Driver Code

var str = "aaaabbbcc";

// Function Call
document.write( solution(str));

</script>
```

**Output:** 

```
abababac
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)