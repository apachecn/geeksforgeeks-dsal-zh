# 几何级数求和程序

> 原文:[https://www.geeksforgeeks.org/program-sum-geometric-series/](https://www.geeksforgeeks.org/program-sum-geometric-series/)

几何级数是连续项之间具有恒定比率的级数。级数的第一项用 **a** 表示，公比用 **r** 表示。系列看起来是这样的:- **a，ar，ar <sup>2</sup> ，ar <sup>3</sup> ，ar <sup>4</sup> 。。。**。任务是找到这样一个级数的和。

**示例:**

```
Input : a = 1
        r = 0.5
        n = 10
Output : 1.99805

Input : a = 2
        r = 2
        n = 15
Output : 65534

```

一个**简单解**来计算几何级数的和。

## C++