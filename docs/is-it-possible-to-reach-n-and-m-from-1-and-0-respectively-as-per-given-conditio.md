# 按照给定的条件

是否可以从 1 和 0 分别达到 N 和 M

> 原文:[https://www . geesforgeks . org/根据给定条件分别从 1 和 0 到达 n 和 m 是可能的吗/](https://www.geeksforgeeks.org/is-it-possible-to-reach-n-and-m-from-1-and-0-respectively-as-per-given-conditio/)

给定两个整数 **N** 和 **M** ，任务是检查是否可以通过多次执行这两个操作分别从 **X = 1** 和 **Y = 0** 获得这些值:

*   当且仅当 x>0 时，将 X 和 Y 增加 1。
*   当且仅当 y>0 时，将 Y 增加 2。

**示例:**

> **输入:** N = 3，M = 4
> **输出:**是
> **解释:**
> 最初 X = 1，Y = 0
> 运算 1: X = 2，Y = 1
> 运算 1: X = 3，Y = 2
> 运算 2: X = 3，Y = 4，由此得到最终值，所以答案是肯定的。
> 
> **输入:** N = 5，M = 2
> **输出:**否
> **说明:**
> 从 X = 1 和 Y = 0 获得 X = 5 和 Y = 2 是不可能的。

**方法:**上述问题可以通过以下观察来解决:

1.  如果 **N 小于 2****M 不等于零**，则无法得到最终值，因此答案为**否**。
2.  否则，**从 M 中减去** N，如果 **M？0** 和 **M 可被 2** 整除那么答案是**是**。
3.  在所有其他情况下，答案是**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that find given x and y
// is possible or not
bool is_possible(int x, int y)
{
    // Check if x is less than 2 and
    // y is not equal to 0
    if (x < 2 && y != 0)
        return false;

    // Perform subtraction
    y = y - x + 1;

    // Check if y is divisible by 2
    // and greater than equal to 0
    if (y % 2 == 0 && y >= 0)
        return true;

    else
        return false;
}

// Driver Code
int main()
{
    // Given X and Y
    int x = 5, y = 2;

    // Function Call
    if (is_possible(x, y))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that find given x and y
// is possible or not
static boolean is_possible(int x, int y)
{
    // Check if x is less than 2 and
    // y is not equal to 0
    if (x < 2 && y != 0)
        return false;

    // Perform subtraction
    y = y - x + 1;

    // Check if y is divisible by 2
    // and greater than equal to 0
    if (y % 2 == 0 && y >= 0)
        return true;

    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    // Given X and Y
    int x = 5, y = 2;

    // Function Call
    if (is_possible(x, y))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that find given x and y
# is possible or not
def is_possible(x, y):

    # Check if x is less than 2 and
    # y is not equal to 0
    if (x < 2 and y != 0):
        return false

    # Perform subtraction
    y = y - x + 1

    # Check if y is divisible by 2
    # and greater than equal to 0
    if (y % 2 == 0 and y >= 0):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':

    # Given X and Y
    x = 5
    y = 2

    # Function Call
    if (is_possible(x, y)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that find given x and y
// is possible or not
static bool is_possible(int x, int y)
{
    // Check if x is less than 2 and
    // y is not equal to 0
    if (x < 2 && y != 0)
        return false;

    // Perform subtraction
    y = y - x + 1;

    // Check if y is divisible by 2
    // and greater than equal to 0
    if (y % 2 == 0 && y >= 0)
        return true;

    else
        return false;
}

// Driver Code
public static void Main(string[] args)
{
    // Given X and Y
    int x = 5, y = 2;

    // Function Call
    if (is_possible(x, y))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that find given x and y
// is possible or not
function is_possible(x, y)
{

    // Check if x is less than 2 and
    // y is not equal to 0
    if (x < 2 && y != 0)
        return false;

    // Perform subtraction
    y = y - x + 1;

    // Check if y is divisible by 2
    // and greater than equal to 0
    if (y % 2 == 0 && y >= 0)
        return true;
    else
        return false;
}

// Driver code

// Given X and Y
let x = 5, y = 2;

// Function Call
if (is_possible(x, y))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyesh072019       

</script>
```

**Output:** 

```
No
```

**时间复杂度:** *O(1)*
**辅助空间:** *O(1)*