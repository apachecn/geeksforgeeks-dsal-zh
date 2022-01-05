# 检查给定字符串是否是奇怪的回文|设置 2

> 原文:[https://www . geesforgeks . org/check-given-string-is-奇怪的回文-or-not-set-2/](https://www.geeksforgeeks.org/check-given-string-is-oddly-palindrome-or-not-set-2/)

给定字符串 **str** ，任务是检查 **str** 奇数索引处的字符是否构成回文字符串。如果不是，则打印**“否”**否则打印**“是”**。

**示例:**

> **输入:** str = "osafdfgsg "，N = 9
> **输出:**是
> **说明:**
> 奇数索引字符为= { s，f，f，s }
> 所以会做成回文串，“sffs”。
> 
> **输入:** str = "addwfefwkll "，N = 11
> **输出:** No
> **说明:**
> 奇数索引字符为= {d，w，e，w，l}
> 所以不会做成回文串，“dwewl”

**天真方法:**天真方法请参考本文的[集 1](https://www.geeksforgeeks.org/check-given-string-is-oddly-palindrome-or-not/)

**有效方法:**想法是检查由给定[串的奇数索引附加形成的奇数串是否形成回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。因此，我们可以使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)来优化运行时间，而不是创建 oddString 然后检查回文。以下是步骤:

1.  为了检查 oddString 是否为回文，我们需要将字符串前半部分的奇数索引字符与字符串后半部分的奇数字符进行比较。
2.  将字符串前半部分的奇数索引字符推入堆栈。
3.  要比较后半部分和前半部分的奇数索引字符，请执行以下操作:
    *   从堆栈中弹出字符，并将其与字符串后半部分的下一个奇数索引字符匹配。
    *   如果以上两个字符不相等，那么由奇数索引组成的字符串就不是回文。打印**“否”**并断开回路。
    *   否则匹配字符串后半部分的剩余奇数字符。
4.  最后，我们需要检查堆栈的大小是否为零。如果是，那么由奇数索引组成的字符串将是回文，否则不是。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if string formed
// by odd indices is palindromic or not
bool isOddStringPalindrome(
    string str, int n)
{
    int oddStringSize = n / 2;

    // Check if length of OddString
    // odd, to consider edge case
    bool lengthOdd
        = ((oddStringSize % 2 == 1)
               ? true
               : false);

    stack<char> s;

    int i = 1;
    int c = 0;

    // Push odd index character of
    // first  half of str in stack
    while (i < n
           && c < oddStringSize / 2) {
        s.push(str[i]);
        i += 2;
        c++;
    }

    // Middle element of odd length
    // palindromic string is not
    // compared
    if (lengthOdd)
        i = i + 2;

    while (i < n && s.size() > 0) {
        if (s.top() == str[i])
            s.pop();
        else
            break;
        i = i + 2;
    }

    // If stack is empty
    // then return true
    if (s.size() == 0)
        return true;

    return false;
}

// Driver Code
int main()
{
    int N = 10;

    // Given string
    string s = "aeafacafae";

    if (isOddStringPalindrome(s, N))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if String formed
// by odd indices is palindromic or not
static boolean isOddStringPalindrome(String str,
                                     int n)
{
    int oddStringSize = n / 2;

    // Check if length of OddString
    // odd, to consider edge case
    boolean lengthOdd = ((oddStringSize % 2 == 1) ?
                                   true : false);

    Stack<Character> s = new Stack<Character>();

    int i = 1;
    int c = 0;

    // Push odd index character of
    // first half of str in stack
    while (i < n && c < oddStringSize / 2)
    {
        s.add(str.charAt(i));
        i += 2;
        c++;
    }

    // Middle element of odd length
    // palindromic String is not
    // compared
    if (lengthOdd)
        i = i + 2;

    while (i < n && s.size() > 0)
    {
        if (s.peek() == str.charAt(i))
            s.pop();
        else
            break;
        i = i + 2;
    }

    // If stack is empty
    // then return true
    if (s.size() == 0)
        return true;

    return false;
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    // Given String
    String s = "aeafacafae";

    if (isOddStringPalindrome(s, N))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if string formed
# by odd indices is palindromic or not
def isOddStringPalindrome(str, n):

    oddStringSize = n // 2;

    # Check if length of OddString
    # odd, to consider edge case
    lengthOdd = True if (oddStringSize % 2 == 1) else False

    s = []

    i = 1
    c = 0

    # Push odd index character of
    # first  half of str in stack
    while (i < n and c < oddStringSize // 2):
        s.append(str[i])
        i += 2
        c += 1

    # Middle element of odd length
    # palindromic string is not
    # compared
    if (lengthOdd):
        i = i + 2

    while (i < n and len(s) > 0):
        if (s[len(s) - 1] == str[i]):
            s.pop()
        else:
            break

        i = i + 2

    # If stack is empty
    # then return true
    if (len(s) == 0):
        return True

    return False;

# Driver code
if __name__=="__main__":

    N = 10

    # Given string
    s = "aeafacafae"

    if (isOddStringPalindrome(s, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to check if String formed
// by odd indices is palindromic or not
static bool isOddStringPalindrome(String str,
                                  int n)
{
    int oddStringSize = n / 2;

    // Check if length of OddString
    // odd, to consider edge case
    bool lengthOdd = ((oddStringSize % 2 == 1) ?
                                true : false);

    Stack<char> s = new Stack<char>();

    int i = 1;
    int c = 0;

    // Push odd index character of
    // first half of str in stack
    while (i < n && c < oddStringSize / 2)
    {
        s.Push(str[i]);
        i += 2;
        c++;
    }

    // Middle element of odd length
    // palindromic String is not
    // compared
    if (lengthOdd)
        i = i + 2;

    while (i < n && s.Count > 0)
    {
        if (s.Peek() == str[i])
            s.Pop();
        else
            break;
        i = i + 2;
    }

    // If stack is empty
    // then return true
    if (s.Count == 0)
        return true;

    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 10;

    // Given String
    String s = "aeafacafae";

    if (isOddStringPalindrome(s, N))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if string formed
// by odd indices is palindromic or not
function isOddStringPalindrome(  str, n)
{
    var oddStringSize = parseInt(n / 2);

    // Check if length of OddString
    // odd, to consider edge case
    var lengthOdd
        = ((oddStringSize % 2 == 1)
               ? true
               : false);

    var s = [];

    var i = 1;
    var c = 0;

    // Push odd index character of
    // first  half of str in stack
    while (i < n
           && c < parseInt(oddStringSize / 2)) {
        s.push(str[i]);
        i += 2;
        c++;
    }

    // Middle element of odd length
    // palindromic string is not
    // compared
    if (lengthOdd)
        i = i + 2;

    while (i < n && s.length > 0) {
        if (s[s.length-1] == str[i])
            s.pop();
        else
            break;
        i = i + 2;
    }

    // If stack is empty
    // then return true
    if (s.length == 0)
        return true;

    return false;
}

// Driver Code
var N = 10;

// Given string
var s = "aeafacafae";
if (isOddStringPalindrome(s, N))
    document.write( "Yes");
else
    document.write( "No\n");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(N)*

**高效方法 2:** 上面的幼稚方法可以在不使用额外空间的情况下解决。我们将使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)，从开始和结束分别向左和向右指向第一个奇数索引。以下是步骤:

1.  检查字符串的长度是奇数还是偶数。
2.  如果长度为奇数，则初始化左= 1，右= N-2
3.  否则，初始化左= 1 和右= N-1
4.  左指针增加 2 个位置，右指针减少 2 个位置。
5.  继续比较指针指向的字符，直到左< =右。
6.  如果没有出现不匹配，那么这个字符串就是回文，否则就不是回文。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Functions checks if characters at
// odd index of the string forms
// palindrome or not
bool isOddStringPalindrome(string str,
                           int n)
{

    // Initialise two pointers
    int left, right;

    if (n % 2 == 0) {
        left = 1;
        right = n - 1;
    }
    else {
        left = 1;
        right = n - 2;
    }

    // Iterate till left <= right
    while (left < n && right >= 0
           && left < right) {

        // If there is a mismatch occurs
        // then return false
        if (str[left] != str[right])
            return false;

        // Increment and decrement the left
        // and right pointer by 2
        left += 2;
        right -= 2;
    }

    return true;
}

// Driver Code
int main()
{
    int n = 10;

    // Given String
    string s = "aeafacafae";

    // Function Call
    if (isOddStringPalindrome(s, n))
        cout << "Yes\n";
    else
        cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Functions checks if characters at
// odd index of the String forms
// palindrome or not
static boolean isOddStringPalindrome(String str,
                                     int n)
{

    // Initialise two pointers
    int left, right;

    if (n % 2 == 0)
    {
        left = 1;
        right = n - 1;
    }
    else
    {
        left = 1;
        right = n - 2;
    }

    // Iterate till left <= right
    while (left < n && right >= 0 &&
           left < right)
    {

        // If there is a mismatch occurs
        // then return false
        if (str.charAt(left) !=
            str.charAt(right))
            return false;

        // Increment and decrement the left
        // and right pointer by 2
        left += 2;
        right -= 2;
    }

    return true;
}

// Driver Code
public static void main(String[] args)
{
    int n = 10;

    // Given String
    String s = "aeafacafae";

    // Function Call
    if (isOddStringPalindrome(s, n))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Functions checks if characters at
# odd index of the string forms
# palindrome or not
def isOddStringPalindrome(Str, n):

    # Initialise two pointers
    left, right = 0, 0

    if (n % 2 == 0):
        left = 1
        right = n - 1
    else:
        left = 1
        right = n - 2

    # Iterate till left <= right
    while (left < n and right >= 0 and
           left < right):

        # If there is a mismatch occurs
        # then return false
        if (Str[left] != Str[right]):
            return False

        # Increment and decrement the left
        # and right pointer by 2
        left += 2
        right -= 2

    return True

# Driver Code
if __name__ == '__main__':

    n = 10

    # Given string
    Str = "aeafacafae"

    # Function call
    if (isOddStringPalindrome(Str, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Functions checks if characters at
// odd index of the String forms
// palindrome or not
static bool isOddStringPalindrome(String str,
                                  int n)
{

    // Initialise two pointers
    int left, right;

    if (n % 2 == 0)
    {
        left = 1;
        right = n - 1;
    }
    else
    {
        left = 1;
        right = n - 2;
    }

    // Iterate till left <= right
    while (left < n && right >= 0 &&
           left < right)
    {

        // If there is a mismatch occurs
        // then return false
        if (str[left] !=
            str[right])
            return false;

        // Increment and decrement the left
        // and right pointer by 2
        left += 2;
        right -= 2;
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 10;

    // Given String
    String s = "aeafacafae";

    // Function Call
    if (isOddStringPalindrome(s, n))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Functions checks if characters at
// odd index of the string forms
// palindrome or not
function isOddStringPalindrome(str, n)
{

    // Initialise two pointers
    var left, right;

    if (n % 2 == 0) {
        left = 1;
        right = n - 1;
    }
    else {
        left = 1;
        right = n - 2;
    }

    // Iterate till left <= right
    while (left < n && right >= 0
           && left < right) {

        // If there is a mismatch occurs
        // then return false
        if (str[left] != str[right])
            return false;

        // Increment and decrement the left
        // and right pointer by 2
        left += 2;
        right -= 2;
    }

    return true;
}

// Driver Code
var n = 10;

// Given String
var s = "aeafacafae";

// Function Call
if (isOddStringPalindrome(s, n))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by importantly.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N)*
T5】空间复杂度: *O(1)*