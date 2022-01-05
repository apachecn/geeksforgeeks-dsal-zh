# Python |如果半径增加，半球体积增加的百分比

> 原文:[https://www . geeksforgeeks . org/python-百分比-半球增加-体积-如果半径增加/](https://www.geeksforgeeks.org/python-percentage-increase-in-hemisphere-volume-if-radius-is-increased/)

假设半球的半径增加了一个固定的百分比，那么目标是计算半球体积增加的百分比。

> **例:**
> **输入:**
> 20
> **输出:**
> 72.8 %
> 
> **输入:**T2 70
> T4【输出:T6】391.3%

**进场:**
让，半球半径= ![a](img/6afcd73f7a647e96831df2711ab82fb0.png "Rendered by QuickLaTeX.com")
给定百分比增加= ![x%](img/123b6cc9f3fbdb8d739eb01a1dc95060.png "Rendered by QuickLaTeX.com")
体积增加前= ![\frac{2}{3} * 3.14*a^3](img/ab49624ff4e9e9490d419ede518e86c8.png "Rendered by QuickLaTeX.com")
新半径增加后= ![a + \frac{ax}{100}](img/71715b81b8bd8a73cf76f7c44529be25.png "Rendered by QuickLaTeX.com")
所以，新体积= ![\frac{2}{3}*3.14*(a^3 + (\frac{ax}{100})^3 + \frac{3a^3x}{100} + \frac{3a^3x^2}{10000})](img/a6cd6d6034e73bfe228cfcb7e55c3a0f.png "Rendered by QuickLaTeX.com")
体积变化= ![\frac{2}{3}*3.14*((\frac{ax}{100})^3 + \frac{3a^3x}{100} + \frac{3a^3x^2}{10000})](img/82a656a567eb7809f4e4d7ce9fe76d0c.png "Rendered by QuickLaTeX.com")
体积增加百分比= ![(\frac{2}{3}*3.14*((\frac{ax}{100})^3 + \frac{3a^3x}{100} + \frac{3a^3x^2}{10000})/\frac{2}{3}*3.14*a^3) * 100 = \frac{x^3}{10000} + 3x + \frac{3x^2}{100}](img/befd7a12f3c77dd34078ef389aa2e5ba.png "Rendered by QuickLaTeX.com")

**下面是上述方法的 Python 代码实现。**

```
# Python3 program to find percentage increase 
# in the volume of the hemisphere 
# if the radius is increased by a given percentage 

def newvol(x): 

    print("percentage increase in the  volume of the"
          " hemisphere is ", pow(x, 3) / 10000 + 3 * x 
                + (3 * pow(x, 2)) / 100, "%") 

# Driver code 
x = 10.0
newvol(x) 
```

**输出:**

```
percentage increase in the volume of the hemisphere is  33.1 %
```