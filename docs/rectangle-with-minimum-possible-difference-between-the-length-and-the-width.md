# 长度和宽度之间差异最小的矩形

> 原文:[https://www . geesforgeks . org/长宽差尽可能小的矩形/](https://www.geeksforgeeks.org/rectangle-with-minimum-possible-difference-between-the-length-and-the-width/)

给定一个整数**面积**，任务是找到给定面积的矩形的长度和宽度，使得长度和宽度之差尽可能最小。

**示例:**

> **输入:**面积= 99
> **输出:** l = 11，b = 9
> 所有可能的矩形(l，b)都是(99，1)，(33，3)和(11，9)
> 最小的| l–b |是(11，9)
> 
> **输入:**面积= 25
> T3】输出: l = 5，b = 5

**方法:**任务是找到两个整数 **l** 和 **b** ，使得 **l * b =面积**和**| l–b |**尽可能最小。因子分解可以用来解决问题，但是从 **1** 到 **N** 只做简单的因子分解，对于 **N** 的较大值，需要很长时间才能得到需要的输出。
要克服这一点，只需迭代到。考虑到![          ](img/43bdb2b1d78ea7f771b56deae47919d0.png "Rendered by QuickLaTeX.com") **< l ≤ N** ，那么对于 **l** 、 **b** 的所有值将始终为 **<** ![          ](img/43bdb2b1d78ea7f771b56deae47919d0.png "Rendered by QuickLaTeX.com")。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the length (l)
// and breadth (b) of the rectangle
// having area = N and |l - b| as
// minimum as possible
void find_rectangle(int area)
{
    int l, b;
    int M = sqrt(area), ans;

    for (int i = M; i >= 1; i--) {

        // i is a factor
        if (area % i == 0) {

            // l >= sqrt(area) >= i
            l = (area / i);

            // so here l is +ve always
            b = i;
            break;
        }
    }

    // Here l and b are length and
    // breadth of the rectangle
    cout << "l = " << l << ", b = "
         << b << endl;
}

// Driver code
int main()
{
    int area = 99;
    find_rectangle(area);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the length (l)
    // and breadth (b) of the rectangle
    // having area = N and |l - b| as
    // minimum as possible
    static void find_rectangle(int area)
    {
        int l = 0, b = 0;
        int M = (int)Math.sqrt(area), ans;

        for (int i = M; i >= 1; i--) {

            // i is a factor
            if (area % i == 0) {

                // l >= sqrt(area) >= i
                l = (area / i);

                // so here l is +ve always
                b = i;
                break;
            }
        }

        // Here l and b are length and
        // breadth of the rectangle
        System.out.println("l = " + l + ", b = " + b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int area = 99;
        find_rectangle(area);
    }
}

// This code is contributed by Ita_c.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function to print the length (l)
# and breadth (b) of the rectangle
# having area = N and |l - b| as
# minimum as possible
def find_rectangle(area):

    l, b = 0, 0
    M = mt.ceil(mt.sqrt(area))
    ans = 0

    for i in range(M, 0, -1):

        # i is a factor
        if (area % i == 0):

            # l >= sqrt(area) >= i
            l = (area // i)

            # so here l is + ve always
            b = i
            break

    # Here l and b are length and
    # breadth of the rectangle
    print("l =", l, ", b =", b)

# Driver code
area = 99
find_rectangle(area)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to print the length (l)
    // and breadth (b) of the rectangle
    // having area = N and |l - b| as
    // minimum as possible
    static void find_rectangle(int area)
    {
        int l = 0, b = 0;
        int M = (int)Math.Sqrt(area);

        for (int i = M; i >= 1; i--) {

            // i is a factor
            if (area % i == 0) {

                // l >= sqrt(area) >= i
                l = (area / i);

                // so here l is +ve always
                b = i;
                break;
            }
        }

        // Here l and b are length and
        // breadth of the rectangle
        Console.WriteLine("l = " + l + ", b = " + b);
    }

    // Driver code
    public static void Main()
    {
        int area = 99;
        find_rectangle(area);
    }
}

// This code is contributed by Mukul Singh.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to print the length (l)
// and breadth (b) of the rectangle
// having area = N and |l - b| as
// minimum as possible
function find_rectangle($area)
{
    $M = floor(sqrt($area));

    for ($i = $M; $i >= 1; $i--)
    {

        // i is a factor
        if ($area % $i == 0)
        {

            // l >= sqrt(area) >= i
            $l = floor($area / $i);

            // so here l is +ve always
            $b = $i ;
            break;
        }
    }

    // Here l and b are length and
    // breadth of the rectangle
    echo "l = ", $l, ", b = ", $b, "\n";
}

// Driver code
$area = 99;
find_rectangle($area);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to print the length (l)
    // and breadth (b) of the rectangle
    // having area = N and |l - b| as
    // minimum as possible
    function find_rectangle(area)
    {
        let l = 0, b = 0;
        let M = Math.floor(Math.sqrt(area)), ans;

        for (let i = M; i >= 1; i--) {

            // i is a factor
            if (area % i == 0) {

                // l >= sqrt(area) >= i
                l = Math.floor(area / i);

                // so here l is +ve always
                b = i;
                break;
            }
        }

        // Here l and b are length and
        // breadth of the rectangle
        document.write("l = " + l + ", b = " + b);
    }

// Driver code

    let area = 99;
    find_rectangle(area);

</script>
```

**Output:** 

```
l = 11, b = 9
```

**时间复杂度:** O( ![\sqrt{N} ](img/2800a7a2aff8fc294a3314b96487d039.png "Rendered by QuickLaTeX.com") )

下面是一个简单的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the length (l)
// and breadth (b) of the rectangle
// having area = N and |l - b| as
// minimum as possible
void find_rectangle(int area)
{
    for (int i = ceil(sqrt(area)); i <= area; i++) {
        if (area / i * i == area) {
            printf("%d %d", i, area / i);
            return;
        }
    }
}

// Driver code
int main()
{
    int area = 99;
    find_rectangle(area);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
class GFG {
    // Function to print the length (l)
    // and breadth (b) of the rectangle
    // having area = N and |l - b| as
    // minimum as possible
    static void find_rectangle(int area)
    {
        for(int i = (int)Math.ceil(Math.sqrt(area)); i <= area; i++)
        {
            if(area / i * i == area)
            {
                System.out.println(i + " " + (int)(area / i));
                return;
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int area = 99;
        find_rectangle(area);       
    }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to print the length (l)
# and breadth (b) of the rectangle
# having area = N and |l - b| as
# minimum as possible
def find_rectangle(area):
    for i in range(int(math.ceil(math.sqrt(area))) , area + 1):
        if((int(area / i) * i) == area):
            print(i, int(area / i))
            return

# Driver code
area = 99
find_rectangle(area)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

  // Function to print the length (l)
  // and breadth (b) of the rectangle
  // having area = N and |l - b| as
  // minimum as possible
  static void find_rectangle(int area)
  {
    for(int i = (int)Math.Ceiling(Math.Sqrt(area)); i <= area; i++)
    {
      if(area / i * i == area)
      {
        Console.WriteLine(i + " " + (int)(area / i));
        return;
      }
    }
  }

  // Driver code
  static void Main()
  {
    int area = 99;
    find_rectangle(area);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to print the length (l)
// and breadth (b) of the rectangle
// having area = N and |l - b| as
// minimum as possible
function find_rectangle(are)
{
    for(let i = Math.floor(Math.ceil(Math.sqrt(area))); i <= area; i++)
        {
            if(Math.floor(area / i) * i == area)
            {
                document.write(i + " " + Math.floor(area / i));
                return;
            }
        }
}

 // Driver code
let area = 99;
find_rectangle(area);  

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
11 9
```