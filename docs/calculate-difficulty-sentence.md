# 计算一句话的难度

> 原文:[https://www . geesforgeks . org/calculate-难度-句子/](https://www.geeksforgeeks.org/calculate-difficulty-sentence/)

计算给定句子的难度。在这里，如果一个单词有 4 个连续的辅音或者辅音的数量多于元音的数量，那么这个单词就被认为是硬的。否则的话很容易。句子难度定义为 5*(硬词数)+ 3*(易词数)。
**例:**

```
Input : str = "Difficulty of sentence"
Output : 13
Hard words = 2(Difficulty and sentence)
Easy words = 1(of)
So, answer is 5*2+3*1 = 13
```

问于:[微软](https://www.geeksforgeeks.org/microsoft-interview-experience-set-98-on-campus-for-idc/)T2】

**实现:**
开始遍历字符串并执行以下步骤:-

*   如果当前字符是元音，则增加元音计数，并将连续辅音计数设置为 0。
*   否则增加辅音计数，也增加连续辅音计数。
*   检查连续的辅音是否变成 4，然后-当前单词是硬的，所以增加它的计数并移动到下一个单词。将所有计数重置为 0。
*   否则检查一个单词是否完成，辅音的数量是否大于元音的数量，
    则该单词为硬单词，否则为易单词。将所有计数重置为 0。

## C++

```
// C++ program to find difficulty of a sentence
#include <iostream>
using namespace std;

// Utility function to check character is vowel
// or not
bool isVowel(char ch)
{
    return ( ch == 'a' || ch == 'e' ||
             ch == 'i' || ch == 'o' ||
             ch == 'u');
}

// Function to calculate difficulty
int calcDiff(string str)
{

    int count_vowels = 0, count_conso = 0;
    int hard_words = 0, easy_words = 0;
    int consec_conso = 0;

    // Start traversing the string
    for (int i = 0; i < str.length(); i++)
    {
        // Check if current character is vowel
        // or consonant
        if (str[i] != ' ' && isVowel(tolower(str[i])))
        {
            // Increment if vowel
            count_vowels++;
            consec_conso = 0;
        }

        // Increment counter for consonant
        // also maintain a separate counter for
        // counting consecutive consonants
        else if (str[i]!= ' ')
        {
            count_conso++;
            consec_conso++;
        }

        // If we get 4 consecutive consonants
        // then it is a hard word
        if (consec_conso == 4)
        {
            hard_words++;

            // Move to the next word
            while (i < str.length() && str[i]!= ' ')
                i++;

            // Reset all counts
            count_conso = 0;
            count_vowels = 0;
            consec_conso = 0;
        }

        else if ( i < str.length() &&
                  (str[i] == ' ' || i == str.length()-1))
        {
            // Increment hard_words, if no. of consonants are
            // higher than no. of vowels, otherwise increment
            // count_vowels
            count_conso > count_vowels ? hard_words++
                                       : easy_words++;

            // Reset all counts
            count_conso = 0;
            count_vowels = 0;
            consec_conso = 0;
        }
    }

    // Return difficulty of sentence
    return 5 * hard_words + 3 * easy_words;
}

// Drivers code
int main()
{
    string str = "I am a geek";
    string str2 = "We are geeks";
    cout << calcDiff(str) << endl;
    cout << calcDiff(str2) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find difficulty of a sentence

class GFG
{
    // Utility method to check character is vowel
    // or not
    static boolean isVowel(char ch)
    {
        return ( ch == 'a' || ch == 'e' ||
                 ch == 'i' || ch == 'o' ||
                 ch == 'u');
    }

    // Method to calculate difficulty
    static int calcDiff(String str)
    {

        int count_vowels = 0, count_conso = 0;
        int hard_words = 0, easy_words = 0;
        int consec_conso = 0;

        // Start traversing the string
        for (int i = 0; i < str.length(); i++)
        {
            // Check if current character is vowel
            // or consonant
            if (str.charAt(i) != ' ' && isVowel(Character.toLowerCase(str.charAt(i))))
            {
                // Increment if vowel
                count_vowels++;
                consec_conso = 0;
            }

            // Increment counter for consonant
            // also maintain a separate counter for
            // counting consecutive consonants
            else if (str.charAt(i)!= ' ')
            {
                count_conso++;
                consec_conso++;
            }

            // If we get 4 consecutive consonants
            // then it is a hard word
            if (consec_conso == 4)
            {
                hard_words++;

                // Move to the next word
                while (i < str.length() && str.charAt(i)!= ' ')
                    i++;

                // Reset all counts
                count_conso = 0;
                count_vowels = 0;
                consec_conso = 0;
            }

            else if ( i < str.length() &&
                      (str.charAt(i) == ' ' || i == str.length()-1))
            {
                // Increment hard_words, if no. of consonants are
                // higher than no. of vowels, otherwise increment
                // count_vowels
                if(count_conso > count_vowels)
                    hard_words++;
                else
                    easy_words++;

                // Reset all counts
                count_conso = 0;
                count_vowels = 0;
                consec_conso = 0;
            }
        }

        // Return difficulty of sentence
        return 5 * hard_words + 3 * easy_words;
    }

    // Driver method
    public static void main (String[] args)
    {
        String str = "I am a geek";
        String str2 = "We are geeks";
        System.out.println(calcDiff(str));
        System.out.println(calcDiff(str2));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find difficulty
# of a sentence

# Utility function to check character
# is vowel or not
def isVowel(ch):
    return (ch == 'a' or ch == 'e' or
            ch == 'i' or ch == 'o' or
            ch == 'u')

# Function to calculate difficulty
def calcDiff(str):
    str = str.lower()
    count_vowels = 0
    count_conso = 0
    consec_conso = 0
    hard_words = 0
    easy_words = 0

    # Start traversing the string
    for i in range(0, len(str)):

        # Check if current character is
        # vowel or consonant
        if(str[i]!= " " and isVowel(str[i])):

            # Increment if vowel
            count_vowels += 1
            consec_conso = 0

        # Increment counter for consonant
        # also maintain a separate counter for
        # counting consecutive consonants
        elif(str[i] != " "):
            count_conso += 1
            consec_conso += 1

        # If we get 4 consecutive consonants
        # then it is a hard word
        if(consec_conso == 4):
            hrad_words += 1

            # Move to the next word
            while(i < len(str) and str[i] != " "):
                i += 1

            # Reset all counts
            count_conso = 0
            count_vowels = 0
            consec_conso = 0
        elif(i < len(str) and (str[i] == ' ' or
                          i == len(str) - 1)):

            # Increment hard_words, if no. of
            # consonants are higher than no. of
            # vowels, otherwise increment count_vowels
            if(count_conso > count_vowels):
                hard_words += 1
            else:
                easy_words += 1

            # Reset all counts
            count_conso = 0
            count_vowels = 0
            consec_conso = 0

    # Return difficulty of sentence    
    return (5 * hard_words + 3 * easy_words)

# Driver Code
if __name__=="__main__":
    str = "I am a geek"
    str2 = "We are geeks"
    print(calcDiff(str))
    print(calcDiff(str2))

# This code is contributed
# by Sairahul Jella
```

## C#

```
// C# program to find difficulty
// of a sentence
using System;

public class GFG {

    // Utility method to check character
    // is vowel or not
    static bool isVowel(char ch)
    {
        return (ch == 'a' || ch == 'e' ||
                ch == 'i' || ch == 'o' ||
                ch == 'u');
    }

    // Method to calculate difficulty
    static int calcDiff(string str)
    {
        int count_vowels = 0, count_conso = 0;
        int hard_words = 0, easy_words = 0;
        int consec_conso = 0;

        // Start traversing the string
        for (int i = 0; i < str.Length; i++)
        {

            // Check if current character
            // is vowel or consonant
            if (str[i] != ' ' &&
                isVowel(char.ToLower( str[i])))
            {
                // Increment if vowel
                count_vowels++;
                consec_conso = 0;
            }

            // Increment counter for consonant
            // also maintain a separate counter for
            // counting consecutive consonants
            else if (str[i]!= ' ')
            {
                count_conso++;
                consec_conso++;
            }

            // If we get 4 consecutive consonants
            // then it is a hard word
            if (consec_conso == 4)
            {
                hard_words++;

                // Move to the next word
                while (i < str.Length && str[i]!= ' ')
                    i++;

                // Reset all counts
                count_conso = 0;
                count_vowels = 0;
                consec_conso = 0;
            }

            else if ( i < str.Length &&
                    (str[i] == ' ' || i == str.Length-1))
            {

                // Increment hard_words, if no. of
                // consonants are higher than no.
                // of vowels, otherwise increment
                // count_vowels
                if(count_conso > count_vowels)
                    hard_words++;
                else
                    easy_words++;

                // Reset all counts
                count_conso = 0;
                count_vowels = 0;
                consec_conso = 0;
            }
        }

        // Return difficulty of sentence
        return 5 * hard_words + 3 * easy_words;
    }

    // Driver code
    public static void Main ()
    {
        string str = "I am a geek";
        string str2 = "We are geeks";
        Console.WriteLine(calcDiff(str));
        Console.WriteLine(calcDiff(str2));
    }
}

// This code is contributed by Sam007.
```

## java 描述语言

```
<script>

    // JavaScript program to find
    // difficulty of a sentence

    // Utility method to check character
    // is vowel or not
    function isVowel(ch)
    {
        return (ch == 'a' || ch == 'e' ||
                ch == 'i' || ch == 'o' ||
                ch == 'u');
    }

    // Method to calculate difficulty
    function calcDiff(str)
    {
        let count_vowels = 0, count_conso = 0;
        let hard_words = 0, easy_words = 0;
        let consec_conso = 0;

        // Start traversing the string
        for (let i = 0; i < str.length; i++)
        {

            // Check if current character
            // is vowel or consonant
            if (str[i] != ' ' &&
                isVowel(str[i].toLowerCase()))
            {
                // Increment if vowel
                count_vowels++;
                consec_conso = 0;
            }

            // Increment counter for consonant
            // also maintain a separate counter for
            // counting consecutive consonants
            else if (str[i]!= ' ')
            {
                count_conso++;
                consec_conso++;
            }

            // If we get 4 consecutive consonants
            // then it is a hard word
            if (consec_conso == 4)
            {
                hard_words++;

                // Move to the next word
                while (i < str.length && str[i]!= ' ')
                    i++;

                // Reset all counts
                count_conso = 0;
                count_vowels = 0;
                consec_conso = 0;
            }

            else if ( i < str.length &&
                    (str[i] == ' ' || i == str.length-1))
            {

                // Increment hard_words, if no. of
                // consonants are higher than no.
                // of vowels, otherwise increment
                // count_vowels
                if(count_conso > count_vowels)
                    hard_words++;
                else
                    easy_words++;

                // Reset all counts
                count_conso = 0;
                count_vowels = 0;
                consec_conso = 0;
            }
        }

        // Return difficulty of sentence
        return 5 * hard_words + 3 * easy_words;
    }

    let str = "I am a geek";
    let str2 = "We are geeks";
    document.write(calcDiff(str) + "</br>");
    document.write(calcDiff(str2));

</script>
```

**输出:**

```
12
11
```

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。