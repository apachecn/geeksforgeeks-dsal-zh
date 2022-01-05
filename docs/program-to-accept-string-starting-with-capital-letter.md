# 接受以大写字母

开头的字符串的程序

> 原文:[https://www . geesforgeks . org/program-to-accept-string-以大写字母开头/](https://www.geeksforgeeks.org/program-to-accept-string-starting-with-capital-letter/)

给定一个由字母组成的字符串 **str** ，任务是检查给定的字符串是否以大写字母开头。
**例:**

```
Input: str = "GeeksforGeeks"
Output: Accepted

Input: str = "geeksforgeeks"
Output: Not Accepted
```

**进场:**

*   找到字符串第一个字符
    的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)
*   检查该值是否在[65，90]范围内

*   如果是，打印接受

*   否则打印不接受

以下是上述方法的实现:

## C++

```
// C++ program to accept String
// starting with Capital letter

#include <iostream>
using namespace std;

// Function to check if first
// character is Capital
int checkIfStartsWithCapital(string str)
{

    if (str[0] >= 'A' && str[0] <= 'Z')
        return 1;
    else
        return 0;
}

// Function to check
void check(string str)
{
    if (checkIfStartsWithCapital(str))
        cout << "Accepted\n";
    else
        cout << "Not Accepted\n";
}

// Driver function
int main()
{
    string str = "GeeksforGeeks";
    check(str);

    str = "geeksforgeeks";
    check(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to accept String
// starting with Capital letter
class GFG
{

    // Function to check if first
    // character is Capital
    static int checkIfStartsWithCapital(String str)
    {

        if (str.charAt(0) >= 'A' && str.charAt(0)<= 'Z')
            return 1;
        else
            return 0;
    }

    // Function to check
    static void check(String str)
    {
        if (checkIfStartsWithCapital(str) == 1)
            System.out.println("Accepted");
        else
            System.out.println("Not Accepted");
    }

    // Driver function
    public static void main (String[] args)
    {
        String str = "GeeksforGeeks";
        check(str);

        str = "geeksforgeeks";
        check(str);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to accept String
# starting with Capital letter

# Function to check if first
# character is Capital
def checkIfStartsWithCapital(string) :

    if (string[0] >= 'A' and string[0] <= 'Z') :
        return 1;
    else :
        return 0;

# Function to check
def check(string) :

    if (checkIfStartsWithCapital(string)) :
        print("Accepted");
    else :
        print("Not Accepted");

# Driver function
if __name__ == "__main__" :

    string = "GeeksforGeeks";
    check(string);

    string = "geeksforgeeks";
    check(string);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to accept String
// starting with Capital letter
using System;

class GFG
{

    // Function to check if first
    // character is Capital
    static int checkIfStartsWithCapital(string str)
    {

        if (str[0] >= 'A' && str[0]<= 'Z')
            return 1;
        else
            return 0;
    }

    // Function to check
    static void check(string str)
    {
        if (checkIfStartsWithCapital(str) == 1)
            Console.WriteLine("Accepted");
        else
            Console.WriteLine("Not Accepted");
    }

    // Driver function
    public static void Main()
    {
        string str = "GeeksforGeeks";
        check(str);

        str = "geeksforgeeks";
        check(str);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to accept String
// starting with Capital letter

// Function to check if first
// character is Capital
function checkIfStartsWithCapital(str)
{

    if (str[0] >= 'A' && str[0] <= 'Z')
        return 1;
    else
        return 0;
}

// Function to check
function check(str)
{
    if (checkIfStartsWithCapital(str))
        document.write( "Accepted<br>");
    else
        document.write( "Not Accepted<br>");
}

// Driver function

var str = "GeeksforGeeks";
check(str);
str= "geeksforgeeks";
check(str);

</script>
```

**Output:** 

```
Accepted
Not Accepted
```