# 超 ASCII 字串检查器| TCS 码寿命

> 哎哎哎:# t0]https://www . geeksforgeeks . org/super ascii 字符串检查器-tcs 代码生命/

在字节兰国家，当且仅当字符串中每个字符的计数等于其 ASCII 值时，字符串 **S** 被称为超级 ASCII 字符串。在**的字节国家 ASCII 码中，“a”是 1，“b”是 2，…，“z”是 26** 。任务是找出给定的字符串是否是超级 ASCII 字符串。如果是，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:**S = " BBA "
> T3】输出:是
> **说明:**
> 字符‘b’的计数为 2，‘b’的 ASCII 值也为 2。
> 字符“a”的计数为 1。“a”的 ASCII 值也是 1。
> 因此，字符串“bba”是超级 ASCII 字符串。
> 
> **输入:** S = "ssba"
> **输出:**否
> **说明:**
> 字符的计数为 2，【S】的 ASCII 值为 19。
> 字符“b”的计数为 1。“b”的 ASCII 值是 2。
> 因此，字符串“ssba”不是超级 ASCII 字符串。

**方法:**字节区域中字符“ **ch** 的 ASCII 值可以通过以下公式计算:

> ch 的 ASCII 值= ch 的整数等价物–a '(97)+1 的整数等价物

现在，使用这个公式，字符串中每个字符的频率计数可以与其 ASCII 值进行比较。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)来存储字符串每个字符的[频率计数。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** ，将每个字符的频率计数增加 **1** 。
*   再次，遍历字符串 **S** 并检查是否有任何字符具有非零频率并且不等于其 ASCII 值，然后打印**“否”**。
*   完成上述步骤后，如果上述步骤中没有这样的字符，则打印**“是”**。

下面是上述方法的实现:

## 蟒蛇 3

```
import string #for accessing alphabets

dicti = {}
a = []

#creating a list with the alphabets
for i in string.ascii_lowercase:
    a.append(i)

#creating a dictionary for the alphabets and correpondind ascii code
for i in string.ascii_lowercase:
    for j in range (1,27):
        if (a.index(i)+1) == j: #if the number is equal to the position of the alphabet
            dicti[i] = j        #in the list, then the number will be ascii code for the
            break               #aplhabet in the dictionary

s = 'bba'
t = True #t is initialized as true

for i in s:
    if s.count(i) != dicti[i]: #if any of the alphabet count is not equal to its
        t = False              #corresponding ascii code in the dictionary, t will be false

if t:
    print("Yes")            #printing yes if t remains true after checking all alphabets
else:
    print("No")

#code written by jayaselva
```

## C

```
// C program for the above approach
#include <stdio.h>
#include <string.h>

// Function to check whether the
// string is super ASCII or not
void checkSuperASCII(char s[])
{
    // Stores the frequency count
    // of characters 'a' to 'z'
    int b[26] = { 0 };

    // Traverse the string
    for (int i = 0; i < strlen(s); i++) {

        // AscASCIIii value of the
        // current character
        int index = (int)s[i] - 97 + 1;

        // Count frequency of each
        // character in the string
        b[index - 1]++;
    }

    // Traverse the string
    for (int i = 0; i < strlen(s); i++) {

        // ASCII value of the current
        // character
        int index = (int)s[i] - 97 + 1;

        // Check if the frequency of
        // each character in string
        // is same as ASCII code or not
        if (b[index - 1] != index) {
            printf("No");
            return;
        }
    }

    // Else print "Yes"
    printf("Yes");
}

// Driver Code
int main()
{
    // Given string S
    char s[] = "bba";

    // Function Call
    checkSuperASCII(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check whether the
// string is super ASCII or not
public static void checkSuperASCII(String s)
{

    // Stores the frequency count
    // of characters 'a' to 'z'
    int b[] = new int[26];

    // Traverse the string
    for(int i = 0; i < s.length(); i++)
    {

        // AscASCIIii value of the
        // current character
        int index = (int)s.charAt(i) - 97 + 1;

        // Count frequency of each
        // character in the string
        b[index - 1]++;
    }

    // Traverse the string
    for(int i = 0; i < s.length(); i++)
    {

        // ASCII value of the current
        // character
        int index = (int)s.charAt(i) - 97 + 1;

        // Check if the frequency of
        // each character in string
        // is same as ASCII code or not
        if (b[index - 1] != index)
        {
            System.out.println("No");
            return;
        }
    }

    // Else print "Yes"
    System.out.println("Yes");
}

// Driver Code
public static void main(String args[])
{

    // Given string S
    String s = "bba";

    // Function Call
    checkSuperASCII(s);
}
}

// This code is contributed by Md Shahbaz Alam
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether the
# string is super ASCII or not
def checkSuperASCII(s):

    # Stores the frequency count
    # of characters 'a' to 'z'
    b = [0 for i in range(26)]

    # Traverse the string
    for i in range(len(s)):

        # AscASCIIii value of the
        # current character
        index = ord(s[i]) - 97 + 1;

        # Count frequency of each
        # character in the string
        b[index - 1] += 1

    # Traverse the string
    for i in range(len(s)):

        # ASCII value of the current
        # character
        index = ord(s[i]) - 97 + 1

        # Check if the frequency of
        # each character in string
        # is same as ASCII code or not
        if (b[index - 1] != index):
            print("No")
            return

    # Else print "Yes"
    print("Yes")

# Driver Code
if __name__ == '__main__':

    # Given string S
    s = "bba"

    # Function Call
    checkSuperASCII(s)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to check whether the
    // string is super ASCII or not
    static void checkSuperASCII(string s)
    {

        // Stores the frequency count
        // of characters 'a' to 'z'
        int[] b = new int[26];

        // Traverse the string
        for(int i = 0; i < s.Length; i++)
        {

            // AscASCIIii value of the
            // current character
            int index = (int)s[i] - 97 + 1;

            // Count frequency of each
            // character in the string
            b[index - 1]++;
        }

        // Traverse the string
        for(int i = 0; i < s.Length; i++)
        {

            // ASCII value of the current
            // character
            int index = (int)s[i] - 97 + 1;

            // Check if the frequency of
            // each character in string
            // is same as ASCII code or not
            if (b[index - 1] != index)
            {
                Console.WriteLine("No");
                return;
            }
        }

        // Else print "Yes"
        Console.WriteLine("Yes");
    }

  // Driver code
  static void Main()
 {

    // Given string S
    string s = "bba";

    // Function Call
    checkSuperASCII(s);
  }
}

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)