# 根据给定的不等式排列数组中的数字

> 原文:[https://www . geesforgeks . org/按给定不等式排列数组中的数字/](https://www.geeksforgeeks.org/arrange-the-numbers-in-the-array-as-per-given-inequalities/)

给定一列 **N** 个不同的整数和一列 **N-1** 个不等式符号，任务是在不等式符号之间插入整数，这样最终形成的不等式总是成立的。
***注:**不平等标志的顺序不应改变。*

**示例:**

> **输入:**整数:【2，5，1，0】，符号:【<、>、<】
> **输出:**0<5>1<2
> T6】说明:
> 形成的不等式一致有效。
> 
> **输入:**整数:【8，34，25，1，-5，10】，符号:【>、>、<、<、>】
> **输出:**34>25>-5<1<10>8
> **解释:**
> 形成的不等式一致有效。

**方法:**不等式符号列表可以包含任意顺序的符号。所以为了获得一致的不等式，把数组中最小的整数**放在每个 **<** 符号之前，把最大的整数**放在每个 **>** 符号之前。基于这个想法，以下是步骤:

1.  [按升序排列整数列表](https://www.geeksforgeeks.org/python-list-sort/)。
2.  保持两个变量，说*低*和*高*，指向整数列表的第一个和最后一个索引。
3.  遍历不等式符号列表。如果当前符号为**少，**则在 **<** 前加上*低*所指的整数，递增*低*指向下一个指标。如果当前符号大于**，**则在 **>** 前加上*高*指向的整数，递减*高*指向前一个索引。
4.  最后，将剩余的元素添加到最后一个位置。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

public class PlacingNumbers {

    // Function to place the integers
    // in between the inequality signs
    static String
    formAnInequality(int[] integers,
                     char[] inequalities)
    {

        // Sort the integers array and
        // set the index of smallest
        // and largest element
        Arrays.sort(integers);

        int lowerIndex = 0;
        int higherIndex = integers.length - 1;

        StringBuilder sb = new StringBuilder();

        // Iterate over the inequalities
        for (char ch : inequalities) {

            // Append the necessary
            // integers per symbol
            if (ch == '<') {
                sb.append(" "
                          + integers[lowerIndex++]
                          + " "
                          + ch);
            }
            else {
                sb.append(" "
                          + integers[higherIndex--]
                          + " "
                          + ch);
            }
        }

        // Add the final integer
        sb.append(" " + integers[lowerIndex]);

        // Return the answer
        return sb.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given List of Integers
        int[] integers = { 2, 5, 1, 0 };

        // Given list of inequalities
        char[] inequalities = { '<', '>', '<' };

        // Function Call
        String output
            = formAnInequality(integers,
                               inequalities);

        // Print the output
        System.out.println(output);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to place the integers
# in between the inequality signs
def formAnInequality(integers,
                     inequalities):

    # Sort the integers array and
    # set the index of smallest
    # and largest element
    integers.sort()

    lowerIndex = 0
    higherIndex = len(integers) - 1
    sb = ""

    # Iterate over the inequalities
    for ch in  inequalities:

        # Append the necessary
        # integers per symbol
        if (ch == '<'):
            sb += (" " + chr(integers[lowerIndex]) +
                   " " + ch)
            lowerIndex += 1
        else:
            sb += (" " + chr(integers[higherIndex]) +
                   " " + ch)
            higherIndex -= 1

    # Add the final integer
    sb += (" " + chr(integers[lowerIndex]))

    # Return the answer
    return sb

# Driver Code
if __name__ ==  "__main__":

    # Given List of Integers
    integers = [2, 5, 1, 0]

    # Given list of inequalities
    inequalities = ['<', '>', '<']

    # Function Call
    output = formAnInequality(integers,
                              inequalities)

    # Print the output
    print(output)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Text;

class GFG{

// Function to place the integers
// in between the inequality signs
static String
formAnInequality(int[] integers,
                char[] inequalities)
{

    // Sort the integers array and
    // set the index of smallest
    // and largest element
    Array.Sort(integers);

    int lowerIndex = 0;
    int higherIndex = integers.Length - 1;

    StringBuilder sb = new StringBuilder();

    // Iterate over the inequalities
    foreach(char ch in inequalities)
    {

        // Append the necessary
        // integers per symbol
        if (ch == '<')
        {
            sb.Append(" " + integers[lowerIndex++] +
                      " " + ch);
        }
        else
        {
            sb.Append(" " + integers[higherIndex--] +
                      " " + ch);
        }
    }

    // Add the readonly integer
    sb.Append(" " + integers[lowerIndex]);

    // Return the answer
    return sb.ToString();
}

// Driver Code
public static void Main(String[] args)
{

    // Given List of ints
    int[] integers = { 2, 5, 1, 0 };

    // Given list of inequalities
    char[] inequalities = { '<', '>', '<' };

    // Function call
    String output = formAnInequality(integers,
                                      inequalities);

    // Print the output
    Console.WriteLine(output);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to place the integers
// in between the inequality signs
function formAnInequality(integers, inequalities)
{

    // Sort the integers array and
    // set the index of smallest
    // and largest element
    (integers).sort(function(a, b){return a - b;});

    let lowerIndex = 0;
    let higherIndex = integers.length - 1;

    let sb = "";

    // Iterate over the inequalities
    for(let ch = 0; ch < inequalities.length; ch++)
    {

        // Append the necessary
        // integers per symbol
        if (inequalities[ch] == '<')
        {
            sb += " " + (integers[lowerIndex++]) +
                  " " + inequalities[ch];
        }
        else
        {
            sb += " " + (integers[higherIndex--]) +
                  " " + inequalities[ch];
        }
    }

    // Add the final integer
    sb += " " + (integers[lowerIndex]);

    // Return the answer
    return sb;
}

// Driver Code

// Given List of Integers
let integers = [ 2, 5, 1, 0 ];

// Given list of inequalities
let inequalities = [ '<', '>', '<' ];

// Function Call
let output = formAnInequality(
    integers, inequalities);

// Print the output
document.write(output);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
0 < 5 > 1 < 2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*