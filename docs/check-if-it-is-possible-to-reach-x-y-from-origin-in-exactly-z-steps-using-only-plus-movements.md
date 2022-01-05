# 检查仅使用正运动

是否可以从原点以精确的 Z 步到达(x，y)

> 原文:[https://www . geeksforgeeks . org/check-如果有可能到达-x-y-in-origin-in-z-steps-仅使用-plus-movements/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-x-y-from-origin-in-exactly-z-steps-using-only-plus-movements/)

给定一个点 **(x，y)** ，任务是检查从原点到 **(x，y)** 是否有可能准确到达 **Z** 步。从给定点 **(x，y)** 开始，我们只能向四个方向移动左**(x–1，y)** 、右 **(x + 1，y)** 、上 **(x，y + 1)** 和下 **(x，y–1)**。
**举例:**

> **输入:** x = 5，y = 5，z = 11
> **输出:**不可能
> **输入:** x = 10，y = 15，z = 25
> **输出:**可能

**进场:**

1.  从原点到 **(x，y)** 的最短路径，是 **|x|+|y|** 。
2.  所以，很明显如果 **Z** 小于 **|x|+|y|** ，那么我们就无法从原点准确到达 **(x，y)** 在 **Z** 步。
3.  如果步数不小于 **|x|+|y|** 那么，我们要检查以下两个条件来检查我们是否能到达 **(x，y)** :
    *   如果 **Z ≥ |x| + |y|** ，并且
    *   如果**(Z –| x |+| y |)% 2**为 **0** 。
4.  对于上一步的第二个条件，如果我们到达 **(x，y)** ，我们可以多走两步如 **(x，y)–>(x，y+1)–>(x，y)** 回到同一位置 **(x，y)** 。只有当它们之间的差异相等时，这才是可能的。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to
// reach (x, y) from origin in exactly z steps
void possibleToReach(int x, int y, int z)
{

    // Condition if we can't reach in Z steps
    if (z < abs(x) + abs(y)
        || (z - abs(x) - abs(y)) % 2) {
        cout << "Not Possible" << endl;
    }
    else
        cout << "Possible" << endl;
}

// Driver Code
int main()
{
    // Destination point coordinate
    int x = 5, y = 5;

    // Number of steps allowed
    int z = 11;

    // Function Call
    possibleToReach(x, y, z);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if it is possible
// to reach (x, y) from origin in
// exactly z steps
static void possibleToReach(int x, int y, int z)
{

    // Condition if we can't reach in Z steps
    if (z < Math.abs(x) + Math.abs(y) ||
       (z - Math.abs(x) - Math.abs(y)) % 2 == 1)
    {
        System.out.print("Not Possible" + "\n");
    }
    else
        System.out.print("Possible" + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Destination point coordinate
    int x = 5, y = 5;

    // Number of steps allowed
    int z = 11;

    // Function Call
    possibleToReach(x, y, z);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible to
# reach (x, y) from origin in exactly z steps
def possibleToReach(x, y, z):

    #Condition if we can't reach in Z steps
    if (z < abs(x) + abs(y) or
       (z - abs(x) - abs(y)) % 2):
        print("Not Possible")
    else:
        print("Possible")

# Driver Code
if __name__ == '__main__':

    # Destination pocoordinate
    x = 5
    y = 5

    # Number of steps allowed
    z = 11

    # Function call
    possibleToReach(x, y, z)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if it is possible
// to reach (x, y) from origin in
// exactly z steps
static void possibleToReach(int x, int y, int z)
{

    // Condition if we can't reach in Z steps
    if (z < Math.Abs(x) + Math.Abs(y) ||
       (z - Math.Abs(x) - Math.Abs(y)) % 2 == 1)
    {
        Console.Write("Not Possible" + "\n");
    }
    else
        Console.Write("Possible" + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Destination point coordinate
    int x = 5, y = 5;

    // Number of steps allowed
    int z = 11;

    // Function Call
    possibleToReach(x, y, z);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to check if it is possible
// to reach (x, y) from origin in
// exactly z steps
function possibleToReach(x , y , z)
{

    // Condition if we can't reach in Z steps
    if (z < Math.abs(x) + Math.abs(y) ||
       (z - Math.abs(x) - Math.abs(y)) % 2 == 1)
    {
        document.write("Not Possible" + "\n");
    }
    else
        document.write("Possible" + "\n");
}

// Driver Code
// Destination point coordinate
var x = 5, y = 5;

// Number of steps allowed
var z = 11;

// Function Call
possibleToReach(x, y, z);

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
Not Possible
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*