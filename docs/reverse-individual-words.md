# 颠倒单个单词

> 原文:[https://www.geeksforgeeks.org/reverse-individual-words/](https://www.geeksforgeeks.org/reverse-individual-words/)

给定一个字符串，我们需要打印单个单词的反串。
**例:**

```
Input : Hello World
Output : olleH dlroW

Input :  Geeks for Geeks
Output : skeeG rof skeeG
```

**方法 1(简单):**生成所有用空格分隔的单词。一个一个倒排单词，用空格隔开打印出来。
**方法二(空间高效):**我们用一个栈把所有的字推到空间之前。一遇到空位，我们就清空堆栈。

## C++

```
// C++ program to reverse individual words in a given
// string using STL list
#include <bits/stdc++.h>
using namespace std;

// reverses individual words of a string
void reverseWords(string str)
{
    stack<char> st;

    // Traverse given string and push all characters
    // to stack until we see a space.
    for (int i = 0; i < str.length(); ++i) {
        if (str[i] != ' ')
            st.push(str[i]);

        // When we see a space, we print contents
        // of stack.
        else {
            while (st.empty() == false) {
                cout << st.top();
                st.pop();
            }
            cout << " ";
        }
    }

    // Since there may not be space after
    // last word.
    while (st.empty() == false) {
        cout << st.top();
        st.pop();
    }
}

// Driver program to test function
int main()
{
    string str = "Geeks for Geeks";
    reverseWords(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse individual
// words in a given string using STL list
import java.io.*;
import java.util.*;

class GFG {

// reverses individual words of a string
static void reverseWords(String str)
{
    Stack<Character> st=new Stack<Character>();

    // Traverse given string and push all
    // characters to stack until we see a space.
    for (int i = 0; i < str.length(); ++i) {
        if (str.charAt(i) != ' ')
            st.push(str.charAt(i));

        // When we see a space, we print
        // contents of stack.
        else {
            while (st.empty() == false) {
                System.out.print(st.pop());

            }
            System.out.print(" ");
        }
    }

    // Since there may not be space after
    // last word.
    while (st.empty() == false) {
        System.out.print(st.pop());

    }
}

// Driver program to test above function
public static void main(String[] args)
{
   String str = "Geeks for Geeks";
    reverseWords(str);
  }
}
```

## 蟒蛇 3

```
# Python3 program to reverse individual words
# in a given string using STL list

# reverses individual words of a string
def reverserWords(string):
    st = list()

    # Traverse given string and push all characters
    # to stack until we see a space.
    for i in range(len(string)):
        if string[i] != " ":
            st.append(string[i])

        # When we see a space, we print
        # contents of stack.
        else:
            while len(st) > 0:
                print(st[-1], end= "")
                st.pop()
            print(end = " ")

    # Since there may not be space after
    # last word.
    while len(st) > 0:
        print(st[-1], end = "")
        st.pop()

# Driver Code
if __name__ == "__main__":
    string = "Geeks for Geeks"
    reverserWords(string)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to reverse individual
// words in a given string using STL list
using System;
using System.Collections.Generic;

class GFG
{

// reverses individual words
// of a string
public static void reverseWords(string str)
{
    Stack<char> st = new Stack<char>();

    // Traverse given string and push
    // all characters to stack until
    // we see a space.
    for (int i = 0; i < str.Length; ++i)
    {
        if (str[i] != ' ')
        {
            st.Push(str[i]);
        }

        // When we see a space, we
        // print contents of stack.
        else
        {
            while (st.Count > 0)
            {
                Console.Write(st.Pop());

            }
            Console.Write(" ");
        }
    }

    // Since there may not be
    // space after last word.
    while (st.Count > 0)
    {
        Console.Write(st.Pop());

    }
}

// Driver Code
public static void Main(string[] args)
{
    string str = "Geeks for Geeks";
    reverseWords(str);
}
}

// This code is contributed
// by Shrikant13
```

**输出:**

```
skeeG rof skeeG
```

[Python |反转一个句子中的每个单词](https://www.geeksforgeeks.org/python-reverse-word-sentence/)
**使用 C++中的**[**string stream**](https://www.geeksforgeeks.org/stringstream-c-applications/)**:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include<bits/stdc++.h>
using namespace std;

void printWords(string str)
{
    // word variable to store word
    string word;

    // making a string stream
    stringstream iss(str);

    // Read and print each word.
    while (iss >> word){
        reverse(word.begin(),word.end());
        cout<<word<<" ";
    }
}

// Driver code
int main()
{
    string s = "GeeksforGeeks is good to learn";
    printWords(s);
    return 0;
}
// This code is contributed by Nikhil Rawat
```

**输出:**

```
skeeGrofskeeG si doog ot nrael 
```

时间复杂度:O(n)
空间复杂度:O(n)
**使用 Java 8 Streams**

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
import java.util.stream.Collectors;

// This code is contributed by Mayank Sharma
public class reverseIndividual {

    public static void main(String[] args) {

        String str = "Welcome to GFG";

        // Splitting the string based on space and reverse each part
        // and then join
        String result = Arrays.asList(str.split(" "))
                .stream()
                .map(s -> new StringBuilder(s).reverse())
                .collect(Collectors.joining(" "));

        System.out.println(result);

    }

}
```

**输出:**

```
emocleW ot GFG
```

**<u>替代方法:</u>** 存储反转的字符串，而不仅仅是打印

**步骤:**

1.  创建一个堆栈并推送给定输入字符串的所有字符。
2.  创建“版本”和“临时”字符串
3.  执行以下步骤，直到堆栈变空。
4.  如果堆栈的 peek()是一个字符，将其附加到 temp
5.  如果堆栈的 peek()是一个空格，那么在 rev 中添加空格，在 rev 中添加 temp
6.  最后，如果 temp 不为空，将 temp 追加到前面的 rev 中
7.  返回反转的字符串

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
//java program to reverse the individual words
import java.util.Stack;

public class Reverse {

    //function to reverse the individual words
    String reverse(String str) {
        //create a stack to access the string from end
        Stack<Character> s = new Stack<>();

        //push all the characters of the stack
        for(int i = 0; i < str.length();i++)
            s.push(str.charAt(i));

        //rev string to store the required output
        String rev = "";
        String temp = "";

        //till the stack becomes empty
        while(!s.isEmpty()) {
            //if top of the stack is a letter,
            //then append it to temp;
            if(Character.isLetter(s.peek()))
                temp = temp + s.pop();
            //if it is a space, the append space to rev
            //and also temp to rev
            else {
                rev = " " + temp +rev;
                //make the temp empty
                temp = "";
                s.pop();
            }
        }
        //if temp is not empty, add temp to rev at the front
        if(temp != "")
            rev = temp + rev;

        //return the output string
        return rev;
    }

    public static void main(String[] args) {
        String str = "Geeks for Geeks";

        Reverse obj = new Reverse();
        System.out.println(obj.reverse(str));
    }
}

//This method is contributed by Likhita AVL
```

**Output**

```
skeeG rof skeeG

```

**时间复杂度:** O(n)。