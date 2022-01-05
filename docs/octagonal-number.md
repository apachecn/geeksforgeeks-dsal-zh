# 八角号

> 原文:[https://www.geeksforgeeks.org/octagonal-number/](https://www.geeksforgeeks.org/octagonal-number/)

给你一个数字 n，任务是找到 n <sup>第</sup>个八角数。另外，找到八角系列直到 n.
一个[八角数字](https://en.wikipedia.org/wiki/Octagonal_number)是代表八角的数字。八边形数字可以通过在正方形的四个边上放置三角形数字来形成。八角数采用公式**(3n<sup>2</sup>–2n)**计算。
示例:

```
Input : 5
Output : 65

Input : 10
Output : 280

Input : 15
Output : 645
```

## C++

```
// C++ program to find
// nth octagonal number
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
//octagonal number
int octagonal(int n)
{
    // Formula for finding
    // nth octagonal number
    return 3 * n * n - 2 * n;
}

// Driver function
int main()
{
    int n = 10;
    cout << n << "th octagonal number :"
         << octagonal(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// nth octagonal number
import java.util.*;
import java.lang.*;

public class GfG {

    // Function to calculate
    //octagonal number
    public static int octagonal(int n)
    {
        // Formula for finding
        // nth octagonal number
        return 3 * n * n - 2 * n;
    }

    // Driver function
    public static void main(String argc[])
    {
        int n = 10;
        System.out.println(n + "th octagonal" +
                     " number :" + octagonal(n));
    }
}

/* This code is contributed by Sagar Shukla */
```

## 计算机编程语言

```
# Python program to find
# nth octagonal number
def octagonal(n):
    return 3 * n * n - 2 * n

# Driver code
n = 10
print(n, "th octagonal number :",
       octagonal(n))
```

## C#

```
// C# program to find nth octagonal number
using System;

public class GfG {

    // Function to calculate
    //octagonal number
    public static int octagonal(int n)
    {

        // Formula for finding
        // nth octagonal number
        return 3 * n * n - 2 * n;
    }

    // Driver function
    public static void Main()
    {
        int n = 10;

        Console.WriteLine(n + "th octagonal"
              + " number :" + octagonal(n));
    }
}

/* This code is contributed by Vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// nth octagonal number

// Function to calculate
//octagonal number
function octagonal($n)
{

    // Formula for finding
    // nth octagonal number
    return 3 * $n * $n - 2 * $n;
}

    // Driver Code
    $n = 10;
    echo $n , "th octagonal number :"
                     , octagonal($n);

// This code is contributed by Vt_m .
?>
```

## java 描述语言

```
<script>

// JavaScript program to convert
// Binary code to Gray code

    // Function to calculate
    //octagonal number
    function octagonal(n)
    {
        // Formula for finding
        // nth octagonal number
        return 3 * n * n - 2 * n;
    }

// Driver code                  
        let n = 10;
        document.write(n + "th octagonal" +
                     " number :" + octagonal(n));

   // This code is contributed by code_hunt.
</script>
```

输出:

```
10th octagonal number : 280
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

#### 给定 n，求八角级数直到 n。

我们还可以找到八角系列。八角系列包含八角上的点。

```
Octagonal series 1, 8, 21, 40, 65, 96, 133, 176, 225, 280, . . .
```

## C++

```
// C++ program to display the
// octagonal series
#include <bits/stdc++.h>
using namespace std;

// Function to display
// octagonal series
void octagonalSeries(int n)
{
    // Formula for finding
    //nth octagonal number
    for (int i = 1; i <= n; i++)

        // Formula for computing
        // octagonal number
        cout << (3 * i * i - 2 * i);   
}

// Driver function
int main()
{
    int n = 10;
    octagonalSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// nth octagonal number
import java.util.*;
import java.lang.*;

public class GfG {

    // Function to display octagonal series
    public static void octagonalSeries(int n)
    {
        // Formula for finding
        //nth octagonal number
        for (int i = 1; i <= n; i++)

            // Formula for computing
            // octagonal number
            System.out.print(3 * i * i - 2 * i);
    }

    // Driver function
    public static void main(String argc[])
    {
        int n = 10;
        octagonalSeries(n);
    }

    /* This code is contributed by Sagar Shukla */
}
```

## 计算机编程语言

```
# Python program to find
# nth octagonal number
def octagonalSeries(n):
    for i in range(1, n + 1):
        print(3 * i * i - 2 * i,
                   end = ", ")

# Driver code
n = 10
octagonalSeries(n)
```

## C#

```
// C# program to find
// nth octagonal number
using System;

public class GfG {

    // Function to display octagonal series
    public static void octagonalSeries(int n)
    {

        // Formula for finding
        //nth octagonal number
        for (int i = 1; i <= n; i++)

            // Formula for computing
            // octagonal number
            Console.Write(3 * i * i - 2 * i + ", ");
    }

    // Driver function
    public static void Main()
    {
        int n = 10;

        octagonalSeries(n);
    }
}

/* This code is contributed by Vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to display the
// octagonal series

// Function to display
// octagonal series
function octagonalSeries($n)
{

    // Formula for finding
    // nth octagonal number
    for ($i = 1; $i <= $n; $i++)

        // Formula for computing
        // octagonal number
        echo (3 * $i * $i - 2 * $i),",";
}

    // Driver Code
    $n = 10;
    octagonalSeries($n);

// This code is contributed by Vt_m .
?>
```

## java 描述语言

```
<script>
// Javascript program to display the
// octagonal series

// Function to display
// octagonal series
function octagonalSeries(n)
{

    // Formula for finding
    // nth octagonal number
    for (let i = 1; i <= n; i++)

        // Formula for computing
        // octagonal number
        document.write(3 * i * i - 2 * i + ", ");
}

    // Driver Code
    let n = 10;
    octagonalSeries(n);

// This code is contributed by _saurabh_jaiswal

</script>
```

输出:

```
1, 8, 21, 40, 65, 96, 133, 176, 225, 280
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)