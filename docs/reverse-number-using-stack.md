# 使用堆叠

反转一个号码

> 原文:[https://www.geeksforgeeks.org/reverse-number-using-stack/](https://www.geeksforgeeks.org/reverse-number-using-stack/)

给定一个数字，编写一个程序，使用堆栈反转这个数字。
**例:**

```
Input : 365
Output : 563

Input : 6899
Output : 9986
```

我们已经在[这个](https://www.geeksforgeeks.org/write-a-c-program-to-reverse-digits-of-a-number/)帖子中讨论了反转一个数字的简单方法。在这篇文章中，我们将讨论如何使用堆栈反转一个数字。
这样做的想法是提取数字的位数，并将位数推送到堆栈上。一旦数字的所有数字都被推入堆栈，我们将开始逐个弹出堆栈的内容并形成一个数字。
由于栈是后进先出的数据结构，新形成的数字的位数将是相反的顺序。
以下是以上想法的实现:

## C++

```
// CPP program to reverse the number
// using a stack

#include <bits/stdc++.h>
using namespace std;

// Stack to maintain order of digits
stack <int> st;

// Function to push digits into stack
void push_digits(int number)
{
    while (number != 0)
    {
        st.push(number % 10);
        number = number / 10;
    }
}

// Function to reverse the number
int reverse_number(int number)
{
    // Function call to push number's
    // digits to stack
    push_digits(number);

    int reverse = 0;
    int i = 1;

    // Popping the digits and forming
    // the reversed number
    while (!st.empty())
    {
        reverse = reverse + (st.top() * i);
        st.pop();
        i = i * 10;
    }

    // Return the reversed number formed
    return reverse;
}

// Driver program to test above function
int main()
{
    int number = 39997;

    // Function call to reverse number
    cout << reverse_number(number);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse the number
// using a stack
import java.util.Stack;

public class GFG
{
    // Stack to maintain order of digits
    static Stack<Integer> st= new Stack<>();

    // Function to push digits into stack
    static void push_digits(int number)
    {
        while(number != 0)
        {
            st.push(number % 10);
            number = number / 10;
        }
    }

    // Function to reverse the number
    static int reverse_number(int number)
    {
        // Function call to push number's
        // digits to stack
        push_digits(number);
        int reverse = 0;
        int i = 1;

        // Popping the digits and forming
        // the reversed number
        while (!st.isEmpty())
        {
            reverse = reverse + (st.peek() * i);
            st.pop();
            i = i * 10;
        }

        // Return the reversed number formed
        return reverse;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int number = 39997;
        System.out.println(reverse_number(number));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to reverse the
# number using a stack

# Stack to maintain order of digits
st = [];

# Function to push digits into stack
def push_digits(number):

    while (number != 0):
        st.append(number % 10);
        number = int(number / 10);

# Function to reverse the number
def reverse_number(number):

    # Function call to push number's
    # digits to stack
    push_digits(number);

    reverse = 0;
    i = 1;

    # Popping the digits and forming
    # the reversed number
    while (len(st) > 0):
        reverse = reverse + (st[len(st) - 1] * i);
        st.pop();
        i = i * 10;

    # Return the reversed number formed
    return reverse;

# Driver Code
number = 39997;

# Function call to reverse number
print(reverse_number(number));

# This code is contributed by mits
```

## C#

```
// C# program to reverse the number
// using a stack
using System;
using System.Collections.Generic;

class GFG
{
// Stack to maintain order of digits
public static Stack<int> st = new Stack<int>();

// Function to push digits into stack
public static void push_digits(int number)
{
    while (number != 0)
    {
        st.Push(number % 10);
        number = number / 10;
    }
}

// Function to reverse the number
public static int reverse_number(int number)
{
    // Function call to push number's
    // digits to stack
    push_digits(number);
    int reverse = 0;
    int i = 1;

    // Popping the digits and forming
    // the reversed number
    while (st.Count > 0)
    {
        reverse = reverse + (st.Peek() * i);
        st.Pop();
        i = i * 10;
    }

    // Return the reversed number formed
    return reverse;
}

// Driver Code
public static void Main(string[] args)
{
    int number = 39997;
    Console.WriteLine(reverse_number(number));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to reverse the number
// using a stack

// Stack to maintain order of digits
$st = array();

// Function to push digits into stack
function push_digits($number)
{
    global $st;
    while ($number != 0)
    {
        array_push($st, $number % 10);
        $number = (int)($number / 10);
    }
}

// Function to reverse the number
function reverse_number($number)
{
    global $st;

    // Function call to push number's
    // digits to stack
    push_digits($number);

    $reverse = 0;
    $i = 1;

    // Popping the digits and forming
    // the reversed number
    while (!empty($st))
    {
        $reverse = $reverse +
                  ($st[count($st) - 1] * $i);
        array_pop($st);
        $i = $i * 10;
    }

    // Return the reversed number formed
    return $reverse;
}

// Driver Code
$number = 39997;

// Function call to reverse number
echo reverse_number($number);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
 // JavaScript program for the above approach

        // Stack to maintain order of digits
        let st = [];

        // Function to push digits into stack
        function push_digits(number)
        {
            while (number != 0)
            {
                st.push(number % 10);
                number = Math.floor(number / 10);
            }
        }

        // Function to reverse the number
        function reverse_number(number)
        {

            // Function call to push number's
            // digits to stack
            push_digits(number);

            let reverse = 0;
            let i = 1;

            // Popping the digits and forming
            // the reversed number
            while (st.length != 0) {
                reverse = reverse + (st[st.length - 1] * i);
                st.pop();
                i = i * 10;
            }

            // Return the reversed number formed
            return reverse;
        }

        // Driver program to test above function
        let number = 39997;

        // Function call to reverse number
        document.write(reverse_number(number));

// This code is contributed by Potta Lokesh
</script>
```

**输出:**

```
79993
```

**时间复杂度:**O(logN)
T3】辅助空间: O( logN)，其中 N 为输入数。

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。