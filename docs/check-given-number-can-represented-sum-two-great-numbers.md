# 检查给定的数是否可以表示为两个大数之和

> 原文:[https://www . geesforgeks . org/check-给定数字-可表示-和-二-伟大数字/](https://www.geeksforgeeks.org/check-given-number-can-represented-sum-two-great-numbers/)

给我们一个数字 N，我们需要检查给定的数字 N 是否可以表示为两个**大**数的和。如果是，则打印这两个大数字，否则打印编号。大数字是以下列形式表示的数字:((b)*(b+1)*(2*b+1))/6 其中 b 是自然数。

示例:

```
Input  : N = 35
Output : 5 and 30

Input  : 105
Output : 14 and 91

Input : 99
Output : No the given number is not 
a sum of two great numbers

```

正如我们所知((b)*(b+1)*(2*b+1))/6 其中 b 是自然数表示前 b 个自然数的平方和。例如，如果 b = 3，那么 1+4+9 = 14。因此，为了检查输入数 n 是否可以表示为两个大数之和，我们将首先计算数组中小于 n 的所有大数。然后，我们将使用两个指针的方法来找到比可以加起来给定数字 n 的对。

为了计算所有大数的数组，我们将迭代 i=0 到 i <n and="" then="" in="" a="" variable="" temp="" we="" will="" add="" i="" at="" last="" of="" every="" iteration="" store="" it.="" using="" two="" pointer="" approach="" check="" if="" the="" given="" array="" contains="" pair="" such="" that="" it="" sums="" up="" to="" n="" print="" them="" other="" wise="" no.="" java="" program="" find="" number="" is="" sum="" great="" numbers="" import="" java.util.arraylist="" class="" greatnumbersum="" o="" time="" auxiliary="" space="" public="" static="" void="" greatnumbercomputation="" precompute="" all="" less="" than="" arraylist="" arr="new" traverse="" from="" square="" current="" with="" previous="" index="" int="" for="" arr.add="" a.length="" countpairs="" tar="" here="" already="" sorted="" so="" can="" lo="0," hi="arr.length" boolean="" while="" both="" pointers="" equal="" target="" system.out.println="" hi--="" else="" increment="" lower="" increase="" greater="" decrement="" higher="" decrease="" no="" single="" was="" found="" be="" false="" not="" driver="" code="" main="" args="" output:="">14 和 91</n>

时间复杂度:O(N)
辅助空间:O(N)

本文由 [**Sanket Singh 2**](https://auth.geeksforgeeks.org/profile.php?user=Sanket Singh 2) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。