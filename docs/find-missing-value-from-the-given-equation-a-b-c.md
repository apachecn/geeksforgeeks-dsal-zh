# 从给定的方程 a + b = c 中找出缺失值

> 原文:[https://www . geeksforgeeks . org/find-从给定方程中缺失值-a-b-c/](https://www.geeksforgeeks.org/find-missing-value-from-the-given-equation-a-b-c/)

给定以下形式的方程:

> **a+b = c**T2】

其中缺少术语![a       ](img/52bc59826aafbb34ac7c40efc202e06a.png "Rendered by QuickLaTeX.com")、![b       ](img/a54f2ddff94c305c1eda8909719a86bd.png "Rendered by QuickLaTeX.com")或![c       ](img/fd8fbe40683b28d605e6a44f922cd3b2.png "Rendered by QuickLaTeX.com")中的任何一个**。任务是找到丢失的术语。**

**示例**:

```
Input: 2 + 6 = ?
Output: 8

Input: ? + 3 =6
Output: 3
```

**方法:**简单地使用方程![a + b = c       ](img/a97e66ca08b258b3e39ad3f7238585f5.png "Rendered by QuickLaTeX.com")就可以找到缺失的数字。首先，我们将从给定的等式中找到两个已知的数字(在程序中读取为字符串)，并将它们转换为整数，并放入等式中。这样，我们就可以找到第三个缺失的数字。我们可以通过将方程存储到字符串中来实现它。

下面是分步算法:

*   从空格的位置将字符串拆分成更小的字符串，并存储在数组中。因此该阵列将包含:

```
arr[0] = "a"
arr[1] = "+"
arr[2] = "b"
arr[3] = "="
arr[4] = "c"
```

*   丢失的字符可能出现在向量中的位置 0、2 或 4。找到丢失字符的位置。
*   将已知字符转换为整数。
*   使用公式查找丢失的字符。

下面是上述方法的实现:

## C++

```
// C++ program to find the missing number
// in the equation a + b = c
#include <bits/stdc++.h>
using namespace std;

// Function to find the missing number
// in the equation a + b = c
int findMissing(string str)
{
    // Array of string to store individual strings
    // after splitting the strings from spaces
    string arrStr[5];

    // Using stringstream to read a string object
    // and split
    stringstream ss(str);

    int i = 0;

    while (ss.good() && i < 5) {
        ss >> arrStr[i];
        ++i;
    }

    int pos = -1;

    // Find position of missing character
    if(arrStr[0] == "?")
        pos = 0;
    else if(arrStr[2] == "?")
        pos = 2;
    else
        pos = 4;

    if(pos == 0)
    {
        string b,c;
        b = arrStr[2];
        c = arrStr[4];

        // Using stoi() to convert strings to int
        int a = stoi(c) - stoi(b);

        return a;
    }
    else if(pos==2)
    {
        string a,c;
        a = arrStr[0];
        c = arrStr[4];

        // Using stoi() to convert strings to int
        int b = stoi(c) - stoi(a);

        return b;
    }
    else if(pos == 4)
    {
        string b,a;
        a = arrStr[0];
        b = arrStr[2];

        // Using stoi() to convert strings to int
        int c = stoi(a) + stoi(b);

        return c;
    }
}

// Driver code
int main()
{
    // Equation with missing value
    string str = "? + 3 = 7";

    cout<<findMissing(str);

    return 0;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the missing number
// in the equation a + b = c
import java.util.*;

class GFG{

// Function to find the missing number
// in the equation a + b = c
static int findMissing(String str)
{

    // Array of String to store individual
    // strings after splitting the strings
    // from spaces
    String arrStr[] = str.split(" ");

    int pos = -1;

    // Find position of missing character
    if (arrStr[0].equals("?"))
        pos = 0;
    else if (arrStr[2].equals("?"))
        pos = 2;
    else
        pos = 4;

    if (pos == 0)
    {
        String b, c;
        b = arrStr[2];
        c = arrStr[4];

        // Using Integer.parseInt() to
        // convert strings to int
        int a = Integer.parseInt(c) -
                Integer.parseInt(b);

        return a;
    }

    else if (pos == 2)
    {
        String a, c;
        a = arrStr[0];
        c = arrStr[4];

        // Using Integer.parseInt() to
        // convert strings to int
        int b = Integer.parseInt(c) -
                Integer.parseInt(a);

        return b;
    }

    else if (pos == 4)
    {
        String b, a;
        a = arrStr[0];
        b = arrStr[2];

        // Using Integer.parseInt() to
        // convert strings to int
        int c = Integer.parseInt(a) +
                Integer.parseInt(b);

        return c;
    }
    return 0;
}

// Driver code
public static void main(String []args)
{

    // Equation with missing value
    String str = "? + 3 = 7";

    System.out.print(findMissing(str));
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program to find the missing number
# in the equation a + b = c

# Function to find the missing number
# in the equation a + b = c
def findMissing(s):

    # Array of string to store individual strings
    # after splitting the strings from spaces
    arrStr = s.split()

    # Using stringstream to read a string object
    # and split
    pos = -1;

    # Find position of missing character
    if(arrStr[0] == "?"):
        pos = 0;
    elif(arrStr[2] == "?"):
        pos = 2;
    else:
        pos = 4;

    if(pos == 0):

        b = arrStr[2];
        c = arrStr[4];

        # Using int() to convert strings to int
        a = int(c) - int(b);

        return a;

    elif(pos == 2):

        a = arrStr[0];
        c = arrStr[4];

        # Using int() to convert strings to int
        b = int(c) - int(a);

        return b;

    elif(pos == 4):

        a = arrStr[0];
        b = arrStr[2];

        # Using int() to convert strings to int
        c = int(a) + int(b);

        return c;

# Driver code
if __name__=='__main__':

    # Equation with missing value
    s = "? + 3 = 7";

    print(findMissing(s))

    # This code is contributed by rutvik_56
```

## C#

```
// C# program to find the missing number
// in the equation a + b = c
using System;
class GFG
{

    // Function to find the missing number
    // in the equation a + b = c
    static int findMissing(string str)
    {

        // Array of String to store individual
        // strings after splitting the strings
        // from spaces
        string[] arrStr = str.Split(" ");
        int pos = -1;

        // Find position of missing character
        if (arrStr[0].Equals("?"))
            pos = 0;
        else if (arrStr[2].Equals("?"))
            pos = 2;
        else
            pos = 4;
        if (pos == 0)
        {
            string b, c;
            b = arrStr[2];
            c = arrStr[4];

            // Using Integer.parseInt() to
            // convert strings to int
            int a = int.Parse(c) - int.Parse(b);
            return a;
        }
        else if (pos == 2)
        {
            string a, c;
            a = arrStr[0];
            c = arrStr[4];

            // Using Integer.parseInt() to
            // convert strings to int
            int b = int.Parse(c) - int.Parse(a);
            return b;
        }

        else if (pos == 4)
        {
            string b, a;
            a = arrStr[0];
            b = arrStr[2];

            // Using Integer.parseInt() to
            // convert strings to int
            int c = int.Parse(a) + int.Parse(b);
            return c;
        }
        return 0;
    }

    // Driver code
    public static void Main(string[] args)
    {

        // Equation with missing value
        string str = "? + 3 = 7";
        Console.WriteLine(findMissing(str));
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript program to find the missing number
// in the equation a + b = c

    // Function to find the missing number
// in the equation a + b = c
    function findMissing(str)
    {
        // Array of String to store individual
    // strings after splitting the strings
    // from spaces
    let arrStr = str.split(" ");

    let pos = -1;

    // Find position of missing character
    if (arrStr[0]==("?"))
        pos = 0;
    else if (arrStr[2]==("?"))
        pos = 2;
    else
        pos = 4;

    if (pos == 0)
    {
        let b, c;
        b = arrStr[2];
        c = arrStr[4];

        // Using Integer.parseInt() to
        // convert strings to int
        let a = parseInt(c) -
                parseInt(b);

        return a;
    }

    else if (pos == 2)
    {
        let a, c;
        a = arrStr[0];
        c = arrStr[4];

        // Using Integer.parseInt() to
        // convert strings to int
        let b = parseInt(c) -
                parseInt(a);

        return b;
    }

    else if (pos == 4)
    {
        let b, a;
        a = arrStr[0];
        b = arrStr[2];

        // Using Integer.parseInt() to
        // convert strings to int
        let c = parseInt(a) +
                parseInt(b);

        return c;
    }
    return 0;
    }

    // Driver code
    // Equation with missing value
    let str = "? + 3 = 7";
    document.write(findMissing(str));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
4
```