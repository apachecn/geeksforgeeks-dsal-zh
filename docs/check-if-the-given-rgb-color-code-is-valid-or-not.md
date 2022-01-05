# 检查给定的 RGB 颜色代码是否有效

> 原文:[https://www . geesforgeks . org/check-如果给定的 rgb 颜色代码有效或无效/](https://www.geeksforgeeks.org/check-if-the-given-rgb-color-code-is-valid-or-not/)

给定三个数字 **R** 、 **G** 和 **B** 分别作为红、绿、蓝的颜色代码，形式为 **RGB 颜色代码**。任务是知道给定的颜色代码是否有效。

> **RGB 格式:**RGB(红、绿、蓝)格式用于通过指定 0 到 255 之间的 R、G、B 值来定义 HTML 元素的颜色。例如:红色的 RGB 值为(255，0，0)，绿色为(0，255，0)，蓝色为(0，0，255)等。
> 
> 颜色:rgb(R、g、b)；

**注意:**当所有数字都在[0，255]范围内时，颜色代码有效。

**示例:**

> **输入:** R=0，G=100，B=255
> **输出:**真
> **说明:**每种颜色都在【0，255】范围内
> 
> **输入:** R=0，G=200，B=355
> **输出:**假
> **说明:**蓝色不在范围内【0，255】

**方法:**要检查颜色代码是否有效，我们需要检查每种颜色是否在[0，255]范围内。如果任何颜色不在此范围内，则返回 false，否则返回 true。

以下是该方法的实施情况:

## C++

```
#include <iostream>
using namespace std;

// Function to check validity
// of the color code
bool isValidRGB(int R, int G, int B)
{

    if (R < 0 || R > 255)
        return false;
    else if (G < 0 || G > 255)
        return false;
    else if (B < 0 || B > 255)
        return false;
    else
        return true;
}

// Driver code
int main()
{

    int R, G, B;

    // Check if rgb(0, 0, 0) is valid or not
    R = 0, G = 0, B = 0;
    (isValidRGB(R, G, B)) ? cout << "true\n"
                          : cout << "false\n";

    // Check if rgb(0, 100, 255) is valid or not
    R = 0, G = 100, B = 255;
    (isValidRGB(R, G, B)) ? cout << "true\n"
                          : cout << "false\n";

    // Check if rgb(0, 200, 355) is valid or not
    R = 0, G = 200, B = 355;
    (isValidRGB(R, G, B)) ? cout << "true\n"
                          : cout << "false\n";

    // Check if rgb(-100, 0, 255) is valid or not
    R = -100, G = 0, B = 255;
    (isValidRGB(R, G, B)) ? cout << "true\n"
                          : cout << "false\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // Function to check validity
    // of the color code
    public static boolean isValidRGB(int R, int G, int B) {

        if (R < 0 || R > 255)
            return false;
        else if (G < 0 || G > 255)
            return false;
        else if (B < 0 || B > 255)
            return false;
        else
            return true;
    }

    // Driver code
    public static void main(String args[]) {

        int R, G, B;

        // Check if rgb(0, 0, 0) is valid or not
        R = 0;
        G = 0;
        B = 0;
        if (isValidRGB(R, G, B))
            System.out.println("true");
        else
            System.out.println("false");

        // Check if rgb(0, 100, 255) is valid or not
        R = 0;
        G = 100;
        B = 255;
        if (isValidRGB(R, G, B))
            System.out.println("true");
        else
            System.out.println("false");

        // Check if rgb(0, 200, 355) is valid or not
        R = 0;
        G = 200;
        B = 355;
        if (isValidRGB(R, G, B))
            System.out.println("true");
        else
            System.out.println("false");

        // Check if rgb(-100, 0, 255) is valid or not
        R = -100;
        G = 0;
        B = 255;
        if (isValidRGB(R, G, B))
            System.out.println("true");
        else
            System.out.println("false");
    }
}

// This code is contributed by saurabh_jaiswal
```

## 蟒蛇 3

```
# Function to check validity
# of the color code
def isValidRGB(R, G, B) :

    if (R < 0 or R > 255) :
        return False;

    elif (G < 0 or G > 255) :
        return False;

    elif (B < 0 or B > 255) :
        return False;

    else :
        return True;

# Driver code
if __name__ ==  "__main__" :

    # Check if rgb(0, 0, 0) is valid or not
    R = 0; G = 0; B = 0;

    if isValidRGB(R, G, B) :
        print("true")
    else :
        print("false")

    # Check if rgb(0, 100, 255) is valid or not
    R = 0; G = 100; B = 255;

    if isValidRGB(R, G, B) :
        print("true")
    else :
        print("false")

    # Check if rgb(0, 200, 355) is valid or not
    R = 0; G = 200; B = 355;

    if isValidRGB(R, G, B) :
        print("true")
    else :
        print("false")

    # Check if rgb(-100, 0, 255) is valid or not
    R = -100; G = 0; B = 255;

    if isValidRGB(R, G, B) :
        print("true")
    else :
        print("false")

    # This code is contributed by AnkThon
```

## C#

```
using System;
public class GFG {

    // Function to check validity
    // of the color code
    public static bool isValidRGB(int R, int G, int B) {

        if (R < 0 || R > 255)
            return false;

        else if (G < 0 || G > 255)
            return false;

        else if (B < 0 || B > 255)
            return false;

        else
            return true;
    }

    // Driver code
    public static void Main(string []args) {

        int R, G, B;

        // Check if rgb(0, 0, 0) is valid or not
        R = 0;
        G = 0;
        B = 0;
        if (isValidRGB(R, G, B))
            Console.WriteLine("true");
        else
            Console.WriteLine("false");

        // Check if rgb(0, 100, 255) is valid or not
        R = 0;
        G = 100;
        B = 255;
        if (isValidRGB(R, G, B))
            Console.WriteLine("true");
        else
            Console.WriteLine("false");

        // Check if rgb(0, 200, 355) is valid or not
        R = 0;
        G = 200;
        B = 355;
        if (isValidRGB(R, G, B))
            Console.WriteLine("true");
        else
            Console.WriteLine("false");

        // Check if rgb(-100, 0, 255) is valid or not
        R = -100;
        G = 0;
        B = 255;
        if (isValidRGB(R, G, B))
            Console.WriteLine("true");
        else
            Console.WriteLine("false");
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

    // Function to check validity
    // of the color code
    const isValidRGB = (R, G, B) => {

        if (R < 0 || R > 255)
            return false;
        else if (G < 0 || G > 255)
            return false;
        else if (B < 0 || B > 255)
            return false;
        else
            return true;
    }

    // Driver code

    let R, G, B;

    // Check if rgb(0, 0, 0) is valid or not
    R = 0, G = 0, B = 0;
    (isValidRGB(R, G, B)) ? document.write("true<br/>")
        : document.write("false<br/>");

    // Check if rgb(0, 100, 255) is valid or not
    R = 0, G = 100, B = 255;
    (isValidRGB(R, G, B)) ? document.write("true<br/>")
        : document.write("false<br/>");

    // Check if rgb(0, 200, 355) is valid or not
    R = 0, G = 200, B = 355;
    (isValidRGB(R, G, B)) ? document.write("true<br/>")
        : document.write("false<br/>");

    // Check if rgb(-100, 0, 255) is valid or not
    R = -100, G = 0, B = 255;
    (isValidRGB(R, G, B)) ? document.write("true<br/>")
        : document.write("false<br/>");

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
true
true
false
false
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)