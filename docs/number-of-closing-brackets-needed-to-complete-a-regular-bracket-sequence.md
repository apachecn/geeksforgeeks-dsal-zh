# 完成常规括号序列所需的结束括号数量

> 原文:[https://www . geesforgeks . org/需要完成的右括号数量-常规括号序列/](https://www.geeksforgeeks.org/number-of-closing-brackets-needed-to-complete-a-regular-bracket-sequence/)

给定一个不完整的括号序列，任务是找到使其成为常规括号序列所需的结束括号')'的数量，并打印完整的括号序列。您只能在给定括号序列的末尾添加括号。如果无法完成括号顺序，则打印“不可能”。
让我们定义一个**常规括号序列**如下:

*   空字符串是一个常规的括号序列。
*   如果 s 是常规括号序列，那么(s)就是常规括号序列。
*   如果 s & t 是正则括号序列，那么 st 是正则括号序列。

**示例** :

> **输入**:str =(()((()(“
> )T3】输出:(()((())))
> **解释**:使序列规则所需的最少个数)为 3，并在末尾追加。
> **输入**:str =()(()"
> **输出**:不可能

我们需要添加最小数量的右括号')'，因此我们将计算不平衡的左括号的数量，然后我们将添加该数量的右括号。如果在任何一点上，结束括号的数量大于开始括号的数量，那么答案是**不可能**。
以下是上述办法的实施情况:

## C++

```
// C++ program to find number of closing
// brackets needed and complete a regular
// bracket sequence
#include <iostream>
using namespace std;

// Function to find number of closing
// brackets and complete a regular
// bracket sequence
void completeSuquence(string s)
{
    // Finding the length of sequence
    int n = s.length();

    int open = 0, close = 0;

    for (int i = 0; i < n; i++)
    {
        // Counting opening brackets
        if (s[i] == '(')
            open++;
        else
            // Counting closing brackets
            close++;

        // Checking if at any position the
        // number of closing bracket
        // is more then answer is impossible
        if (close > open)
        {
            cout << "Impossible" << endl;
            return;
        }
    }

    // If possible, print 's' and
    // required closing brackets.
    cout << s;
    for (int i = 0; i < open - close; i++)
        cout << ')';
    cout << endl;
}

// Driver code
int main()
{
    string s = "(()(()(";
    completeSuquence(s);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of closing
// brackets needed and complete a regular
// bracket sequence
class GFG {

    // Function to find number of closing
    // brackets and complete a regular
    // bracket sequence
    static void completeSequence(String s)
    {
        // Finding the length of sequence
        int n = s.length();

        int open = 0, close = 0;

        for (int i = 0; i < n; i++) {

            // Counting opening brackets
            if (s.charAt(i) == '(')
                open++;
            else
                // Counting closing brackets
                close++;

            // Checking if at any position the
            // number of closing bracket
            // is more then answer is impossible
            if (close > open) {
                System.out.print("IMPOSSIBLE");
                return;
            }
        }

        // If possible, print 's' and required closing
        // brackets.
        System.out.print(s);
        for (int i = 0; i < open - close; i++)
            System.out.print(")");         
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "(()(()(";
        completeSequence(s);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find number of
# closing brackets needed and complete
# a regular bracket sequence

# Function to find number of closing
# brackets and complete a regular
# bracket sequence
def completeSequence(s):

    # Finding the length of sequence
    n = len(s)

    open = 0
    close = 0

    for i in range(n):

        # Counting opening brackets
        if (s[i] == '('):
            open += 1
        else:

            # Counting closing brackets
            close += 1

        # Checking if at any position the
        # number of closing bracket
        # is more then answer is impossible
        if (close > open):
            print("IMPOSSIBLE")
            return

    # If possible, print 's' and
    # required closing brackets.
    print(s, end = "")
    for i in range(open - close):
        print(")", end = "")

# Driver code
if __name__ == "__main__":

    s = "(()(()("
    completeSequence(s)

# This code is contributed by ita_c
```

## C#

```
// C# program to find number of closing
// brackets needed and complete a
// regular bracket sequence
using System;

class GFG
{
// Function to find number of closing
// brackets and complete a regular
// bracket sequence
static void completeSequence(String s)
{
    // Finding the length of sequence
    int n = s.Length;

    int open = 0, close = 0;

    for (int i = 0; i < n; i++)
    {

        // Counting opening brackets
        if (s[i] == '(')
            open++;
        else
            // Counting closing brackets
            close++;

        // Checking if at any position the
        // number of closing bracket
        // is more then answer is impossible
        if (close > open)
        {
            Console.Write("IMPOSSIBLE");
            return;
        }
    }

    // If possible, print 's' and
    // required closing brackets.
    Console.Write(s);
    for (int i = 0; i < open - close; i++)
        Console.Write(")");        
}

// Driver Code
static void Main()
{
    String s = "(()(()(";
    completeSequence(s);
}
}

// This code is contributed
// by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of closing
// brackets needed and complete a
// regular bracket sequence

// Function to find number of closing
// brackets and complete a regular
// bracket sequence
function completeSequence($s)
{
    // Finding the length of sequence
    $n = strlen($s);
    $open = 0;
    $close = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // Counting opening brackets
        if ($s[$i] == '(')
            $open++;
        else
            // Counting closing brackets
            $close++;

        // Checking if at any position the
        // number of closing bracket
        // is more then answer is impossible
        if ($close > $open)
        {
            echo ("IMPOSSIBLE");
            return;
        }
    }

    // If possible, print 's' and
    // required closing brackets.
    echo ($s);
    for ($i = 0; $i < $open - $close; $i++)
        echo (")");    
}

// Driver Code
$s = "(()(()(";
completeSequence($s);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find number of closing
    // brackets needed and complete a
    // regular bracket sequence

    // Function to find number of closing
    // brackets and complete a regular
    // bracket sequence
    function completeSequence(s)
    {
        // Finding the length of sequence
        let n = s.length;

        let open = 0, close = 0;

        for (let i = 0; i < n; i++)
        {

            // Counting opening brackets
            if (s[i] == '(')
                open++;
            else
                // Counting closing brackets
                close++;

            // Checking if at any position the
            // number of closing bracket
            // is more then answer is impossible
            if (close > open)
            {
                document.write("IMPOSSIBLE");
                return;
            }
        }

        // If possible, print 's' and
        // required closing brackets.
        document.write(s);
        for (let i = 0; i < open - close; i++)
            document.write(")");        
    }

    let s = "(()(()(";
    completeSequence(s);

</script>
```

**Output:** 

```
(()(()()))
```