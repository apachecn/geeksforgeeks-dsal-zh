# 打印句子中的每个单词及其相应的 ASCII 值平均值

> 原文:[https://www . geesforgeks . org/print-每个句子中的单词及其对应的 ascii 平均值/](https://www.geeksforgeeks.org/print-each-word-in-a-sentence-with-their-corresponding-average-of-ascii-values/)

给定一个句子，任务是找出句子中每个单词的 ASCII 值的平均值，并与单词一起打印出来。
**例:**

```
Input: sentence = "Learning a string algorithm"
Output: 
Learning - 102
a - 97
string - 110
algorithm - 107
```

**进场:**

1.  取一个空字符串，开始一个字母一个字母地遍历句子。
2.  将字母添加到字符串中，并将其 ASCII 值添加到总和中。
3.  如果有空格，用总和除以字符串(单词)的长度来计算平均值
4.  清除字符串，以便它可以用于下一个单词
5.  也将总和设置为零。

以下是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// average of each word in a sentence
void calculateAverage(string sentence)
{
    // Word initialised to an empty string
    string word = "";

    // Sum of ascii values
    int sum = 0;

    int len = sentence.length();

    for (int i = 0; i < len; ++i) {

        // If character is a space
        if (sentence[i] == ' ') {

            // Calculate the average
            int average = sum / word.length();

            cout << word << " - "
                 << average << endl;

            // Clear the word and
            // set the sum to 0
            word.clear();
            sum = 0;
        }

        else {

            // Add the ascii value to sum and
            // also add the letter to the word
            sum += sentence[i];
            word += sentence[i];
        }
    }

    // Calculate the average of last word
    int average = sum / word.length();

    cout << word << " - " << average;
}

// Driver code
int main()
{

    // Get the sentence
    string sentence
            = "Learning a string algorithm";

    // Calculate the average
    calculateAverage(sentence);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
public class Solution
{
// Function to calculate the
// average of each word in a sentence
static void calculateAverage(String sentence)
{
    // Word initialised to an empty string
    String word = "";

    // Sum of ascii values
    int sum = 0;

    int len = sentence.length();

    for (int i = 0; i < len; ++i) {

        // If character is a space
        if (sentence.charAt(i) == ' ') {

            // Calculate the average
            int average = sum / word.length();

            System.out.println( word + " - "+ average );

            // Clear the word and
            // set the sum to 0
            word="";
            sum = 0;
        }

        else {

            // Add the ascii value to sum and
            // also add the letter to the word
            sum += sentence.charAt(i);
            word += sentence.charAt(i);
        }
    }

    // Calculate the average of last word
    int average = sum / word.length();

System.out.print( word + " - " + average);
}

// Driver code
public static void main(String[] args)
{

    // Get the sentence
    String sentence
            = "Learning a string algorithm";

    // Calculate the average
    calculateAverage(sentence);

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to calculate the
# average of each word in a sentence
def calculateAverage(sentence):

    # Word initialised to
    # an empty string
    word = ""

    # Sum of ascii values
    sum = 0

    l = len(sentence)

    for i in range(l):

        # If character is a space
        if (sentence[i] == ' ') :

            # Calculate the average
            average = sum // len(word)

            print(word , " - ", average)

            # Clear the word and
            # set the sum to 0
            word = ""
            sum = 0

        else :

            # Add the ascii value to sum and
            # also add the letter to the word
            sum += ord(sentence[i])
            word += sentence[i]

    # Calculate the average of last word
    average = sum // len(word)

    print(word , " - " , average)

# Driver code
if __name__ == "__main__":

    # Get the sentence
    sentence = "Learning a string algorithm"

    # Calculate the average
    calculateAverage(sentence)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// Function to calculate the
// average of each word in a sentence
static void calculateAverage(String sentence)
{
    // Word initialised to an empty string
    String word = "";

    // Sum of ascii values
    int sum = 0;

    int len = sentence.Length;
    int average = 0;
    for (int i = 0; i < len; ++i)
    {

        // If character is a space
        if (sentence[i] == ' ')
        {

            // Calculate the average
            average = sum / word.Length;

            Console.WriteLine(word + " - " + average);

            // Clear the word and
            // set the sum to 0
            word="";
            sum = 0;
        }

        else
        {

            // Add the ascii value to sum and
            // also add the letter to the word
            sum += sentence[i];
            word += sentence[i];
        }
    }

    // Calculate the average of last word
    average = sum / word.Length;

    Console.Write(word + " - " + average);
}

// Driver code
public static void Main()
{
    // Get the sentence
    String sentence = "Learning a string algorithm";

    // Calculate the average
    calculateAverage(sentence);
}
}

// This code is contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>
      // JavaScript implementation of above approach
      // Function to calculate the
      // average of each word in a sentence
      function calculateAverage(sentence) {
        // Word initialised to an empty string
        var word = "";

        // Sum of ascii values
        var sum = 0;

        var len = sentence.length;
        var average = 0;
        for (var i = 0; i < len; ++i) {
          // If character is a space
          if (sentence[i] === " ") {
            // Calculate the average
            average = parseInt(sum / word.length);

            document.write(word + " - " + average + "<br>");

            // Clear the word and
            // set the sum to 0
            word = "";
            sum = 0;
          } else {
            // Add the ascii value to sum and
            // also add the letter to the word

            sum += sentence[i].charCodeAt(0);
            word += sentence[i];
          }
        }

        // Calculate the average of last word
        average = parseInt(sum / word.length);
        document.write(word + " - " + average + "<br>");
      }

      // Driver code
      // Get the sentence
      var sentence = "Learning a string algorithm";

      // Calculate the average
      calculateAverage(sentence);
    </script>
```

**Output:** 

```
Learning - 102
a - 97
string - 110
algorithm - 107
```

**时间复杂度** : O(N)