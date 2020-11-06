# 吉尔布雷斯猜想产生的数字三角形

> 原文：[https://www.geeksforgeeks.org/triangle-of-numbers-arising-from-gilbreaths-conjecture/](https://www.geeksforgeeks.org/triangle-of-numbers-arising-from-gilbreaths-conjecture/)

我们的任务是找到由 [Gilbreath 猜想](https://en.wikipedia.org/wiki/Gilbreath%27s_conjecture)产生的数字三角形。

**吉尔布雷斯的猜想**：

观察到，给定质数序列，可以通过第 i 个与（i + 1）<sup>之间的绝对差形成一个序列 给定序列和给定过程的</sup>项可以重复以形成数字的三角形。 这个数字构成了吉尔布雷思猜想三角形的元素。

**吉尔布雷斯三角形形成如下**：

*   让我们进行质数：2、3、5、7。

*   现在，相邻质数之间的差为：1、2、2。

*   现在，相邻元素之间的差为：1、0。

*   现在相邻元素之间的区别是：1。

*   这样，吉尔布雷思三角形形成为：

    ```
    2 3 5 7
     1 2 2
      1 0
       1

    ```

*   该三角形将反斜向上读取为

    ```
    2, 1, 3, 1, 2, 5, 1, 0, 2, 7, 
    ```

**示例**：

```
Input: n = 10
Output: 2, 1, 3, 1, 2, 
        5, 1, 0, 2, 7,

Input: n = 15
Output: 2, 1, 3, 1, 2, 
        5, 1, 0, 2, 7,
        1, 2, 2, 4, 11

```

**方法**：

1.  **Gilbreath 序列**的第（n，k）个<sup>第</sup>项由下式给出

    *   <center>![](img/6ec4722679a47b712a766a27f8f2514b.png "\huge {\color{DarkGreen} F(n, k) = \left | F(n-1, k+1)-F(n-1, k) \right | }")</center>

        ，其中 **n > 0** ，

    *   **F（0，k）**是第 k 个质数，其中 **n = 0** 。

2.  定义一个递归函数，我们可以将（n，k） <sup>th</sup> 项映射到映射中并将其存储以减少计算量。 我们将用质数填充第 0 <sup>行至第</sup>行。

3.  沿反对角向上遍历吉尔布雷斯三角形，因此我们将从 n = 0，k = 0 开始，并在每个步骤中增加 k 并减小 n（如果 n <0），则我们将 n = k 和 k = 0， 我们可以对角向上对角地穿越三角形。

4.  我们用 100 个质数填充了第 0 <sup>行和第</sup>行。 如果需要查找级数更大的项，可以增加质数。

下面是上述方法的实现：

```
// C++ code for printing the Triangle of numbers
// arising from Gilbreath's conjecture
#include <bits/stdc++.h>
using namespace std;
// Check whether the number
// is prime or not
bool is_Prime( int n)
{
if (n < 2)
return false ;
的
for ( int i = 2; i <= sqrt (n); i++)
if (n % i == 0)
return false ;
return true ;
}
// Set the 0th row of the matrix
// with c primes from 0, 0 to 0, c-1
void set_primes(map< int , map< int , int > >& mp,
map< int ,
map< int , int > >& hash,
int c)
{
int count = 0;
for ( int i = 2; count < c; i++) {
if (is_Prime(i)) {
mp[0][count++] = i;
hash[0][count - 1] = 1;
}
}
}
// Find the n, k term of matrix of
// Gilbreath's conjecture
int Gilbreath(map< int , map< int , int > >& mp,
map< int , map< int , int > >& hash,
int n, int k)
{
if (hash[n][k] != 0)
return mp[n][k];
// recursively find
int ans
= abs (Gilbreath(mp, hash, n - 1, k + 1)
- Gilbreath(mp, hash, n - 1, k));
// store the ans
mp[n][k] = ans;
return ans;
}
// Print first n terms of Gilbreath sequence
// successive absolute differences of primes
// read by antidiagonals upwards.
void solve( int n)
{
int i = 0, j = 0, count = 0;
// map to store the matrix
// and hash to check if the
// element is present or not
map< int , map< int , int > > mp, hash;
[HTG35 8]  〔HTG359〕〔HTG360〕〔HTG168〕〔HTG169〕〔HTG361〕〔HTG362〕〔HTG170〕〔HTG171〕〔HTG363〕〔HTG364〕〔HTG172〕 (count < n) {
// print the Gilbreath number
cout << Gilbreath(mp, hash, i, j)
] ;
// increase the count
count++;
// anti diagonal upwards
i--;
j++;
if (i < 0) {
i = j;
j = 0;
}
}
}
// Driver code
int main()
{
int n = 15;
solve(n);
return 0;
}
```

**Output:**

```
2, 1, 3, 1, 2, 5, 1, 0, 2, 7, 1, 2, 2, 4, 11,

```

**参考**： [http://oeis.org/A036262](http://oeis.org/A036262)



* * *

* * *



