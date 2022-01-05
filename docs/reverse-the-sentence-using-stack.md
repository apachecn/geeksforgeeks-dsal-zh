# 使用堆栈反转字符串的单词

> 原文:[https://www . geeksforgeeks . org/使用堆栈反转句子/](https://www.geeksforgeeks.org/reverse-the-sentence-using-stack/)

给定由多个单词组成的字符串 **str** ，任务是逐字倒排整个字符串。
**例:**

> **输入:** str = "I Love To Code"
> **输出:** Code To Love I
> **输入:** str = "数据结构和算法"
> **输出:**算法和结构数据

**方法:**这个问题不仅可以在 [strtok()](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/) 的帮助下解决，还可以通过在 STL C++中使用 Stack Container 类按照给定的步骤来解决:

1.  创建一个空堆栈。
2.  遍历整个字符串，遍历时将字符串的字符添加到一个临时
    变量中，直到得到一个空格(')并将该临时变量推入堆栈。
3.  重复上述步骤，直到字符串结束。
4.  从堆栈中弹出单词，直到堆栈不是空的，这将是相反的顺序。

以下是上述方法的实现:

## C++

```
//C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

//function to reverse the words
//of the given string without using strtok().
void reverse(string s)
{
  //create an empty string stack
  stack<string> stc;

  //create an empty temporary string
  string temp="";

  //traversing the entire string
  for(int i=0;i<s.length();i++)
  {
    if(s[i]==' ')
    {

      //push the temporary variable into the stack
      stc.push(temp);

      //assigning temporary variable as empty
      temp="";         
    }
    else
    {
      temp=temp+s[i];
    }

  }

  //for the last word of the string
  stc.push(temp);

  while(!stc.empty()) {

    // Get the words in reverse order
    temp=stc.top();
    cout<<temp<<" ";
    stc.pop();
  }
  cout<<endl;
}

//Driver code
int main()
{
  string s="I Love To Code";
  reverse(s);
  return 0;
}
// This code is contributed by Konderu Hrishikesh.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to reverse the words
// of the given String without
// using strtok().
static void reverse(String s)
{
  // Create an empty String stack
  Stack<String> stc = new Stack<>();

  // Create an empty temporary String
  String temp = "";

  // Traversing the entire String
  for(int i = 0; i < s.length(); i++)
  {
    if(s.charAt(i) == ' ')
    {

      // Push the temporary
      // variable into the stack
      stc.add(temp);

      // Assigning temporary
      // variable as empty
      temp = "";         
    }
    else
    {
      temp = temp + s.charAt(i);
    }

  }

  // For the last word
  // of the String
  stc.add(temp);

  while(!stc.isEmpty())
  {
    // Get the words in
    // reverse order
    temp = stc.peek();
    System.out.print(temp + " ");
    stc.pop();
  }

  System.out.println();
}

//Driver code
public static void main(String[] args)
{
  String s = "I Love To Code";
  reverse(s);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# function to reverse the
# words of the given string
# without using strtok().
def reverse(s):

  # create an empty string
  # stack
  stc = []

  # create an empty temporary
  # string
  temp = ""

  # traversing the entire string
  for i in range(len(s)):

    if s[i] == ' ':

      # push the temporary variable
      # into the stack
      stc.append(temp)

      # assigning temporary variable
      # as empty
      temp = ""         

    else:
      temp = temp + s[i]

  # for the last word of the string
  stc.append(temp)

  while len(stc) != 0:

    # Get the words in reverse order
    temp = stc[len(stc) - 1]
    print(temp, end = " ")
    stc.pop()

  print()

# Driver code
s = "I Love To Code"
reverse(s)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections;

class GFG
{

    // Function to reverse the words
    // of the given String without
    // using strtok().
    static void reverse(string s)
    {

      // Create an empty String stack
      Stack stc = new Stack();

      // Create an empty temporary String
      string temp = "";

      // Traversing the entire String
      for(int i = 0; i < s.Length; i++)
      {
        if(s[i] == ' ')
        {

          // Push the temporary
          // variable into the stack
          stc.Push(temp);

          // Assigning temporary
          // variable as empty
          temp = "";         
        }
        else
        {
          temp = temp + s[i];
        }

      }

      // For the last word
      // of the String
      stc.Push(temp);

      while(stc.Count != 0)
      {

        // Get the words in
        // reverse order
        temp = (string)stc.Peek();
        Console.Write(temp + " ");
        stc.Pop();
      }

      Console.WriteLine();
    }

  // Driver code
  static void Main()
  {
    string s = "I Love To Code";
    reverse(s);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

      // Function to reverse the words
    // of the given String without
    // using strtok().
    function reverse(s)
    {

      // Create an empty String stack
      let stc = [];

      // Create an empty temporary String
      let temp = "";

      // Traversing the entire String
      for(let i = 0; i < s.length; i++)
      {
        if(s[i] == ' ')
        {

          // Push the temporary
          // variable into the stack
          stc.push(temp);

          // Assigning temporary
          // variable as empty
          temp = "";        
        }
        else
        {
          temp = temp + s[i];
        }

      }

      // For the last word
      // of the String
      stc.push(temp);

      while(stc.length != 0)
      {

        // Get the words in
        // reverse order
        temp = stc[stc.length - 1];
        document.write(temp + " ");
        stc.pop();
      }
    }

    let s = "I Love To Code";
    reverse(s);

</script>
```

**Output:** 

```
Code To Love I
```

**时间复杂度:** O(N)

**另一种方法:**不使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)的方法在这里[讨论](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)。使用 stack 也可以通过以下步骤解决这个问题:

1.  创建一个空堆栈。
2.  借助 [strtok()](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/) ，使用空格作为分隔符将输入字符串标记为单词
3.  把单词推进堆栈。
4.  从堆栈中弹出单词，直到堆栈不是空的，这将是相反的顺序。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the words
// of the given sentence
void reverse(char k[])
{

    // Create an empty character array stack
    stack<char*> s;
    char* token = strtok(k, " ");

    // Push words into the stack
    while (token != NULL) {
        s.push(token);
        token = strtok(NULL, " ");
    }

    while (!s.empty()) {

        // Get the words in reverse order
        cout << s.top() << " ";
        s.pop();
    }
}

// Driver code
int main()
{
    char k[] = "geeks for geeks";
    reverse(k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
import java.util.Stack;

class GFG {

    // Function to reverse the words
    // of the given sentence
    static void reverse(String k)
    {

        // Create an empty character array stack
        Stack<String> s = new Stack<>();
        String[] token = k.split(" ");

        // Push words into the stack
        for (int i = 0; i < token.length; i++) {
            s.push(token[i]);
        }

        while (!s.empty()) {

            // Get the words in reverse order
            System.out.print(s.peek() + " ");
            s.pop();
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        String k = "geeks for geeks";
        reverse(k);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to reverse the words
# of the given sentence
def reverse(k):
    # Create an empty character array stack
    s = []
    token = k.split()

    # Push words into the stack
    for word in token :
        s.append(word);

    while (len(s)) :
        # Get the words in reverse order
        print(s.pop(), end = " ");

# Driver code
if __name__ == "__main__" :

    k = "geeks for geeks";
    reverse(k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to reverse the words
    // of the given sentence
    static void reverse(String k)
    {

        // Create an empty character array stack
        Stack<String> s = new Stack<String>();
        String[] token = k.Split(' ');

        // Push words into the stack
        for (int i = 0; i < token.Length; i++) {
            s.Push(token[i]);
        }

        while (s.Count != 0) {

            // Get the words in reverse order
            Console.Write(s.Peek() + " ");
            s.Pop();
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        String k = "geeks for geeks";
        reverse(k);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to reverse the words
    // of the given sentence
    function reverse(k)
    {

        // Create an empty character array stack
        let s = [];
          let token = k.split(" ");

        // Push words into the stack
        for (let i = 0; i < token.length; i++) {
            s.push(token[i]);
        }

        while (s.length > 0) {

            // Get the words in reverse order
            document.write(s[s.length - 1] + " ");
            s.pop();
        }
    }

    // Driver code
    let k = "geeks for geeks";
    reverse(k);

</script>
```

**Output:** 

```
geeks for geeks
```

**时间复杂度:** O(N)