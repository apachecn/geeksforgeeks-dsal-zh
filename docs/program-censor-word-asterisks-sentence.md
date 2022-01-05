# 用星号替换句子中单词的程序

> 原文:[https://www . geesforgeks . org/program-御史-word-星号-句子/](https://www.geeksforgeeks.org/program-censor-word-asterisks-sentence/)

对于输入的给定句子，用星号“ ***** ”检查特定单词。
**例:**

> **输入:**word = " computer "
> text = " geeks forgeeks 是一个面向极客的计算机科学门户。热爱计算机和计算机代码的人可以在这里的计算机代码/结构上贡献他们的宝贵财富/想法。”
> **输出:**极客 forGeeks 是一个面向极客的*******科学门户。喜欢********和*******代码的人可以在这里贡献他们在*******代码/结构上的宝贵/想法。

这个想法是首先把给定的句子分成不同的单词。然后遍历单词列表。对于单词列表中的每个单词，检查它是否与给定的单词匹配。如果是，则在列表中用星号替换该单词。最后合并列表和打印的单词。

## C++

```
// C++ program to censor a word
// with asterisks in a sentence
#include<bits/stdc++.h>
#include <boost/algorithm/string.hpp>
using namespace std;

// Function takes two parameter
string censor(string text,
                    string word)
{

    // Break down sentence by ' ' spaces
    // and store each individual word in
    // a different list
    vector<string> word_list;
    boost::split(word_list, text, boost::is_any_of("\\ +"));

    // A new string to store the result
    string result = "";

    // Creating the censor which is an asterisks
    // "*" text of the length of censor word
    string stars = "";
    for (int i = 0; i < word.size(); i++)
        stars += '*';

    // Iterating through our list
    // of extracted words
    int index = 0;
    for (string i : word_list)
    {

        if (i.compare(word) == 0)
        {

            // changing the censored word to
            // created asterisks censor
            word_list[index] = stars;
        }
        index++;
    }

    // join the words
    for (string i : word_list)
    {
        result += i + ' ';
    }
    return result;
}

// Driver code
int main()
{
    string extract = "GeeksforGeeks is a computer science "
                    "portal for geeks. I am pursuing my "
                    "major in computer science. ";
    string cen = "computer";
    cout << (censor(extract, cen));
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to censor a word
// with asterisks in a sentence
class GFG
{

// Function takes two parameter
static String censor(String text,
                     String word)
{

    // Break down sentence by ' ' spaces
    // and store each individual word in
    // a different list
    String[] word_list = text.split("\\s+");

    // A new string to store the result
    String result = "";

    // Creating the censor which is an asterisks
    // "*" text of the length of censor word
    String stars = "";
    for (int i = 0; i < word.length(); i++)
        stars += '*';

    // Iterating through our list
    // of extracted words
    int index = 0;
    for (String i : word_list)
    {
        if (i.compareTo(word) == 0)

            // changing the censored word to
            // created asterisks censor
            word_list[index] = stars;
        index++;
    }

    // join the words
    for (String i : word_list)
        result += i + ' ';

    return result;
}

// Driver code
public static void main(String[] args)
{
    String extract = "GeeksforGeeks is a computer science "+
                     "portal for geeks. I am pursuing my " +
                     "major in computer science. ";
    String cen = "computer";
    System.out.println(censor(extract, cen));
}
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python Program to censor a word
# with asterisks in a sentence

# Function takes two parameter
def censor(text, word):

    # Break down sentence by ' ' spaces
    # and store each individual word in
    # a different list
    word_list = text.split()

    # A new string to store the result
    result = ''

    # Creating the censor which is an asterisks
    # "*" text of the length of censor word
    stars = '*' * len(word)

    # count variable to
    # access our word_list
    count = 0

    # Iterating through our list
    # of extracted words
    index = 0;
    for i in word_list:

        if i == word:

            # changing the censored word to
            # created asterisks censor
            word_list[index] = stars
        index += 1

    # join the words
    result =' '.join(word_list)

    return result

# Driver code
if __name__== '__main__':

    extract = "GeeksforGeeks is a computer science portal for geeks.\
               I am pursuing my major in computer science. "              
    cen = "computer"   
    print(censor(extract, cen))
```

## C#

```
// C# program to censor a word
// with asterisks in a sentence
using System;
using System.Collections.Generic;

class GFG
{

// Function takes two parameter
static String censor(String text,
                     String word)
{

    // Break down sentence by ' ' spaces
    // and store each individual word in
    // a different list
    String[] word_list = text.Split(' ');

    // A new string to store the result
    String result = "";

    // Creating the censor which is an asterisks
    // "*" text of the length of censor word
    String stars = "";
    for (int i = 0; i < word.Length; i++)
        stars += '*';

    // Iterating through our list
    // of extracted words
    int index = 0;
    foreach (String i in word_list)
    {
        if (i.CompareTo(word) == 0)

            // changing the censored word to
            // created asterisks censor
            word_list[index] = stars;
        index++;
    }

    // join the words
    foreach (String i in word_list)
        result += i + " ";

    return result;
}

// Driver code
public static void Main(String[] args)
{
    String extract = "GeeksforGeeks is a computer science "+
                     "portal for geeks. I am pursuing my " +
                     "major in computer science. ";
    String cen = "computer";
    Console.WriteLine(censor(extract, cen));
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to censor a word
// with asterisks in a sentence

// Function takes two parameter
function censor($text, $word)
{

    // Break down sentence by ' ' spaces
    // and store each individual word in
    // a different list
    $word_list = explode(" ", $text);

    // A new string to store the result
    $result = '';

    // Creating the censor which is an
    // asterisks "*" text of the length
    // of censor word
    $stars = "";
    for($i = 0; $i < strlen($word); $i++)
    $stars .= "*";

    // count variable to access
    // our word_list
    $count = 0;

    // Iterating through our list of
    // extracted words
    $index = 0;
    for($i = 0; $i < sizeof($word_list); $i++)
    {
        if($word_list[$i] == $word)

            // changing the censored word to
            // created asterisks censor
            $word_list[$index] = $stars;
        $index += 1;
    }

    // join the words
    return implode(' ', $word_list);
}

// Driver code
$extract = "GeeksforGeeks is a computer science ".
           "portal for geeks.\nI am pursuing my ".
                    "major in computer science. ";        
$cen = "computer";
echo censor($extract, $cen);

// This code is contributed
// by Aman ojha
?>
```

## java 描述语言

```
<script>

      // JavaScript program to censor a word
      // with asterisks in a sentence

      // Function takes two parameter
      function censor(text, word) {
        // Break down sentence by ' ' spaces
        // and store each individual word in
        // a different list
        var word_list = text.split(" ");

        // A new string to store the result
        var result = "";

        // Creating the censor which is an asterisks
        // "*" text of the length of censor word
        var stars = "";
        for (var i = 0; i < word.length; i++) stars += "*";

        // Iterating through our list
        // of extracted words
        var index = 0;
        for (const i of word_list) {
          if (i === word)
            // changing the censored word to
            // created asterisks censor
            word_list[index] = stars;
          index++;
        }

        // join the words
        for (const i of word_list) {
          result += i + " ";
        }

        return result;
      }

      // Driver code
      var extract =
        "GeeksforGeeks is a computer science " +
        "portal for geeks. I am pursuing my " +
        "major in computer science. ";

      var cen = "computer";
      document.write(censor(extract, cen) + "<br>");

</script>
```

**输出:**

```
GeeksforGeeks is a ******** science portal for geeks.
I am pursuing my major in ******** science.
```