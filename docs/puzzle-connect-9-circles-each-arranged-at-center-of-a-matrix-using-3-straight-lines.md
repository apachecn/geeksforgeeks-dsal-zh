# 拼图|用 3 条直线连接 9 个排列在矩阵中心的圆

> 原文:[https://www . geeksforgeeks . org/拼图-连接-9 圈-每个圈-排列在矩阵中心-使用-3 条直线/](https://www.geeksforgeeks.org/puzzle-connect-9-circles-each-arranged-at-center-of-a-matrix-using-3-straight-lines/)

考虑 9 个圆，每个圆排列在 3*3 形状的二维矩阵的单元中心。在不将笔从纸上移开的情况下画出 **3 条直线**，使得 9 个圆中的每一个都与至少一条线接触。

**解决方案:**
这里也有类似的问题[用 4 条线连接 9 个点。](www.geeksforgeeks.org/puzzle-draw-4-straight-line-33-matrix-9-dots/)
与上面问题的区别在于这里有 9 个圈而不是 9 个点。**同样我们只能画 3 条线。**
这样一种做被要求的事情的方式是:

![](img/46ccd475c1de30a63c2b1a5d072f517c.png)

需要注意的是，因为这些是圆，不是点，所以我们可以画一条与圆相切的线。不需要通过中心线，因为只需要与圆接触。