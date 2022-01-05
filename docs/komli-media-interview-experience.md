# 科姆利媒体采访体验

> 原文:[https://www . geesforgeks . org/kom Li-media-interview-experience/](https://www.geeksforgeeks.org/komli-media-interview-experience/)

最近参加了 Komli 的媒体采访，想分享一下经验。

**首轮(笔试)**
1。Midas 有大、中、小三种尺寸的盒子。他在桌子上放了 11 个大盒子。他把其中一些盒子留空，在所有其他的盒子里，他放了 8 个中盒。他把其中一些中盒留空，在所有其他中盒中放入 8 个(空的)小盒。现在，桌子上 102 个盒子都是空的。迈达斯一共用过几盒？

见此处答案:[https://www.easycalculation.com/puzzles/hard/boxes.php](https://www.easycalculation.com/puzzles/hard/boxes.php)

2.给你一个文件，它包含一个 0 和 1 的非常小的序列，并对它进行排序。因此所有的 0 都在 1 的前面。需要在文件中找到 1 的第一个 orrcurance(返回位置)。

访问文件的唯一方法是通过一个签名为-int getBitAtPosition(int position)的方法，该方法返回文件中指定位置的位。

3.给定一个字符串，根据给定的参数找到该字符串的短版本。
方法签名:shortenString(字符串 s，int n)

```
    ex:
    s = aaabbbaa   n=2   output = aabbaa
    s= aaabbaacccc n=1   output = abac 
```

如果一个字符超过 n，基本上截断它的连续运行。

4.编写一个函数，将两个数字除以 4 位小数。
只能使用加减运算符。

5.查尔斯走过一座铁路桥。就在他离桥中央十米远的时候，他听到一列火车从后面驶来。那一刻，以 90 公里/小时的速度行驶的火车，离桥的距离正好是桥的长度。查尔斯毫不犹豫地径直奔向火车，准备下桥。就这样，他只差 4 米就错过火车了！然而，如果查尔斯朝另一个方向冲得一样快，火车就会在桥的尽头前 8 米撞上他。
答案:[http://dailybraintreater . blogspot . in/2011/08/train-拼图. html](http://dailybrainteaser.blogspot.in/2011/08/train-puzzle.html)

**第二轮:**
第一轮问题讨论及优化。
简历中提到的项目讨论很多。

**第三轮:**
1。给定一个整数数组，对于每个位置，找出数组中剩余元素的乘积。
不允许使用除法运算符。
对所有的位置计算同样的东西，并在不同的数组中输出。

```
    ex: input = {4,3,2,4}
        output = {24,32,48,24} 
```

2.给一个数 n，找出所有可能的数的集合，其和为 n。一个数可以在一个集合内重复。

```
    ex : input n=4
    output : {1,1,1,1},{1,1,2},{1,3},{2,2},{4} 
```

如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。