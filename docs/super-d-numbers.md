# 超 D 号

> 原文:[https://www.geeksforgeeks.org/super-d-numbers/](https://www.geeksforgeeks.org/super-d-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否为超 d 数。

> 超 D 数是一个数字 N，使得 D*N <sup>D</sup> 包含一个由仅包含 D 的 D 个数字组成的子串，其中 D 大于 1 且小于 10

**例:**

> **输入:** N = 261
> **输出:**是
> **解释:**
> 对于 D = 3
> D * N<sup>D</sup>= 3 * 261<sup>3</sup>= 53338743
> 将为真，其中包含由 3 位数字 333 组成的子串，仅包含 3。
> **输入:** N = 10
> **输出:**否

**方法:**想法是创建每一个可能的字符串串联数字 D，D 的次数，然后将检查串联是否作为子串出现在 D*N <sup>D</sup> 中，其中 D 将在范围[2，9]内。
以下是上述方法的实施:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check if N is a super-d number
class GFG{

// Function to check if N
// is a super-d number
static boolean isSuperdNum(int n)
{
    for (int d = 2; d < 10; d++)
    {
        String subString = newString(d);
        if (String.valueOf(
           (d * Math.pow(n, d))).contains(subString))
            return true;
    }
    return false;
}

// Driver Code
private static String newString(int d)
{
    String ans = "";
    for (int i = 0; i < d; i++)
    {
        ans += String.valueOf(d);
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 261;
    if (isSuperdNum(n) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to
# check if N is a super-d number

# Function to check if N
# is a super-d number
def isSuperdNum(n):
    for d in range (2, 10):
        substring = str(d) * d;
        if substring in str(d * pow(n, d)):
            return True
    return False

# Driver Code
n = 261
if isSuperdNum(n) == True:
    print("Yes")
else :
    print("No")
```

## C#

```
// C# implementation to
// check if N is a super-d number
using System;

class GFG{

// Function to check if N
// is a super-d number
static bool isSuperdNum(int n)
{
    for(int d = 2; d < 10; d++)
    {
       String subString = newString(d);
       if (String.Join("",
          (d * Math.Pow(n, d))).Contains(subString))
           return true;
    }
    return false;
}

private static String newString(int d)
{
    String ans = "";

    for(int i = 0; i < d; i++)
    {
       ans += String.Join("", d);
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 261;

    if (isSuperdNum(n) == true)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
Yes
```

**时间复杂度:** O(1)

**参考文献:**[OEIS](http://oeis.org/A032743)T4】