# 亚马逊面试|第 40 集(校内第一轮)

> 原文:[https://www . geesforgeks . org/Amazon-interview-set-40-campus-round-1/](https://www.geeksforgeeks.org/amazon-interview-set-40-campus-round-1/)

20 个客观类型问题(技术类:操作系统、Java、网络)和 2 个程序。给出的时间是 90 分钟。

1)最长剩余时间计划

2)螺纹

3)子网掩码–CLaSS b–64 个部门

4)匹配以下
SMTP
BGP
TCP
PPP

5)关于递归，f(513，2)的值

```
 if(n<0)
   return 0;
 else 
   return ( n%10 + f(n/10, 2) )
```

6)复杂性？

```
f(i) = 2*f(i+1) + 3*f(i+2)
For (int i=0; i < n; i++)
   F[i] = 2*f[i+1] 
```

7)青蛙走 1 步、2 步或 3 步到达顶部。它以多少种方式到达顶端？
基于递归，选项
a)f(I)= f(I+1)+f(I+2)+f(I+3)+1
b)f(I)= f(I-1)+f(I-2)+f(I-3)+1
c)f(I)= f(I+1)+f(I+2)+f(I+3)
d)f(I)= f(I-1)+f(I-2)+1

8)基于 java 2 的问题，一个来自异常

9)给出了前序，我们必须找出后序

10)内存管理，pa = 32 位，la = 36 位，帧 size=2^12，第一页条目，第二页条目

11)这个问题来自 GATE CS 之前的试题卷

```
   for (int i=0; i < n; i++)
    Fork();
   No of child process?
```

**程序:**
1) [打印二叉树左视图](https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1)

2)3 个链表之和

```
 Digit..   123------1->2->3------------linkedlist1
       234----2->3->4--------------linkedlist2
       34567----3->4->5->6->7---linkedlist3
 Output: 34924-------3->4->9->2->4 
```

Sum(linkedlist1，linkedlist2，linkedlist3)
我们必须打印数字的 linkedlist 形式。

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

[**亚马逊所有练习题**](https://practice.geeksforgeeks.org/company/Amazon/) **！**