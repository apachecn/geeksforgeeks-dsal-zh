# 从两个数的和中移除尾随零(使用堆栈)

> 原文:[https://www . geeksforgeeks . org/从两个数字的和中移除尾随零-使用堆栈/](https://www.geeksforgeeks.org/remove-trailing-zeros-from-the-sum-of-two-numbers-using-stack/)

给定两个数字 **A** 和 **B** ，任务是使用[堆栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)移除两个给定数字总和中的尾随零。

**示例:**

> **输入:** A = 124，B = 186
> **输出:** 31
> **说明:**A 和 B 之和为 310。删除尾随零会将总和修改为 31。
> 
> **输入:** A=130246，B = 450164
> T3】输出: 58041

**方法:**给定的问题可以使用[字符串](https://www.geeksforgeeks.org/string-data-structure/)和[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)数据结构来解决。按照以下步骤解决问题:

*   计算 **A + B** 并存储在变量中，比如 **N** 。
*   初始化一个[栈< char >](https://www.geeksforgeeks.org/stack-in-cpp-stl/) ，说 **S** ，存储 **N** 的数字。
*   [将整数 **N** 转换为字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/)，然后将字符推入堆栈 **S** 。
*   当 **S** 不为空()时迭代，如果堆栈的[顶部元素为“0”，则](https://www.geeksforgeeks.org/stack-top-c-stl/)[将其弹出堆栈](https://www.geeksforgeeks.org/stack-pop-method-in-java/)。否则，[断开](https://www.geeksforgeeks.org/break-statement-cc/)。
*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，比如说 **res** ，来存储结果字符串。
*   在 [S 不为空的情况下迭代()](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，推送 **res** 中的所有字符，然后弹出顶部元素。
*   [反转字符串](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/) **res** 并打印 **res** 作为答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to remove trailing
// zeros from the sum of two numbers
string removeTailing(int A, int B)
{
    // Stores the sum of A and B
    int N = A + B;

    // Stores the digits
    stack<int> s;

    // Stores the equivalent
    // string of integer N
    string strsum = to_string(N);

    // Traverse the string
    for (int i = 0; i < strsum.length(); i++) {

        // Push the digit at i
        // in the stack
        s.push(strsum[i]);
    }

    // While top element is '0'
    while (s.top() == '0')

        // Pop the top element
        s.pop();

    // Stores the resultant number
    // without tailing 0's
    string res = "";

    // While s is not empty
    while (!s.empty()) {

        // Append top element of S in res
        res = res + char(s.top());

        // Pop the top element of S
        s.pop();
    }

    // Reverse the string res
    reverse(res.begin(), res.end());

    return res;
}

// Driver Code
int main()
{
    // Input
    int A = 130246, B = 450164;

    // Function Call
    cout << removeTailing(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to remove trailing
// zeros from the sum of two numbers
static String removeTailing(int A, int B)
{

    // Stores the sum of A and B
    int N = A + B;

    // Stores the digits
    Stack<Character> s = new Stack<Character>();

    // Stores the equivalent
    // string of integer N
    String strsum = Integer.toString(N);

    // Traverse the string
    for(int i = 0; i < strsum.length(); i++)
    {

        // Push the digit at i
        // in the stack
        s.push(strsum.charAt(i));
    }

    // While top element is '0'
    while (s.peek() == '0')
    {

        // Pop the top element
        s.pop();
    }

    // Stores the resultant number
    // without tailing 0's
    String res = "";

    // While s is not empty
    while (s.empty() == false)
    {

        // Append top element of S in res
        res = res + (char)s.peek();

        // Pop the top element of S
        s.pop();
    }

    StringBuilder str = new StringBuilder();
    str.append(res);

    // Reverse the string res
    str.reverse();

    return str.toString();
}

// Driver Code
public static void main (String[] args)
{

    // Input
    int A = 130246, B = 450164;

    // Function Call
    System.out.println(removeTailing(A, B));
}
}

// This code is contributed by Dharanendra.L.V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to remove trailing
# zeros from the sum of two numbers
def removeTailing(A,  B):

    # Stores the sum of A and B
    N = A + B

    # Stores the digits
    s = []

    # Stores the equivalent
    # string of integer N
    strsum = str(N)

    # Traverse the string
    for i in range(len(strsum)):

        # Push the digit at i
        # in the stack
        s.append(strsum[i])

    # While top element is '0'
    while (s[-1] == '0'):

        # Pop the top element
        s.pop()

    # Stores the resultant number
    # without tailing 0's
    res = ""

    # While s is not empty
    while (len(s) != 0):

        # Append top element of S in res
        res = res + (s[-1])

        # Pop the top element of S
        s.pop()

    # Reverse the string res
    res = list(res)
    res.reverse()
    res = ''.join(res)

    return res

# Driver Code
if __name__ == "__main__":

    # Input
    A = 130246
    B = 450164

    # Function Call
    print(removeTailing(A, B))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to remove trailing
// zeros from the sum of two numbers
static string removeTailing(int A, int B)
{

    // Stores the sum of A and B
    int N = A + B;

    // Stores the digits
    Stack<char> s = new Stack<char>();

    // Stores the equivalent
    // string of integer N
    string strsum = N.ToString();

    // Traverse the string
    for(int i = 0; i < strsum.Length; i++)
    {

        // Push the digit at i
        // in the stack
        s.Push(strsum[i]);
    }

    // While top element is '0'
    while (s.Peek() == '0')
    {

        // Pop the top element
        s.Pop();
    }

    // Stores the resultant number
    // without tailing 0's
    string res = "";

    // While s is not empty
    while (s.Count != 0)
    {

        // Append top element of S in res
        res = res + (char)s.Peek();

        // Pop the top element of S
        s.Pop();
    }

    char[] str = res.ToCharArray();
    Array.Reverse(str);

    // Reverse the string res
    return new string( str);
}

// Driver Code
static public void Main()
{

    // Input
    int A = 130246, B = 450164;

    // Function Call
    Console.WriteLine(removeTailing(A, B));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

        // Javascript program for the above approach

        // Function to remove trailing
        // zeros from the sum of two numbers
        function removeTailing(A, B) {

            // Stores the sum of A and B
            let N = A + B;

            // Stores the digits
            let s = new Array();

            // Stores the equivalent
            // string of integer N
            let strsum = N.toString();

            // Traverse the string
            for (let i = 0; i < strsum.length; i++) {

                // Push the digit at i
                // in the stack
                s.push(strsum.charAt(i));
            }

            // While top element is '0'
            while (s[s.length-1] === '0') {

                // Pop the top element
                s.pop();
            }

            // Stores the resultant number
            // without tailing 0's
            let res = "";

            // While s is not empty
            while (s.length != 0) {

                // Append top element of S in res
                res = res.concat(s[s.length-1]);

                // Pop the top element of S
                s.pop();
            }

            let str = "";
            str = str.concat(res)

            // Reverse the string res
            str = str.split("").reverse().join("");

            return str.toString();
        }

        // Driver Code

        // Input
        let A = 130246, B = 450164;

        // Function Call
        document.write(removeTailing(A, B));

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
58041
```

***时间复杂度:** O(len(A + B))*
***辅助空间:** O(len(A + B))*