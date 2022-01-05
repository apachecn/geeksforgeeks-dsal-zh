# 反转给定字符串中的单词|集合 2

> 原文:[https://www . geesforgeks . org/reverse-word-in-a-给定字符串-set-2/](https://www.geeksforgeeks.org/reverse-words-in-a-given-string-set-2/)

给定字符串 **str** ，任务是通过将字符串的每个单词 **str** 视为一个单元来反转字符串。

**示例:**

> **输入:** str *=* 【极客问答练习代码】
> **输出:** 代码练习问答极客
> ***解释:***
> 给定字符串中的单词为[“极客”、“问答”、“练习”、“代码”]。
> 因此，颠倒单词顺序后，需要的输出是“*代码练习小测验极客”。*
> 
> ***输入** : str = "擅长编码需要大量练习"*
> ***输出**:大量练习需要擅长编码获取*

**原位反转法:**参考文章[反转给定字符串中的单词](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)了解单词的原位反转，然后反转整个字符串。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

[**栈**](https://www.geeksforgeeks.org/stack-data-structure/) **基方法:**在本文中，将讨论使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)解决问题的方法。这里的思路是把 **str** 的所有字都推到**栈**中，然后打印栈的所有元素。按照以下步骤解决问题:

1.  创建一个**栈**来存储字符串**串**的每个单词。
2.  遍历字符串**串**，用空格分隔符分隔**串**的每个单词。
3.  将 **str** 的所有单词推入堆栈。
4.  逐一打印堆栈的所有元素。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to reverse the words
// of a given string
void printRev(string str)
{
    // Stack to store each
    // word of the string
    stack<string> st;

    // Store the whole string
    // in string stream
    stringstream ss(str);

    string temp;
    while (getline(ss, temp, ' ')) {

        // Push each word of the
        // string into the stack
        st.push(temp);
    }

    // Print the string in reverse
    // order of the words
    while (!st.empty()) {
        cout << st.top() << " ";
        st.pop();
    }
}

// Driver Code
int main()
{
    string str;
    str = "geeks quiz practice code";

    printRev(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

    // Function to reverse the words
    // of a given String
    static void printRev(String str)
    {
        // Stack to store each
        // word of the String
        Stack<String> st = new Stack<String>();

        // Store the whole String
        // in String stream
        String[] ss = str.split(" ");

        for (String temp : ss)
        {

            // Push each word of the
            // String into the stack
            st.add(temp);
        }

        // Print the String in reverse
        // order of the words
        while (!st.isEmpty())
        {
            System.out.print(st.peek() + " ");
            st.pop();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str;
        str = "geeks quiz practice code";
        printRev(str);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to reverse the words
# of a given string
def printRev(strr):

    # Stack to store each
    # word of the string
    strr = strr.split(" ")
    st = []

    # Store the whole string
    # in stream
    for i in strr:

        # Push each word of the
        # into the stack
        st.append(i)

    # Print the in reverse
    # order of the words
    while len(st) > 0:
        print(st[-1], end = " ")
        del st[-1]

# Driver Code
if __name__ == '__main__':

    strr = "geeks quiz practice code"

    printRev(strr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;

class GFG{

// Function to reverse the words
// of a given String
static void printRev(string str)
{

    // Stack to store each
    // word of the String
    Stack st = new Stack();

    String[] separator = {" "};

    // Store the whole String
    // in String stream
    string[] ss = str.Split(separator,
                            int.MaxValue,
             StringSplitOptions.RemoveEmptyEntries);

    foreach(string temp in ss)
    {

        // Push each word of the
        // String into the stack
        st.Push(temp);
    }

    // Print the String in reverse
    // order of the words
    while (st.Count > 0)
    {
        Console.Write(st.Peek() + " ");
        st.Pop();
    }
}

// Driver Code
public static void Main(string[] args)
{
    string str;
    str = "geeks quiz practice code";

    printRev(str);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to reverse the words
// of a given String
function printRev(str)
{
        // Stack to store each
        // word of the String
        let st = [];

        // Store the whole String
        // in String stream
        let ss = str.split(" ");

        for (let temp=0;temp< ss.length;temp++)
        {

            // Push each word of the
            // String into the stack
            st.push(ss[temp]);
        }

        // Print the String in reverse
        // order of the words
        while (st.length!=0)
        {
            document.write(st.pop() + " ");

        }
}

// Driver Code
let str;
str = "geeks quiz practice code";
printRev(str);

// This code is contributed by unknown2108
</script>
```

**Output**

```
code practice quiz geeks 
```

**时间复杂度:** O(N)，其中 N 表示字符串的长度。
**辅助空间:** O(N)

#### 方法 2:使用内置的 python 函数

*   因为一个句子中的所有单词都用空格隔开。
*   我们必须使用 [**split()通过空格来分割句子。**T3】](https://www.geeksforgeeks.org/python-string-split/)
*   我们将所有的单词用空格分开，并存储在一个列表中。
*   反转这个列表并打印出来。

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to reverse the words
// of a given string
void printRev(string lis[])
{

    // reverse the list
    reverse(lis, lis + 4);

    for(int i = 0; i < 4; i++)
    {
        cout << lis[i] << " ";
    }
}

int main()
{
    string strr[] = {"geeks", "quiz", "practice", "code"};

    printRev(strr);

    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to reverse the words
// of a given string
static void printRev(String string)
{

    // Split by space and converting
    // string to list
    String[] lis = string.split(" ", 0);

    // Reverse the list
    Collections.reverse(Arrays.asList(lis));

    // Printing the list
    for(String li : lis)
    {
        System.out.print(li + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    String strr = "geeks quiz practice code";

    printRev(strr);
}
}

// This code is contributed by decode2207
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to reverse the words
# of a given string

def printRev(string):
    # split by space and converting
    # string to list
    lis = list(string.split())
    # reverse the list
    lis.reverse()
    # printing the list
    print(*lis)

# Driver Code
if __name__ == '__main__':

    strr = "geeks quiz practice code"

    printRev(strr)

# This code is contributed by vikkycirus
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG {

    // Function to reverse the words
    // of a given string
    static void printRev(string String)
    {
        // split by space and converting
        // string to list
        string[] lis = String.Split(' ');

        // reverse the list
        Array.Reverse(lis);

        // printing the list
        foreach(string li in lis)
        {
            Console.Write(li + " ");
        }
    }

  static void Main() {
    string strr = "geeks quiz practice code";

    printRev(strr);
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to reverse the words
// of a given string

function printRev(string){
    // split by space and converting
    // string to list
    var lis = string.split(' ');
    console.log(lis);
    // reverse the list
    lis.reverse();
    console.log(lis);   
    // printing the list
    document.write(lis.join(' '));
}   

// Driver Code

    var strr = "geeks quiz practice code"

    printRev(strr)

</script>
```

**Output**

```
code practice quiz geeks
```