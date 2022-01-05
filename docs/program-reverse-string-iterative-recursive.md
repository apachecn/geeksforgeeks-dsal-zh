# 反转字符串的程序(迭代和递归)

> 原文:[https://www . geesforgeks . org/program-reverse-string-iterative-recursive/](https://www.geeksforgeeks.org/program-reverse-string-iterative-recursive/)

给定一个字符串，编写一个递归程序来反转它。

![string-reverse](img/cae5a93160f0bfede3e4c4695e484c6f.png)

**方法 1(使用堆栈)**

## C++

```
// C++ program to reverse a string using stack
#include <bits/stdc++.h>
using namespace std;

void recursiveReverse(string &str)
{
   stack<char> st;
   for (int i=0; i<str.length(); i++)
       st.push(str[i]);

   for (int i=0; i<str.length(); i++) {
       str[i] = st.top();
       st.pop();
   }      
}

// Driver program
int main()
{
    string str = "geeksforgeeks";
    recursiveReverse(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a string using stack
import java.util.*;
class GFG
{
  public static String recursiveReverse(char []str)
 {
   Stack<Character> st = new Stack<>();
   for(int i=0; i<str.length; i++)
        st.push(str[i]);

   for (int i=0; i<str.length; i++) {
    str[i] = st.peek();
    st.pop();
   }    
   return String.valueOf(str);// converting character array to string
 }

// Driver program
   public static void main(String []args)
   {
      String str = "geeksforgeeks";
      str = recursiveReverse(str.toCharArray());// passing character array as parameter
      System.out.println(str);
   }
}
// This code is contributed by Adarsh_Verma
```

## 蟒蛇 3

```
# Python program to reverse a string using stack

def recursiveReverse(str):

    # using as stack
    stack = []

    for i in range(len(str)):
        stack.append(str[i])

    for i in range(len(str)):
        str[i] = stack.pop()

if __name__ == "__main__":
    str = "geeksforgeeks"

    # converting string to list
    # because strings do not support
    # item assignment
    str = list(str)
    recursiveReverse(str)

    # converting list to string
    str = ''.join(str)
    print(str)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to reverse a string using stack
using System;
using System.Collections.Generic;

class GFG
{
    public static String recursiveReverse(char []str)
    {
        Stack<char> st = new Stack<char>();
        for(int i = 0; i < str.Length; i++)
            st.Push(str[i]);

        for (int i = 0; i < str.Length; i++)
        {
            str[i] = st.Peek();
            st.Pop();
        }

        // converting character array to string
        return String.Join("",str);
    }

    // Driver program
    public static void Main()
    {
        String str = "geeksforgeeks";

        // passing character array as parameter
        str = recursiveReverse(str.ToCharArray());
        Console.WriteLine(str);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program to reverse a string

      function recursiveReverse(str)
      {
        var revString = "";

        for (var i = str.length - 1; i >= 0; i--)
        {
          revString += str[i];
        }

        return revString;
      }

      // Driver program
      var str = "geeksforgeeks";
      document.write(recursiveReverse(str));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
skeegrofskeeg
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

**方法 2(迭代)**

## C++

```
// A Simple Iterative C++ program to reverse
// a string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse a string
void reverseStr(string& str)
{
    int n = str.length();

    // Swap character starting from two
    // corners
    for (int i = 0; i < n / 2; i++)
        swap(str[i], str[n - i - 1]);
}

// Driver program
int main()
{
    string str = "geeksforgeeks";
    reverseStr(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program
// to reverse a string
import java.util.Scanner;

public class reverseStr
{
// Function to reverse
// a string
void stringReverse()
{
    String str = "geeksforgeeks";
    int length = str.length();
    StringBuffer revString = new StringBuffer();
    for (int i = length - 1;
             i >= 0; i--)
    {
        revString.append(str.charAt(i));
    }
    System.out.println(revString);
}

// Driver Code
public static void main(String []args)
{
    reverseStr s= new reverseStr();
    s.stringReverse();
}
}

// This code is contributed
// by prabhat kumar singh
```

## 计算机编程语言

```
# A Simple python program
# to reverse a string

# Function to
# reverse a string
def reverseStr(str):
    n = len(str)

    # initialising a empty
    # string 'str1'
    str1 = ''
    i = n - 1
    while i >= 0:

        # copy str
        # to str1
        str1 += str[i]
        i -= 1
    print(str1)    

# Driver Code
def main():
    str = "geeksforgeeks";
    reverseStr(str);

if __name__=="__main__":
    main()    

# This code is contributed
# by prabhat kumar singh
```

## C#

```
// A Simple Iterative C# program to reverse
// a string
using System;

class GFG
{

// Function to reverse a string
static String reverseStr(String str)
{
    int n = str.Length;

    // Swap character starting from two
    // corners
    for (int i = 0; i < n / 2; i++)
        str = swap(str,i,n - i - 1);
    return str;
}
static String swap(String str, int i, int j)
{
    char []ch = str.ToCharArray();
    char temp = ch[i];
    ch[i] = ch[j];
    ch[j] = temp;
    return String.Join("",ch);
}

// Driver code
public static void Main(String[] args)
{
    string str = "geeksforgeeks";
    str= reverseStr(str);
    Console.WriteLine(str);
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple Iterative PHP
// program to reverse
// a string

// Function to reverse a string
function reverseStr(&$str)
{
    $n = strlen($str);

    // Swap character starting
    // from two corners
    for ($i = 0; $i < $n / 2; $i++)
        //swap the string
        list($str[$i],
             $str[$n - $i - 1]) = array($str[$n - $i - 1],
                                        $str[$i]);
}

// Driver Code
$str = "geeksforgeeks";

reverseStr($str);
echo $str;

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // A Simple Iterative Javascript program to reverse a string

    // Function to reverse a string
    function reverseStr(str)
    {
        let n = str.length;

        // Swap character starting from two
        // corners
        for (let i = 0; i < parseInt(n / 2, 10); i++)
            str = swap(str,i,n - i - 1);
        return str;
    }

    function swap(str, i, j)
    {
        let ch = str.split('');
        let temp = ch[i];
        ch[i] = ch[j];
        ch[j] = temp;
        return ch.join("");
    }

    let str = "geeksforgeeks";
    str= reverseStr(str);
    document.write(str);

</script>
```

**Output:** 

```
skeegrofskeeg
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**方法 3(使用两个指针迭代)**

## C++

```
// A Simple Iterative C++ program to reverse
// a string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse a string
void reverseStr(string& str)
{
    int n = str.length();

    // Swap character starting from two
    // corners
    for (int i=0, j=n-1; i<j; i++,j--)
        swap(str[i], str[j]); 
}

// Driver program
int main()
{
    string str = "geeksforgeeks";
    reverseStr(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//A Simple Iterative Java program to reverse
//a string
class GFG {

    //Function to reverse a string
    static void reverseStr(String str)
    {
     int n = str.length();
     char []ch = str.toCharArray();
     char temp;

     // Swap character starting from two
     // corners
     for (int i=0, j=n-1; i<j; i++,j--)
     {
         temp = ch[i];
         ch[i] = ch[j];
         ch[j] = temp;
     }

     System.out.println(ch);
    }

    //Driver program
    public static void main(String[] args) {

        String str = "geeksforgeeks";
         reverseStr(str);
    }
}
// This code is contributed by Ita_c.
```

## 蟒蛇 3

```
# A Simple Iterative Python program to
# reverse a string

# Function to reverse a string
def reverseStr(str):
    n = len(str)

    i, j = 0, n-1

    # Swap character starting from
    # two corners
    while i < j:
        str[i], str[j] = str[j], str[i]

        i += 1
        j -= 1

# Driver code
if __name__ == "__main__":
    str = "geeksforgeeks"

    # converting string to list
    # because strings do not support
    # item assignment
    str = list(str)
    reverseStr(str)

    # converting list to string
    str = ''.join(str)

    print(str)

# This code is contributed by
# sanjeev2552
```

## C#

```
// A Simple Iterative C# program 
// to reverse a string
using System;

class GFG
{

    //Function to reverse a string
    static void reverseStr(String str)
    {
        int n = str.Length;
        char []ch = str.ToCharArray();
        char temp;

        // Swap character starting from two
        // corners
        for (int i=0, j=n-1; i<j; i++,j--)
        {
            temp = ch[i];
            ch[i] = ch[j];
            ch[j] = temp;
        }
        Console.WriteLine(ch);
    }

    //Driver program
    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";
        reverseStr(str);
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple Iterative PHP
// program to reverse a string

// Function to reverse a string
function reverseStr (&$str)
{
    $n = strlen($str);

    // Swap character starting
    // from two corners
    for ($i = 0, $j = $n - 1;
         $i < $j; $i++, $j--)
        //swap function
        list($str[$i],
             $str[$j]) = array($str[$j],
                               $str[$i]);
}

// Driver Code
$str = "geeksforgeeks";
reverseStr($str);
echo $str;

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
//A Simple Iterative Javascript program to reverse
//a string

//Function to reverse a string
function reverseStr(str)
{
    let n = str.length;
     let ch = str.split("");
     let temp;

     // Swap character starting from two
     // corners
     for (let i=0, j=n-1; i<j; i++,j--)
     {
         temp = ch[i];
         ch[i] = ch[j];
         ch[j] = temp;
     }

     document.write(ch.join("")+"<br>");
}

//Driver program
let str = "geeksforgeeks";
reverseStr(str);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
skeegrofskeeg
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**方法 4(递归)**

## C++

```
// Recursive C++ program to reverse a string
#include <bits/stdc++.h>
using namespace std;

void recursiveReverse(string &str, int i = 0)
{
    int n = str.length();
    if (i == n / 2)
        return;
    swap(str[i], str[n - i - 1]);
    recursiveReverse(str, i + 1);
}

// Driver program
int main()
{
    string str = "geeksforgeeks";
    recursiveReverse(str);
    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to reverse a string
class GFG
{

static void recursiveReverse(char[] str, int i)
{
    int n = str.length;
    if (i == n / 2)
        return;
    swap(str,i,n - i - 1);
    recursiveReverse(str, i + 1);
}
static void swap(char []arr, int i, int j)
{
    char temp= arr[i];
    arr[i]=arr[j];
    arr[j]=temp;
}

// Driver program
public static void main(String[] args)
{
    char[] str = "geeksforgeeks".toCharArray();
    recursiveReverse(str,0);
    System.out.println(String.valueOf(str));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Recursive Python program to reverse a string

def recursiveReverse(str, i = 0):
    n = len(str)

    if i == n // 2:
        return

    str[i], str[n-i-1] = str[n-i-1], str[i]

    recursiveReverse(str, i+1)

if __name__ == "__main__":
    str = "geeksforgeeks"

    # converting string to list
    # because strings do not support
    # item assignment
    str = list(str)
    recursiveReverse(str)

    # converting list to string
    str = ''.join(str)
    print(str)

# This code is contributed by
# sanjeev2552
```

## C#

```
// Recursive C# program to reverse a string
using System;

public class GFG
{

static void recursiveReverse(char[] str, int i)
{
    int n = str.Length;
    if (i == n / 2)
        return;
    swap(str,i,n - i - 1);
    recursiveReverse(str, i + 1);
}
static char[] swap(char []arr, int i, int j)
{
    char temp= arr[i];
    arr[i]=arr[j];
    arr[j]=temp;
    return arr;
}

// Driver program
public static void Main(String[] args)
{
    char[] str = "geeksforgeeks".ToCharArray();
    recursiveReverse(str,0);
    Console.WriteLine(String.Join("",str));
}
}
// This code is contributed by Princi Singh
```

## C++

```
// A quickly written program for reversing a string
// using reverse()
#include<bits/stdc++.h>
using namespace std;
int main()
{
   string str = "geeksforgeeks";

   // Reverse str[begin..end]
   reverse(str.begin(),str.end());

   cout << str;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple Java program
// to reverse a string

class GFG
{

    public static void main(String[] args)
    {
        String str = "geeksforgeeks";

        // Reverse str[begin..end]
        str = reverse(str);

        System.out.println(str);
    }

    static String reverse(String input)
    {
        char[] temparray = input.toCharArray();
        int left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.valueOf(temparray);
    }
}

// This code is contributed by 29AjayKumar
```

## 计算机编程语言

```
# A Simple python program
# to reverse a string

# Function to
# reverse a string
def reverseStr(str):

    # print the string
    # from last
    print(str[::-1])    

# Driver Code
def main():
    str = "geeksforgeeks";
    reverseStr(str);

if __name__=="__main__":
    main()    

# This code is contributed
# by prabhat kumar singh
```

## C#

```
// A Simple C# program to reverse a string
using System;

class GFG
{

    public static void Main(String[] args)
    {
        String str = "geeksforgeeks";

        // Reverse str[begin..end]
        str = reverse(str);

        Console.WriteLine(str);
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Simple PHP program
// to reverse a string

// Function to reverse a string
function reverseStr($str)
{

    // print the string
    // from last
    echo strrev($str);
}

// Driver Code
$str = "geeksforgeeks";

reverseStr($str);

// This code is contributed
// by Srathore
?>
```

**Output:** 

```
skeegrofskeeg
```