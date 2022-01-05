# Python |长方体总表面积的百分比增加

> 原文:[https://www . geeksforgeeks . org/python-长方体总表面积增加百分比/](https://www.geeksforgeeks.org/python-percentage-increase-in-the-total-surface-area-of-the-cuboid/)

给定一个长度为 **L** 、宽度为 **B** 和高度为 **H** 的长方体，如果长度、宽度和高度都增加了固定的百分比，那么任务就是求出长方体总表面积的百分比增加量。
**举例:**

```
Input :
L = 20, B = 30, H = 50, l = 10 %, b = 12 %, h = 15 %
Output :
26.97 %

Input :
L = 40, B = 60, H = 15, l = 5 %, b = 7 %, h = 12 %
Output :
14.88 %
```

**代码:Python 代码求长方体总表面积的增加。**

## 蟒蛇 3

```
# Function to return the percentage increase
# in the total surface area of the cuboid
# Total surface area of a cuboid = 2(L * B) + (L * H) + (B * H)
def increaseIntsa(L, B, H, l, b, h):
    oldsurfacearea = 2*((L * B) + (L * H) + (B * H))
    newsurfacearea = 2*((L + (L * l * 0.01))*(B + (B * b*0.01)) +
                        (L + (L * l * 0.01))*(H + (H * h*0.01)) +
                        (B + (B * b * 0.01))*(H + (H * h*0.01)))
    increase = (newsurfacearea - oldsurfacearea)
    increasepercent = (increase / oldsurfacearea) * 100
    return(increasepercent)

# Cuboid dimensions
L = 20
B = 30
H = 50

# percentage increase
l = 10
b = 12
h = 15
print(increaseIntsa(L, B, H, l, b, h), "%")
```

**输出:**

```
26.974193548387092 %
```