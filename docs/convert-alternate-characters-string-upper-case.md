# 将字符串的字符转换为相反的大小写

> 原文:[https://www . geesforgeks . org/convert-alternate-characters-string-大写/](https://www.geeksforgeeks.org/convert-alternate-characters-string-upper-case/)

给定一个字符串，将该字符串的字符转换成相反的大小写，即如果一个字符是小写，那么将其转换成大写，反之亦然。

**示例:**

```
Input : geeksForgEeks
Output : GEEKSfORGeEKS

Input : hello every one
Output : HELLO EVERY ONE
```

字母表的 ASCII 值:A–Z = 65 到 90，A–Z = 97 到 122
**步数:**

1.  取一个任意长度的字符串，计算它的长度。
2.  逐字符扫描字符串，并不断检查索引。
    *   如果索引中的一个字符是小写，那么减去 32 转换成大写，否则加上 32 转换成小写
3.  打印最后一个字符串。

## C++

```
// CPP program to Convert characters
// of a string to opposite case
#include <iostream>
using namespace std;

// Function to convert characters
// of a string to opposite case
void convertOpposite(string& str)
{
    int ln = str.length();

    // Conversion according to ASCII values
    for (int i = 0; i < ln; i++) {
        if (str[i] >= 'a' && str[i] <= 'z')
            // Convert lowercase to uppercase
            str[i] = str[i] - 32;
        else if (str[i] >= 'A' && str[i] <= 'Z')
            // Convert uppercase to lowercase
            str[i] = str[i] + 32;
    }
}

// Driver function
int main()
{
    string str = "GeEkSfOrGeEkS";

    // Calling the Function
    convertOpposite(str);

    cout << str;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Convert characters
// of a string to opposite case
class Test {

    // Method to convert characters
    // of a string to opposite case
    static void convertOpposite(StringBuffer str)
    {
        int ln = str.length();

        // Conversion using predefined methods
        for (int i = 0; i < ln; i++) {
            Character c = str.charAt(i);
            if (Character.isLowerCase(c))
                str.replace(i, i + 1,
                            Character.toUpperCase(c) + "");
            else
                str.replace(i, i + 1,
                            Character.toLowerCase(c) + "");
        }
    }

    public static void main(String[] args)
    {
        StringBuffer str
            = new StringBuffer("GeEkSfOrGeEkS");
        // Calling the Method
        convertOpposite(str);

        System.out.println(str);
    }
}
// This code is contributed by Gaurav Miglani
```

## 蟒蛇 3

```
# Python3 program to Convert characters
# of a string to opposite case

# Function to convert characters
# of a string to opposite case
def convertOpposite(str):
    ln = len(str)

    # Conversion according to ASCII values
    for i in range(ln):
        if str[i] >= 'a' and str[i] <= 'z':

            # Convert lowercase to uppercase
            str[i] = chr(ord(str[i]) - 32)

        elif str[i] >= 'A' and str[i] <= 'Z':

            # Convert lowercase to uppercase
            str[i] = chr(ord(str[i]) + 32)

# Driver code
if __name__ == "__main__":
    str = "GeEkSfOrGeEkS"
    str = list(str)

    # Calling the Function
    convertOpposite(str)

    str = ''.join(str)
    print(str)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to Convert characters
// of a string to opposite case
using System;
using System.Text;

class GFG{

    // Method to convert characters
    // of a string to opposite case
    static void convertOpposite(StringBuilder str)
    {
        int ln = str.Length;

        // Conversion according to ASCII values
        for (int i=0; i<ln; i++)
        {
            if (str[i]>='a' && str[i]<='z')

                //Convert lowercase to uppercase
                str[i] = (char)(str[i] - 32);

            else if(str[i]>='A' && str[i]<='Z')

                //Convert uppercase to lowercase
                str[i] = (char)(str[i] + 32);
        }
    }

    // Driver code
    public static void Main()
    {
        StringBuilder str = new StringBuilder("GeEkSfOrGeEkS");
        // Calling the Method
        convertOpposite(str);
        Console.WriteLine(str);
        }
}
// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Function to convert characters
// of a string to opposite case
function convertOpposite(str)
{
    var ln = str.length;

    // Conversion according to ASCII values
    for (var i = 0; i < ln; i++)
    {
        if (str[i] >= 'a' && str[i] <= 'z')
            // Convert lowercase to uppercase
            document.write(
            String.fromCharCode(str.charCodeAt(i) - 32)
            );
        else if (str[i] >= 'A' && str[i] <= 'Z')
            // Convert uppercase to lowercase
            document.write(
            String.fromCharCode(str.charCodeAt(i) + 32)
            );
    }
}

// Driver function
var str = "GeEkSfOrGeEkS";

    // Calling the Function
    convertOpposite(str);

</script>
```

**Output**

```
gEeKsFoRgEeKs
```