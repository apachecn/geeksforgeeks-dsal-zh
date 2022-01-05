# 反转给定字符串中的单词

> 原文:[https://www . geesforgeks . org/给定字符串中的反向单词/](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)

示例:让输入字符串为“我非常喜欢这个程序”。该函数应该将字符串更改为“非常像我这样的程序”

![reverse-words](img/369767928f21e752cfabf4c1b77a30e2.png)

**示例**:

> **输入** : s =【极客问答练习代码】
> **输出** : s =【代码练习问答极客】
> 
> **输入** : s =“擅长编码需要大量练习”
> **输出** : s =“擅长编码需要大量练习”

**算法**:

*   最初，逐个反转给定字符串的单个单词，对于上面的示例，反转单个单词后，字符串应该是“i ekil siht margorp yrev hcum”。
*   [从头到尾反转整个字符串](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)得到想要的输出“非常像我这个程序”在上例中。

下面是上述方法的实现:

## C++

```
// C++ program to reverse a string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse words*/
void reverseWords(string s)
{

    // temporary vector to store all words
    vector<string> tmp;
    string str = "";
    for (int i = 0; i < s.length(); i++)
    {

        // Check if we encounter space
        // push word(str) to vector
        // and make str NULL
        if (s[i] == ' ')
        {
            tmp.push_back(str);
            str = "";
        }

        // Else add character to
        // str to form current word
        else
            str += s[i];
    }

    // Last word remaining,add it to vector
    tmp.push_back(str);

    // Now print from last to first in vector
    int i;
    for (i = tmp.size() - 1; i > 0; i--)
        cout << tmp[i] << " ";
    // Last word remaining,print it
    cout << tmp[0] << endl;
}

// Driver Code
int main()
{
    string s = "i like this program very much";
    reverseWords(s);
    return 0;
}
```

## C

```
// C program to reverse a string
#include <stdio.h>

// Function to reverse any sequence
// starting with pointer begin and
// ending with pointer end
void reverse(char* begin, char* end)
{
    char temp;
    while (begin < end) {
        temp = *begin;
        *begin++ = *end;
        *end-- = temp;
    }
}

// Function to reverse words*/
void reverseWords(char* s)
{
    char* word_begin = s;

    // Word boundary
    char* temp = s;

    // Reversing individual words as
    // explained in the first step
    while (*temp) {
        temp++;
        if (*temp == '\0') {
            reverse(word_begin, temp - 1);
        }
        else if (*temp == ' ') {
            reverse(word_begin, temp - 1);
            word_begin = temp + 1;
        }
    }

    // Reverse the entire string
    reverse(s, temp - 1);
}

// Driver Code
int main()
{
    char s[] = "i like this program very much";
    char* temp = s;
    reverseWords(s);
    printf("%s", s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// reverse a String
import java.util.*;
class GFG{

// Reverse the letters
// of the word
static void reverse(char str[],
                    int start,
                    int end)
{
  // Temporary variable
  // to store character
  char temp;

  while (start <= end)
  {
    // Swapping the first
    // and last character
    temp = str[start];
    str[start] = str[end];
    str[end] = temp;
    start++;
    end--;
  }
}
// Function to reverse words
static char[] reverseWords(char []s)
{
  // Reversing individual words as
  // explained in the first step

  int start = 0;
  for (int end = 0; end < s.length; end++)
  {
    // If we see a space, we
    // reverse the previous
    // word (word between
    // the indexes start and end-1
    // i.e., s[start..end-1]
    if (s[end] == ' ')
    {
      reverse(s, start, end);
      start = end + 1;
    }
  }

  // Reverse the last word
  reverse(s, start, s.length - 1);

  // Reverse the entire String
  reverse(s, 0, s.length - 1);
  return s;
}

// Driver Code
public static void main(String[] args)
{
  String s = "i like this program very much ";
  char []p = reverseWords(s.toCharArray());
  System.out.print(p);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to reverse a string

# Function to reverse each word in the string
def reverse_word(s, start, end):
    while start < end:
        s[start], s[end] = s[end], s[start]
        start = start + 1
        end -= 1

s = "i like this program very much"

# Convert string to list to use it as a char array
s = list(s)
start = 0
while True:

    # We use a try catch block because for
    # the last word the list.index() function
    # returns a ValueError as it cannot find
    # a space in the list
    try:
        # Find the next space
        end = s.index(' ', start)

        # Call reverse_word function
        # to reverse each word
        reverse_word(s, start, end - 1)

        #Update start variable
        start = end + 1

    except ValueError:

        # Reverse the last word
        reverse_word(s, start, len(s) - 1)
        break

# Reverse the entire list
s.reverse()

# Convert the list back to
# string using string.join() function
s = "".join(s)

print(s)

# Solution contributed by Prem Nagdeo
```

## C#

```
// C# program to
// reverse a String
using System;

class GFG
{

// Reverse the letters
// of the word
static void reverse(char []str,
                    int start,
                    int end)
{

  // Temporary variable
  // to store character
  char temp;

  while (start <= end)
  {

    // Swapping the first
    // and last character
    temp = str[start];
    str[start] = str[end];
    str[end] = temp;
    start++;
    end--;
  }
}

// Function to reverse words
static char[] reverseWords(char []s)
{

  // Reversing individual words as
  // explained in the first step

  int start = 0;
  for (int end = 0; end < s.Length; end++)
  {

    // If we see a space, we
    // reverse the previous
    // word (word between
    // the indexes start and end-1
    // i.e., s[start..end-1]
    if (s[end] == ' ')
    {
      reverse(s, start, end);
      start = end + 1;
    }
  }

  // Reverse the last word
  reverse(s, start, s.Length - 1);

  // Reverse the entire String
  reverse(s, 0, s.Length - 1);
  return s;
}

// Driver Code
public static void Main(String[] args)
{
  String s = "i like this program very much ";
  char []p = reverseWords(s.ToCharArray());
  Console.Write(p);
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>
    // Javascript program to
    // reverse a String

    // Reverse the letters
    // of the word
    function reverse(str,start,end)
    {
        // Temporary variable
        // to store character
        let temp;

        while (start <= end)
        {
            // Swapping the first
            // and last character
            temp = str[start];
            str[start]=str[end];
            str[end]=temp;
            start++;
            end--;
        }
    }
    // Function to reverse words
    function reverseWords(s)
    {
        // Reversing individual words as
        // explained in the first step
        s=s.split("");
        let start = 0;
        for (let end = 0; end < s.length; end++)
        {
            // If we see a space, we
            // reverse the previous
            // word (word between
            // the indexes start and end-1
            // i.e., s[start..end-1]
            if (s[end] == ' ')
            {
                reverse(s, start, end);
                start = end + 1;
            }
        }
        // Reverse the last word
        reverse(s, start, s.length - 1);

        // Reverse the entire String
        reverse(s, 0, s.length - 1);
        return s.join("");
    }
    // Driver Code
    var s = "i like this program very much ";

    document.write(reverseWords(s));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
much very program this like i
```

上面的代码没有处理字符串以空格开头的情况。下面的版本处理这种特殊情况，在中间有多个空格的情况下，不会对反函数进行不必要的调用。感谢 rka143 提供这个版本。

## C++

```
// C++ program for above approach:
void reverseWords(char* s)
{
  char* word_begin = NULL;

  //  /* temp is for word boundary */
  char* temp = s;

  /*STEP 1 of the above algorithm */
  while (*temp)
  {

    /*This condition is to make sure that the
          string start with valid character (not
          space) only*/
    if ((word_begin == NULL) &&
        (*temp != ' '))
    {
      word_begin = temp;
    }
    if (word_begin && ((*(temp + 1) == ' ') ||
                       (*(temp + 1) == '\0')))
    {
      reverse(word_begin, temp);
      word_begin = NULL;
    }
    temp++;
  } /* End of while */

  /*STEP 2 of the above algorithm */
  reverse(s, temp - 1);
}

// This code is contributed by rutvik_56.
```

## C

```
// C program for above approach:
void reverseWords(char* s)
{
    char* word_begin = NULL;

    //  /* temp is for word boundary */
    char* temp = s;

    /*STEP 1 of the above algorithm */
    while (*temp)
    {

        /*This condition is to make sure that the
          string start with valid character (not
          space) only*/
        if ((word_begin == NULL) &&
                  (*temp != ' '))
        {
            word_begin = temp;
        }
        if (word_begin && ((*(temp + 1) == ' ') ||
            (*(temp + 1) == '\0')))
        {
            reverse(word_begin, temp);
            word_begin = NULL;
        }
        temp++;
    } /* End of while */

    /*STEP 2 of the above algorithm */
    reverse(s, temp - 1);
}
```

**时间复杂度:**O(n)
T3】另一种方法:

我们可以通过以相反的方式拆分和保存字符串来完成上述任务。

下面是上述方法的实现:

## C++

```
// C++ program to reverse a string
// s = input()
#include <bits/stdc++.h>
using namespace std;

int main()
{
    string s[] = {"i", "like", "this", "program", "very", "much"};

    string ans = "";
    for (int i = 5; i >= 0; i--)
    {
        ans += s[i] + " ";
    }
    cout << ("Reversed String:") << endl;
    cout << (ans.substr(0, ans.length() - 1)) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a string
// s = input()
public class ReverseWords
{

    public static void main(String[] args)
    {
        String s[] = "i like this program very much".
                                        split(" ");
        String ans = "";
        for (int i = s.length - 1; i >= 0; i--)
        {
            ans += s[i] + " ";
        }
        System.out.println("Reversed String:");
        System.out.println(ans.substring(0,
                                  ans.length() - 1));
    }
}
```

## 蟒蛇 3

```
# Python3 program to reverse a string
# s = input()
s = "i like this program very much"
words = s.split(' ')
string =[]
for word in words:
    string.insert(0, word)

print("Reversed String:")
print(" ".join(string))

# Solution proposed bu Uttam
```

## C#

```
// C# program to reverse a string
// s = input()

using System;
public class ReverseWords
{

    public static void Main()
    {
        string[] s = "i like this program very much".
                                         Split(' ');
        string ans = "";
        for (int i = s.Length - 1; i >= 0; i--)
        {
            ans += s[i] + " ";
        }
        Console.Write("Reversed String:\n");
        Console.Write(ans.Substring(0,
                                    ans.Length - 1));
    }
}
```

## java 描述语言

```
<script>

// JavaScript program to reverse a string

var s= ["i", "like", "this", "program", "very", "much"];

    var ans ="";
    for (var i = 5; i >= 0; i--)
    {
        ans += s[i] + " ";
    }
    document.write("Reversed String:"+ "<br>");
    document.write(ans.slice(0,ans.length-1));

</script>
```

**Output:** 

```
Reversed String:
much very program this like i
```

**时间复杂度:** O(n)

**不使用任何额外空间:**
以上任务也可以从中间开始拆分直接对换字符串来完成。由于涉及直接交换，因此占用的空间也更少。

下面是上述方法的实现:

## C++

```
// C++ code to reverse a string
#include <bits/stdc++.h>
using namespace std;

// Reverse the string
string RevString(string s[], int l)
{

    // Check if number of words is even
    if (l % 2 == 0)
    {

        // Find the middle word
        int j = l / 2;

        // Starting from the middle
        // start swapping words at
        // jth position and l-1-j position
        while (j <= l - 1)
        {
            string temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Check if number of words is odd
    else
    {

        // Find the middle word
        int j = (l / 2) + 1;

        // Starting from the middle start
        // swapping the words at jth
        // position and l-1-j position
        while (j <= l - 1)
        {
            string temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    string S = s[0];

    // Return the reversed sentence
    for(int i = 1; i < 9; i++)
    {
        S = S + " " + s[i];
    }
    return S;
}

// Driver code
int main()
{
    string s = "getting good at coding "
               "needs a lot of practice";

    string words[] = { "getting", "good", "at",
                       "coding", "needs", "a",
                       "lot", "of", "practice"};

    cout << RevString(words, 9) << endl;

    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to reverse a string
class GFG{

// Reverse the string
public static String[] RevString(String[] s,
                                 int l)
{

    // Check if number of words is even
    if (l % 2 == 0)
    {

        // Find the middle word
        int j = l / 2;

        // Starting from the middle
        // start swapping words at
        // jth position and l-1-j position
        while (j <= l - 1)
        {
            String temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Check if number of words is odd
    else
    {

        // Find the middle word
        int j = (l / 2) + 1;

        // Starting from the middle start
        // swapping the words at jth
        // position and l-1-j position
        while (j <= l - 1)
        {
            String temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Return the reversed sentence
    return s;
}

// Driver Code
public static void main(String[] args)
{
    String s = "getting good at coding " +
               "needs a lot of practice";
    String[] words = s.split("\\s");

    words = RevString(words, words.length);

    s = String.join(" ", words);

    System.out.println(s);
}
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python3 code to reverse a string

# Reverse the string
def RevString(s,l):

  # Check if number of words is even
  if l%2 == 0:

    # Find the middle word
    j = int(l/2)

    # Starting from the middle
    # start swapping words
    # at jth position and l-1-j position
    while(j <= l - 1):
      s[j], s[l - j - 1] = s[l - j - 1], s[j]
      j += 1

  # Check if number of words is odd
  else:

    # Find the middle word
    j = int(l/2 + 1)

    # Starting from the middle
    # start swapping the words
    # at jth position and l-1-j position
    while(j <= l - 1):
      s[j], s[l - 1 - j] = s[l - j - 1], s[j]
      j += 1

    # return the reversed sentence
    return s;

# Driver Code
s = 'getting good at coding needs a lot of practice'
string = s.split(' ')
string = RevString(string,len(string))
print(" ".join(string))
```

## C#

```
// C# code to reverse a string
using System;
class GFG{

// Reverse the string
public static String[] RevString(String[] s, int l)
{

    // Check if number of words is even
    if (l % 2 == 0)
    {

        // Find the middle word
        int j = l / 2;

        // Starting from the middle
        // start swapping words at
        // jth position and l-1-j position
        while (j <= l - 1)
        {
            String temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Check if number of words is odd
    else
    {

        // Find the middle word
        int j = (l / 2) + 1;

        // Starting from the middle start
        // swapping the words at jth
        // position and l-1-j position
        while (j <= l - 1)
        {
            String temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Return the reversed sentence
    return s;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "getting good at coding " +
            "needs a lot of practice";
    String[] words = s.Split("\\s");

    words = RevString(words, words.Length);

    s = String.Join(" ", words);

    Console.WriteLine(s);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript code to reverse a string

// Reverse the string
function RevString(s, l)
{

    // Check if number of words is even
    if (l % 2 == 0)
    {

        // Find the middle word
        let j = parseInt(l / 2, 10);

        // Starting from the middle
        // start swapping words at
        // jth position and l-1-j position
        while (j <= l - 1)
        {
            let temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Check if number of words is odd
    else
    {

        // Find the middle word
        let j = parseInt((l / 2), 10) + 1;

        // Starting from the middle start
        // swapping the words at jth
        // position and l-1-j position
        while (j <= l - 1)
        {
            let temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    let S = s[0];

    // Return the reversed sentence
    for(let i = 1; i < 9; i++)
    {
        S = S + " " + s[i];
    }
    return S;
}

// Driver code
let s = "getting good at coding "
        "needs a lot of practice";

let words = [ "getting", "good", "at",
              "coding", "needs", "a",
              "lot", "of", "practice"];

document.write(RevString(words, 9));

// This code is contributed by suresh07

</script>
```

**Output**

```
practice of lot a needs coding at good getting
```

**另一个直观的恒空间解**:遍历字符串，镜像字符串中的每个单词，然后，在最后，镜像整个字符串。

下面的 C++代码可以处理多个连续的空格。

## C++

```
#include <algorithm>
#include <iostream>
#include <string>

using namespace std;

string reverse_words(string s)
{
    int left = 0, i = 0, n = s.size();

    while (s[i] == ' ')
        i++;

    left = i;

    while (i < n)
    {
        if (i + 1 == n || s[i] == ' ')
        {
            int j = i - 1;
            if (i + 1 == n)
                j++;

            while (left < j)
                swap(s[left++], s[j--]);

            left = i + 1;
        }
        if (s[left] == ' ' && i > left)
            left = i;

        i++;
    }
    reverse(s.begin(), s.end());
    return s;
}

int main()
{

    string str = "Be a game changer the world is already full of players";

    str = reverse_words(str);

    cout << str;

    return 0;
  // This code is contributed
  // by Gatea David
}
```

**输出**

```
players of full already is world the changer game a Be
```

如果发现以上代码/算法有任何 bug，请写评论，或者找其他方法解决同样的问题。