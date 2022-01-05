# 检查句子中是否有单词

> 原文:[https://www . geeksforgeeks . org/check-if-a-word-in-in-a-in-a-in-a-in-a-in-a-in-a-in-a-in-a-in-a-in-a-a-a-a-a-a-a-a-a-a-](https://www.geeksforgeeks.org/check-if-a-word-is-present-in-a-sentence/)

给定一个句子作为字符串 **str** 和一个单词**单词**，任务是检查该单词是否存在于 **str** 中。一个句子是由多个单词组成的字符串，每个单词用空格隔开。
**示例:**

> **输入:** str = "极客为极客"，word = "极客"
> T3】输出:单词出现在句子中
> 
> **输入:** str = "Geeks for Geeks "，Word = " eeks "
> T3】输出:句子中没有单词

**方法:**在该算法中， [stringstream](https://www.geeksforgeeks.org/stringstream-c-applications/) 用于将句子分解成单词，然后将句子中的每个单词与给定的单词进行比较。如果找到了这个词，那么函数返回真。
**注意**这个实现不搜索子序列或子串，它只搜索一个句子中完整的单个单词。
以下是区分大小写的搜索方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the word is found
bool isWordPresent(string sentence, string word)
{
    // To break the sentence in words
    stringstream s(sentence);

    // To temporarily store each individual word
    string temp;

    while (s >> temp) {

        // Comparing the current word
        // with the word to be searched
        if (temp.compare(word) == 0) {
            return true;
        }
    }
    return false;
}

// Driver code
int main()
{
    string s = "Geeks for Geeks";
    string word = "Geeks";

    if (isWordPresent(s, word))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if the word is found
static boolean isWordPresent(String sentence, String word)
{
    // To break the sentence in words
    String []s = sentence.split(" ");

    // To temporarily store each individual word
    for ( String temp :s)
    {

        // Comparing the current word
        // with the word to be searched
        if (temp.compareTo(word) == 0)
        {
            return true;
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    String s = "Geeks for Geeks";
    String word = "Geeks";

    if (isWordPresent(s, word))
        System.out.print("Yes");
    else
        System.out.print("No");

}
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function that returns true if the word is found
def isWordPresent(sentence, word):

    # To break the sentence in words
    s = sentence.split(" ")

    for i in s:

        # Comparing the current word
        # with the word to be searched
        if (i == word):
            return True
    return False

# Driver code
s = "Geeks for Geeks"
word = "Geeks"

if (isWordPresent(s, word)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the word is found
static bool isWordPresent(String sentence, String word)
{
    // To break the sentence in words
    String []s = sentence.Split(' ');

    // To temporarily store each individual word
    foreach(String temp in s)
    {

        // Comparing the current word
        // with the word to be searched
        if (temp.CompareTo(word) == 0)
        {
            return true;
        }
    }
    return false;
}

// Driver code
public static void Main(String[] args)
{
    String s = "Geeks for Geeks";
    String word = "Geeks";

    if (isWordPresent(s, word))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if the word is found
function isWordPresent(sentence, word)
{
     // To break the sentence in words
    let s = sentence.split(" ");

    // To temporarily store each individual word
    for ( let temp=0;temp<s.length;temp++)
    {

        // Comparing the current word
        // with the word to be searched
        if (s[temp] == (word) )
        {
            return true;
        }
    }
    return false;
}

// Driver code
let s = "Geeks for Geeks";
let  word = "Geeks";

if (isWordPresent(s, word))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Yes
```

以下是不区分大小写的搜索方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the word is found
bool isWordPresent(string sentence, string word)
{
    // To convert the word in uppercase
    transform(word.begin(),
              word.end(), word.begin(), ::toupper);

    // To convert the complete sentence in uppercase
    transform(sentence.begin(), sentence.end(),
              sentence.begin(), ::toupper);

    // Both strings are converted to the same case,
    // so that the search is not case-sensitive

    // To break the sentence in words
    stringstream s(sentence);

    // To store the individual words of the sentence
    string temp;

    while (s >> temp) {

        // Compare the current word
        // with the word to be searched
        if (temp.compare(word) == 0) {
            return true;
        }
    }
    return false;
}

// Driver code
int main()
{
    string s = "Geeks for Geeks";
    string word = "geeks";

    if (isWordPresent(s, word))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if the word is found
static boolean isWordPresent(String sentence,
                            String word)
{
    // To convert the word in uppercase
    word = transform(word);

    // To convert the complete sentence in uppercase
    sentence = transform(sentence);

    // Both Strings are converted to the same case,
    // so that the search is not case-sensitive

    // To break the sentence in words
    String []s = sentence.split(" ");

    // To store the individual words of the sentence
    for ( String temp :s)
    {

        // Comparing the current word
        // with the word to be searched
        if (temp.compareTo(word) == 0)
        {
            return true;
        }
    }
    return false;
}

static String transform(String word)
{
    return word.toUpperCase();
}

// Driver code
public static void main(String[] args)
{
    String s = "Geeks for Geeks";
    String word = "geeks";

    if (isWordPresent(s, word))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the word is found
def isWordPresent(sentence, word) :

    # To convert the word in uppercase
    word = word.upper()

    # To convert the complete sentence in uppercase
    sentence = sentence.upper()

    # Both strings are converted to the same case,
    # so that the search is not case-sensitive

    # To break the sentence in words
    s = sentence.split();

    for temp in s :

        # Compare the current word
        # with the word to be searched
        if (temp == word) :
            return True;

    return False;

# Driver code
if __name__ == "__main__" :

    s = "Geeks for Geeks";
    word = "geeks";

    if (isWordPresent(s, word)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the word is found
static bool isWordPresent(String sentence,
                            String word)
{
    // To convert the word in uppercase
    word = transform(word);

    // To convert the complete sentence in uppercase
    sentence = transform(sentence);

    // Both Strings are converted to the same case,
    // so that the search is not case-sensitive

    // To break the sentence in words
    String []s = sentence.Split(' ');

    // To store the individual words of the sentence
    foreach ( String temp in s)
    {

        // Comparing the current word
        // with the word to be searched
        if (temp.CompareTo(word) == 0)
        {
            return true;
        }
    }
    return false;
}

static String transform(String word)
{
    return word.ToUpper();
}

// Driver code
public static void Main(String[] args)
{
    String s = "Geeks for Geeks";
    String word = "geeks";

    if (isWordPresent(s, word))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true if the word is found
function isWordPresent(sentence,word)
{
    // To convert the word in uppercase
    word = transform(word);

    // To convert the complete sentence in uppercase
    sentence = transform(sentence);

    // Both Strings are converted to the same case,
    // so that the search is not case-sensitive

    // To break the sentence in words
    let s = sentence.split(" ");

    // To store the individual words of the sentence
    for ( let temp=0;temp<s.length;temp++)
    {

        // Comparing the current word
        // with the word to be searched
        if (s[temp] == (word))
        {
            return true;
        }
    }
    return false;
}

function transform(word)
{
    return word.toUpperCase();
}

// Driver code
let s = "Geeks for Geeks";
let word = "geeks";
if (isWordPresent(s, word))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Yes
```

#### 方法 3:使用内置的 Python 函数:

*   因为一个句子中的所有单词都用空格隔开。
*   我们必须用 split()将句子用空格分开。
*   我们将所有的单词用空格分开，并存储在一个列表中。
*   我们使用 [**count()**](https://www.geeksforgeeks.org/python-list-function-count/) 功能检查单词是否在数组中
*   如果计数值大于 0，则单词出现在字符串中

下面是实现:

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true
# if the word is found
def isWordPresent(sentence, word):

    # To convert the word in uppercase
    word = word.upper()

    # To convert the complete
    # sentence in uppercase
    sentence = sentence.upper()

    # splitting the sentence to list
    lis = sentence.split()
    # checking if word is present
    if(lis.count(word) > 0):
        return True
    else:
        return False

# Driver code
s = "Geeks for Geeks"
word = "geeks"
if (isWordPresent(s, word)):
    print("Yes")
else:
    print("No")

# This code is contributed by vikkycirus
```

**输出:**

```
Yes
```