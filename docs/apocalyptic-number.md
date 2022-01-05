# 启示录号

> 原文:[https://www.geeksforgeeks.org/apocalyptic-number/](https://www.geeksforgeeks.org/apocalyptic-number/)

给定一个数字 **N** ，任务是检查 **N** 是否是**启示录数字**。如果 **N** 是**启示录号**，则打印**“是”**否则打印**“否”**。

> 启示录数字是这样一个数字:2 <sup>N</sup> 包含**“666”**作为子串。

**示例:**

> **输入:** N = 157
> **输出:**是
> **解释:**
> 2<sup>157</sup>= 1826877046636286475460604089535377456991567872
> 包含作为子串的“666”。
> 
> **输入:**N = 10
> T3】输出:否

**方法:**思路是计算 2 <sup>N</sup> 的值，检查结果数是否包含**“666”**作为子串。如果有**“666”**作为子串，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to check if a number
    // N is Apocalyptic
    static boolean isApocalyptic(int n)
    {
        if (String.valueOf((
                               Math.pow(2, n)))
                .contains("666"))
            return true;
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Number N
        int N = 157;

        // Function Call
        if (isApocalyptic(N))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if a number
# N is Apocalyptic 
def isApocalyptic(n):     
    if '666' in str(2**n):
        return True
    return False

# Driver Code

# Given Number N
N = 157

# Function Call
if(isApocalyptic(157)):
    print("Yes")
else:
    print("No")
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if a number
// N is Apocalyptic
static bool isApocalyptic(int n)
{
    if (Math.Pow(2, n).ToString().Contains("666"))
        return true;

    return false;
}

static public void Main()
{

    // Given Number N
    int N = 157;

    // Function Call
    if (isApocalyptic(N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// Javascript implementation

// Function to check if N isApocalyptic
function isApocalyptic(n)
{
    var x = Math.pow(2,n);
    if(x.toString().indexOf('666'))
        return true
    return false
}

// Driver Code
// Given Number N
var N = 157;

// Function Call
if (isApocalyptic(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by shubhamsingh10
</script>
```

**Output**

```
Yes
```

**时间复杂度:**T2【O(n)T4】