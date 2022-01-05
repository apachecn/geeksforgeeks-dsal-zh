# 将 RGB 颜色模型更改为 HSV 颜色模型的程序

> 原文:[https://www . geesforgeks . org/program-change-RGB-color-model-HSV-color-model/](https://www.geeksforgeeks.org/program-change-rgb-color-model-hsv-color-model/)

给定 RGB 颜色范围，我们的任务是将 RGB 颜色转换为 HSV 颜色。
**RGB 颜色模型:**
RGB 颜色模型是一种加色模型，其中红色、绿色和蓝色光以各种方式添加在一起，以再现广泛的颜色。该型号的名称来自三种附加原色红、绿、蓝的首字母。

**HSV 色彩模型:**
HSV –(色相、饱和度、值)，也称为 HSB(色相、饱和度、亮度)，经常被艺术家使用，因为用色相和饱和度来考虑一种颜色往往比用加色或减色成分来考虑更自然。HSV 是一个 RGB 颜色空间的变换，它的组成部分和色度学是相对于它所源自的 RGB 颜色空间的。

**例:**

```
Input : r, g, b = 45, 215, 0
Output :
h, s, v = 107.44186046511628, 100.0, 84.31372549019608

Input : r, g, v = 31, 52, 29
Output :
h, s, v = 114.78260869565217, 44.230769230769226, 20.392156862745097
```

> **进场:**
> 
> 1.  将 r、g、b 除以 255
> 2.  计算 cmax、cmin、差值
> 3.  色调计算:
>     *   如果 cmax 和 cmin 等于 0，则 h = 0
>     *   如果 cmax 等于 r，则计算 h =(60 *(g–b)/diff)+360)% 360
>     *   如果 cmax 等于 g，则计算 h =(60 *(b–r)/diff)+120)% 360
>     *   如果 cmax 等于 b，则计算 h =(60 *(r–g)/diff)+240)% 360
> 4.  饱和度计算:
>     *   如果 cmax = 0，则 s = 0
>     *   如果 cmax 不等于 0，则计算 s = (diff/cmax)*100
> 5.  价值计算:
>     *   v = cmax*100

以下是上述方法的实施:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program change RGB Color
// Model to HSV Color Model
class GFG
{

    static void rgb_to_hsv(double r, double g, double b)
    {

        // R, G, B values are divided by 255
        // to change the range from 0..255 to 0..1
        r = r / 255.0;
        g = g / 255.0;
        b = b / 255.0;

        // h, s, v = hue, saturation, value
        double cmax = Math.max(r, Math.max(g, b)); // maximum of r, g, b
        double cmin = Math.min(r, Math.min(g, b)); // minimum of r, g, b
        double diff = cmax - cmin; // diff of cmax and cmin.
        double h = -1, s = -1;

        // if cmax and cmax are equal then h = 0
        if (cmax == cmin)
            h = 0;

        // if cmax equal r then compute h
        else if (cmax == r)
            h = (60 * ((g - b) / diff) + 360) % 360;

        // if cmax equal g then compute h
        else if (cmax == g)
            h = (60 * ((b - r) / diff) + 120) % 360;

        // if cmax equal b then compute h
        else if (cmax == b)
            h = (60 * ((r - g) / diff) + 240) % 360;

        // if cmax equal zero
        if (cmax == 0)
            s = 0;
        else
            s = (diff / cmax) * 100;

        // compute v
        double v = cmax * 100;
        System.out.println("(" + h + " " + s + " " + v + ")");

    }

    // Driver Code
    public static void main(String[] args)
    {
        // rgb_to_hsv(45, 215, 0);
        // rgb_to_hsv(31, 52, 29);
        rgb_to_hsv(129, 88, 47);

    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program change RGB Color
# Model to HSV Color Model

def rgb_to_hsv(r, g, b):

    # R, G, B values are divided by 255
    # to change the range from 0..255 to 0..1:
    r, g, b = r / 255.0, g / 255.0, b / 255.0

    # h, s, v = hue, saturation, value
    cmax = max(r, g, b)    # maximum of r, g, b
    cmin = min(r, g, b)    # minimum of r, g, b
    diff = cmax-cmin       # diff of cmax and cmin.

    # if cmax and cmax are equal then h = 0
    if cmax == cmin:
        h = 0

    # if cmax equal r then compute h
    elif cmax == r:
        h = (60 * ((g - b) / diff) + 360) % 360

    # if cmax equal g then compute h
    elif cmax == g:
        h = (60 * ((b - r) / diff) + 120) % 360

    # if cmax equal b then compute h
    elif cmax == b:
        h = (60 * ((r - g) / diff) + 240) % 360

    # if cmax equal zero
    if cmax == 0:
        s = 0
    else:
        s = (diff / cmax) * 100

    # compute v
    v = cmax * 100
    return h, s, v

''' Driver Code '''
# print(rgb_to_hsv(45, 215, 0))
# print(rgb_to_hsv(31, 52, 29))

print(rgb_to_hsv(129, 88, 47))
```

## C#

```
// C# program change RGB Color
// Model to HSV Color Model
using System;

class GFG
{

    static void rgb_to_hsv(double r, double g, double b)
    {

        // R, G, B values are divided by 255
        // to change the range from 0..255 to 0..1
        r = r / 255.0;
        g = g / 255.0;
        b = b / 255.0;

        // h, s, v = hue, saturation, value
        double cmax = Math.Max(r, Math.Max(g, b)); // maximum of r, g, b
        double cmin = Math.Min(r, Math.Min(g, b)); // minimum of r, g, b
        double diff = cmax - cmin; // diff of cmax and cmin.
        double h = -1, s = -1;

        // if cmax and cmax are equal then h = 0
        if (cmax == cmin)
            h = 0;

        // if cmax equal r then compute h
        else if (cmax == r)
            h = (60 * ((g - b) / diff) + 360) % 360;

        // if cmax equal g then compute h
        else if (cmax == g)
            h = (60 * ((b - r) / diff) + 120) % 360;

        // if cmax equal b then compute h
        else if (cmax == b)
            h = (60 * ((r - g) / diff) + 240) % 360;

        // if cmax equal zero
        if (cmax == 0)
            s = 0;
        else
            s = (diff / cmax) * 100;

        // compute v
        double v = cmax * 100;
        Console.WriteLine("(" + h + " " + s + " " + v + ")");

    }

    // Driver Code
    public static void Main(String[] args)
    {
        // rgb_to_hsv(45, 215, 0);
        // rgb_to_hsv(31, 52, 29);
        rgb_to_hsv(129, 88, 47);

    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program change RGB Color
// Model to HSV Color Model   
function rgb_to_hsv(r , g , b) {

        // R, G, B values are divided by 255
        // to change the range from 0..255 to 0..1
        r = r / 255.0;
        g = g / 255.0;
        b = b / 255.0;

        // h, s, v = hue, saturation, value
        var cmax = Math.max(r, Math.max(g, b)); // maximum of r, g, b
        var cmin = Math.min(r, Math.min(g, b)); // minimum of r, g, b
        var diff = cmax - cmin; // diff of cmax and cmin.
        var h = -1, s = -1;

        // if cmax and cmax are equal then h = 0
        if (cmax == cmin)
            h = 0;

        // if cmax equal r then compute h
        else if (cmax == r)
            h = (60 * ((g - b) / diff) + 360) % 360;

        // if cmax equal g then compute h
        else if (cmax == g)
            h = (60 * ((b - r) / diff) + 120) % 360;

        // if cmax equal b then compute h
        else if (cmax == b)
            h = (60 * ((r - g) / diff) + 240) % 360;

        // if cmax equal zero
        if (cmax == 0)
            s = 0;
        else
            s = (diff / cmax) * 100;

        // compute v
        var v = cmax * 100;
        document.write("(" + h.toFixed(1) + ", " + s + ", " + v + ")");

    }

    // Driver Code

        // rgb_to_hsv(45, 215, 0);
        // rgb_to_hsv(31, 52, 29);
        rgb_to_hsv(129, 88, 47);

// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
(30.0, 63.56589147286821, 50.588235294117645) 
```