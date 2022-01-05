# 检查一个字符串是否是脂肪堆积图

> 原文:[https://www . geesforgeks . org/check-string-pangramatic-lipo gram/](https://www.geeksforgeeks.org/check-string-pangrammatic-lipogram/)

为了理解什么是脂肪图，我们将把这个术语分成两个术语，即脂肪图和脂肪图

**Pangram**:Pangram 或全字母句是使用给定字母表的每个字母至少一次的句子。最著名的英语单词是“敏捷的棕色狐狸跳过懒惰的狗。”

**lipo gram**:lipo gram 是一种由书写段落或较长作品组成的限制性写作或文字游戏，其中避免使用特定的字母或字母组——通常是一个常见的元音，通常是英语中最常见的字母 E。

**例:**原《玛丽有只小羊羔》被小 a .罗斯·埃克勒修改，去掉了字母“S”。

```
Original:
Mary had a little lamb
Its fleece was white as snow
And everywhere that Mary went
The lamb was sure to go

He followed her to school one day
That was against the rule
It made the children laugh and play
To see the lamb in school

Lipogram (Without "S"):
Mary had a little lamb
With fleece a pale white hue
And everywhere that Mary went
The lamb kept her in view

To academe he went with her,
Illegal, and quite rare;
It made the children laugh and play
To view the lamb in there
```

**庞格玛脂图** :
庞格玛脂图是使用字母表中除一个字母以外的所有字母的文本。例如，“敏捷的棕色狐狸跳过了懒惰的狗”省略了字母 S，这是通常的 pangram 通过使用单词跳转包括的。

给定一个字符串，我们的任务是检查这个字符串是否是一个脂肪图？

这样做的想法是，我们将跟踪字符串中找不到的所有字母。

*   如果字母表中的所有字母都存在，那么它就是一个庞加莱
*   如果只省略了一个字母，那么它就是一个脂肪图，否则它可能只是一个脂肪图。

以下是上述想法的实现:

## C++

```
// Javascript program to check if a string
// is Pangrammatic Lipogram

#include<bits/stdc++.h>
using namespace std;

// collection of letters
string alphabets = "abcdefghijklmnopqrstuvwxyz";

// function to check for a Pangrammatic Lipogram
void panLipogramChecker(string s)
{  
    // convert string to lowercase
    for(int i=0; i<s.length(); i++)
    {
        s[i] = tolower(s[i]);
    }

    // variable to keep count of all the letters
    // not found in the string
    int counter = 0 ;

    // traverses the string for every
    // letter of the alphabet
    for(int i=0 ; i<26 ; i++)
    {  
        int pos = s.find(alphabets[i]);

        // if character not found in string
        // then increment count
        if(pos<0 || pos>s.length())
            counter += 1;
    }

    if(counter == 0)
        cout<<"Pangram"<<endl;
    else if(counter >= 2)
        cout<<"Not a pangram but might a lipogram"<<endl;
    else
        cout<<"Pangrammatic Lipogram"<<endl;
}

// Driver program to test above function
int main()
{
    string str = "The quick brown fox jumped over the lazy dog";
    panLipogramChecker(str);

    str = "The quick brown fox jumps over the lazy dog";
    panLipogramChecker(str);

    str = "The quick brown fox jum over the lazy dog";
    panLipogramChecker(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a string
// is Pangrammatic Lipogram
import java.util.*;

class GFG
{

// collection of letters
static String alphabets = "abcdefghijklmnopqrstuvwxyz";

/*
    Category             No of letters unmatched
    Pangram                     0
    Lipogram                 >1
    Pangrammatic Lipogram     1
*/

// function to check for a Pangrammatic Lipogram
static void panLipogramChecker(char []s)
{
    // convert string to lowercase
    for(int i = 0; i < s.length; i++)
    {
        s[i] = Character.toLowerCase(s[i]);
    }

    // variable to keep count of all the letters
    // not found in the string
    int counter = 0 ;

    // traverses the string for every
    // letter of the alphabet
    for(int i = 0 ; i < 26 ; i++)
    {
        int pos = find(s, alphabets.charAt(i));

        // if character not found in string
        // then increment count
        if(pos<0 || pos > s.length)
            counter += 1;
    }

    if(counter == 0)
        System.out.println("Pangram");
    else if(counter >= 2)
        System.out.println("Not a pangram but might a lipogram");
    else
        System.out.println("Pangrammatic Lipogram");
}

static int find(char[]arr, char c)
{
    for(int i = 0; i < arr.length; i++)
    {
        if(c == arr[i])
            return 1;
    }
    return -1;
}

// Driver program to test above function
public static void main(String []args)
{
    char []str = "The quick brown fox jumped over the lazy dog".toCharArray();
    panLipogramChecker(str);

    str = "The quick brown fox jumps over the lazy dog".toCharArray();
    panLipogramChecker(str);

    str = "The quick brown fox jum over the lazy dog".toCharArray();
    panLipogramChecker(str);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to check if a string
# is Pangrammatic Lipogram

# collection of letters
alphabets = 'abcdefghijklmnopqrstuvwxyz'

'''
Category                No of letters unmatched
Pangram                     0
Lipogram                    >1
Pangrammatic Lipogram       1
'''

# function to check for a Pangrammatic Lipogram
def panLipogramChecker(s):
    s.lower()

    # variable to keep count of all the letters
    # not found in the string
    counter = 0

    # traverses the string for every
    # letter of the alphabet
    for ch in alphabets:
        # character not found in string then increment count
        if(s.find(ch) < 0):
            counter += 1

    if(counter == 0):
        result = "Pangram"
    elif(counter == 1):
        result = "Pangrammatic Lipogram"
    else:
        result = "Not a pangram but might a lipogram"

    return result

# Driver program to test above function
def main():
    print(panLipogramChecker("The quick brown fox \
                            jumped over the lazy dog"))

    print(panLipogramChecker("The quick brown fox \
                              jumps over the lazy dog"))

    print(panLipogramChecker("The quick brown fox jum\
                                     over the lazy dog"))

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to check if a string
// is Pangrammatic Lipogram
using System;

class GFG
{

// collection of letters
static String alphabets = "abcdefghijklmnopqrstuvwxyz";

/*
    Category             No of letters unmatched
    Pangram                     0
    Lipogram                 >1
    Pangrammatic Lipogram     1
*/

// function to check for a Pangrammatic Lipogram
static void panLipogramChecker(char []s)
{
    // convert string to lowercase
    for(int i = 0; i < s.Length; i++)
    {
        s[i] = char.ToLower(s[i]);
    }

    // variable to keep count of all the letters
    // not found in the string
    int counter = 0 ;

    // traverses the string for every
    // letter of the alphabet
    for(int i = 0 ; i < 26 ; i++)
    {
        int pos = find(s, alphabets[i]);

        // if character not found in string
        // then increment count
        if(pos<0 || pos > s.Length)
            counter += 1;
    }

    if(counter == 0)
        Console.WriteLine("Pangram");
    else if(counter >= 2)
        Console.WriteLine("Not a pangram but might a lipogram");
    else
        Console.WriteLine("Pangrammatic Lipogram");
}

static int find(char[]arr, char c)
{
    for(int i = 0; i < arr.Length; i++)
    {
        if(c == arr[i])
            return 1;
    }
    return -1;
}

// Driver program to test above function
public static void Main(String []args)
{
    char []str = "The quick brown fox jumped over the lazy dog".
                                                  ToCharArray();
    panLipogramChecker(str);

    str = "The quick brown fox jumps over the lazy dog".   
                                          ToCharArray();
    panLipogramChecker(str);

    str = "The quick brown fox jum over the lazy dog".
                                        ToCharArray();
    panLipogramChecker(str);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to check if a string 
// is Pangrammatic Lipogram
let alphabets = "abcdefghijklmnopqrstuvwxyz";

/*
    Category             No of letters unmatched
    Pangram                     0
    Lipogram                 >1
    Pangrammatic Lipogram     1
*/

// Function to check for a Pangrammatic Lipogram
function panLipogramChecker(s)
{  

    // Convert string to lowercase
    for(let i = 0; i < s.length; i++)
    {
        s[i] = s[i].toLowerCase;
    }

    // Variable to keep count of all the letters
    // not found in the string
    let counter = 0;

    // Traverses the string for every
    // letter of the alphabet
    for(let i = 0; i < 26; i++)
    {
        let pos = s.search(alphabets[i]);

        // If character not found in string
        // then increment count
        if (pos < 0 || pos > s.length)
            counter += 1;
    }

    if (counter == 0)
        document.write("Pangram");
    else if (counter >= 2)
        document.write("Not a pangram but " +
                       "might a lipogram");
    else
        document.write("Pangrammatic Lipogram");
}

// Driver code
let str = "The quick brown fox jumped " +
          "over the lazy dog";
panLipogramChecker(str);
document.write("<br>");

str = "The quick brown fox jumps over " +
      "the lazy dog";
panLipogramChecker(str);
document.write("<br>");

str = "The quick brown fox jum " +
      "over the lazy dog";
panLipogramChecker(str);

// This code is contributed by annianni

</script>
```

**输出:**

```
Pangrammatic Lipogram
Pangram
Not a Pangram but might a Lipogram
```

**时间复杂度** : O(26 * N)，这里 N 是要检查的字符串中的字符数，26 代表字母总数。

**高效方法:**一种高效的方法是，我们可以维护一个散列数组或映射来存储输入字符串中每个字母的出现次数，而不是遍历字母表中的所有字母。最初所有字母的计数将被初始化为零。我们将开始遍历字符串并增加字符数。一旦我们完成了遍历字符串，我们将遍历映射或散列数组来寻找有多少字符被计数为零。
**感谢拉维·泰贾·甘纳瓦拉普提出这个方法**。

下面是上述想法的实现。

## C++

```
// C++ program to check for a Pangrammatic
// Lipogram O(n) approach

/*
Category                No of letters unmatched
Pangram                     0
Lipogram                    >1
Pangrammatic Lipogram       1
*/

#include <bits/stdc++.h>
using namespace std;

// function to check for Pangrammatic Lipogram
void panLipogramChecker(string s)
{

    // using map to keep count of the
    // occurence of each letter
    unordered_map<char, int> mp;

    for (char c = 'a'; c <= 'z'; c++) {
        mp = 0;
    }

    transform(s.begin(), s.end(), s.begin(), ::tolower);

    int i, n = s.length();
    for (i = 0; i <= n - 1; i++) {
        if (isalpha(s[i])) {

            // increment count of characters in dictionary
            mp[s[i]]++;
        }
    }
    int count_zero = 0;

    for (auto it : mp) {
        if (it.second == 0) {
            count_zero++;
        }
    }
    if (count_zero > 1) {
        cout << "Not a pangram, but might be a lipogram.\n";
    }
    else if (count_zero == 1) {
        cout << "Pangrammatic Lipogram.\n";
    }
    else if (count_zero < 1) {
        cout << "Pangram.\n";
    }
}

// Driver program to test above function
int main()
{

    panLipogramChecker("The quick brown fox \
                        jumped over the lazy dog");
    panLipogramChecker("The quick brown fox \
                        jumps over the lazy dog");
    panLipogramChecker("The quick brown fox \
                        jum over the lazy dog");
    return 0;
}

// This code is contributed by rajsanghavi9.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check for a Pangrammatic
// Lipogram O(n) approach

/*
Category                No of letters unmatched
Pangram                     0
Lipogram                    >1
Pangrammatic Lipogram       1
*/

import java.util.*;

class GFG {

    // function to check for Pangrammatic Lipogram
    static void panLipogramChecker(String s)
    {

        // using map to keep count of the
        // occurence of each letter
        HashMap<Character, Integer> mp = new HashMap<>();

        for (char c = 'a'; c <= 'z'; c++) {
            mp.put(c, 0);
        }

        s = s.toLowerCase();

        int i, n = s.length();
        for (i = 0; i <= n - 1; i++) {
            if (Character.isAlphabetic(s.charAt(i))) {

                // increment count of characters in
                // dictionary
                mp.put(s.charAt(i),
                       mp.get(s.charAt(i)) + 1);
            }
        }
        int count_zero = 0;

        // Getting an iterator
        Iterator hmIterator = mp.entrySet().iterator();

        while (hmIterator.hasNext()) {
            Map.Entry mapElement
                = (Map.Entry)hmIterator.next();
            int marks = ((int)mapElement.getValue());

            if (marks == 0)
                count_zero++;
        }
        if (count_zero > 1) {
            System.out.println(
                "Not a pangram, but might be a lipogram.");
        }
        else if (count_zero == 1) {
            System.out.println("Pangrammatic Lipogram.");
        }
        else if (count_zero < 1) {
            System.out.println("Pangram.");
        }
    }

    public static void main(String[] args)
    {
        panLipogramChecker(
            "The quick brown fox jumped over the lazy dog");
        panLipogramChecker(
            "The quick brown fox jumps over the lazy dog");
        panLipogramChecker(
            "The quick brown fox jum over the lazy dog");
    }
}

// This code is contributed by rajsanghavi9.
```

## 计算机编程语言

```
# Python program to check for a Pangrammatic
# Lipogram O(n) approach

'''
Category                No of letters unmatched
Pangram                     0
Lipogram                    >1
Pangrammatic Lipogram       1
'''

# function to check for Pangrammatic Lipogram
def panLipogramChecker(s):

    # dictionary to keep count of the
    # occurence of each letter
    counter = {'a': 0, 'b': 0, 'c': 0, 'd': 0, 'e': 0,
               'f': 0, 'g': 0, 'h': 0, 'i': 0, 'j': 0,
               'k': 0, 'l': 0, 'm': 0, 'n': 0, 'o': 0,
               'p': 0, 'q': 0, 'r': 0, 's': 0, 't': 0,
               'u': 0, 'v': 0, 'w': 0, 'x': 0, 'y': 0,
               'z': 0}

    s = s.lower()

    # increment count of characters in dictionary
    for i in s:
        if (i.isalpha()):
            counter[i] += 1

    # returns a list containing the values of all
    # the keys in h=the dictionary
    b = list(counter.values())

    if (b.count(0) > 1):
        print ("Not a pangram, but might be a lipogram.")
    elif (b.count(0) == 1):
        print ("Pangrammatic Lipogram.")
    elif (b.count(0) < 1):
        print ("Pangram.")

# Driver program to test above function
def main():
    panLipogramChecker("The quick brown fox \
                        jumped over the lazy dog")
    panLipogramChecker("The quick brown fox \
                        jumps over the lazy dog")
    panLipogramChecker("The quick brown fox \
                        jum over the lazy dog")

if __name__ == '__main__':
    main()
```

**输出:**

```
Pangrammatic Lipogram
Pangram
Not a Pangram but might a Lipogram
```

**时间复杂度:** O(N)，其中 N 为输入字符串中的字符数。

**参考:**T2】https://www.wikiwand.com/en/Lipogram

本文由 [Palash Nigam](https://www.linkedin.com/in/palash25) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。