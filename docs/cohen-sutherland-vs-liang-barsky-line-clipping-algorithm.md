# 科恩-萨瑟兰 vs 梁-巴尔斯基线裁剪算法

> 原文:[https://www . geesforgeks . org/Cohen-Sutherland-vs-Liang-bar sky-line-clipping-algorithm/](https://www.geeksforgeeks.org/cohen-sutherland-vs-liang-barsky-line-clipping-algorithm/)

**[科恩-萨瑟兰线裁剪算法](https://www.geeksforgeeks.org/line-clipping-set-1-cohen-sutherland-algorithm/) :**
它是一种线裁剪算法。其中二维空间(线位于其中)被分成 **9** 区域，然后在感兴趣的中心区域中可见的线和线的部分被有效地确定。它可以快速检测并省去两个常见且琐碎的案例。由**丹尼·科恩****伊凡·苏泽兰**开发。

**[【梁-巴尔斯基线裁剪算法】:](https://www.geeksforgeeks.org/liang-barsky-algorithm/)**
也是一种线裁剪算法。在该算法中，使用了线的参数方程，并求解了四个不等式来寻找线在视口中的参数范围。由**优-梁冬**和**布莱恩·巴斯基**开发。

下表详细指出了两种算法的**差异。**

| 没有 | 工厂 | 科恩·萨瑟兰算法 | 梁-巴斯基算法 |
| --- | --- | --- | --- |
| 1. | 效率 | 效率较低。 | 效率更高。 |
| 2. | 操作 | 在这个算法中，每个交集都需要乘法和除法。 | 在该算法中，每次参数更新只需要一次除法。 |
| 3. | 方法 | 它遵循编码方法。 | 它遵循参数化方法。 |
| 4. | 计算 | 它会重复计算沿直线路径的交点，即使该直线可能完全在剪辑窗口之外。 | 在这种情况下，当计算出最终值时，只计算一次窗口交点。 |
| 5. | 使用 | 它只能在矩形剪辑窗口上使用。 | 它可以用于一维、二维、三维线裁剪，有时也可以用于四维线裁剪。 |