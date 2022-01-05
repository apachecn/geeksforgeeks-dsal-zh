# 与 N 乘积的位数和等于 N 的最小数

> 原文:[https://www . geeksforgeeks . org/最小数字-其与 n 的乘积等于 n 的和/](https://www.geeksforgeeks.org/smallest-number-whose-product-with-n-has-sum-of-digits-equal-to-that-of-n/)

给定一个整数 **N** ，任务是找到最小的正整数，当乘以 **N** 时，其位数之和等于 **N** 的位数之和。

**示例:**

> **输入:**N = 4
> T3】输出:28
> T6】说明:
> 
> *   N = 4 的位数之和
> *   4 * 28 = 112
> *   位数之和= 1 + 1 + 2 = 4，等于 n 的位数之和。
> 
> **输入:**N = 3029
> T3】输出:37
> T6】说明:
> 
> *   N = 3 + 0 + 2 + 9 = 14 的位数之和
> *   3029 * 37 = 112073
> *   位数之和= 1 + 1 + 2 + 0 + 7 + 3 = 14，等于 n 的位数之和。

**方法:**按照步骤解决问题:

1.  既然 **N** 可以大，就把 **N** 的输入当成一根弦。[计算 **N**](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/) 的位数之和，存储在变量中，比如 **S** 。
2.  由于答案需要超过 10，从数字 11 开始，乘以 N 并存储在一个变量中，比如 **res** 。
3.  计算 res 的位数总和，检查 res 的位数总和是否等于 S。如果发现为真，则打印整数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the minimum
// integer having sum of digits
// of a number multiplied by n
// equal to sum of digits of n
void find_num(string n)
{

    // Initialize answer
    int ans = 0;
    int sumOfDigitsN = 0;

    // Find sum of digits of N
    for(int c = 0; c < n.length(); c++)
    {
        sumOfDigitsN += n - '0';

    }
    int x=11;

    while(true)
    {
        // Multiply N with x
        int newNum = x * stoi(n);
        int tempSumDigits = 0;
        string temp = to_string(newNum);

        // Sum of digits of the new number
        for(int c = 0; c < temp.length(); c++)
        {
            tempSumDigits += temp - '0';
        }

        // If condition satisfies
        if (tempSumDigits == sumOfDigitsN)
        {
            ans = x;
            break;
        }
        //increase x
          x++;
    }

    // Print answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    string N = "3029";

    // Function call
    find_num(N);
    return 0;
}

// This code is contributed by Sunil Sakariya
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the minimum
    // integer having sum of digits
    // of a number multiplied by n
    // equal to sum of digits of n
    static void find_num(String n)
    {
        // Initialize answer
        int ans = 0;

        // Convert string to
        // character array
        char[] digitsOfN
            = n.toCharArray();

        int sumOfDigitsN = 0;

        // Find sum of digits of N
        for (char c : digitsOfN) {

            sumOfDigitsN
                += Integer.parseInt(
                    Character.toString(c));
        }

        for (int x = 11; x > 0; x++) {

            // Multiply N with x
            int newNum
                = x * Integer.parseInt(n);

            int tempSumDigits = 0;

            char[] temp
                = Integer.toString(
                             newNum)
                      .toCharArray();

            // Sum of digits of the new number
            for (char c : temp) {
                tempSumDigits
                    += Integer.parseInt(
                        Character.toString(c));
            }

            // If condition satisfies
            if (tempSumDigits == sumOfDigitsN) {
                ans = x;
                break;
            }
        }

        // Print answer
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String N = "3029";

        // Function call
        find_num(N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# integer having sum of digits
# of a number multiplied by n
# equal to sum of digits of n
def find_num(n):

    # Initialize answer
    ans = 0

    # Convert string to
    # character array
    digitsOfN = str(n)

    sumOfDigitsN = 0

    # Find sum of digits of N
    for c in digitsOfN:
        sumOfDigitsN += int(c)

    for x in range(11, 50):

        # Multiply N with x
        newNum = x * int(n)

        tempSumDigits = 0

        temp = str(newNum)

        # Sum of digits of the new number
        for c in temp:
            tempSumDigits += int(c)
        #print(tempSumDigits,newNum)

        # If condition satisfies
        if (tempSumDigits == sumOfDigitsN):
            ans = x
            break

    # Print answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    N = "3029"

    # Function call
    find_num(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach 
using System;
using System.Globalization;

class GFG{

// Function to find the minimum
// integer having sum of digits
// of a number multiplied by n
// equal to sum of digits of n
static void find_num(string n)
{

    // Initialize answer
    int ans = 0;

    // Convert string to
    // character array
    char[] digitsOfN = n.ToCharArray();

    int sumOfDigitsN = 0;

    // Find sum of digits of N
    foreach(char c in digitsOfN)
    {
        sumOfDigitsN += Int32.Parse(
                Char.ToString(c));
    }

    for(int x = 11; x > 0; x++)
    {

        // Multiply N with x
        int newNum = x * Int32.Parse(n);

        int tempSumDigits = 0;

        string str = newNum.ToString();
        char[] temp = str.ToCharArray();

        // Sum of digits of the new number
        foreach(char c in temp)
        {
            tempSumDigits += Int32.Parse(
                    Char.ToString(c));
        }

        // If condition satisfies
        if (tempSumDigits == sumOfDigitsN)
        {
            ans = x;
            break;
        }
    }

    // Print answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{
    string N = "3029";

    // Function call
    find_num(N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum
// integer having sum of digits
// of a number multiplied by n
// equal to sum of digits of n
function find_num(n)
{

    // Initialize answer
    var ans = 0;
    var sumOfDigitsN = 0;

    // Find sum of digits of N
    for(var c = 0; c < n.length; c++)
    {
        sumOfDigitsN += n - '0';

    }
    var x=11;

    while(true)
    {
        // Multiply N with x
        var newNum = x * parseInt(n);
        var tempSumDigits = 0;
        var temp = (newNum.toString());

        // Sum of digits of the new number
        for(var c = 0; c < temp.length; c++)
        {
            tempSumDigits += temp - '0';
        }

        // If condition satisfies
        if (tempSumDigits == sumOfDigitsN)
        {
            ans = x;
            break;
        }
        //increase x
          x++;
    }

    // Print answer
    document.write( ans );
}

// Driver Code
var N = "3029";

// Function call
find_num(N);

</script>
```

**Output: **

```
37
```

***时间复杂度:** O(N)*
***辅助空间:** O(log N)*