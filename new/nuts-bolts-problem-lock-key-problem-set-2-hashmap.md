# 螺母&螺栓问题（锁定&键问题） | 系列 2（哈希映射）

> 原文：[https://www.geeksforgeeks.org/nuts-bolts-problem-lock-key-problem-set-2-hashmap/](https://www.geeksforgeeks.org/nuts-bolts-problem-lock-key-problem-set-2-hashmap/)

给定一组 n 个不同尺寸的螺母和 n 个不同尺寸的螺栓。 螺母和螺栓之间存在一对一的映射。 有效地匹配螺母和螺栓。

**约束**：不允许将螺母与另一个螺母或一个螺栓与另一个螺栓进行比较。 这意味着只能将螺母与螺栓进行比较，而只能将螺栓与螺母进行比较以查看哪个更大或更小。

例子：

```
Input : nuts[] = {'@', '#', '{content}apos;, '%', '^', '&'}
        bolts[] = {'{content}apos;, '%', '&', '^', '@', '#'}
Output : Matched nuts and bolts are-
        $ % & ^ @ # 
        $ % & ^ @ #  

```

提出此问题的另一种方法是，给定一个带有锁和键的盒子，在其中可以用盒子中的一个键打开一个锁。 我们需要配对。

我们在下面的文章中讨论了基于排序的解决方案。

[螺母&螺栓问题（锁定&键问题） | 系列 1](https://www.geeksforgeeks.org/nuts-bolts-problem-lock-key-problem/)

在这篇文章中，讨论了基于哈希映射的方法。

1.  遍历坚果数组并创建一个哈希表

2.  遍历 bolts 数组并在 hashmap 中搜索。

3.  如果在螺母的哈希映射中找到它，则意味着该螺母存在螺栓。

```
// Hashmap based solution to solve
#include <bits/stdc++.h>
using namespace std;
// function to match nuts and bolts
void nutboltmatch( char nuts[], char bolts[], int n)
{
unordered_map< char , int > hash;
// creating a hashmap for nuts
for ( int i = 0; i < n; i++)
hash[nuts[i]] = i;
// searching for nuts for each bolt in hash map
] ( int i = 0; i < n; i++)
if (hash.find(bolts[i]) != hash.end())
nuts[i] = bolts[i];
// print the result
cout << "matched nuts and bolts are-" << endl;
for ( int i = 0; i < n; i++)
cout << nuts[i] << " " ;
cout << endl;
for ( int i = 0; i < n; i++)
cout << bolts[i] << " " ;
}
// Driver code
int main()
{
char nuts[] = { '@' , '#' , '{content}apos; , '%' , '^' , '&' };
char bolts[] = { '{content}apos; , '%' , '&' , '^' , '@' , '#' };
int n = sizeof (nuts) / sizeof (nuts[0]);
nutboltmatch(nuts, bolts, n);
return 0;
}
```

输出：

```
matched nuts and bolts are-
$ % & ^ @ # 
$ % & ^ @ # 

```

该解决方案的时间复杂度为`O(n)`。

本文由 **Niteesh kumar** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

