# 将数字从国际系统转换为印度系统

> 原文:[https://www . geesforgeks . org/convert-the-number-from-international-system-to-Indian-system/](https://www.geeksforgeeks.org/convert-the-number-from-international-system-to-indian-system/)

给定在国际数字系统中用分隔符(，)表示数字的字符串 **str** ，任务是将该字符串表示转换为印度数字系统。
**例:**

> **输入:** str = "123，456，789"
> **输出:** 12，34，56，789
> **说明:**
> 给定的字符串代表国际体系中的一个数字。它被转换为印度体系。
> **输入:** str = "90，050，000，000"
> **输出:** 90，05，00，00，000

**国际数字系统:**国际编号系统在印度次大陆以外地区使用，表示大数字。它遵循以下模式:

<figure class="table">

| 数字 | 应用分隔符 | 用语言 |
| --- | --- | --- |
| one | one | 一个 |
| Ten | Ten | 十 |
| One hundred | One hundred | 一百 |
| One thousand | 1, 000 | 一千 |
| ten thousand | 10, 000 | 一万 |
| One hundred thousand | 100, 000 | 十万 |
| One million | 1, 000, 000 | 一百万 |
| Ten million | 10, 000, 000 | 一千万 |
| One hundred million | 100, 000, 000 | 一亿 |
| One billion | 1, 000, 000, 000 | 十亿 |

**印度数字系统:**印度的编号系统在印度次大陆被用来表示大数字。它遵循以下模式:

<figure class="table">

| 数字 | 应用分隔符 | 用语言 |
| --- | --- | --- |
| one | one | 一个 |
| Ten | Ten | 十 |
| One hundred | One hundred | 一百 |
| One thousand | 1, 000 | 一千 |
| ten thousand | 10, 000 | 一万 |
| One hundred thousand | 1, 00, 000 | 10 万英镑 |
| One million | 10, 00, 000 | 十万 |
| Ten million | 1, 00, 00, 000 | 一个亿 |
| One hundred million | 10, 00, 00, 000 | 十亿 |
| One billion | 100, 00, 00, 000 | 十亿欧元 |

</figure>

**方法:**从上面的表示来看，思路是先得到没有任何分隔符的数字。因此:

1.  从字符串中移除所有分隔符(，)。
2.  [倒弦](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)。
3.  处理字符串，并在第三个数字后放一个分隔符(，)。
4.  现在在每一秒钟的数字后面放一个分隔符(，)。这将数字转换成*印度数字系统。*
5.  再次反转字符串并打印出来。

以下是上述方法的实现:

## C++

```
// C++ program to convert the number
// from International system
// to Indian system

#include <bits/stdc++.h>
using namespace std;

// Function to convert a number represented
// in International numeric system to
// Indian numeric system.
string convert(string input)
{
    // Find the length of the
    // input string
    int len = input.length();

    // Removing all the separators(, )
    // from the input string
    for (int i = 0; i < len;) {

        if (input[i] == ', ') {
            input.erase(input.begin() + i);
            len--;
            i--;
        }
        else if (input[i] == ' ') {
            input.erase(input.begin() + i);
            len--;
            i--;
        }
        else {
            i++;
        }
    }

    // Reverse the input string
    reverse(input.begin(), input.end());

    // Declaring the output string
    string output;

    // Process the input string
    for (int i = 0; i < len; i++) {
        // Add a separator(, ) after the
        // third number
        if (i == 2) {
            output += input[i];
            output += ", ";
        }

        // Then add a separator(, ) after
        // every second number
        else if (i > 2 && i % 2 == 0
                 && i + 1 < len) {
            output += input[i];
            output += ", ";
        }
        else {
            output += input[i];
        }
    }

    // Reverse the output string
    reverse(output.begin(), output.end());

    // Return the output string back
    // to the main function
    return output;
}

// Driver code
int main()
{
    string input1 = "123, 456, 789";
    string input2 = "90, 050, 000, 000";

    cout << convert(input1) << endl;
    cout << convert(input2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert the number
// from International system
// to Indian system
import java.util.*;
class GFG{

// Function to convert a number represented
// in International numeric system to
// Indian numeric system.
static String convert(String input)
{
    StringBuilder sbInput = new StringBuilder(input);

    // Find the length of the
    // sbInput
    int len = sbInput.length();

    // Removing all the separators(, )
    // from the sbInput
    for (int i = 0; i < len;)
    {
        if (sbInput.charAt(i) == ',')
        {
            sbInput.deleteCharAt(i);
            len--;
            i--;
        }
        else if (sbInput.charAt(i) == ' ')
        {
            sbInput.deleteCharAt(i);
            len--;
            i--;
        }
        else
        {
            i++;
        }
    }

    // Reverse the sbInput
    StringBuilder sbInputReverse = sbInput.reverse();

    // Declaring the output
    StringBuilder output = new StringBuilder();

    // Process the sbInput
    for (int i = 0; i < len; i++)
    {

        // Add a separator(, ) after the
        // third number
        if (i == 2)
        {
            output.append(sbInputReverse.charAt(i));
            output.append(" ,");
        }

        // Then add a separator(, ) after
        // every second number
        else if (i > 2 && i % 2 == 0 && i + 1 < len)
        {
            output.append(sbInputReverse.charAt(i));
            output.append(" ,");
        }
        else
        {
            output.append(sbInputReverse.charAt(i));
        }
    }

    // Reverse the output
    StringBuilder reverseOutput = output.reverse();

    // Return the output string back
    // to the main function
    return reverseOutput.toString();
}

// Driver code
public static void main(String[] args)
{
    String input1 = "123, 456, 789";
    String input2 = "90, 050, 000, 000";

    System.out.println(convert(input1));
    System.out.println(convert(input2));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to convert
# the number from International
# system to Indian system

# Function to convert a number
# represented in International
# numeric system to Indian numeric
# system.
def convert(input):

    # Find the length of the
    # input string
    Len = len(input)

    # Removing all the separators(, )
    # from the input string
    i = 0
    while(i < Len):
        if(input[i] == ","):
            input = input[:i] + input[i + 1:]
            Len -= 1
            i -= 1
        elif(input[i] == " "):
            input=input[:i] + input[i + 1:]
            Len -= 1
            i -= 1
        else:
            i += 1
    # Reverse the input string
    input=input[::-1]

    # Declaring the output string
    output = ""

    # Process the input string
    for i in range(Len):

        # Add a separator(, ) after the
        # third number
        if(i == 2):
            output += input[i]
            output += " ,"

        # Then add a separator(, ) after
        # every second number
        elif(i > 2 and i % 2 == 0 and
             i + 1 < Len):
            output += input[i]
            output += " ,"
        else:
            output += input[i]

    # Reverse the output string
    output=output[::-1]

    # Return the output string back
    # to the main function
    return output

# Driver code
input1 = "123, 456, 789"
input2 = "90, 050, 000, 000"
print(convert(input1))
print(convert(input2))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
12, 34, 56, 789
90, 05, 00, 00, 000

```

</figure>