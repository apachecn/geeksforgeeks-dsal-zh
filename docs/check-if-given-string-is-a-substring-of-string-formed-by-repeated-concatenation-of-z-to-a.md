# 检查给定的字符串是否是由 z 和 a 重复连接而成的字符串的子字符串

> 原文:[https://www . geesforgeks . org/check-if-给定字符串是由 z 到 a 的重复串联形成的字符串子字符串/](https://www.geeksforgeeks.org/check-if-given-string-is-a-substring-of-string-formed-by-repeated-concatenation-of-z-to-a/)

给定一个字符串 **str** ，任务是检查字符串 **str** 是否是无限长字符串 **S** 的子字符串，其中小写字母以相反的顺序连接为:

> s = " zyxwvutsntsmkjgfycbyxwtsntmlkjgfedcba . " "

**示例:**

> **输入:** str **= "** cbaz"
> **输出:** YES
> **解释:**
> 给定字符串“cbaz”是 s 的有效子字符串
> 
> **输入:**字符串**= "**yxtuv "
> **输出:** NO
> **解释:**
> 给定字符串“yxtuv”是 s 的有效子字符串

**方法:**可以观察到，除了 **'a'** 后面跟有 **'z'** 之外，每个下一个字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)都比上一个字符低。解决这个问题的最好方法是简单地检查每个字符，看它后面的字符是否有较低的 ASCII 值。当当前字符为“a”时，忽略此比较。如果当前字符“a”出现，则检查它后面是否跟着字符“z”。

以下是步骤:

1.  创建一个标志变量来标记给定的字符串是否是有效的子字符串。最初将其设置为 true。
2.  遍历给定的字符串 **str** ，对于每个字符，**str【I】**执行以下操作:
    *   如果 str[i+1] + 1 < str[i]，继续循环。
    *   如果 str[i] = 'a '和 str[i+1] = 'z '，再次继续循环。
    *   否则将标志变量标记为 false，并从循环中断开。
3.  最后，如果标志为真，打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function checks if a given string is
// valid or not and prints the output
void checkInfinite(string s)
{
    // Boolean flag variable to mark
    // if given string is valid
    bool flag = 1;

    int N = s.length();

    // Traverse the given string
    for (int i = 0; i < N - 1; i++) {

        // If adjacent character
        // differ by 1
        if (s[i] == char(int(s[i + 1]) + 1)) {
            continue;
        }

        // If character 'a' is
        // followed by 4
        else if (s[i] == 'a'
                 && s[i + 1] == 'z') {
            continue;
        }

        // Else flip the flag and
        // break from the loop
        else {
            flag = 0;
            break;
        }
    }

    // Output according to flag variable
    if (flag == 0)
        cout << "NO";
    else
        cout << "YES";
}

// Driver Code
int main()
{
    // Given string
    string s = "ecbaz";

    // Function Call
    checkInfinite(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function checks if a given string is
// valid or not and prints the output
public static void checkInfinite(String s)
{

    // Boolean flag variable to mark
    // if given string is valid
    boolean flag = true;

    int N = s.length();

    // Traverse the given string
    for(int i = 0; i < N - 1; i++)
    {

        // If adjacent character
        // differ by 1
        if (s.charAt(i) == (char)((int)
           (s.charAt(i + 1)) + 1))
        {
            continue;
        }

        // If character 'a' is
        // followed by 4
        else if (s.charAt(i) == 'a' &&
                 s.charAt(i + 1) == 'z')
        {
            continue;
        }

        // Else flip the flag and
        // break from the loop
        else
        {
            flag = false;
            break;
        }
    }

    // Output according to flag variable
    if (!flag)
        System.out.print("NO");
    else
        System.out.print("YES");
}

// Driver code
public static void main(String[] args)
{

    // Given string
    String s = "ecbaz";

    // Function call
    checkInfinite(s);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function checks if a given is
# valid or not and prints the output
def checkInfinite(s):

    # Boolean flag variable to mark
    # if given is valid
    flag = 1

    N = len(s)

    # Traverse the given string
    for i in range(N - 1):

        # If adjacent character
        # differ by 1
        if (s[i] == chr(ord(s[i + 1]) + 1)):
            continue

        # If character 'a' is
        # followed by 4
        elif (s[i] == 'a' and s[i + 1] == 'z'):
            continue

        # Else flip the flag and
        # break from the loop
        else:
            flag = 0
            break

    # Output according to flag variable
    if (flag == 0):
        print("NO")
    else:
        print("YES")

# Driver Code
if __name__ == '__main__':

    # Given string
    s = "ecbaz"

    # Function Call
    checkInfinite(s)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function checks if a given string is
// valid or not and prints the output
public static void checkInfinite(String s)
{

    // Boolean flag variable to mark
    // if given string is valid
    bool flag = true;

    int N = s.Length;

    // Traverse the given string
    for(int i = 0; i < N - 1; i++)
    {

        // If adjacent character
        // differ by 1
        if (s[i] == (char)((int)
           (s[i + 1]) + 1))
        {
            continue;
        }

        // If character 'a' is
        // followed by 4
        else if (s[i] == 'a' &&
                 s[i + 1] == 'z')
        {
            continue;
        }

        // Else flip the flag and
        // break from the loop
        else
        {
            flag = false;
            break;
        }
    }

    // Output according to flag variable
    if (!flag)
        Console.Write("NO");
    else
        Console.Write("YES");
}

// Driver code
public static void Main(String[] args)
{

    // Given string
    String s = "ecbaz";

    // Function call
    checkInfinite(s);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function checks if a given string is
// valid or not and prints the output
function checkInfinite(s)
{

    // Boolean flag variable to mark
    // if given string is valid
    var flag = 1;

    var N = s.length;

    // Traverse the given string
    for (var i = 0; i < N - 1; i++) {

        // If adjacent character
        // differ by 1
        if (s[i] == String.fromCharCode((s[i + 1].charCodeAt(0)) + 1)) {
            continue;
        }

        // If character 'a' is
        // followed by 4
        else if (s[i] == 'a'
                 && s[i + 1] == 'z') {
            continue;
        }

        // Else flip the flag and
        // break from the loop
        else {
            flag = 0;
            break;
        }
    }

    // Output according to flag variable
    if (flag == 0)
        document.write( "NO");
    else
        document.write( "YES");
}

// Driver Code
// Given string
var s = "ecbaz";

// Function Call
checkInfinite(s);

// This code is contributed by famously.
</script>
```

**Output:** 

```
NO
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*