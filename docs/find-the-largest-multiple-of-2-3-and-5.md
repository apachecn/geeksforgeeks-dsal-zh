# 求 2、3、5 的最大倍数

> 原文:[https://www . geesforgeks . org/find-2-3-5 的最大倍数/](https://www.geeksforgeeks.org/find-the-largest-multiple-of-2-3-and-5/)

给出了一个大小为 n 的数组。数组包含从 0 到 9 的数字。使用数组中的数字生成最大的数字，使该数字可被 2、3 和 5 整除。
例如，如果数组是{1，8，7，6，0}，输出必须是:8760。如果数组是{7，7，7，6}，输出必须是:“不能形成数字”。

来源:[亚马逊采访|第七集](https://www.geeksforgeeks.org/microsoft-interview-set-7-2/)

这个问题是“[求 3 的最大倍数](https://www.geeksforgeeks.org/find-the-largest-number-multiple-of-3/)的变种。

因为数字必须能被 2 和 5 整除，所以最后一位必须是 0。所以如果给定的数组不包含任何零，那么就不存在解。

一旦 0 可用，就从给定数组中提取 0。唯一剩下的是，这个数应该能被 3 整除，并且是所有数中最大的。这里已经讨论过了。

发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。