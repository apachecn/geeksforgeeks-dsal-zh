# 检查给定句子的一组简单语法规则

> 原文:[https://www . geesforgeks . org/check-given-句子-given-set-simple-grammer-rules/](https://www.geeksforgeeks.org/check-given-sentence-given-set-simple-grammer-rules/)

一个简单的句子，如果语法正确，如果它满足给定的规则。以下是给定的规则。
1。句子必须以大写字符开头(如名词/我/我们/他等)。)
2。然后是小写字符。
3。单词之间必须有空格。
4。那么这个句子必须以句号结尾。)后一句话。
5。不允许有两个连续的空格。
6。不允许两个连续的大写字符。
7。但是，句子可以在大写字符后结束。
**示例:**

```
Correct sentences -
   "My name is Ram."
   "The vertex is S."
   "I am single."
   "I love Geeksquiz and Geeksforgeeks."

Incorrect sentence - 
   "My name is KG."
   "I lovE cinema."
   "GeeksQuiz. is a quiz site."
   "  You are my friend."
   "I love cinema" 
```

**问题:**给定一个句子，根据上述给定规则验证给定句子。
**强烈建议尽量减少浏览器，先自己试试这个。**
想法是对给定的规则集使用自动机。
算法:
1。检查角箱
…..1.a)检查句子中的第一个字符是否大写。
…..1.b)检查最后一个字符是否是句号。
2。对于字符串的其余部分，这个问题可以通过遵循状态图来解决。请参考下面的状态图。

![](img/ff50dead3ef3a96e38fd0d4d11cb9894.png)

3.我们需要保持字符串中不同字符的先前和当前状态。基于此，我们总是可以验证每个被遍历字符的句子。
下面是一个基于 C 的实现。(顺便说一下，根据规则和代码，这句话也是正确的)

## C++

```
// C program to validate a given sentence for a set of rules
#include<stdio.h>
#include<string.h>
#include<stdbool.h>

// Method to check a given sentence for given rules
bool checkSentence(char str[])
{
    // Calculate the length of the string.
    int len = strlen(str);

    // Check that the first character lies in [A-Z].
    // Otherwise return false.
    if (str[0] < 'A' || str[0] > 'Z')
        return false;

    //If the last character is not a full stop(.) no
    //need to check further.
    if (str[len - 1] != '.')
        return false;

    // Maintain 2 states. Previous and current state based
    // on which vertex state you are. Initialise both with
    // 0 = start state.
    int prev_state = 0, curr_state = 0;

    //Keep the index to the next character in the string.
    int index = 1;

    //Loop to go over the string.
    while (str[index])
    {
        // Set states according to the input characters in the
        // string and the rule defined in the description.
        // If current character is [A-Z]. Set current state as 0.
        if (str[index] >= 'A' && str[index] <= 'Z')
            curr_state = 0;

        // If current character is a space. Set current state as 1.
        else if (str[index] == ' ')
            curr_state = 1;

        // If current character is [a-z]. Set current state as 2.
        else if (str[index] >= 'a' && str[index] <= 'z')
            curr_state = 2;

        // If current state is a dot(.). Set current state as 3.
        else if (str[index] == '.')
            curr_state = 3;

        // Validates all current state with previous state for the
        // rules in the description of the problem.
        if (prev_state == curr_state && curr_state != 2)
            return false;

        if (prev_state == 2 && curr_state == 0)
            return false;

        // If we have reached last state and previous state is not 1,
        // then check next character. If next character is '\0', then
        // return true, else false
        if (curr_state == 3 && prev_state != 1)
            return (str[index + 1] == '\0');

        index++;

        // Set previous state as current state before going over
        // to the next character.
        prev_state = curr_state;
    }
    return false;
}

// Driver program
int main()
{
    char *str[] = { "I love cinema.", "The vertex is S.",
                    "I am single.", "My name is KG.",
                    "I lovE cinema.", "GeeksQuiz. is a quiz site.",
                    "I love Geeksquiz and Geeksforgeeks.",
                    "  You are my friend.", "I love cinema" };
    int str_size = sizeof(str) / sizeof(str[0]);
    int i = 0;
    for (i = 0; i < str_size; i++)
     checkSentence(str[i])? printf("\"%s\" is correct \n", str[i]):
                            printf("\"%s\" is incorrect \n", str[i]);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to validate a given sentence
// for a set of rules
class GFG
{

    // Method to check a given sentence for given rules
    static boolean checkSentence(char[] str)
    {

        // Calculate the length of the string.
        int len = str.length;

        // Check that the first character lies in [A-Z].
        // Otherwise return false.
        if (str[0] < 'A' || str[0] > 'Z')
            return false;

        // If the last character is not a full stop(.)
        // no need to check further.
        if (str[len - 1] != '.')
            return false;

        // Maintain 2 states. Previous and current state
        // based on which vertex state you are.
        // Initialise both with 0 = start state.
        int prev_state = 0, curr_state = 0;

        // Keep the index to the next character in the string.
        int index = 1;

        // Loop to go over the string.
        while (index <= str.length)
        {

            // Set states according to the input characters
            // in the string and the rule defined in the description.
            // If current character is [A-Z]. Set current state as 0.
            if (str[index] >= 'A' && str[index] <= 'Z')
                curr_state = 0;

            // If current character is a space.
            // Set current state as 1.
            else if (str[index] == ' ')
                curr_state = 1;

            // If current character is [a-z].
            // Set current state as 2.
            else if (str[index] >= 'a' && str[index] <= 'z')
                curr_state = 2;

            // If current state is a dot(.).
            // Set current state as 3.
            else if (str[index] == '.')
                curr_state = 3;

            // Validates all current state with previous state
            // for the rules in the description of the problem.
            if (prev_state == curr_state && curr_state != 2)
                return false;

            if (prev_state == 2 && curr_state == 0)
                return false;

            // If we have reached last state and previous state
            // is not 1, then check next character. If next character
            // is '\0', then return true, else false
            if (curr_state == 3 && prev_state != 1)
                return (index + 1 == str.length);

            index++;

            // Set previous state as current state
            // before going over to the next character.
            prev_state = curr_state;
        }
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String[] str = { "I love cinema.", "The vertex is S.",
                         "I am single.", "My name is KG.",
                         "I lovE cinema.", "GeeksQuiz. is a quiz site.",
                         "I love Geeksquiz and Geeksforgeeks.",
                         " You are my friend.", "I love cinema" };
        int str_size = str.length;

        int i = 0;
        for (i = 0; i < str_size; i++)
        {
            if (checkSentence(str[i].toCharArray()))
                System.out.println("\"" + str[i] +
                                   "\"" + " is correct");
            else
                System.out.println("\"" + str[i] +
                                   "\"" + " is incorrect");
        }
    }
}

// This code is contributed by
// sanjeev2552
```

## 计算机编程语言

```
# Python program to validate a given sentence for a set of rules

# Method to check a given sentence for given rules
def checkSentence(string):

    # Calculate the length of the string.
    length = len(string)

    # Check that the first character lies in [A-Z].
    # Otherwise return false.
    if string[0] < 'A' or string[0] > 'Z':
        return False

    # If the last character is not a full stop(.) no
    # need to check further.
    if string[length-1] != '.':
        return False

    # Maintain 2 states. Previous and current state based
    # on which vertex state you are. Initialise both with
    # 0 = start state.
    prev_state = 0
    curr_state = 0

    # Keep the index to the next character in the string.
    index = 1

    # Loop to go over the string.
    while (string[index]):
        # Set states according to the input characters in the
        # string and the rule defined in the description.
        # If current character is [A-Z]. Set current state as 0.
        if string[index] >= 'A' and string[index] <= 'Z':
            curr_state = 0

        # If current character is a space. Set current state as 1.
        elif string[index] == ' ':
            curr_state = 1

        # If current character is a space. Set current state as 2.
        elif string[index] >= 'a' and string[index] <= 'z':
            curr_state = 2

        # If current character is a space. Set current state as 3.
        elif string[index] == '.':
            curr_state = 3

        # Validates all current state with previous state for the
        # rules in the description of the problem.
        if prev_state == curr_state and curr_state != 2:
            return False

        # If we have reached last state and previous state is not 1,
        # then check next character. If next character is '\0', then
        # return true, else false
        if prev_state == 2 and curr_state == 0:
            return False

        # Set previous state as current state before going over
        # to the next character.
        if curr_state == 3 and prev_state != 1:
            return True

        index += 1

        prev_state = curr_state

    return False

# Driver program
string = ["I love cinema.", "The vertex is S.",
            "I am single.", "My name is KG.",
            "I lovE cinema.", "GeeksQuiz. is a quiz site.",
            "I love Geeksquiz and Geeksforgeeks.",
            "  You are my friend.", "I love cinema"]
string_size = len(string)
for i in xrange(string_size):
    if checkSentence(string[i]):
        print "\"" +  string[i] + "\" is correct"
    else:
        print "\"" + string[i] + "\" is incorrect"

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to validate a given sentence
// for a set of rules
using System;

class GFG
{

    // Method to check a given sentence for given rules
    static bool checkSentence(char[] str)
    {

        // Calculate the length of the string.
        int len = str.Length;

        // Check that the first character lies in [A-Z].
        // Otherwise return false.
        if (str[0] < 'A' || str[0] > 'Z')
            return false;

        // If the last character is not a full stop(.)
        // no need to check further.
        if (str[len - 1] != '.')
            return false;

        // Maintain 2 states. Previous and current state
        // based on which vertex state you are.
        // Initialise both with 0 = start state.
        int prev_state = 0, curr_state = 0;

        // Keep the index to the next character in the string.
        int index = 1;

        // Loop to go over the string.
        while (index <= str.Length)
        {

            // Set states according to the input characters
            // in the string and the rule defined in the description.
            // If current character is [A-Z]. Set current state as 0.
            if (str[index] >= 'A' && str[index] <= 'Z')
                curr_state = 0;

            // If current character is a space.
            // Set current state as 1.
            else if (str[index] == ' ')
                curr_state = 1;

            // If current character is [a-z].
            // Set current state as 2.
            else if (str[index] >= 'a' && str[index] <= 'z')
                curr_state = 2;

            // If current state is a dot(.).
            // Set current state as 3.
            else if (str[index] == '.')
                curr_state = 3;

            // Validates all current state with previous state
            // for the rules in the description of the problem.
            if (prev_state == curr_state && curr_state != 2)
                return false;

            if (prev_state == 2 && curr_state == 0)
                return false;

            // If we have reached last state and previous state
            // is not 1, then check next character. If next character
            // is '\0', then return true, else false
            if (curr_state == 3 && prev_state != 1)
                return (index + 1 == str.Length);

            index++;

            // Set previous state as current state
            // before going over to the next character.
            prev_state = curr_state;
        }
        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String[] str = { "I love cinema.", "The vertex is S.",
                        "I am single.", "My name is KG.",
                        "I lovE cinema.", "GeeksQuiz. is a quiz site.",
                        "I love Geeksquiz and Geeksforgeeks.",
                        " You are my friend.", "I love cinema" };
        int str_size = str.Length;

        int i = 0;
        for (i = 0; i < str_size; i++)
        {
            if (checkSentence(str[i].ToCharArray()))
                Console.WriteLine("\"" + str[i] +
                                "\"" + " is correct");
            else
                Console.WriteLine("\"" + str[i] +
                                "\"" + " is incorrect");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript program to validate a given sentence
      // for a set of rules
      // Method to check a given sentence for given rules
      function checkSentence(str) {
        // Calculate the length of the string.
        var len = str.length;

        // Check that the first character lies in [A-Z].
        // Otherwise return false.
        if (
          str[0].charCodeAt(0) < "A".charCodeAt(0) ||
          str[0].charCodeAt(0) > "Z".charCodeAt(0)
        )
          return false;

        // If the last character is not a full stop(.)
        // no need to check further.
        if (str[len - 1] !== ".") return false;

        // Maintain 2 states. Previous and current state
        // based on which vertex state you are.
        // Initialise both with 0 = start state.
        var prev_state = 0,
          curr_state = 0;

        // Keep the index to the next character in the string.
        var index = 1;

        // Loop to go over the string.
        while (index <= str.length) {
          // Set states according to the input characters
          // in the string and the rule defined in the description.
          // If current character is [A-Z]. Set current state as 0.
          if (
            str[index].charCodeAt(0) >= "A".charCodeAt(0) &&
            str[index].charCodeAt(0) <= "Z".charCodeAt(0)
          )
            curr_state = 0;
          // If current character is a space.
          // Set current state as 1.
          else if (str[index] === " ") curr_state = 1;
          // If current character is [a-z].
          // Set current state as 2.
          else if (
            str[index].charCodeAt(0) >= "a".charCodeAt(0) &&
            str[index].charCodeAt(0) <= "z".charCodeAt(0)
          )
            curr_state = 2;
          // If current state is a dot(.).
          // Set current state as 3.
          else if (str[index] === ".") curr_state = 3;

          // Validates all current state with previous state
          // for the rules in the description of the problem.
          if (prev_state === curr_state && curr_state !== 2) return false;

          if (prev_state === 2 && curr_state === 0) return false;

          // If we have reached last state and previous state
          // is not 1, then check next character. If next character
          // is '\0', then return true, else false
          if (curr_state === 3 && prev_state !== 1)
            return index + 1 == str.length;

          index++;

          // Set previous state as current state
          // before going over to the next character.
          prev_state = curr_state;
        }
        return false;
      }

      // Driver Code
      var str = [
        "I love cinema.",
        "The vertex is S.",
        "I am single.",
        "My name is KG.",
        "I lovE cinema.",
        "GeeksQuiz. is a quiz site.",
        "I love Geeksquiz and Geeksforgeeks.",
        " You are my friend.",
        "I love cinema",
      ];
      var str_size = str.length;

      var i = 0;
      for (i = 0; i < str_size; i++) {
        var temp = str[i].split("");
        if (checkSentence(temp))
          document.write('"' + str[i] + '"' + " is correct" + "<br>");
        else document.write('"' + str[i] + '"' + " is incorrect" + "<br>");
      }
    </script>
```

**输出:**

```
"I love cinema." is correct
"The vertex is S." is correct
"I am single." is correct
"My name is KG." is incorrect
"I lovE cinema." is incorrect
"GeeksQuiz. is a quiz site." is incorrect
"I love Geeksquiz and Geeksforgeeks." is correct
"  You are my friend." is incorrect
"I love cinema" is incorrect
```

**时间复杂度**–O(n)，最坏的情况，因为我们必须遍历整个句子，其中 n 是句子的长度。
**辅助空间**–O(1)
本文由**库马尔·高塔姆**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。