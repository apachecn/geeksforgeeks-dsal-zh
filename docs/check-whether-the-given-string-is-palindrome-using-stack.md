# 使用堆栈

检查给定字符串是否为回文

> 原文:[https://www . geesforgeks . org/check-给定字符串是否是回文-使用-stack/](https://www.geeksforgeeks.org/check-whether-the-given-string-is-palindrome-using-stack/)

给定字符串 **str** ，任务是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)查找给定字符串是否是回文。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:**否
> **输入:** str = "夫人"
> **输出:**是

**进场:**

*   找到绳子的长度，说出 **len** 。现在，找到 mid 作为 **mid = len / 2** 。
*   将所有元素推到堆栈中间，即 **str[0…mid-1]** 。
*   如果字符串的长度是奇数，那么忽略中间的字符。
*   直到字符串结束，继续从堆栈中弹出元素，并将其与当前字符进行比较，即**字符串[i]** 。
*   如果不匹配，则该字符串不是回文。如果所有的元素都匹配，那么这个字符串就是一个回文。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if string is a palindrome
bool isPalindrome(string s)
{
    int length = s.size();

    // Creating a Stack
    stack<char> st;

    // Finding the mid
    int i, mid = length / 2;

    for (i = 0; i < mid; i++) {
        st.push(s[i]);
    }

    // Checking if the length of the string
    // is odd, if odd then neglect the
    // middle character
    if (length % 2 != 0) {
        i++;
    }

    char ele;
    // While not the end of the string
    while (s[i] != '\0')
    {
         ele = st.top();
         st.pop();

    // If the characters differ then the
    // given string is not a palindrome
    if (ele != s[i])
        return false;
        i++;
    }

return true;
}

// Driver code
int main()
{
    string s = "madam";

    if (isPalindrome(s)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }

    return 0;
}

// This Code is Contributed by Harshit Srivastava
```

## C

```
// C implementation of the approach
#include <malloc.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char* stack;
int top = -1;

// push function
void push(char ele)
{
    stack[++top] = ele;
}

// pop function
char pop()
{
    return stack[top--];
}

// Function that returns 1
// if str is a palindrome
int isPalindrome(char str[])
{
    int length = strlen(str);

    // Allocating the memory for the stack
    stack = (char*)malloc(length * sizeof(char));

    // Finding the mid
    int i, mid = length / 2;

    for (i = 0; i < mid; i++) {
        push(str[i]);
    }

    // Checking if the length of the string
    // is odd, if odd then neglect the
    // middle character
    if (length % 2 != 0) {
        i++;
    }

    // While not the end of the string
    while (str[i] != '\0') {
        char ele = pop();

        // If the characters differ then the
        // given string is not a palindrome
        if (ele != str[i])
            return 0;
        i++;
    }

    return 1;
}

// Driver code
int main()
{
    char str[] = "madam";

    if (isPalindrome(str)) {
        printf("Yes");
    }
    else {
        printf("No");
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static char []stack;
static int top = -1;

// push function
static void push(char ele)
{
    stack[++top] = ele;
}

// pop function
static char pop()
{
    return stack[top--];
}

// Function that returns 1
// if str is a palindrome
static int isPalindrome(char str[])
{
    int length = str.length;

    // Allocating the memory for the stack
    stack = new char[length * 4];

    // Finding the mid
    int i, mid = length / 2;

    for (i = 0; i < mid; i++)
    {
        push(str[i]);
    }

    // Checking if the length of the String
    // is odd, if odd then neglect the
    // middle character
    if (length % 2 != 0)
    {
        i++;
    }

    // While not the end of the String
    while (i < length)
    {
        char ele = pop();

        // If the characters differ then the
        // given String is not a palindrome
        if (ele != str[i])
            return 0;
        i++;
    }

    return 1;
}

// Driver code
public static void main(String[] args)
{
    char str[] = "madam".toCharArray();

    if (isPalindrome(str) == 1)
    {
        System.out.printf("Yes");
    }
    else
    {
        System.out.printf("No");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
stack = []
top = -1

# push function
def push(ele: str):
    global top
    top += 1
    stack[top] = ele

# pop function
def pop():
    global top
    ele = stack[top]
    top -= 1
    return ele

# Function that returns 1
# if str is a palindrome
def isPalindrome(string: str) -> bool:
    global stack
    length = len(string)

    # Allocating the memory for the stack
    stack = ['0'] * (length + 1)

    # Finding the mid
    mid = length // 2
    i = 0
    while i < mid:
        push(string[i])
        i += 1

    # Checking if the length of the string
    # is odd, if odd then neglect the
    # middle character
    if length % 2 != 0:
        i += 1

    # While not the end of the string
    while i < length:
        ele = pop()

        # If the characters differ then the
        # given string is not a palindrome
        if ele != string[i]:
            return False
        i += 1
    return True

# Driver Code
if __name__ == "__main__":

    string = "madam"

    if isPalindrome(string):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static char []stack;
static int top = -1;

// push function
static void push(char ele)
{
    stack[++top] = ele;
}

// pop function
static char pop()
{
    return stack[top--];
}

// Function that returns 1
// if str is a palindrome
static int isPalindrome(char []str)
{
    int length = str.Length;

    // Allocating the memory for the stack
    stack = new char[length * 4];

    // Finding the mid
    int i, mid = length / 2;

    for (i = 0; i < mid; i++)
    {
        push(str[i]);
    }

    // Checking if the length of the String
    // is odd, if odd then neglect the
    // middle character
    if (length % 2 != 0)
    {
        i++;
    }

    // While not the end of the String
    while (i < length)
    {
        char ele = pop();

        // If the characters differ then the
        // given String is not a palindrome
        if (ele != str[i])
            return 0;
        i++;
    }
    return 1;
}

// Driver code
public static void Main(String[] args)
{
    char []str = "madam".ToCharArray();

    if (isPalindrome(str) == 1)
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true
// if string is a palindrome
function isPalindrome(s)
{
    var length = s.length;

    // Creating a Stack
    var st = [];

    // Finding the mid
    var i, mid = parseInt(length / 2);

    for (i = 0; i < mid; i++) {
        st.push(s[i]);
    }

    // Checking if the length of the string
    // is odd, if odd then neglect the
    // middle character
    if (length % 2 != 0) {
        i++;
    }

    var ele;
    // While not the end of the string
    while (i != s.length)
    {
         ele = st[st.length-1];
         st.pop();

    // If the characters differ then the
    // given string is not a palindrome
    if (ele != s[i])
        return false;
        i++;
    }

return true;
}

// Driver code
var s = "madam";
if (isPalindrome(s)) {
    document.write( "Yes");
}
else {
    document.write( "No");
}

</script>
```

**Output:** 

```
Yes
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。