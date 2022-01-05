# 伊多尼尔数字

> 原文:[https://www.geeksforgeeks.org/idoneal-numbers/](https://www.geeksforgeeks.org/idoneal-numbers/)

**伊多尼尔数**是一个数 **N** 当且仅当它不能被写成 a > b > c > 0 的 ab + bc + ca。
几个概念数字是:

> 1、2、3、4、5、6、7、8、9、10、12、13、15、16、18、21、22……

### 检查一个数字是否是整数

给定一个数字 **N** ，任务是检查 **N** 是否是一个**伊多尼尔数字**。如果 **N** 是一个身份证号码，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 10
> **输出:**是
> **输入:** N = 11
> **输出:**否

**逼近**思路是从‘1’到‘N’运行三个[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)，检查 ab + bc + ca 是否等于‘N’。如果 ab + bc + ca 等于' N '则返回 false，否则在循环结束时返回 true。
以下是上述方法的实施:

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if number
// is an Idoneal numbers
bool isIdoneal(int n)
{
    // iterate for all
    // triples pairs (a, b, c)
    for (int a = 1; a <= n; a++) {
        for (int b = a + 1; b <= n; b++) {
            for (int c = b + 1; c <= n; c++) {

                // if the condition
                // is satisfied
                if (a * b + b * c + c * a == n)
                    return false;
            }
        }
    }
    return true;
}

// Driver Code
int main()
{
    int N = 10;

    // Function Call
    if (isIdoneal(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the
// above approach
import java.lang.*;

class GFG{

// Function to check if number
// is an Idoneal numbers
static boolean isIdoneal(int n)
{

    // Iterate for all
    // triples pairs (a, b, c)
    for(int a = 1; a <= n; a++)
    {
       for(int b = a + 1; b <= n; b++)
       {
          for(int c = b + 1; c <= n; c++)
          {

             // If the condition
             // is satisfied
             if (a * b + b * c + c * a == n)
                 return false;
          }
       }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;

    // Function Call
    if (isIdoneal(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 implementation for the
# above approach

# Function to check if number
# is an Idoneal numbers
def isIdoneal(n):

    # Iterate for all
    # triples pairs (a, b, c)
    for a in range(1, n + 1):
        for b in range(a + 1, n + 1):
            for c in range(b + 1, n + 1):

                # If the condition
                # is satisfied
                if (a * b + b * c + c * a == n):
                    return False

    return True

# Driver Code
N = 10

# Function call
if (isIdoneal(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to check if number
// is an Idoneal numbers
static bool isIdoneal(int n)
{

    // Iterate for all
    // triples pairs (a, b, c)
    for(int a = 1; a <= n; a++)
    {
        for(int b = a + 1; b <= n; b++)
        {
            for(int c = b + 1; c <= n; c++)
            {

                // If the condition
                // is satisfied
                if (a * b + b * c + c * a == n)
                    return false;
            }
        }
    }
    return true;
}

// Driver Code
public static void Main()
{
    int N = 10;

    // Function Call
    if (isIdoneal(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation for the
// above approach

// Function to check if number
// is an Idoneal numbers
function isIdoneal(n)
{

    // iterate for all
    // triples pairs (a, b, c)
    for (var a = 1; a <= n; a++) {
        for (var b = a + 1; b <= n; b++) {
            for (var c = b + 1; c <= n; c++) {

                // if the condition
                // is satisfied
                if (a * b + b * c + c * a == n)
                    return false;
            }
        }
    }
    return true;
}

// Driver Code
var N = 10;

// Function Call
if (isIdoneal(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n * n * n)*
T5】参考:[https://en.wikipedia.org/wiki/Idoneal_number](https://en.wikipedia.org/wiki/Idoneal_number)