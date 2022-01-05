# 递归程序，在一对相同的字符之间插入一个星号

> 原文:[https://www . geeksforgeeks . org/递归程序插入一对相同字符之间的星号/](https://www.geeksforgeeks.org/recursive-program-to-insert-a-star-between-pair-of-identical-characters/)

给定一个重复字符的字符串，我们必须使用递归在相邻的相同字符对之间插入一个星号，即**“***”。

**示例:**

```
Input : aabb 
Output : a*ab*b

Input : xxxy
Output : x*x*xy 
```

**进场:**

*   如果有空字符串，则简单地返回。这就形成了我们的**基础条件**。
*   检查前两个字符是否相同。如果是，则在它们之间插入“*”。
*   因为我们现在已经检查了字符串前两个位置的相同字符，所以我们现在进行递归调用**，而没有字符串的第一个字符**。

上述方法已实施如下:

## C++

```
// Recursive CPP program to insert * between
// two consecutive same characters.
#include <iostream>
using namespace std;

// Function to insert * at desired position
void pairStar(string& input, string& output,
              int i = 0)
{
    // Append current character
    output = output + input[i];

    // If we reached last character
    if (i == input.length() - 1)
        return;

    // If next character is same,
    // append '*'
    if (input[i] == input[i + 1])
        output = output + '*';      

    pairStar(input, output, i+1);
}

// Driver code
int main()
{
    string input = "geeks", output = "";
    pairStar(input, output);
    cout << output << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to insert * between
// two consecutive same characters.
class GFG
{

static String output="";

// Function to insert * at desired position
static void pairStar(String input,
            int i)
{
    // Append current character
    output = output + input.charAt(i);

    // If we reached last character
    if (i == input.length() - 1)
        return;

    // If next character is same,
    // append '*'
    if (input.charAt(i) == input.charAt(i+1))
        output = output + '*';    

    pairStar(input, i+1);
}

// Driver code
public static void main(String[] args)
{
    String input = "geeks";
    pairStar(input,0);
    System.out.println(output);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Recursive CPP program to insert * between
# two consecutive same characters.

# Function to insert * at desired position
def pairStar(Input, Output, i = 0) :

    # Append current character
    Output = Output + Input[i]

    # If we reached last character
    if (i == len(Input) - 1) :
        print(Output)
        return;

    # If next character is same,
    # append '*'
    if (Input[i] == Input[i + 1]) :
        Output = Output + '*';

    pairStar(Input, Output, i + 1);

# Driver code
if __name__ == "__main__" :

    Input = "geeks"
    Output = ""
    pairStar(Input, Output);

# This code is contributed by Ryuga
```

## C#

```
// Recursive C# program to insert * between
// two consecutive same characters.
using System;

class GFG
{

static String output="";

// Function to insert * at desired position
static void pairStar(String input,
            int i)
{
    // Append current character
    output = output + input[i];

    // If we reached last character
    if (i == input.Length - 1)
        return;

    // If next character is same,
    // append '*'
    if (input[i] == input[i+1])
        output = output + '*';    

    pairStar(input, i+1);
}

// Driver code
public static void Main(String[] args)
{
    String input = "geeks";
    pairStar(input,0);
    Console.WriteLine(output);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Recursive PHP program to insert * between
// two consecutive same characters.

// Function to insert * at desired position
function pairStar(&$input, &$output, $i = 0)
{
    // Append current character
    $output = $output . $input[$i];

    // If we reached last character
    if ($i == strlen($input) - 1)
        return;

    // If next character is same,
    // append '*'
    if ($input[$i] == $input[$i + 1])
        $output = $output . '*';    

    pairStar($input, $output, $i+1);
}

    // Driver code
    $input = "geeks";
    $output = "";
    pairStar($input, $output);
    echo $output;
    return 0;

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Recursive Javascript program to insert * between
// two consecutive same characters.

let output="";

// Function to insert * at desired position
function pairStar(input,i)
{
    // Append current character
    output = output + input[i];

    // If we reached last character
    if (i == input.length - 1)
        return;

    // If next character is same,
    // append '*'
    if (input[i] == input[i+1])
        output = output + '*';    

    pairStar(input, i+1);
}

// Driver code
let input = "geeks";
pairStar(input,0);
document.write(output);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
ge*eks
```

**注意:**上面代码中的递归函数是 [**尾递归**](https://www.geeksforgeeks.org/tail-recursion/) 因为递归调用是函数执行的最后一件事。