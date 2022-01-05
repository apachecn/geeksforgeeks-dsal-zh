# 检查给定四个整数(或边)是否构成矩形

> 原文:[https://www . geesforgeks . org/check-给定-四个整数-边-制作-矩形/](https://www.geeksforgeeks.org/check-given-four-integers-sides-make-rectangle/)

给定四个正整数，确定矩形的边长是否为 a、b、c 和 d(任意顺序)。
**例:**

```
Input : 1 1 2 2
Output : Yes

Input : 1 2 3 4
Output : No
```

**方法 1 :-** 我们将检查两个整数中是否有任何一个是相等的，并使用几个 if else 条件确保其余两个也是相等的。

## C++

```
// A simple program to find if given 4
// values can represent 4 sides of rectangle
#include <iostream>
using namespace std;

// Function to check if the given
// integers value make a rectangle
bool isRectangle(int a, int b, int c, int d)
{
    // Square is also a rectangle
    if (a == b == c == d)
        return true;

    else if (a == b && c == d)
        return true;
    else if (a == d && c == b)
        return true;
    else if (a == c && d == b)
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int a, b, c, d;
    a = 1, b = 2, c = 3, d = 4;
    if (isRectangle(a, b, c, d))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple program to find if
// given 4 values can represent
// 4 sides of rectangle
class GFG {

    // Function to check if the given
    // integers value make a rectangle
    static boolean isRectangle(int a, int b,
                               int c, int d)
    {
        // Square is also a rectangle
        if (a == b && a == c &&
            a == d && c == d &&
            b == c && b == d)
            return true;

        else if (a == b && c == d)
            return true;
        else if (a == d && c == b)
            return true;
        else if (a == c && d == b)
            return true;
        else
            return false;
    }

    // Driver code
    public static void main(String[] args)
    {

        int a = 1, b = 2, c = 3, d = 4;
        if (isRectangle(a, b, c, d))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# A simple program to find if given 4
# values can represent 4 sides of rectangle

# Function to check if the given
# integers value make a rectangle
def isRectangle(a, b, c, d):

    # check all sides of rectangle combinations
    if (a==b and d==c) or (a==c and b==d) or (a==d and b==c):
        return True
    else:    
           return False

# Driver code
a, b, c, d = 1, 2, 3, 4
print("Yes" if isRectangle(a, b, c, d) else "No")

# This code is contributed by Jatinder SIngh
```

## C#

```
// A simple program to find if
// given 4 values can represent
// 4 sides of rectangle
using System;

class GFG {

    // Function to check if the given
    // integers value make a rectangle
    static bool isRectangle(int a, int b,
                            int c, int d)
    {
        // Square is also a rectangle
        if (a == b && a == c && a == d &&
            c == d && b == c && b == d)
            return true;

        else if (a == b && c == d)
            return true;

        else if (a == d && c == b)
            return true;

        else if (a == c && d == b)
            return true;

        else
            return false;
    }

    // Driver code
    public static void Main()
    {

        int a = 1, b = 2, c = 3, d = 4;
        if (isRectangle(a, b, c, d))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// A simple program to find if
// given 4 values can represent
// 4 sides of rectangle

    // Function to check if the given
    // integers value make a rectangle
    function isRectangle(a, b, c, d)
    {
        // Square is also a rectangle
        if (a == b && a == c &&
            a == d && c == d &&
            b == c && b == d)
            return true;

        else if (a == b && c == d)
            return true;
        else if (a == d && c == b)
            return true;
        else if (a == c && d == b)
            return true;
        else
            return false;
    }

// Driver code

        let a = 1, b = 2, c = 3, d = 4;
        if (isRectangle(a, b, c, d))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**输出:**

```
No
```