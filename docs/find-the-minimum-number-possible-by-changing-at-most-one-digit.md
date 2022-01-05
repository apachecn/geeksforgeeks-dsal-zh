# 通过最多改变一个数字找到可能的最小数字

> 原文:[https://www . geesforgeks . org/通过最多改变一位数字来找到可能的最小数字/](https://www.geeksforgeeks.org/find-the-minimum-number-possible-by-changing-at-most-one-digit/)

给定一个仅由两种数字组成的正整数**N****6**和 **9** ，任务是通过最多反转一个数字来生成**最小可能数**，即 **9** 变为 **6** ，反之亦然。
**示例:**

> **输入:**9996
> T3】输出: 6996
> **说明:**
> 更改第一位数字结果为 6996。
> 更改第二位数字会导致 9696。
> 更改第三位数会导致 9966。
> 更改第四位数字会导致 9999。
> 因此，所有可能性中的最小数量是 6996。
> **输入:** 6696
> **输出:** 6666
> **解释:**
> 更改第一位数字会导致 9696。
> 更改第二位数字会导致 6996。
> 更改第三位数会得到 6666。
> 更改第四位数字会导致 6699。
> 因此，所有可能性中的最小数量是 6666。

**进场:**
为了解决问题，我们需要按照下面给出的步骤:

*   首先将给定的整数转换成字符串。
*   从左开始遍历字符串，将第一次出现的“9”更改为“6”，并退出循环。如果在初始字符串中没有出现 9，那么它已经是可能的最低数字。
*   将最后一个字符串转换回整数并打印出来。

以下是上述方法的实现:

## C++

```
// C++ implementation to change at most
// one digit to make the number
// as minimum as possible

#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// possible number
int minimum69Number(int num)
{

    // Converting given number to string
    string s_num = to_string(num);

    // Traversing the string
    for (auto& c : s_num) {
        // change first 9 to 6
        if (c == '9') {
            c = '6';
            break;
        }
    }

    // Change the string back to the integer
    int result = stoi(s_num);

    // Return the final result
    return result;
}

// Driver code
int main()
{
    // Input number
    int n = 9996;

    int result = minimum69Number(n);

    // Print the result
    cout << result << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to change at most
// one digit to make the number
// as minimum as possible
class GFG{

// Function to return the minimum
// possible number
static int minimum69Number(int num)
{

    // Converting given number to String
    char []s_num = String.valueOf(num).toCharArray();

    // Traversing the String
    for(int i = 0; i < s_num.length; i++)
    {

       // change first 9 to 6
       if (s_num[i] == '9')
       {
           s_num[i] = '6';
           break;
       }
    }

    // Change the String back to the integer
    int result = Integer.valueOf(String.valueOf(s_num));

    // Return the final result
    return result;
}

// Driver code
public static void main(String[] args)
{

    // Input number
    int n = 9996;
    int result = minimum69Number(n);

    // Print the result
    System.out.print(result + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to change at most
# one digit to make the number
# as minimum as possible

# Function to return the minimum
# possible number
def minimum69Number(num):

    # Converting given number to string
    s_num = str(num)

    s_num = s_num.replace('9','6', 1)

    # Change the string back to the integer
    result = int(s_num)

    # Return the final result
    return result

# Driver code
if __name__ == '__main__':

    # Input number
    n = 9996

    result = minimum69Number(n)

    # Print the result
    print(result)

# This code is contributed by Samarth
```

## C#

```
// C# implementation to change at most
// one digit to make the number
// as minimum as possible
using System;

class GFG{

// Function to return the minimum
// possible number
static int minimum69Number(int num)
{

    // Converting given number to String
    char []s_num = String.Join("", num).ToCharArray();

    // Traversing the String
    for(int i = 0; i < s_num.Length; i++)
    {
       // change first 9 to 6
       if (s_num[i] == '9')
       {
           s_num[i] = '6';
           break;
       }
    }

    // Change the String back to the integer
    int result = Int32.Parse(String.Join("", s_num));

    // Return the readonly result
    return result;
}

// Driver code
public static void Main(String[] args)
{

    // Input number
    int n = 9996;
    int result = minimum69Number(n);

    // Print the result
    Console.Write(result + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

    // JavaScript implementation to change at most
    // one digit to make the number
    // as minimum as possible

    // Function to return the minimum
    // possible number
    function minimum69Number(num)
    {

        // Converting given number to string
        let s_num = (num.toString()).split('');

        // Traversing the String
        for(let i = 0; i < s_num.length; i++)
        {

           // change first 9 to 6
           if (s_num[i] == '9')
           {
               s_num[i] = '6';
               break;
           }
        }

        // Change the String back to the integer
        let result = parseInt(s_num.join(""));

        // Return the final result
        return result;
    }

    // Driver code

    // Input number
    let n = 9996;

    let result = minimum69Number(n);

    // Print the result
   document.write(result);

</script>
```

**Output:** 

```
6996
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)