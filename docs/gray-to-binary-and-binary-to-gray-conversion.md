# 灰度到二进制和二进制到灰度的转换

> 原文:[https://www . geesforgeks . org/灰度到二进制和二进制到灰度的转换/](https://www.geeksforgeeks.org/gray-to-binary-and-binary-to-gray-conversion/)

二进制数是存储数字的默认方式，但在许多应用中，二进制数很难使用，需要二进制数的变体。这就是格雷码非常有用的地方。

格雷码的特性是**两个连续的数字仅在一位**上不同，因为这个特性，格雷码以最小的努力在各种状态之间循环，并用于 K 图、纠错、通信等。

**如何生成 n 位格雷码？**

```
Following is 2-bit sequence (n = 2)
  00 01 11 10
Following is 3-bit sequence (n = 3)
  000 001 011 010 110 111 101 100
And Following is 4-bit sequence (n = 4)
  0000 0001 0011 0010 0110 0111 0101 0100 1100 1101 1111 
  1110 1010 1011 1001 1000
```

可以使用以下步骤从(n-1)位格雷码列表中生成 n 位格雷码。

1.  让(n-1)位格雷码的列表是 L1。创建另一个与 L1 相反的 L2 名单。
2.  通过在 L1 的所有代码中加前缀“0”来修改 L1 列表。
3.  通过在 L2 的所有代码中加前缀“1”来修改 L2 列表。
4.  连接 L1 和 L2。级联列表是 n 位格雷码的必需列表。

详细程序请参考生成 [n 位格雷码](https://www.geeksforgeeks.org/given-a-number-n-generate-bit-patterns-from-0-to-2n-1-so-that-successive-patterns-differ-by-one-bit/)。

**如何将二进制转换为灰色，反之亦然？**

```
Binary : 0011
Gray   : 0010

Binary : 01001
Gray   : 01101
```

在计算机科学中，很多时候我们需要将二进制代码转换成格雷码，反之亦然。这种转换可以通过应用以下规则来完成:

***二进制到灰度的转换:***

1.  格雷码的最高有效位总是等于给定二进制码的最高有效位。
2.  输出格雷码的其他位可以通过在该索引和先前索引处异或二进制码位来获得。

***灰度到二进制的转换:***

1.  二进制码的最高有效位总是等于给定格雷码的最高有效位。
2.  输出二进制码的其他位可以通过检查该索引处的格雷码位来获得。如果当前格雷码位为 0，则复制前一个二进制码位，否则复制前一个二进制码位的反转。

下面是以上步骤的实现。

## C++

```
// C++ program for Binary To Gray
// and Gray to Binary conversion
#include <iostream>
using namespace std;

// Helper function to xor two characters
char xor_c(char a, char b) { return (a == b) ? '0' : '1'; }

// Helper function to flip the bit
char flip(char c) { return (c == '0') ? '1' : '0'; }

// function to convert binary string
// to gray string
string binarytoGray(string binary)
{
    string gray = "";

    // MSB of gray code is same as binary code
    gray += binary[0];

    // Compute remaining bits, next bit is computed by
    // doing XOR of previous and current in Binary
    for (int i = 1; i < binary.length(); i++) {
        // Concatenate XOR of previous bit
        // with current bit
        gray += xor_c(binary[i - 1], binary[i]);
    }

    return gray;
}

// function to convert gray code string
// to binary string
string graytoBinary(string gray)
{
    string binary = "";

    // MSB of binary code is same as gray code
    binary += gray[0];

    // Compute remaining bits
    for (int i = 1; i < gray.length(); i++) {
        // If current bit is 0, concatenate
        // previous bit
        if (gray[i] == '0')
            binary += binary[i - 1];

        // Else, concatenate invert of
        // previous bit
        else
            binary += flip(binary[i - 1]);
    }

    return binary;
}

// Driver program to test above functions
int main()
{
    string binary = "01001";
    cout << "Gray code of " << binary << " is "
         << binarytoGray(binary) << endl;

    string gray = "01101";
    cout << "Binary code of " << gray << " is "
         << graytoBinary(gray) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Binary To Gray
// and Gray to Binary conversion
import java.io.*;
class code_conversion
{

    // Helper function to xor
    // two characters
    char xor_c(char a, char b)
    {
        return (a == b) ? '0' : '1';
    }

    // Helper function to flip the bit
    char flip(char c)
    {
        return (c == '0') ? '1' : '0';
    }

    // function to convert binary
  // string to gray string
    String binarytoGray(String binary)
    {
        String gray = "";

        // MSB of gray code is same
        // as binary code
        gray += binary.charAt(0);

        // Compute remaining bits, next bit is
        // computed by doing XOR of previous
        // and current in Binary
        for (int i = 1; i < binary.length(); i++)
        {

            // Concatenate XOR of previous bit
            // with current bit
            gray += xor_c(binary.charAt(i - 1),
                          binary.charAt(i));
        }
       return gray;
    }

    // function to convert gray code
    // string to binary string
    String graytoBinary(String gray)
    {
        String binary = "";

        // MSB of binary code is same
        // as gray code
        binary += gray.charAt(0);

        // Compute remaining bits
        for (int i = 1; i < gray.length(); i++)
        {

            // If current bit is 0,
            // concatenate previous bit
            if (gray.charAt(i) == '0')
                binary += binary.charAt(i - 1);

          // Else, concatenate invert of
            // previous bit
            else
                binary += flip(binary.charAt(i - 1));
        }

        return binary;
    }

    // Driver program to test above functions
    public static void main(String args[])
        throws IOException
    {
        code_conversion ob = new code_conversion();
        String binary = "01001";
        System.out.println("Gray code of " +
                           binary + " is " +
                           ob.binarytoGray(binary));

        String gray = "01101";
        System.out.println("Binary code of " +
                           gray + " is " +
                           ob.graytoBinary(gray));
    }
  }

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Python3 program for Binary To Gray
# and Gray to Binary conversion

# Helper function to xor two characters
def xor_c(a, b):
    return '0' if(a == b) else '1';

# Helper function to flip the bit
def flip(c):
    return '1' if(c == '0') else '0';

# function to convert binary string
# to gray string
def binarytoGray(binary):
    gray = "";

    # MSB of gray code is same as
    # binary code
    gray += binary[0];

    # Compute remaining bits, next bit
    # is computed by doing XOR of previous
    # and current in Binary
    for i in range(1, len(binary)):

        # Concatenate XOR of previous
        # bit with current bit
        gray += xor_c(binary[i - 1],
                      binary[i]);

    return gray;

# function to convert gray code
# string to binary string
def graytoBinary(gray):

    binary = "";

    # MSB of binary code is same
    # as gray code
    binary += gray[0];

    # Compute remaining bits
    for i in range(1, len(gray)):

        # If current bit is 0,
        # concatenate previous bit
        if (gray[i] == '0'):
            binary += binary[i - 1];

        # Else, concatenate invert
        # of previous bit
        else:
            binary += flip(binary[i - 1]);

    return binary;

# Driver Code
binary = "01001";
print("Gray code of", binary, "is",
             binarytoGray(binary));

gray = "01101";
print("Binary code of", gray, "is",
               graytoBinary(gray));

# This code is contributed by mits
```

## C#

```
// C# program for Binary To Gray
// and Gray to Binary conversion.
using System;

class GFG {

    // Helper function to xor
    // two characters
    static char xor_c(char a, char b)
    {
        return (a == b) ? '0' : '1';
    }

    // Helper function to flip the bit
    static char flip(char c)
    {
        return (c == '0') ? '1' : '0';
    }

    // function to convert binary
    // string to gray string
    static String binarytoGray(String binary)
    {
        String gray = "";

        // MSB of gray code is same
        // as binary code
        gray += binary[0];

        // Compute remaining bits, next
        // bit is computed by doing XOR
        // of previous and current in
        // Binary
        for (int i = 1; i < binary.Length; i++) {

            // Concatenate XOR of previous
            // bit with current bit
            gray += xor_c(binary[i - 1],
                          binary[i]);
        }

        return gray;
    }

    // function to convert gray code
    // string to binary string
    static String graytoBinary(String gray)
    {

        String binary = "";

        // MSB of binary code is same
        // as gray code
        binary += gray[0];

        // Compute remaining bits
        for (int i = 1; i < gray.Length; i++) {

            // If current bit is 0,
            // concatenate previous bit
            if (gray[i] == '0')
                binary += binary[i - 1];

            // Else, concatenate invert of
            // previous bit
            else
                binary += flip(binary[i - 1]);
        }

        return binary;
    }

    // Driver program to test above
    // functions
    public static void Main()

    {
        String binary = "01001";
        Console.WriteLine("Gray code of "
                          + binary + " is "
                          + binarytoGray(binary));

        String gray = "01101";
        Console.Write("Binary code of "
                      + gray + " is "
                      + graytoBinary(gray));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Binary To Gray
// and Gray to Binary conversion

// Helper function to xor two characters
function xor_c($a, $b)
{
    return ($a == $b) ? '0' : '1';
}

// Helper function to flip the bit
function flip($c)
{
    return ($c == '0') ? '1' : '0';
}

// function to convert binary string
// to gray string
function binarytoGray($binary)
{
    $gray = "";

    // MSB of gray code is same as
    // binary code
    $gray .= $binary[0];

    // Compute remaining bits, next bit is
    // computed by doing XOR of previous
    // and current in Binary
    for ($i = 1; $i < strlen($binary); $i++)
    {
        // Concatenate XOR of previous bit
        // with current bit
        $gray .= xor_c($binary[$i - 1], $binary[$i]);
    }

    return $gray;
}

// function to convert gray code string
// to binary string
function graytoBinary($gray)
{
    $binary = "";

    // MSB of binary code is same as gray code
    $binary .= $gray[0];

    // Compute remaining bits
    for ($i = 1; $i < strlen($gray); $i++)
    {
        // If current bit is 0, concatenate
        // previous bit
        if ($gray[$i] == '0')
            $binary .= $binary[$i - 1];

        // Else, concatenate invert of
        // previous bit
        else
            $binary .= flip($binary[$i - 1]);
    }

    return $binary;
}

// Driver Code
$binary = "01001";
print("Gray code of " . $binary . " is " .
            binarytoGray($binary) . "\n");

$gray = "01101";
print("Binary code of " . $gray . " is " .
                     graytoBinary($gray));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>  

// Javascript program for Binary To Gray
// and Gray to Binary conversion

// Helper function to xor two characters
function xor_c(a, b){ return (a == b) ? '0' : '1'; }

// Helper function to flip the bit
function flip(c){ return (c == '0') ? '1' : '0'; }

// Function to convert binary string
// to gray string
function binarytoGray(binary)
{
    let gray = "";

    // MSB of gray code is same
    // as binary code
    gray += binary[0];

    // Compute remaining bits, next bit
    // is computed by doing XOR of previous
    // and current in Binary
    for(let i = 1; i < binary.length; i++)
    {

        // Concatenate XOR of previous bit
        // with current bit
        gray += xor_c(binary[i - 1], binary[i]);
    }
    return gray;
}

// Function to convert gray code string
// to binary string
function graytoBinary(gray)
{
    let binary = "";

    // MSB of binary code is same
    // as gray code
    binary += gray[0];

    // Compute remaining bits
    for(let i = 1; i < gray.length; i++)
    {

        // If current bit is 0, concatenate
        // previous bit
        if (gray[i] == '0')
            binary += binary[i - 1];

        // Else, concatenate invert of
        // previous bit
        else
            binary += flip(binary[i - 1]);
    }
    return binary;
}

// Driver code
let binary = "01001";
document.write("Gray code of " + binary + " is " +
               binarytoGray(binary) + "</br>");

let gray = "01101";
document.write("Binary code of " + gray + " is " +
               graytoBinary(gray));

// This code is contributed by vaibhavrabadiya3

</script>
```

**Output**

```
Gray code of 01001 is 01101
Binary code of 01101 is 01001
```

**使用按位运算符将二进制转换为灰色**

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

int greyConverter(int n) { return n ^ (n >> 1); }

int main()
{
    int n = 3;
    cout << greyConverter(n) << endl;

    n = 9;
    cout << greyConverter(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
public class Main {
    public static int greyConverter(int n)
    {
        return n ^ (n >> 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        System.out.println(greyConverter(n));

        n = 9;
        System.out.println(greyConverter(n));
    }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 code for above approach
def greyConverter(n):

    return n ^ (n >> 1)

n = 3
print(greyConverter(n))

n = 9
print(greyConverter(n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for above approach
using System;

class GFG {

    static int greyConverter(int n) { return n ^ (n >> 1); }

    // Driver Code
    public static void Main(string[] args)
    {
        int n = 3;
        Console.WriteLine(greyConverter(n));

        n = 9;
        Console.WriteLine(greyConverter(n));
    }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for above approach
function greyConverter(n)
{
    return n ^ (n >> 1);
}

// Driver code
let n = 3;
document.write(greyConverter(n) + "</br>");

n = 9;
document.write(greyConverter(n));

// This code is contributed by suresh07

</script>
```

**Output**

```
2
13
```

**使用按位运算符将灰度转换为二进制**

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

int binaryConverter(int n)
{
    int res = n;
    while (n > 0)
    {
        n >>= 1;
        res ^= n;
    }
    return res;
}

// Driver Code
int main()
{
    int n = 4;

    // Function call
    cout << binaryConverter(n) << endl;

    return 0;
}

// This code is contributed by sshrey47
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
public class Main {
    public static int binaryConverter(int n)
    {
        int res = n;

        while (n > 0) {
            n >>= 1;
            res ^= n;
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        System.out.println(binaryConverter(n));
    }
}

// This code is contributed by sshrey47
```

## 蟒蛇 3

```
# Python3 code for above approach
def binaryConverter(n):
    res = n

    while n > 0:
        n >>= 1
        res ^= n

    return res

n = 4
print(binaryConverter(n))

# This code is contributed by sshrey47
```

## C#

```
using System;

public class GFG {

    static int binaryConverter(int n)
    {
        int res = n;

        while (n > 0) {
            n >>= 1;
            res ^= n;
        }

        return res;
    }

    static public void Main()
    {
        int n = 4;
        Console.WriteLine(binaryConverter(n));
    }
}

// This code is contributed by sshrey47
```

## java 描述语言

```
<script>
    // Javascript program for above approach

    function binaryConverter(n)
    {
           let res = n;
        while (n > 0)
        {
            n >>= 1;
            res ^= n;
        }
        return res;
    }

    let n = 4;

    // Function call
    document.write(binaryConverter(n));

    // This code is contributed by mukesh07.
</script>
```

**Output**

```
7
```

本文由乌卡什·特里维迪供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息