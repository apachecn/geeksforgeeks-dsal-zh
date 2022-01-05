# 给定字符串中第 Kth 个空格分隔的数字

> 原文:[https://www . geeksforgeeks . org/kth-space-separated-number-from-给定字符串/](https://www.geeksforgeeks.org/kth-space-seperated-number-from-a-given-string/)

给定一个由空格分隔的整数组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是提取字符串中的 **K <sup>th</sup> 号**。

***注:**字符串中至少包含 K 个数字。*

**示例:**

> **输入:**S =“12 13 15”，K= 3
> **输出:** 15
> **说明:**以上字符串中的 3 <sup>rd</sup> 整数为 15。
> 
> **输入:S**=“10 20 30 40”，K = 2
> **输出:** 20
> **说明:**上述字符串中的 2 <sup>nd</sup> 整数为 20。

**天真方法:**解决问题最简单的方法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并记录遇到的空格数。一旦遇到**K–1**空格，将数字打印到下一个空格作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <iostream>
using namespace std;

// Function to print kth integer
// in a given string
void print_kth_string(string s, int K)
{
    // Size of the string
    int N = s.length();

    // Pointer for iteration
    int i;
    for (i = 0; i < N; i++) {
        // If space char found
        // decrement K
        if (s[i] == ' ')
            K--;

        // If K becomes 1, the next
        // string is the required one
        if (K == 1)
            break;
    }

    // Print the required number
    while (i++ < N && s[i] != ' ')
        cout << s[i];
}

// Driver Code
int main()
{
    // Given string
    string s("10 20 30 40");

    // Given K
    int K = 4;

    // Function call
    print_kth_string(s, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to print kth integer
// in a given string
static void print_kth_string(String s, int K)
{

    // Size of the string
    int N = s.length();

    // Pointer for iteration
    int i;

    for(i = 0; i < N; i++)
    {

        // If space char found
        // decrement K
        if (s.charAt(i) == ' ')
            K--;

        // If K becomes 1, the next
        // string is the required one
        if (K == 1)
            break;
    }

    // Print the required number
    while (i++ < N - 1 && s.charAt(i) != ' ')
        System.out.print(s.charAt(i));
}

// Driver Code
public static void main (String[] args)
{

    // Given string
    String s = "10 20 30 40";

    // Given K
    int K = 4;

    // Function call
    print_kth_string(s, K);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to prkth integer
# in a given string
def print_kth_string(s, K):

    # Size of the string
    N = len(s);

    for i in range(0, N, 1):

        # If space char found
        # decrement K
        if (s[i] == ' '):
            K -= 1;

        # If K becomes 1, the next
        # string is the required one
        if (K == 1):
            break;

    # Print required number
    while (i < N):
        if(s[i] != ' '):
            print(s[i], end = "");
        i += 1;

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "10 20 30 40";

    # Given K
    K = 4;

    # Function call
    print_kth_string(s, K);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to print kth integer
// in a given string
static void print_kth_string(string s, int K)
{

    // Size of the string
    int N = s.Length;

    // Pointer for iteration
    int i;

    for(i = 0; i < N; i++)
    {

        // If space char found
        // decrement K
        if (s[i] == ' ')
            K--;

        // If K becomes 1, the next
        // string is the required one
        if (K == 1)
            break;
    }

    // Print the required number
    while (i++ < N - 1 && s[i] != ' ')
        Console.Write(s[i]);
}

// Driver Code
public static void Main ()
{

    // Given string
    string s = "10 20 30 40";

    // Given K
    int K = 4;

    // Function call
    print_kth_string(s, K);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to prvar kth integer
    // in a given string
    function print_kth_string( s , K) {

        // Size of the string
        var N = s.length;

        // Pointer for iteration
        var i;

        for (i = 0; i < N; i++) {

            // If space char found
            // decrement K
            if (s.charAt(i) == ' ')
                K--;

            // If K becomes 1, the next
            // string is the required one
            if (K == 1)
                break;
        }

        // Prvar the required number
        while (i++ < N - 1 && s.charAt(i) != ' ')
            document.write(s.charAt(i));
    }

    // Driver Code

        // Given string
        var s = "10 20 30 40";

        // Given K
        var K = 4;

        // Function call
        print_kth_string(s, K);

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
40
```

***时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)*

[**Stringstream**](https://www.geeksforgeeks.org/stringstream-c-applications/) **方法:**想法是在 C++中使用 [stringstream](https://www.geeksforgeeks.org/stringstream-c-applications/) ，它将字符串对象与流相关联，并允许我们从字符串中读取，就像它是流一样(就像 cin 一样)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print Kth integer
// from a given string
void print_kth_string(string str, int K)
{
    // Split input into words
    // using stringstream
    stringstream iss(str);

    // Stores individual words
    string kth;

    // Extract words from stream
    while (iss >> kth && K) {
        K--;

        // If kth position
        // is reached
        if (K == 0) {
            cout << kth;
            break;
        }
    }
}

// Driver Code
int main()
{
    // Given string
    string s("10 20 30 40");

    // Given K
    int K = 4;

    // Function call
    print_kth_string(s, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to print Kth integer
// from a given String
static void print_kth_String(String str,
                             int K)
{
  // Split input into words
  // using spilt
  String[] iss = str.split(" ");
  K--;

  System.out.print(iss[K]);
}

// Driver Code
public static void main(String[] args)
{
  // Given String
  String s = ("10 20 30 40");

  // Given K
  int K = 4;

  // Function call
  print_kth_String(s, K);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print Kth integer
# from a given string
def print_kth_string(str1, K):

    # Split input into words
    # using stringstream
    st = str1.split(" ")

    # Stores individual words
    print(st[K - 1])

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "10 20 30 40"

    # Given K
    K = 4

    # Function call
    print_kth_string(s, K)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function to print Kth integer
// from a given String
static void print_kth_String(String str,
                             int K)
{
  // Split input into words
  // using spilt
  String[] iss = str.Split(' ');

  K--; 
  Console.Write(iss[K]);
}

// Driver Code
public static void Main(String[] args)
{
  // Given String
  String s = ("10 20 30 40");

  // Given K
  int K = 4;

  // Function call
  print_kth_String(s, K);
}
}

// This code is contributed by Rajput-Ji
```

**Output**

```
40
```

***时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)*

**内置** [**字符串**](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) **基于函数的方法:**思路是使用 [strtok()](https://www.geeksforgeeks.org/strtok-strtok_r-functions-c-examples/) 函数提取按键处的字符串。使用 [c_str()](https://www.geeksforgeeks.org/basic_string-c_str-function-in-c-stl/) 函数获取字符数组的[字符指针](https://www.geeksforgeeks.org/char-vs-stdstring-vs-char-c/)引用。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <cstring>
#include <iostream>
using namespace std;

// Function to extract integer at key
// position in the given string
void print_kth_string(string str, int K)
{
    // strtok(): Extracts the number at key
    // c_str(): Type cast string to char*
    char* s = strtok((char*)str.c_str(),
                     " ");

    while (K > 1) {
        // Get the token at position -> key
        s = strtok(NULL, " ");
        K--;
    }

    // Print the kth integer
    cout << string(s) << " ";
}

// Driver Code
int main()
{
    // Given string
    string s("10 20 30 40");

    // Given K
    int K = 2;

    // Function call
    print_kth_string(s, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;
class GFG{

// Function to extract integer
// at key position in the given String
static void print_kth_String(String str,
                             int K)
{
  // StringTokenizer(): Extracts
  // the number at key
  // c_str(): Type cast
  // String to char*
  StringTokenizer st =
        new StringTokenizer(str);
  int count = 1;

  while (st.hasMoreTokens() && K > 0 )
  {
    if(count == K)
      System.out.println(st.nextToken());
    count++;
    st.nextToken();
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given String
  String s = ("10 20 30 40");

  // Given K
  int K = 2;

  // Function call
  print_kth_String(s, K);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program of the
// above approach
using System;
class GFG{

// Function to extract integer
// at key position in the given String
static void print_kth_String(String str,
                             int K)
{
  // StringTokenizer(): Extracts
  // the number at key
  // c_str(): Type cast
  // String to char*
  String[] iss = str.Split(' ');

  K--; 
  Console.Write(iss[K]);
}

// Driver Code
public static void Main(String[] args)
{
  // Given String
  String s = ("10 20 30 40");

  // Given K
  int K = 2;

  // Function call
  print_kth_String(s, K);
}
}

// This code is contributed by Rajput-Ji
```

**Output**

```
20 
```

***时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)*