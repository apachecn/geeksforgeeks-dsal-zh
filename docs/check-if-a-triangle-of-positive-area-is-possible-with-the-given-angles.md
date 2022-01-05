# 检查给定角度下是否可能出现正面积三角形

> 原文:[https://www . geeksforgeeks . org/检查给定角度的正面积三角形是否可行/](https://www.geeksforgeeks.org/check-if-a-triangle-of-positive-area-is-possible-with-the-given-angles/)

给定三个角度。任务是检查是否有可能用这些角度形成一个正面积的三角形。如果可能，打印“是”，否则打印“否”。
**例** :

```
Input : ang1 = 50, ang2 = 60, ang3 = 70 
Output : YES

Input : ang1 = 50, ang2 = 65, ang3 = 80
Output : NO
```

**方法:**如果满足以下条件，我们可以形成一个有效的三角形:

*   三个给定角度之和等于 180°。
*   任意两个角之和大于等于第三个角。
*   没有一个给定的角度是零。

以下是上述方法的实现:

## C++

```
// C++ program to check if a triangle
// of positive area is possible with
// the given angles
#include <bits/stdc++.h>
using namespace std;

string isTriangleExists(int a, int b, int c)
{
    // Checking if the sum of three
    // angles is 180 and none of
    // the angles is zero
    if(a != 0 && b != 0 && c != 0 && (a + b + c)== 180)
        // Checking if sum of any two angles
        // is greater than equal to the third one
        if((a + b)>= c || (b + c)>= a || (a + c)>= b)
            return "YES";
        else
            return "NO";
    else
        return "NO";
}
// Driver Code
int main()
{
int a=50, b=60, c = 70;
cout << isTriangleExists(a, b, c) << endl;
return 0;
}
// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a triangle
// of positive area is possible with
// the given angles

class GFG
{
static String isTriangleExists(int a, int b, int c)
{
    // Checking if the sum of three
    // angles is 180 and none of
    // the angles is zero
    if(a != 0 && b != 0 && c != 0 && (a + b + c)== 180)
        // Checking if sum of any two angles
        // is greater than equal to the third one
        if((a + b)>= c || (b + c)>= a || (a + c)>= b)
            return "YES";
        else
            return "NO";
    else
        return "NO";
}
// Driver Code
public static void main(String[] args)
{
int a=50, b=60, c = 70;
System.out.println(isTriangleExists(a, b, c));
}
}
// This code is contributed by mits
```

## 计算机编程语言

```
# Python program to check if a triangle
# of positive area is possible with
# the given angles

def isTriangleExists(a, b, c):
    # Checking if the sum of three
    # angles is 180 and none of
    # the angles is zero
    if(a != 0 and b != 0 and c != 0 and (a + b + c)== 180):
        # Checking if sum of any two angles
        # is greater than equal to the third one
        if((a + b)>= c or (b + c)>= a or (a + c)>= b):
            return "YES"
        else:
            return "NO"
    else:
        return "NO"

# Driver Code
a, b, c = 50, 60, 70

print(isTriangleExists(50, 60, 70))
```

## C#

```
// C# program to check if a triangle
// of positive area is possible with
// the given angles
class GFG
{
static string isTriangleExists(int a,
                               int b,
                               int c)
{
    // Checking if the sum of three
    // angles is 180 and none of
    // the angles is zero
    if(a != 0 && b != 0 &&
       c != 0 && (a + b + c) == 180)

        // Checking if sum of any two
        // angles is greater than equal
        // to the third one
        if((a + b) >= c || (b + c) >= a ||
                           (a + c) >= b)
            return "YES";
        else
            return "NO";
    else
        return "NO";
}

// Driver Code
static void Main()
{
    int a = 50, b = 60, c = 70;
    System.Console.WriteLine(isTriangleExists(a, b, c));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a triangle
// of positive area is possible with
// the given angles

function isTriangleExists($a, $b, $c)
{
    // Checking if the sum of three
    // angles is 180 and none of
    // the angles is zero
    if($a != 0 && $b != 0 &&
       $c != 0 && ($a + $b + $c) == 180)

        // Checking if sum of any two
        // angles is greater than equal
        // to the third one
        if(($a + $b)>= $c ||
           ($b + $c)>= $a || ($a + $c)>= $b)
            return "YES";
        else
            return "NO";
    else
        return "NO";
}

// Driver Code
$a = 50;
$b = 60;
$c = 70;
echo isTriangleExists($a, $b, $c);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to check if a triangle
// of positive area is possible with
// the given angles   
function isTriangleExists(a , b , c)
{

        // Checking if the sum of three
        // angles is 180 and none of
        // the angles is zero
        if (a != 0 && b != 0 && c != 0 && (a + b + c) == 180)

            // Checking if sum of any two angles
            // is greater than equal to the third one
            if ((a + b) >= c || (b + c) >= a || (a + c) >= b)
                return "YES";
            else
                return "NO";
        else
            return "NO";
    }

    // Driver Code
    var a = 50, b = 60, c = 70;
    document.write(isTriangleExists(a, b, c));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
YES
```