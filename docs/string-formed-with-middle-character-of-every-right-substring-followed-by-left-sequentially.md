# 由每个右子串的中间字符依次跟在左后形成的字符串

> 原文:[https://www . geesforgeks . org/string-formed-with-in-character-of-right-substring-后跟-left-sequential/](https://www.geeksforgeeks.org/string-formed-with-middle-character-of-every-right-substring-followed-by-left-sequentially/)

给定一个长度为 **N** 的字符串 **str** ，任务是使用一组给定的解密规则对其进行解密，并打印解密后的字符串。
解密规则如下:

*   从字符串**字符串**的中间字符开始打印。
*   重复遍历右子字符串并打印它的中间字符。
*   对左边的子串也重复同样的过程。

**例:**

```
Input: N = 4, str = "abcd" 
Output: bcda
Explanation:
              abcd  ------ b
              / \
             a   cd ------ c
            /     \
           a       d ----- d
          /
         a --------------- a
Hence, the final string is "bcda".

Input: N = 6, str = "gyuitp"
Output: utpigy
Explanation:
            gyuitp ------- u
             / \
           gy  itp ------- t
          /    /\
         gy   i  p ------ p
         /   /
        gy  i ----------- i
        /
       gy --------------- g
       \
        y  -------------- y
Hence, the final string is "utpigy".
```

**进场:**
主要思路是用[递归](https://www.geeksforgeeks.org/recursion/)。继续将整个字符串分成左右两个子字符串，并打印每一个这样的子字符串的中间元素，直到字符串只剩下一个字符，无法进一步分割。
该方法的详细步骤如下:

*   初始化开始= 0，结束= N -1，表示字符串的第一个和最后一个字符。
*   打印字符串中间的字符，即 mid =(开始+结束)/ 2。
*   递归遍历它的右子串(开始=中间+1，结束)，然后遍历它的左子串(开始，中间–1)。
*   对遍历的每个子串重复上述步骤。继续，直到遍历整个字符串并打印给定的字符串。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <iostream>
using namespace std;

// Function to decrypt and
// print the new string
void decrypt(string Str,
             int Start, int End)
{
    // If the whole string
    // has been traversed
    if (Start > End) {
        return;
    }

    // To calculate middle
    // index of the string
    int mid = (Start + End) >> 1;

    // Print the character
    // at middle index
    cout << Str[mid];

    // Recursively call
    // for right-substring
    decrypt(Str, mid + 1, End);

    // Recursive call
    // for left-substring
    decrypt(Str, Start, mid - 1);
}

// Driver Code
int main()
{

    int N = 4;
    string Str = "abcd";
    decrypt(Str, 0, N - 1);
    cout << "\n";

    N = 6;
    Str = "gyuitp";
    decrypt(Str, 0, N - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG{

// Function to decrypt and
// print the new String
static void decrypt(String Str,
            int Start, int End)
{
    // If the whole String
    // has been traversed
    if (Start > End)
    {
        return;
    }

    // To calculate middle
    // index of the String
    int mid = (Start + End) >> 1;

    // Print the character
    // at middle index
    System.out.print(Str.charAt(mid));

    // Recursively call
    // for right-subString
    decrypt(Str, mid + 1, End);

    // Recursive call
    // for left-subString
    decrypt(Str, Start, mid - 1);
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;
    String Str = "abcd";
    decrypt(Str, 0, N - 1);
    System.out.print("\n");

    N = 6;
    Str = "gyuitp";
    decrypt(Str, 0, N - 1);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to decrypt and
# print the new string
def decrypt(Str, Start, End):

    # If the whole string
    # has been traversed
    if (Start > End):
        return;

    # To calculate middle
    # index of the string
    mid = (Start + End) >> 1;

    # Print the character
    # at middle index
    print(Str[mid], end = "");

    # Recursively call
    # for right-substring
    decrypt(Str, mid + 1, End);

    # Recursive call
    # for left-substring
    decrypt(Str, Start, mid - 1);

# Driver Code
N = 4;
Str = "abcd";
decrypt(Str, 0, N - 1);
print();

N = 6;
Str = "gyuitp";
decrypt(Str, 0, N - 1);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to decrypt and
// print the new String
static void decrypt(String Str,
            int Start, int End)
{
    // If the whole String
    // has been traversed
    if (Start > End)
    {
        return;
    }

    // To calculate middle
    // index of the String
    int mid = (Start + End) >> 1;

    // Print the character
    // at middle index
    Console.Write(Str[mid]);

    // Recursively call
    // for right-subString
    decrypt(Str, mid + 1, End);

    // Recursive call
    // for left-subString
    decrypt(Str, Start, mid - 1);
}

// Driver Code
public static void Main()
{
    int N = 4;
    String Str = "abcd";
    decrypt(Str, 0, N - 1);
    Console.Write("\n");

    N = 6;
    Str = "gyuitp";
    decrypt(Str, 0, N - 1);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to decrypt and
// print the new String
function decrypt(Str, Start, End)
{

    // If the whole String
    // has been traversed
    if (Start > End)
    {
        return;
    }

    // To calculate middle
    // index of the String
    let mid = (Start + End) >> 1;

    // Print the character
    // at middle index
    document.write(Str[mid]);

    // Recursively call
    // for right-subString
    decrypt(Str, mid + 1, End);

    // Recursive call
    // for left-subString
    decrypt(Str, Start, mid - 1);
}

// Driver Code
    let N = 4;
    let Str = "abcd";
    decrypt(Str, 0, N - 1);
    document.write("<br/>");

    N = 6;
    Str = "gyuitp";
    decrypt(Str, 0, N - 1);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
bcda
utpigy
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*