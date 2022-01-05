# 使用 4 根桩/杆的河内递归塔

> 原文:[https://www . geesforgeks . org/recursive-tower-Hanoi-using-4-peg-rods/](https://www.geeksforgeeks.org/recursive-tower-hanoi-using-4-pegs-rods/)

河内塔是一个数学难题。**传统上**由三个磁极和多个大小不同的圆盘组成，圆盘可以滑动到任意磁极上。这个谜题从圆盘开始，在一个磁极中按照大小的升序排列，最小的在顶部，从而形成一个圆锥形。谜题的目的是在第三极(比如辅助极)的帮助下，将所有的圆盘从一极(比如源极)移动到另一极(比如目的极)。

这个谜题有以下两个规则:

1.您不能将较大的磁盘放在较小的磁盘上
2。一次只能移动一个磁盘

我们已经讨论了时间复杂度为 O(2^n).的汉诺塔的递归解使用 4 个杆，同样的方法显示时间复杂度显著降低。

示例:

```
Input : 3
Output :
Move disk 1 from rod A to rod B
Move disk 2 from rod A to rod C
Move disk 3 from rod A to rod D
Move disk 2 from rod C to rod D
Move disk 1 from rod B to rod D

Input : 5
Output : 
Move disk 1 from rod A to rod C
Move disk 2 from rod A to rod D
Move disk 3 from rod A to rod B
Move disk 2 from rod D to rod B
Move disk 1 from rod C to rod B
Move disk 4 from rod A to rod C
Move disk 5 from rod A to rod D
Move disk 4 from rod C to rod D
Move disk 1 from rod B to rod A
Move disk 2 from rod B to rod C
Move disk 3 from rod B to rod D
Move disk 2 from rod C to rod D
Move disk 1 from rod A to rod D

```

## C++

```
CJava 语言(一种计算机语言，尤用于创建网站)
```

//递归函数求解
//汉诺塔拼图
静态空塔汉诺塔(int n，char from_rod，
char to_rod，char aux_rod1，
char aux _ rod 2)
{
if(n = = 0)
返回；
if(n = = 1){
system . out . println("移动磁盘"+ n +
"从棒"+从 _ 棒+
"到棒"+到 _ 棒")；
返回；
}

towerrohanoi(n–2，从 _rod，aux_rod1，aux_rod2，
到 _ rod)；
System.out.println(“移动磁盘”+(n–1)+
“从杆”+从 _ 杆+
“到杆”+辅助 _ 杆 2)；
System.out.println(“移动磁盘”+ n +
“从杆”+从 _ 杆+
“到杆”+到 _ 杆”)；
System.out.println(“移动磁盘”+(n–1)+
“从杆”+ aux_rod2 +
“到杆”+to _ rod)；
towerOfHanoi(n–2，aux_rod1，to_rod，from_rod，
aux _ rod 2)；
}

//驱动方法
公共静态 void main(String args[])
{
int n = 4；//磁盘数量

// A、B、C、D 为棒的名称
towerOfHanoi(n，' A '，' D '，' B '，' C ')；
}