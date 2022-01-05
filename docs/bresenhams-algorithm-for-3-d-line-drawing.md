# 布雷森汉三维线描算法

> 原文:[https://www . geeksforgeeks . org/bresenhams-3d 线描算法/](https://www.geeksforgeeks.org/bresenhams-algorithm-for-3-d-line-drawing/)

给定两个三维坐标，我们需要找到连接它们的线上的点。所有的点都有整数坐标。

示例:

```
Input  : (-1, 1, 1), (5, 3, -1)
Output : (-1, 1, 1), (0, 1, 1), (1, 2, 0),
          (2, 2, 0), (3, 2, 0), (4, 3, -1), 
          (5, 3, -1)

Input  : (-7, 0, -3), (2, -5, -1)
Output : (-7, 0, -3), (-6, -1, -3), (-5, -1, -3),
         (-4, -2, -2), (-3, -2, -2), (-2, -3, -2),
         (-1, -3, -2), (0, -4, -1), (1, -4, -1),
          (2, -5, -1)

```

Bresenham 算法是有效的，因为它避免了浮点算术运算。与[二维线图](https://www.geeksforgeeks.org/bresenhams-line-generation-algorithm)的情况一样，我们使用一个变量来存储斜率误差，即从实际几何线绘制的线的斜率误差。一旦斜率误差超过允许值，我们就修改数字以消除误差。

要绘制的线的驱动轴是该线行进最远的轴，即轴坐标的差异最大。因此，坐标值沿着驱动轴线性增加 1，并且斜率误差变量用于确定另一个轴的坐标值的变化。

对于二维线，我们使用一个斜率误差变量，但是对于三维线，对于每个非驱动轴，我们需要两个斜率误差变量。如果当前点是![P_{k}](img/5ed510a4095e1cc6d770fcb027850b3e.png "Rendered by QuickLaTeX.com") **(x，y，z)** ，驱动轴是正的 X 轴，那么下一个点![P_{k+1}](img/c76ea34f32b7c6b825cd6f040cd774ea.png "Rendered by QuickLaTeX.com")可能是

*   **(x+1，y，z)**
*   **(x+1，y+1，z)**
*   **(x+1，y，z+1)**
*   **(x+1，y+1，z+1)**

![Candidate points for next point on a 3D Line](img/8296c1c99c82c1821673f3ef89460f22.png)

斜率误差变量的值根据以下等式确定:-
![ py_{k+1} = py_{k} + 2dy - 2dx(y_{k+1} - y_{k})\\ pz_{k+1} = pz_{k} + 2dz - 2dx(z_{k+1} - z_{k}) ](img/d994d4995093a76159a5550075336871.png "Rendered by QuickLaTeX.com")

斜率误差变量的初始值由以下等式给出:-
![ py_{0} = 2dy - dx\\ pz_{0} = 2dz - dx ](img/63ae2a078d34d698d7ea47bfa9479005.png "Rendered by QuickLaTeX.com")
![dx, dy, dz](img/878493c8b1a4462259e598fb096e7e5c.png "Rendered by QuickLaTeX.com")这里表示两个端点沿 X、Y、Z 轴的坐标差。

**算法:-**

1.  输入两个端点，并将起始点存储为![(x_{0}, y_{0}, z_{0})](img/171c2a0ed4f03cc2e4a75b957633de25.png "Rendered by QuickLaTeX.com")
2.  剧情 ![(x_{0}, y_{0}, z_{0})](img/171c2a0ed4f03cc2e4a75b957633de25.png "Rendered by QuickLaTeX.com")
3.  计算常数![dx, dy, dz](img/878493c8b1a4462259e598fb096e7e5c.png "Rendered by QuickLaTeX.com")并通过比较
    ![dx, dy, dz](img/878493c8b1a4462259e598fb096e7e5c.png "Rendered by QuickLaTeX.com")
    的绝对值确定驱动轴如果 abs( ![dx](img/0f630b5c0e5a8d4a1945a3d2ab94f7a4.png "Rendered by QuickLaTeX.com"))最大，则 X 轴为驱动轴
    如果 abs( ![dy](img/c7c0ad627b96215b012e31d5e49041ca.png "Rendered by QuickLaTeX.com"))最大，则 Y 轴为驱动轴
    如果 abs( ![dz](img/fcfbe5188cd4e8def5b1d0fa1596d135.png "Rendered by QuickLaTeX.com"))最大，则 Z 轴为驱动轴
4.  假设 X 轴是驱动轴，那么
    ![ py_{0} = 2dy - dx\\ pz_{0} = 2dz - dx ](img/63ae2a078d34d698d7ea47bfa9479005.png "Rendered by QuickLaTeX.com")
5.  在沿线的每个![x_{k}](img/1e8c1a9938707c073527b410cc5a6d28.png "Rendered by QuickLaTeX.com")处，从 k = 0 开始，检查以下条件
    并确定下一个点:-
    *   如果![py_{k} < 0](img/61eb7f7e1f041b6c8ddd3d7c4e80e0de.png "Rendered by QuickLaTeX.com")和![pz_{k} < 0](img/15abc82c091975da607b4b9bb05121f1.png "Rendered by QuickLaTeX.com")，则
        绘制![(x_{k}+1, y_{k}, z_{k})](img/fa0af81dc9cfeef3f6dc6b63cae25827.png "Rendered by QuickLaTeX.com")和
        设置![py_{k+1}=py_{k}+2dy, pz_{k+1}=pz_{k}+2dz](img/76fc0263169187cd593c1258d2c9038e.png "Rendered by QuickLaTeX.com")
    *   否则如果![py_{k} > 0](img/e144d72198f6d381a057c9457c69ea05.png "Rendered by QuickLaTeX.com")和![pz_{k} < 0](img/15abc82c091975da607b4b9bb05121f1.png "Rendered by QuickLaTeX.com")，则
        绘制![(x_{k}+1, y_{k}+1, z_{k})](img/2f9e30622302109b285ade3dfa9a29f5.png "Rendered by QuickLaTeX.com")和
        设置![py_{k+1}=py_{k}+2dy-2dx, pz_{k+1}=pz_{k}+2dz](img/0b834ddb890d98743e9d938d138a9c1e.png "Rendered by QuickLaTeX.com")
    *   否则如果![py_{k}  0](img/65346373a748ab1ee69deb3a7737c5a5.png "Rendered by QuickLaTeX.com")，则
        出![(x_{k}+1, y_{k}, z_{k}+1)](img/6cd4d6036a8634c335612adcc6839f03.png "Rendered by QuickLaTeX.com")和
        设定![py_{k+1}=py_{k}+2dy, pz_{k+1}=pz_{k}+2dz-2dx](img/417e27bf4d96afe2212c48a34d771257.png "Rendered by QuickLaTeX.com")
    *   否则接着
        剧情![(x_{k}+1, y_{k}+1, z_{k}+1)](img/7fee1ae2d7cbb9d22aa4201a1c08440a.png "Rendered by QuickLaTeX.com")和
        设定![py_{k+1}=py_{k}+2dy-2dx, pz_{k+1}=pz_{k}+2dz-2dx](img/92168cc54dbb7a6fb05637e8ad339c19.png "Rendered by QuickLaTeX.com")T4】
6.  重复第 5 步![dx-1](img/62ae34683c2ecb4077fd46147071d2aa.png "Rendered by QuickLaTeX.com")次

## 蟒蛇 3

```
# Python3 code for generating points on a 3-D line 
# using Bresenham's Algorithm

def Bresenham3D(x1, y1, z1, x2, y2, z2):
    ListOfPoints = []
    ListOfPoints.append((x1, y1, z1))
    dx = abs(x2 - x1)
    dy = abs(y2 - y1)
    dz = abs(z2 - z1)
    if (x2 > x1):
        xs = 1
    else:
        xs = -1
    if (y2 > y1):
        ys = 1
    else:
        ys = -1
    if (z2 > z1):
        zs = 1
    else:
        zs = -1

    # Driving axis is X-axis"
    if (dx >= dy and dx >= dz):        
        p1 = 2 * dy - dx
        p2 = 2 * dz - dx
        while (x1 != x2):
            x1 += xs
            if (p1 >= 0):
                y1 += ys
                p1 -= 2 * dx
            if (p2 >= 0):
                z1 += zs
                p2 -= 2 * dx
            p1 += 2 * dy
            p2 += 2 * dz
            ListOfPoints.append((x1, y1, z1))

    # Driving axis is Y-axis"
    elif (dy >= dx and dy >= dz):       
        p1 = 2 * dx - dy
        p2 = 2 * dz - dy
        while (y1 != y2):
            y1 += ys
            if (p1 >= 0):
                x1 += xs
                p1 -= 2 * dy
            if (p2 >= 0):
                z1 += zs
                p2 -= 2 * dy
            p1 += 2 * dx
            p2 += 2 * dz
            ListOfPoints.append((x1, y1, z1))

    # Driving axis is Z-axis"
    else:        
        p1 = 2 * dy - dz
        p2 = 2 * dx - dz
        while (z1 != z2):
            z1 += zs
            if (p1 >= 0):
                y1 += ys
                p1 -= 2 * dz
            if (p2 >= 0):
                x1 += xs
                p2 -= 2 * dz
            p1 += 2 * dy
            p2 += 2 * dx
            ListOfPoints.append((x1, y1, z1))
    return ListOfPoints

def main():
    (x1, y1, z1) = (-1, 1, 1)
    (x2, y2, z2) = (5, 3, -1)
    ListOfPoints = Bresenham3D(x1, y1, z1, x2, y2, z2)
    print(ListOfPoints)

main()
```

**Output:**

```
[(-1, 1, 1), (0, 1, 1), (1, 2, 0), (2, 2, 0), (3, 2, 0), (4, 3, -1), (5, 3, -1)]

```