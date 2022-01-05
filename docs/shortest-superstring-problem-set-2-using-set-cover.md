# 最短超弦问题|集合 2(使用集合覆盖)

> 原文:[https://www . geesforgeks . org/最短-超弦-问题-集合-2-使用-集合-封面/](https://www.geeksforgeeks.org/shortest-superstring-problem-set-2-using-set-cover/)

给定一组 n 个字符串，找到给定集合中包含每个字符串的最小字符串作为子字符串。我们可以假设 arr[]中没有字符串是另一个字符串的子字符串。

示例:

```
Input:  S = {"001", "01101", "010"}
Output: 0011010  

Input:  S = {"geeks", "quiz", "for"}
Output: geeksquizfor

Input:  S = {"catg", "ctaagt", "gcta", "ttca", "atgcatc"}
Output: gctaagttcatgcatc
```

在[之前的帖子](https://www.geeksforgeeks.org/shortest-superstring-problem/)中，我们讨论了一个被证明是 4 近似(推测为 2 近似)的解。
在这篇文章中，讨论了一个可以证明为 2H <sub>n</sub> 近似的解决方案。其中 H <sub>n</sub> = 1 + 1/2 + 1/3 + … 1/n，思路是将最短超弦问题转化为[集合覆盖问题](https://www.geeksforgeeks.org/set-cover-problem-set-1-greedy-approximate-algorithm/)(集合覆盖问题是给定一个宇宙的某些子集，每个给定子集都有一个关联代价。任务是找到给定子集的最低成本集合，从而覆盖宇宙的所有元素)。对于集合覆盖问题，我们需要有一个宇宙和宇宙的子集以及它们的相关成本。

以下是将最短超弦转换为[套盖](https://www.geeksforgeeks.org/set-cover-problem-set-1-greedy-approximate-algorithm/)的步骤。

```
1) Let S be the set of given strings.
   S = {s1, s2, ... sn}

2) Universe for Set Cover problem is S (We need
   to find a superstring that has every string
   as substring)

3) Let us initialize subsets to be considered for universe as
     Subsets =  {{s1}, {s2}, ... {sn}}
   Cost of every subset is length of string in it.

3) For all pairs of strings si and sj in S,
     If si and sj overlap
      a) Construct a string rijk where k is
         the maximum overlap between the two.
      b) Add the set represented by rijk to Subsets,
           i.e., Subsets = Subsets U Set(rijk)
         The set represented by rijk is the set 
         of all strings which are substring of it.
         Cost of the subset is length of rijk.

4) Now problem is transformed to Set Cover, we can 
   run Greedy Set Cover approximate algorithm to find
   set cover of S using Subsets.  Cost of every element in
   Subsets is length of string in it.

```

**示例:**

```
S = {s1, s2, s3}.
s1 = "001"
s2 = "01101"
s3 = "010"

[Combination of s1 and s2 with 2 overlapping characters]
r122 = 001101 

[Combination of s1 and s3 with 2 overlapping characters]
r132 = 0010 

Similarly,
r232 = 011010
r311 = 01001
r321 = 0101101

Now set cover problem becomes as following:

Universe to cover is {s1, s2, s3}

Subsets of the universe and their costs :

{s1}, cost 3 (length of s1)
{s2}, cost 5 (length of s2)
{s3}, cost 5 (length of s3)

set(r122), cost 6 (length of r122)
The set r122 represents all strings which are
substrings of r122. 
Therefore set(r122) = {s1, s2}

set(r132), cost 3 (length of r132)
The subset r132 represents all strings which are
substrings of r132
Therefore set(r132) = {s1, s3}

Similarly there are more subsets for set(r232), 
set(r311), and set(r321).

So we have a set cover problem with universe and subsets
of universe with costs associated with every subset.

```

我们讨论了最短超弦问题的一个实例可以在多项式时间内转化为集合覆盖问题的一个实例。

关于基于集合覆盖的算法是 2H <sub>n</sub> 近似的证明，请参考本。

**参考:**
[http://www . cs . Dartmouth . edu/~ AC/Teach/CS105-winter 05/Notes/wan-ba-Notes . pdf](http://www.cs.dartmouth.edu/~ac/Teach/CS105-Winter05/Notes/wan-ba-notes.pdf)
[http://file admin . cs . lth . se/cs/Personal/Andrzej _ Lingas/super string . pdf](http://fileadmin.cs.lth.se/cs/Personal/Andrzej_Lingas/superstring.pdf)
T9】http://math.mit.edu/~goemans/18434S06/superstring-lele.pdf

本文由 **Dheeraj Gupta** 供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论