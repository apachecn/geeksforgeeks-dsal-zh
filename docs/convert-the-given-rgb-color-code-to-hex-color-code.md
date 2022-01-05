# 将给定的 RGB 色码转换为十六进制色码

> 原文:[https://www . geesforgeks . org/convert-the-given-RGB-color-code-to-hex-color-code/](https://www.geeksforgeeks.org/convert-the-given-rgb-color-code-to-hex-color-code/)

给定三种颜色，如 **R** 、 **G** 、 **B** ，将这些 [RGB 颜色](https://www.geeksforgeeks.org/computer-graphics-the-rgb-color-model/)转换为**十六进制色码**。如果无法转换，请打印-1。

**示例:**

> **输入:** R = 0，G = 0，B = 0
> T3】输出: #000000
> 
> **输入:** R = 255，G = 255，B = 256
> **输出:** -1
> **解释:**
> A 256 色码是不可能的，因为一种颜色只有 0-255 范围可用。

**进场:**

1.  首先，检查每个给定的颜色是否在 0-255 的范围内。
2.  如果没有，则打印-1 并退出程序，因为在这种情况下无法进行转换。
3.  如果它们在范围内，那么对于每种颜色，[将给定的颜色代码转换为其等效的十六进制数](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)。
4.  如果十六进制值是 1 位数，则在左边加上 0 使其成为 2 位数。
5.  然后，在最终答案中，在开头加上“#”，后面分别加上 R、G 和 B 的十六进制值。

下面是上述方法的实现。

## C++

```
// C++ code to convert the given RGB
// color code to Hex color code

#include <iostream>
using namespace std;

// function to convert decimal to hexadecimal
string decToHexa(int n)
{
    // char array to store hexadecimal number
    char hexaDeciNum[2];

    // counter for hexadecimal number array
    int i = 0;
    while (n != 0) {

        // temporary variable to store remainder
        int temp = 0;

        // storing remainder in temp variable.
        temp = n % 16;

        // check if temp < 10
        if (temp < 10) {
            hexaDeciNum[i] = temp + 48;
            i++;
        }
        else {
            hexaDeciNum[i] = temp + 55;
            i++;
        }

        n = n / 16;
    }

    string hexCode = "";
    if (i == 2) {
        hexCode.push_back(hexaDeciNum[0]);
        hexCode.push_back(hexaDeciNum[1]);
    }
    else if (i == 1) {
        hexCode = "0";
        hexCode.push_back(hexaDeciNum[0]);
    }
    else if (i == 0)
        hexCode = "00";

    // Return the equivalent
    // hexadecimal color code
    return hexCode;
}

// Function to convert the
// RGB code to Hex color code
string convertRGBtoHex(int R, int G, int B)
{
    if ((R >= 0 && R <= 255)
        && (G >= 0 && G <= 255)
        && (B >= 0 && B <= 255)) {

        string hexCode = "#";
        hexCode += decToHexa(R);
        hexCode += decToHexa(G);
        hexCode += decToHexa(B);

        return hexCode;
    }

    // The hex color code doesn't exist
    else
        return "-1";
}

// Driver program to test above function
int main()
{
    int R = 0, G = 0, B = 0;
    cout << convertRGBtoHex(R, G, B) << endl;

    R = 255, G = 255, B = 255;
    cout << convertRGBtoHex(R, G, B) << endl;

    R = 25, G = 56, B = 123;
    cout << convertRGBtoHex(R, G, B) << endl;

    R = 2, G = 3, B = 4;
    cout << convertRGBtoHex(R, G, B) << endl;

    R = 255, G = 255, B = 256;
    cout << convertRGBtoHex(R, G, B) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert the given RGB
// color code to Hex color code

import java.util.*;

class GFG{

// function to convert decimal to hexadecimal
static String decToHexa(int n)
{
    // char array to store hexadecimal number
    char []hexaDeciNum = new char[2];

    // counter for hexadecimal number array
    int i = 0;
    while (n != 0) {

        // temporary variable to store remainder
        int temp = 0;

        // storing remainder in temp variable.
        temp = n % 16;

        // check if temp < 10
        if (temp < 10) {
            hexaDeciNum[i] = (char) (temp + 48);
            i++;
        }
        else {
            hexaDeciNum[i] = (char) (temp + 55);
            i++;
        }

        n = n / 16;
    }

    String hexCode = "";
    if (i == 2) {
        hexCode+=hexaDeciNum[0];
        hexCode+=hexaDeciNum[1];
    }
    else if (i == 1) {
        hexCode = "0";
        hexCode+=hexaDeciNum[0];
    }
    else if (i == 0)
        hexCode = "00";

    // Return the equivalent
    // hexadecimal color code
    return hexCode;
}

// Function to convert the
// RGB code to Hex color code
static String convertRGBtoHex(int R, int G, int B)
{
    if ((R >= 0 && R <= 255)
        && (G >= 0 && G <= 255)
        && (B >= 0 && B <= 255)) {

        String hexCode = "#";
        hexCode += decToHexa(R);
        hexCode += decToHexa(G);
        hexCode += decToHexa(B);

        return hexCode;
    }

    // The hex color code doesn't exist
    else
        return "-1";
}

// Driver program to test above function
public static void main(String[] args)
{
    int R = 0, G = 0, B = 0;
    System.out.print(convertRGBtoHex(R, G, B) +"\n");

    R = 255; G = 255; B = 255;
    System.out.print(convertRGBtoHex(R, G, B) +"\n");

    R = 25; G = 56; B = 123;
    System.out.print(convertRGBtoHex(R, G, B) +"\n");

    R = 2; G = 3; B = 4;
    System.out.print(convertRGBtoHex(R, G, B) +"\n");

    R = 255; G = 255; B = 256;
    System.out.print(convertRGBtoHex(R, G, B) +"\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to convert the given
# RGB color code to Hex color code

# Function to convert decimal to hexadecimal
def decToHexa(n):

    # char array to store hexadecimal number
    hexaDeciNum = ['0'] * 100

    # Counter for hexadecimal number array
    i = 0

    while (n != 0):

        # Temporary variable to store remainder
        temp = 0

        # Storing remainder in temp variable.
        temp = n % 16

        # Check if temp < 10
        if (temp < 10):
            hexaDeciNum[i] = chr(temp + 48)
            i = i + 1

        else:
            hexaDeciNum[i] = chr(temp + 55)
            i = i + 1

        n = int(n / 16)

    hexCode = ""
    if (i == 2):
        hexCode = hexCode + hexaDeciNum[0]
        hexCode = hexCode + hexaDeciNum[1]

    elif (i == 1):
        hexCode = "0"
        hexCode = hexCode + hexaDeciNum[0]

    elif (i == 0):
        hexCode = "00"

    # Return the equivalent
    # hexadecimal color code
    return hexCode

# Function to convert the
# RGB code to Hex color code
def convertRGBtoHex(R, G, B):

    if ((R >= 0 and R <= 255) and
        (G >= 0 and G <= 255) and
        (B >= 0 and B <= 255)):

        hexCode = "#";
        hexCode = hexCode + decToHexa(R)
        hexCode = hexCode + decToHexa(G)
        hexCode = hexCode + decToHexa(B)
        return hexCode

    # The hex color code doesn't exist
    else:
        return "-1"

# Driver Code
R = 0
G = 0
B = 0
print (convertRGBtoHex(R, G, B))

R = 255
G = 255
B = 255
print (convertRGBtoHex(R, G, B))

R = 25
G = 56
B = 123
print (convertRGBtoHex(R, G, B))

R = 2
G = 3
B = 4
print (convertRGBtoHex(R, G, B))

R = 255
G = 255
B = 256
print (convertRGBtoHex(R, G, B))

# This code is contributed by Pratik Basu
```

## C#

```
// C# code to convert the given RGB
// color code to Hex color code
using System;

class GFG{

// Function to convert decimal
// to hexadecimal
static string decToHexa(int n)
{

    // char array to store
    // hexadecimal number
    char []hexaDeciNum = new char[2];

    // Counter for hexadecimal
    // number array
    int i = 0;
    while (n != 0)
    {

        // Temporary variable to
        // store remainder
        int temp = 0;

        // Storing remainder in
        // temp variable.
        temp = n % 16;

        // Check if temp < 10
        if (temp < 10)
        {
            hexaDeciNum[i] = (char) (temp + 48);
            i++;
        }
        else
        {
            hexaDeciNum[i] = (char) (temp + 55);
            i++;
        }
        n = n / 16;
    }
    string hexCode = "";

    if (i == 2)
    {
        hexCode += hexaDeciNum[0];
        hexCode += hexaDeciNum[1];
    }
    else if (i == 1)
    {
        hexCode = "0";
        hexCode += hexaDeciNum[0];
    }
    else if (i == 0)
        hexCode = "00";

    // Return the equivalent
    // hexadecimal color code
    return hexCode;
}

// Function to convert the
// RGB code to Hex color code
static string convertRGBtoHex(int R, int G,
                                     int B)
{
    if ((R >= 0 && R <= 255) &&
        (G >= 0 && G <= 255) &&
        (B >= 0 && B <= 255))
    {
        string hexCode = "#";
        hexCode += decToHexa(R);
        hexCode += decToHexa(G);
        hexCode += decToHexa(B);

        return hexCode;
    }

    // The hex color code doesn't exist
    else
        return "-1";
}

// Driver code
public static void Main(string[] args)
{
    int R = 0, G = 0, B = 0;
    Console.Write(convertRGBtoHex(R, G, B) + "\n");

    R = 255; G = 255; B = 255;
    Console.Write(convertRGBtoHex(R, G, B) + "\n");

    R = 25; G = 56; B = 123;
    Console.Write(convertRGBtoHex(R, G, B) + "\n");

    R = 2; G = 3; B = 4;
    Console.Write(convertRGBtoHex(R, G, B) + "\n");

    R = 255; G = 255; B = 256;
    Console.Write(convertRGBtoHex(R, G, B) + "\n");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript code to convert the given RGB
// color code to Hex color code

// function to convert decimal to hexadecimal
function decToHexa(n)
{
    // char array to store hexadecimal number
    let hexaDeciNum = Array.from({length: 2}, (_, i) => 0);

    // counter for hexadecimal number array
    let i = 0;
    while (n != 0) {

        // temporary variable to store remainder
        let temp = 0;

        // storing remainder in temp variable.
        temp = n % 16;

        // check if temp < 10
        if (temp < 10) {
            hexaDeciNum[i] = String.fromCharCode(temp + 48);
            i++;
        }
        else {
            hexaDeciNum[i] =  String.fromCharCode(temp + 55);
            i++;
        }

        n = Math.floor(n / 16);
    }

    let hexCode = "";
    if (i == 2) {
        hexCode+=hexaDeciNum[0];
        hexCode+=hexaDeciNum[1];
    }
    else if (i == 1) {
        hexCode = "0";
        hexCode+=hexaDeciNum[0];
    }
    else if (i == 0)
        hexCode = "00";

    // Return the equivalent
    // hexadecimal color code
    return hexCode;
}

// Function to convert the
// RGB code to Hex color code
function convertRGBtoHex(R, G, B)
{
    if ((R >= 0 && R <= 255)
        && (G >= 0 && G <= 255)
        && (B >= 0 && B <= 255)) {

        let hexCode = "#";
        hexCode += decToHexa(R);
        hexCode += decToHexa(G);
        hexCode += decToHexa(B);

        return hexCode;
    }

    // The hex color code doesn't exist
    else
        return "-1";
}

// Driver Code

    let R = 0, G = 0, B = 0;
    document.write(convertRGBtoHex(R, G, B) +"<br/>");

    R = 255; G = 255; B = 255;
    document.write(convertRGBtoHex(R, G, B) +"<br/>");

    R = 25; G = 56; B = 123;
    document.write(convertRGBtoHex(R, G, B) +"<br/>");

    R = 2; G = 3; B = 4;
    document.write(convertRGBtoHex(R, G, B) +"<br/>");

    R = 255; G = 255; B = 256;
    document.write(convertRGBtoHex(R, G, B) +"<br/>");

</script>
```

**Output:** 

```
#000000
#FFFFFF
#9183B7
#020304
-1
```

时间复杂度:O(对数 <sub>16</sub> N)

辅助空间:0(1)