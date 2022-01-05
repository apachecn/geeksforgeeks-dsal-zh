# 每个字符连续出现后的打印频率

> 原文:[https://www . geesforgeks . org/printing-每个字符在其连续出现后的频率/](https://www.geeksforgeeks.org/printing-frequency-of-each-character-just-after-its-consecutive-occurrences/)

给定一个字符串，使得每个字符以重复的方式出现。您的任务是通过在字符串后插入每个唯一字符的频率并消除所有重复字符来打印字符串。
**例:**

```
Input : GeeeEEKKKss
Output : G1e3E2K3s2

Input : ccccOddEEE
Output : c4O1d2E3
```

解决上述问题的一种方法是开始一个循环，直到字符串结束，并且对于每次迭代，递增一个计数，直到第 i <sup>个</sup>位置的字符与下面的字符匹配。
下面是对上面给定问题的实现。

## C++

```
// CPP program to print run
// length encoding of a string
#include <iostream>
using namespace std;

void printRLE(string s)
{
    for (int i = 0; s[i] != '\0'; i++) {

        // Counting occurrences of s[i]
        int count = 1;
        while (s[i] == s[i + 1]) {
            i++;
            count++;
        }
        cout << s[i] << count << " ";
    }

    cout << endl;
}

// Driver code
int main()
{
    printRLE("GeeeEEKKKss");
    printRLE("ccccOddEEE");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print run
// length encoding of a string
class GFG {

    static void printRLE(String s)
    {
        for (int i = 0; i < s.length(); i++) {

            // Counting occurrences of s[i]
            int count = 1;
            while (i + 1 < s.length()
                   && s.charAt(i)
                          == s.charAt(i + 1)) {
                i++;
                count++;
            }
            System.out.print(s.charAt(i)
                             + "" + count + " ");
        }

        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        printRLE("GeeeEEKKKss");
        printRLE("ccccOddEEE");
    }
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to print run
# length encoding of a string

def printRLE(s) :

    i = 0
    while( i < len(s) - 1) :

        # Counting occurrences of s[i]
        count = 1

        while s[i] == s[i + 1] :

            i += 1
            count += 1

            if i + 1 == len(s):
                break

        print(str(s[i]) + str(count),  
                          end = " ")
        i += 1

    print()

# Driver Code
if __name__ == "__main__" :

    # function calling
    printRLE("GeeeEEKKKss")
    printRLE("cccc0ddEEE")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to print run
// length encoding of a string
using System;

class GFG {

    static void printRLE(String s)
    {
        for (int i = 0;
             i < s.Length - 1; i++) {

            // Counting occurrences of s[i]
            int count = 1;
            while (s[i] == s[i + 1]) {
                i++;
                count++;
                if (i + 1 == s.Length)
                    break;
            }
            Console.Write(s[i] + "" + count + " ");
        }

        Console.WriteLine();
    }

    // Driver code
    public static void Main(String[] args)
    {
        printRLE("GeeeEEKKKss");
        printRLE("ccccOddEEE");
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to print run
// length encoding of a string
function printRLE(s)
{
    for(var i = 0; i < s.length; i++)
    {

        // Counting occurrences of s[i]
        var count = 1;
        while (i + 1 < s.length &&
               s.charAt(i) == s.charAt(i + 1))
        {
            i++;
            count++;
        }
        document.write(s.charAt(i) + "" +
                             count + " ");
    }
    document.write("<br>");
}

// Driver code
printRLE("GeeeEEKKKss");
printRLE("ccccOddEEE");

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
G1 e3 E2 K3 s2 
c4 O1 d2 E3 
```