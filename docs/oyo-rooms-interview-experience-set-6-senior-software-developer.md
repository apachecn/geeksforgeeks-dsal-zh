# OYO 客房面试体验|第六集(高级软件开发人员)

> 原文:[https://www . geesforgeks . org/oyo-rooms-面试-体验-设置-6-高级-软件-开发人员/](https://www.geeksforgeeks.org/oyo-rooms-interview-experience-set-6-senior-software-developer/)

**第一轮:(书面)**

1.  [数组中不连续元素的最大和](https://practice.geeksforgeeks.org/problems/stickler-theif/0)

    ```
    Input : 1 12 5 4 13
    Output: 25
    ```

2.  [给定一个整数数组，找到数组中四个元素的组合，其和等于给定值 x。](https://practice.geeksforgeeks.org/problems/find-all-four-sum-numbers/0)

    ```
    Input Array : 1 5 1 0 6 0
    Input Sum: 7
    Output : 1 (1 if present, else 0)
    ```

**秒:(F2F)**

1.  以上两个问题的讨论。
2.  如果一个双向链表有整数形式的指针来表示内存位置，而我们想只管理上一个和下一个节点的一个引用，那么这个链表将如何遍历。
3.  [向右旋转二叉树](https://www.geeksforgeeks.org/flip-binary-tree/)

**第三:(F2F)**

1.  [二叉树的直径](https://practice.geeksforgeeks.org/problems/diameter-of-binary-tree/1)
2.  域名系统查找的工作原理
3.  SQL Query with 3 tables : Student, Class, Test

    ```
    Input : Student : SID, CID, Name
        Class : CID, Cname
        Test : TestId, WeekId, SID, Marks 
    ```

    编写一个查询，按类别打印每周的平均分数

    输出示例:

    ```
       ClassName, WeekId, Avg_Marks
       Tenth, 1, 33
       Eleventh, 1, 34
       Tenth, 2, 45
       Eleventh, 2, 21 
    ```

    解决方案:选择(从 CID = S.CID 的班级中选择 Cname)班级名称，T.WeekId，AVG(T.Marks)
    从 T LEFT _ JOIN 学生 S 上 T.SID=S.SID
    按班级名称，T.WeekId 分组

4.  [设计一个卢多/蛇&梯子](https://practice.geeksforgeeks.org/problems/snake-and-ladder-problem/0)

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论