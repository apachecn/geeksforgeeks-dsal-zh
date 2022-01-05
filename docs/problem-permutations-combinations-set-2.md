# 排列组合问题|第二集

> 原文:[https://www . geesforgeks . org/problem-排列-组合-set-2/](https://www.geeksforgeeks.org/problem-permutations-combinations-set-2/)

前提:[排列组合](https://www.geeksforgeeks.org/permutation-and-combination/)

**给定一个有 m 条边的多边形，计算可以使用多边形顶点形成的三角形的数量。**

> 回答:【m(m–1)(m–2)/6】
> 说明:一个有 m 条边的多边形有 m 个顶点。我们需要计算从 m 中选择的三个点的不同[组合](https://www.geeksforgeeks.org/permutation-and-combination/)，所以答案是<sup>m</sup>C<sub>3</sub>= m *(m–1)*(m–2)/6
> 示例:
> 输入:m = 3
> 输出:1
> 我们放入 m = 3 的值，我们得到所需的三角形数量= 3 * 2 * 1 / 6 = 1
> 
> 输入:m = 6
> 输出:20

**给定一个有 m 条边的多边形，计算利用多边形顶点可以形成的对角线数。**

> 回答:[m(m–3)]/2。
> 说明:我们需要从多边形中选择两个顶点。我们可以选择第一个顶点 m 种方式。我们可以用 m-3 种方式选择第二个顶点(注意，我们不能选择相邻的两个顶点形成对角线)。所以总数是 m *(m–3)。这是组合总数的两倍，因为我们考虑了两次对角边 u-v(u-v 和 v-u)
> 示例:
> 输入 m = 4
> 输出:2
> 我们将 m 的值设为 4，我们得到所需对角线的数量= 4 *(4–3)/2 = 2
> 
> 输入:m = 5
> 输出:5

**统计可以用 m 条垂直线和 n 条水平线形成的矩形总数**

> 答案:(<sup>m</sup>C<sub>2</sub>*<sup>n</sup>C<sub>2</sub>)。
> 我们需要选择两条垂直线和两条水平线。因为垂直线和水平线是独立选择的，所以我们将结果相乘。
> 示例:
> 输入:m = 2，n = 2
> 输出:1
> 我们有矩形的总数
> =<sup>2</sup>C<sub>2</sub>*<sup>2</sup>C<sub>2</sub>T22】= 1 * 1 = 1
> 
> 输入:m = 4，n = 4
> 输出:36

**一个平面上有‘n’个点，其中‘m’个点共线。求以点为顶点形成的三角形的个数？**

> 三角形的数量=**<sup>n</sup>C<sub>3</sub>–<sup>m</sup>C<sub>3</sub>**
> 说明:考虑例子 n = 10，m = 4。共有 10 个点，其中 4 个共线。这十个点中的任何三个点将构成一个三角形。因此，形成一个三角形相当于选择 10 个点中的任何三个。在 <sup>n</sup> C <sub>3</sub> 方式的 10 个点中可以选择三个点。
> 三点不共线时 10 个点形成的三角形数=<sup>10</sup>C<sub>3</sub>……(I)
> 同样，三点不共线时 4 个点形成的三角形数=<sup>4</sup>C<sub>3</sub>………..㈡
> 
> 由于这 4 个点形成的三角形无效，因此所需形成的三角形数量=<sup>10</sup>C<sub>3</sub>–<sup>4</sup>C<sub>3</sub>= 120–4 = 116

**一个平面上有‘n’个点，其中‘m’个点共线，计算两点连接形成的不同直线的数量。**

> 答:<sup>n</sup>C<sub>2</sub>–<sup>m</sup>C<sub>2</sub>+1
> 说明:n 个点无共线时形成的直线数=<sup>n</sup>C<sub>2</sub>T13】同样，m 个点无共线时形成的直线数=<sup>m</sup>C<sub>2</sub>T18】m 个点共线后减少所以我们减去 <sup>m</sup> C <sub>2</sub> 再加 1。
> 遂答=<sup>n</sup>C<sub>2</sub>–<sup>m</sup>C<sub>2</sub>+1
> 例:
> 输入:n = 4，m = 3
> 输出:1
> 我们应用此公式
> 答=<sup>4</sup>C<sub>2</sub>–<sup>3</sup>C<sub>2</sub>

**更多排列组合练习题:**
[排列组合小测验](https://www.geeksforgeeks.org/permutation-and-combination-gq/)
[组合排列练习题](https://www.geeksforgeeks.org/combination-permutation-practice-questions/)