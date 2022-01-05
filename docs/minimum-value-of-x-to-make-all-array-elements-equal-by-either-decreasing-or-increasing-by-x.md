# X 的最小值，通过减少或增加 X 使所有数组元素相等

> 原文:[https://www . geesforgeks . org/x 的最小值使所有数组元素等于 x 的减或增/](https://www.geeksforgeeks.org/minimum-value-of-x-to-make-all-array-elements-equal-by-either-decreasing-or-increasing-by-x/)

*   将任意数组元素增加 **X** 一次。
*   将任意数组元素减少 **X** 一次。
*   如果有 3 个唯一的元素，如果**ABS(el2-el1)= = ABS(el3-el2)**，那么答案就是 **abs(el2-el1)** 。如果它们不相等，那么答案是-1。
*   如果有 2 个唯一元素，答案是**(el2–el1)/2**，如果**el2–el1**为偶数，否则答案是(el2–el1)
*   如果存在单一唯一元素，那么答案是 **0**

**时间复杂度:** O(N)

**辅助空间:** O(N)