# 计算两个数差百分比的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-两个数差百分比/](https://www.geeksforgeeks.org/program-to-find-the-percentage-of-difference-between-two-numbers/)

给定两个数字 a 和 b，其中“b”按“a”的某个百分比递增或递减。任务是找出这个百分比。

**示例:**

```
Input: a = 20, b = 25
Output: 25% 
Difference between 20 and 25 is 5, 
which is 25 % of 20.
(+ve sign indicate increment)

Input: a = 25, b = 20
Output: -20% 
( -ve sign indicate decrement)
```

**计算百分比的公式:**

> (百分比 2–百分比 1) * 100 /(百分比 1)

## C++

```
// C++ program to calculate the percentage
#include <iostream>
using namespace std;

// Function to calculate the percentage
int percent(int a, int b)
{
    float result = 0;
    result = ((b - a) * 100) / a;

    return result;
}

// Driver Code.
int main()
{
    int a = 20, b = 25;

    cout << percent(a, b) << "%";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the percentage
class GFG
{

// Function to calculate the percentage
static int percent(int a, int b)
{
    float result = 0;
    result = ((b - a) * 100) / a;

    return (int)result;
}

// Driver Code
public static void main(String[] args)
{
    int a = 20, b = 25;

    System.out.println(percent(a, b) + "%");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to calculate
# the percentage

# Function to calculate the percentage
def percent(a, b) :

    result = int(((b - a) * 100) / a)

    return result

# Driver code
if __name__ == "__main__" :

    a, b = 20, 25

    # Function calling
    print(percent(a, b), "%")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to calculate
// the percentage
class GFG
{

// Function to calculate the percentage
static int percent(int a, int b)
{
    float result = 0;
    result = ((b - a) * 100) / a;

    return (int)result;
}

// Driver Code
static void Main()
{
    int a = 20, b = 25;

    System.Console.WriteLine(percent(a, b) + "%");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// the percentage

// Function to calculate
// the percentage
function percent($a, $b)
{
    $result = 0;
    $result = (($b - $a) * 100) / $a;

    return $result;
}

// Driver Code
$a = 20;
$b = 25;

echo percent($a, $b) . "%";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate the percentage

// Function to calculate the percentage
function percent(a, b)
{
    var result = 0;
    result = ((b - a) * 100) / a;

    return result;
}

// Driver Code.
var a = 20, b = 25;

document.write( percent(a, b) + "%");

// This code is contributed by itsok

</script>
```

**Output:** 

```
25%
```