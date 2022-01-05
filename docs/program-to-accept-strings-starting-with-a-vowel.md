# 接受以元音开头的字符串的程序

> 原文:[https://www . geesforgeks . org/program-to-accept-strings-以元音开头/](https://www.geeksforgeeks.org/program-to-accept-strings-starting-with-a-vowel/)

给定字符串**字符串**由字母组成，任务是检查给定字符串是否以元音开头。

**示例:**

```
Input: str = "Animal"
Output: Accepted

Input: str = "GeeksforGeeks"
Output: Not Accepted 
```

**进场:**

*   查找字符串的第一个字符
*   检查字符串的第一个字符是否是元音
*   如果是，打印接受
*   否则打印不接受

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to accept String
// starting with Vowel

#include <iostream>
using namespace std;

// Function to check if first character is vowel
int checkIfStartsWithVowels(string str)
{

    if (!(str[0] == 'A' || str[0] == 'a'
          || str[0] == 'E' || str[0] == 'e'
          || str[0] == 'I' || str[0] == 'i'
          || str[0] == 'O' || str[0] == 'o'
          || str[0] == 'U' || str[0] == 'u'))
        return 1;
    else
        return 0;
}

// Function to check
void check(string str)
{
    if (checkIfStartsWithVowels(str))
        cout << "Not Accepted\n";
    else
        cout << "Accepted\n";
}

// Driver function
int main()
{
    string str = "animal";
    check(str);

    str = "zebra";
    check(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to accept String
// starting with Vowel
class GFG
{

// Function to check if first character is vowel
static int checkIfStartsWithVowels(char []str)
{

    if (!(str[0] == 'A' || str[0] == 'a'
        || str[0] == 'E' || str[0] == 'e'
        || str[0] == 'I' || str[0] == 'i'
        || str[0] == 'O' || str[0] == 'o'
        || str[0] == 'U' || str[0] == 'u'))
        return 1;
    else
        return 0;
}

// Function to check
static void check(String str)
{
    if (checkIfStartsWithVowels(str.toCharArray()) == 1)
        System.out.print("Not Accepted\n");
    else
        System.out.print("Accepted\n");
}

// Driver code
public static void main(String[] args)
{
    String str = "animal";
    check(str);

    str = "zebra";
    check(str);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to accept String
# starting with Vowel

# Function to check if first character is vowel
def checkIfStartsWithVowels(string) :

    if (not(string[0] == 'A' or string[0] == 'a'
        or string[0] == 'E' or string[0] == 'e'
        or string[0] == 'I' or string[0] == 'i'
        or string[0] == 'O' or string[0] == 'o'
        or string[0] == 'U' or string[0] == 'u')) :
        return 1;
    else :
        return 0;

# Function to check
def check(string) :

    if (checkIfStartsWithVowels(string)) :
        print("Not Accepted");
    else :
        print("Accepted");

# Driver function
if __name__ == "__main__" :

    string = "animal";
    check(string);

    string = "zebra";
    check(string);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to accept String
// starting with Vowel
using System;

class GFG
{

// Function to check if first character is vowel
static int checkIfStartsWithVowels(char []str)
{

    if (!(str[0] == 'A' || str[0] == 'a'
        || str[0] == 'E' || str[0] == 'e'
        || str[0] == 'I' || str[0] == 'i'
        || str[0] == 'O' || str[0] == 'o'
        || str[0] == 'U' || str[0] == 'u'))
        return 1;
    else
        return 0;
}

// Function to check
static void check(String str)
{
    if (checkIfStartsWithVowels(str.ToCharArray()) == 1)
        Console.Write("Not Accepted\n");
    else
        Console.Write("Accepted\n");
}

// Driver code
public static void Main(String[] args)
{
    String str = "animal";
    check(str);

    str = "zebra";
    check(str);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to accept String
// starting with Vowel

// Function to check if first character is vowel
function checkIfStartsWithVowels(str)
{

    if (!(str[0] == 'A' || str[0] == 'a'
          || str[0] == 'E' || str[0] == 'e'
          || str[0] == 'I' || str[0] == 'i'
          || str[0] == 'O' || str[0] == 'o'
          || str[0] == 'U' || str[0] == 'u'))
        return 1;
    else
        return 0;
}

// Function to check
function check(str)
{
    if (checkIfStartsWithVowels(str))
        document.write( "Not Accepted<br>");
    else
        document.write("Accepted<br>");
}

var str = "animal";
check(str);

str = "zebra";
check(str);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
Accepted
Not Accepted
```