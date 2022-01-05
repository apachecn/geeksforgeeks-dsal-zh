# 时间复杂度分析|河内塔(递归)

> 原文:[https://www . geesforgeks . org/时间-复杂性-分析-塔-河内-递归/](https://www.geeksforgeeks.org/time-complexity-analysis-tower-hanoi-recursion/)

[河内塔](https://www.geeksforgeeks.org/c-program-for-tower-of-hanoi/)是一个数学难题，我们有三个杆和 n 个圆盘。拼图的目标是将整个堆叠移动到另一个棒上，遵循以下简单规则:
1)一次只能移动一个磁盘。
2)每次移动包括从一个堆栈中取出上层磁盘，并将其放在另一个堆栈的顶部，即只有当磁盘是堆栈中最上面的磁盘时，才能移动该磁盘。
3)任何磁盘都不能放在较小的磁盘上。

伪代码

```
TOH(n, x, y, z)
{
   if (n >= 1)
   {
      // put (n-1) disk to z by using y
      TOH((n-1), x, z, y)

       // move larger disk to right place
       move:x-->y

      // put (n-1) disk to right place 
      TOH((n-1), z, y, x)
   }
}
```

递归分析

递归方程:![T(n) = 2T(n-1) + 1  ](img/e9f4b9595d68147da261c42ad4ad5ee9.png "Rendered by QuickLaTeX.com")—-方程-1

通过反变换求解:
![T(n-1) = 2T(n-2) + 1  ](img/84ac5efe2db457a33ebf70a421ed98f8.png "Rendered by QuickLaTeX.com") ———方程-2
![T(n-2) = 2T(n-3) + 1  ](img/34eba31e1627a54952b0b053e5741c37.png "Rendered by QuickLaTeX.com") ———方程-3

借助方程-3
![T(n-1)= 2( 2T(n-3) + 1 ) + 1  ](img/603e2907d3f132c3fe882b5d39bcb208.png "Rendered by QuickLaTeX.com")——方程-4，将 T(n-2)的值放入方程-2

借助方程-4
![T(n)= 2( 2( 2T(n-3) + 1 ) + 1 ) + 1  ](img/de9481997ba26ecd414c3e3a1316f565.png "Rendered by QuickLaTeX.com")
![T(n) = 2^3 T(n-3) + 2^2 + 2^1 + 1  ](img/e08cc0c843acd96f7fb56552bf6063cd.png "Rendered by QuickLaTeX.com")将 T(n-1)的值代入方程-1

泛化后:
![T(n)= 2^k T(n-k) + 2^{(k-1)} + 2^{(k-2)} + ............ +2^2 + 2^1 + 1  ](img/0bbf6a262ae775c5c94e40ba594ddcc7.png "Rendered by QuickLaTeX.com")

基础条件 T(1)= 1
n–k = 1
k = n-1
put，k = n-1
T4】

是 GP 系列，和为![2^n - 1  ](img/50ed470c4b4b9ae559f776ecca301cb4.png "Rendered by QuickLaTeX.com")

![T(n)= O( 2^n - 1)  ](img/ba284d2b45cd02fd70f68a12a91bbd29.png "Rendered by QuickLaTeX.com")，或者你可以说![O(2^n)  ](img/da7d0bd5ada051b9f8b532d297814190.png "Rendered by QuickLaTeX.com")是指数

对于 5 个磁盘，即 n=5，需要 2^5-1=31 移动。