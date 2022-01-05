# 通过颠倒所有回文单词的出现顺序来修改句子

> 原文:[https://www . geesforgeks . org/通过反转所有回文单词的出现顺序来修改句子/](https://www.geeksforgeeks.org/modify-a-sentence-by-reversing-order-of-occurrences-of-all-palindrome-words/)

给定一个代表一个句子的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是颠倒句子中所有[回文单词](https://www.geeksforgeeks.org/remove-palindromic-words-given-sentence/)的顺序。

**示例:**

> **输入:** S =“爸爸妈妈去眼科医院”
> **输出:**爸爸妈妈去眼科医院
> **解释:**字符串中出现的所有回文单词都是“妈妈”、“爸爸”和“眼科**”**，按照出现的顺序排列。颠倒它们出现的顺序会生成序列{“眼睛”、“爸爸”、“妈妈”}。因此，修改后的字符串是“眼睛和爸爸去了妈妈医院”。
> 
> **输入:** S =“哇它是下一级”
> T3】输出:级它是下一级哇。

**方法:**按照以下步骤解决问题:

*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并使用 split()从句子中拆分[空格分隔的单词，并将它们存储在列表](https://www.geeksforgeeks.org/python-string-split-including-spaces/)中，例如 **lis** 。
*   使用[追加()](https://www.geeksforgeeks.org/append-extend-python/)功能，将所有[回文单词](https://www.geeksforgeeks.org/remove-palindromic-words-given-sentence/)追加到新列表中，比如说**新列表、**。
*   使用[反向()](https://www.geeksforgeeks.org/python-reversing-list/)功能反向此新列表。
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-words-of-a-string-in-python/) **lis** ，继续用**新列表【I】**(*初始， **i=0*** )替换[回文词](https://www.geeksforgeeks.org/java-program-count-number-palindrome-words-sentence/)，并将 **i** 增加 **1** 。
*   [打印修改后的句子](https://www.geeksforgeeks.org/recursively-print-all-sentences-that-can-be-formed-from-list-of-word-lists/)

下面是上述方法的实现:

## C++

```
<script>
// Javascript implementation of
// the above approach

// Function to check if a
// string S is a palindrome
function palindrome(str)
{
    var st = 0;
    var ed = str.length - 1;

    while (st < ed)
    {
        if (str[st] == str[ed])
        {
            st++;
            ed--;
        }
        else
          return false;
    }
    return true;
}

// Function to print the modified string
// after reversing the order of occurrences
// of all palindromic words in the sentence
function printReverse(sentence)
{

    // Stores the palindromic words
    var newlist = [];
    var lis = [];

    // Stores the words in the list
    var temp = "";

    for(var i =0; i<sentence.length;i++)
    {
        if (sentence[i] == ' ')
        {
            lis.push(temp);
            temp = "";
        }
        else
            temp += sentence[i];
    }
    lis.push(temp);

    // Traversing the list
    for(var i =0; i<lis.length;i++)
    {

        // If current word is a palindrome
        if (palindrome(lis[i]))

            // Update newlist
            newlist.push(lis[i]);
    }

    // Reverse the newlist
    newlist.reverse();

    var j = 0;

    // Traverse the list
    for(var i = 0; i < lis.length; i++)
    {

        // If current word is a palindrome
        if (palindrome(lis[i]))
        {

            // Update lis[i]
            lis[i] = newlist[j];

            // Increment j
            j = j + 1;
        }
    }

    // Print the updated sentence
    for(var i = 0; i < lis.length; i++)
    {
       document.write( lis[i] + " ");
    }
}

// Driver Code
var sentence = "mom and dad went to eye hospital";
printReverse(sentence);

</script>
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function to check if a
// string S is a palindrome
static boolean palindrome(String str)
{
    int st = 0;
    int ed = str.length() - 1;

    while (st < ed)
    {
        if (str.charAt(st) == str.charAt(ed))
        {
            st++;
            ed--;
        }
        else
            return false;
    }
    return true;
}

// Function to print the modified string
// after reversing the order of occurrences
// of all palindromic words in the sentence
static void printReverse(String sentence)
{

    // Stores the palindromic words
    ArrayList<String> newlist = new ArrayList<String>();
    ArrayList<String> lis = new ArrayList<String>();

    // Stores the words in the list
    String temp = "";

    for(char x: sentence.toCharArray())
    {
        if (x == ' ')
        {
            lis.add(temp);
            temp = "";
        }
        else
            temp += x;
    }
    lis.add(temp);

    // Traversing the list
    for(String x:  lis)
    {

        // If current word is a palindrome
        if (palindrome(x))

            // Update newlist
            newlist.add(x);
    }

    // Reverse the newlist
    Collections.reverse(newlist);

    int j = 0;

    // Traverse the list
    for(int i = 0; i < lis.size(); i++)
    {

        // If current word is a palindrome
        if (palindrome(lis.get(i)))
        {

            // Update lis[i]
            lis.set(i,newlist.get(j));

            // Increment j
            j = j + 1;
        }
    }

    // Print the updated sentence
    for(String x : lis)
        System.out.print(x + " ");
}

// Driver code
public static void main(String[] args)
{
    String sentence = "mom and dad went to eye hospital";
    printReverse(sentence);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python implementation of
# the above approach

# Function to check if a
# string S is a palindrome
def palindrome(string):

    if(string == string[::-1]):
        return True
    else:
        return False

# Function to print the modified string
# after reversing the order of occurrences
# of all palindromic words in the sentence
def printReverse(sentence):

    # Stores the palindromic words
    newlist = []

    # Stores the words in the list
    lis = list(sentence.split())

    # Traversing the list
    for i in lis:

        # If current word is a palindrome
        if(palindrome(i)):

              # Update newlist
            newlist.append(i)

    # Reverse the newlist
    newlist.reverse()

    j = 0

    # Traverse the list
    for i in range(len(lis)):

        # If current word is a palindrome
        if(palindrome(lis[i])):

            # Update lis[i]
            lis[i] = newlist[j]

            # Increment j
            j = j + 1

    # Print the updated sentence
    for i in lis:
        print(i, end =" ")

# Driver Code

sentence = "mom and dad went to eye hospital"
printReverse(sentence)
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if a
// string S is a palindrome
static bool palindrome(string str)
{
    int st = 0;
    int ed = str.Length - 1;

    while (st < ed)
    {
        if (str[st] == str[ed])
        {
            st++;
            ed--;
        }
        else
            return false;
    }
    return true;
}

// Function to print the modified string
// after reversing the order of occurrences
// of all palindromic words in the sentence
static void printReverse(string sentence)
{

    // Stores the palindromic words
    List<string> newlist = new List<string>();
    List<string> lis = new List<string>();

    // Stores the words in the list
    string temp = "";

    foreach(char x in sentence)
    {
        if (x == ' ')
        {
            lis.Add(temp);
            temp = "";
        }
        else
            temp += x;
    }
    lis.Add(temp);

    // Traversing the list
    foreach(string x in lis)
    {

        // If current word is a palindrome
        if (palindrome(x))

            // Update newlist
            newlist.Add(x);
    }

    // Reverse the newlist
    newlist.Reverse();

    int j = 0;

    // Traverse the list
    for(int i = 0; i < lis.Count; i++)
    {

        // If current word is a palindrome
        if (palindrome(lis[i]))
        {

            // Update lis[i]
            lis[i] = newlist[j];

            // Increment j
            j = j + 1;
        }
    }

    // Print the updated sentence
    foreach(string x in lis)
        Console.Write(x + " ");
}

// Driver Code
public static void Main()
{
    string sentence = "mom and dad went to eye hospital";
    printReverse(sentence);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Function to check if a
// string S is a palindrome
function palindrome(str)
{
    var st = 0;
    var ed = str.length - 1;

    while (st < ed)
    {
        if (str[st] == str[ed])
        {
            st++;
            ed--;
        }
        else
          return false;
    }
    return true;
}

// Function to print the modified string
// after reversing the order of occurrences
// of all palindromic words in the sentence
function printReverse(sentence)
{

    // Stores the palindromic words
    var newlist = [];
    var lis = [];

    // Stores the words in the list
    var temp = "";

    for(var i =0; i<sentence.length;i++)
    {
        if (sentence[i] == ' ')
        {
            lis.push(temp);
            temp = "";
        }
        else
            temp += sentence[i];
    }
    lis.push(temp);

    // Traversing the list
    for(var i =0; i<lis.length;i++)
    {

        // If current word is a palindrome
        if (palindrome(lis[i]))

            // Update newlist
            newlist.push(lis[i]);
    }

    // Reverse the newlist
    newlist.reverse();

    var j = 0;

    // Traverse the list
    for(var i = 0; i < lis.length; i++)
    {

        // If current word is a palindrome
        if (palindrome(lis[i]))
        {

            // Update lis[i]
            lis[i] = newlist[j];

            // Increment j
            j = j + 1;
        }
    }

    // Print the updated sentence
    for(var i = 0; i < lis.length; i++)
    {
       document.write( lis[i] + " ");
    }
}

// Driver Code
var sentence = "mom and dad went to eye hospital";
printReverse(sentence);

</script>
```

**Output:** 

```
eye and dad went to mom hospital
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)