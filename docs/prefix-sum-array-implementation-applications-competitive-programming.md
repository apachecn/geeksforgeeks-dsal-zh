# 前缀和数组–在竞争编程中的实现和应用

> 原文:[https://www . geesforgeks . org/prefix-sum-array-implementation-applications-competitive-programming/](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)

给定一个大小为 n 的数组 arr[]，它的前缀和数组是另一个相同大小的数组 prefixSum[]，这样 prefixSum[i]的值就是 arr[0] + arr[1] + arr[2] … arr[i]。

**示例:**

```
Input  : arr[] = {10, 20, 10, 5, 15}
Output : prefixSum[] = {10, 30, 40, 45, 60}

Explanation : While traversing the array, update 
the element by adding it with its previous element.
prefixSum[0] = 10, 
prefixSum[1] = prefixSum[0] + arr[1] = 30, 
prefixSum[2] = prefixSum[1] + arr[2] = 40 and so on.
```

为了填充前缀和数组，我们从头到尾运行索引 1，并继续将当前元素与前缀和数组中的前一个值相加。
下面是实现:

## C++

```
// C++ program for Implementing
// prefix sum array
#include <bits/stdc++.h>
using namespace std;

// Fills prefix sum array
void fillPrefixSum(int arr[], int n, int prefixSum[])
{
    prefixSum[0] = arr[0];

    // Adding present element
    // with previous element
    for (int i = 1; i < n; i++)
        prefixSum[i] = prefixSum[i - 1] + arr[i];
}

// Driver Code
int main()
{
    int arr[] = { 10, 4, 16, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int prefixSum[n];

    fillPrefixSum(arr, n, prefixSum);
    for (int i = 0; i < n; i++)
        cout << prefixSum[i] << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for Implementing
// prefix sum arrayclass
class Prefix {
    // Fills prefix sum array
    static void fillPrefixSum(int arr[], int n,
                              int prefixSum[])
    {
        prefixSum[0] = arr[0];

        // Adding present element
        // with previous element
        for (int i = 1; i < n; ++i)
            prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 10, 4, 16, 20 };
        int n = arr.length;
        int prefixSum[] = new int[n];

        fillPrefixSum(arr, n, prefixSum);

        for (int i = 0; i < n; i++)
            System.out.print(prefixSum[i] + " ");
        System.out.println("");
    }
}

// This Code is Contributed by Saket Kumar
```

## 蟒蛇 3

```
# Python Program for Implementing
# prefix sum array

# Fills prefix sum array
def fillPrefixSum(arr, n, prefixSum):

    prefixSum[0] = arr[0]

    # Adding present element
    # with previous element
    for i in range(1, n):
        prefixSum[i] = prefixSum[i - 1] + arr[i]

# Driver code
arr =[10, 4, 16, 20 ]
n = len(arr)

prefixSum = [0 for i in range(n + 1)]

fillPrefixSum(arr, n, prefixSum)

for i in range(n):
    print(prefixSum[i], " ", end ="")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program for Implementing
// prefix sum arrayclass
using System;

class GFG {
    // Fills prefix sum array
    static void fillPrefixSum(int[] arr, int n,
                              int[] prefixSum)
    {
        prefixSum[0] = arr[0];

        // Adding present element
        // with previous element
        for (int i = 1; i < n; ++i)
            prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 10, 4, 16, 20 };
        int n = arr.Length;
        int[] prefixSum = new int[n];

        fillPrefixSum(arr, n, prefixSum);

        for (int i = 0; i < n; i++)
            Console.Write(prefixSum[i] + " ");
        Console.Write("");
    }
}

// This Code is Contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for
// Implementing prefix
// sum array

// Fills prefix sum array
function fillPrefixSum($arr,
                       $n)
{
    $prefixSum = array();
    $prefixSum[0] = $arr[0];

    // Adding present element
    // with previous element
    for ($i = 1; $i < $n; $i++)
        $prefixSum[$i] = $prefixSum[$i - 1] +
                                    $arr[$i];

    for ($i = 0; $i < $n; $i++)
        echo $prefixSum[$i] . " ";
}

// Driver Code
$arr = array(10, 4, 16, 20);
$n = count($arr);

fillPrefixSum($arr, $n);

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>

    // JavaScript Program for Implementing
    // prefix sum arrayclass

    // Fills prefix sum array
    function fillPrefixSum(arr, n, prefixSum)
    {
        prefixSum[0] = arr[0];

        // Adding present element
        // with previous element
        for (let i = 1; i < n; ++i)
            prefixSum[i] = prefixSum[i - 1] + arr[i];
    }

    let arr = [ 10, 4, 16, 20 ];
    let n = arr.length;
    let prefixSum = new Array(n);

    fillPrefixSum(arr, n, prefixSum);

    for (let i = 0; i < n; i++)
        document.write(prefixSum[i] + " ");
    document.write("");

</script>
```

**输出:**

```
10 14 30 50
```

给定大小为 n 的数组 arr[]。给定 Q 个查询，在每个给定 L 和 R 的查询中，打印从索引 L 到 R 的数组元素的总和

## C++14

```
#include <iostream>
using namespace std;
const int N = 1e5+10;
int a[N];
int pf[N];

int main() {
int n;
cin >> n;
for(int i=1; i<=n; i++){
    cin >> a[i];
    if(i==0)
        pf[i]=a[i];
    else
        pf[i] = pf[i-1] + a[i];
    //cout<<pf[i];
}
int q;
cin >> q;
while(q--){
    int l, r;
    cin >> l >> r;
//Calculating sum from l to r.
    if(r>n || l<1)
    {
        cout<<"Please input in range 1 to "<<n<<endl;
        break;
    }
    if(l==1)
        cout << pf[r] << endl;
    else
        cout << pf[r] - pf[l-1] << endl;

}
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

    public static void main(String[] args)
    {
        int n = 6;
        int[] a = { 3, 6, 2, 8, 9, 2 };
        int[] pf = new int[n + 2];
        pf[0] = 0;
        for (int i = 0; i < n; i++) {
            pf[i + 1] = pf[i] + a[i];
        }

        int[][] q
            = { { 2, 3 }, { 4, 6 }, { 1, 5 }, { 3, 6 } };
        for (int i = 0; i < q.length; i++) {
            int l = q[i][0];
            int r = q[i][1];

            // Calculating sum from r to l.
            System.out.print(pf[r] - pf[l - 1] + "\n");
        }
    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
if __name__ == '__main__':
    n = 6;
    a = [ 3, 6, 2, 8, 9, 2 ];
    pf = [0 for i in range(n+2)];
    for i in range(n):
        pf[i + 1] = pf[i] + a[i];

    q =[ [ 2, 3 ],[ 4, 6 ],[ 1, 5 ],[ 3, 6  ]];
    for i in range(4):
        l = q[i][0];
        r = q[i][1];

        # Calculating sum from r to l.
        print(pf[r] - pf[l - 1] );

# This code is contributed by gauravrajput1
```

## C#

```
using System;

public class GFG {

    public static void Main(String[] args) {
        int n = 6;
        int[] a = { 3, 6, 2, 8, 9, 2 };
        int[] pf = new int[n + 2];
        pf[0] = 0;
        for (int i = 0; i < n; i++) {
            pf[i + 1] = pf[i] + a[i];
        }

        int[,] q = { { 2, 3 }, { 4, 6 }, { 1, 5 }, { 3, 6 } };
        for (int i = 0; i < q.GetLength(0); i++) {
            int l = q[i,0];
            int r = q[i,1];

            // Calculating sum from r to l.
            Console.Write(pf[r] - pf[l - 1] + "\n");
        }
    }
}

// This code is contributed by gauravrajput1
```

## C++14

```
<script>

        var n = 6;
        var a = [ 3, 6, 2, 8, 9, 2 ];
        var pf = Array(n + 2).fill(0);
        pf[0] = 0;
        for (i = 0; i < n; i++) {
            pf[i + 1] = pf[i] + a[i];
        }

        var q = [ [ 2, 3 ], [ 4, 6 ], [ 1, 5 ], [ 3, 6 ] ];
        for (i = 0; i < q.length; i++) {
            var l = q[i][0];
            var r = q[i][1];

            // Calculating sum from r to l.
            document.write(pf[r-1] - pf[l - 1] + "<br/>");
        }

// This code is contributed by gauravrajput1
</script>
```

**示例:**

```
Input : n = 6
       a[ ] = {3, 6, 2, 8, 9, 2}
       q = 4
       l = 2, r = 3.
       l = 4, r = 6.
       l = 1, r = 5.
       l = 3, r = 6.
```

```
Output :  8
          19
          28
          21
```

**时间复杂度:** O(n)

**应用:**

*   [数组的平衡指数](https://www.geeksforgeeks.org/equilibrium-index-of-an-array/):数组的平衡指数是指较低指数的元素之和等于较高指数的元素之和的指数。
*   [查找是否有和为 0 的子阵列](https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/):给定一个正负数的数组，查找是否有和为 0 的子阵列(大小至少为 1)。
*   [最大子阵列尺寸，使得该尺寸的所有子阵列的和小于 k:](https://www.geeksforgeeks.org/maximum-subarray-size-subarrays-size-sum-less-k/) 给定 n 个正整数和一个正整数 k 的阵列，任务是找到最大子阵列尺寸，使得该尺寸的所有子阵列的元素和小于 k
*   [找出可以写成最连续素数之和的素数](https://www.geeksforgeeks.org/find-prime-number-can-written-sum-consecutive-primes/):给定一组极限。对于每一个极限，求可以写成小于或等于极限的最连续素数之和的素数。
*   [两个二进制数组中具有相同和的最大跨度:](https://www.geeksforgeeks.org/longest-span-sum-two-binary-arrays/)给定两个二进制数组，相同大小的 arr1[]和 arr 2[]n .求最大公共跨度(I，j)的长度，其中 j > = i，使得 arr1[i] + arr1[i+1] + …。+ arr1[j] = arr2[i] + arr2[i+1] + …。+ arr2[j]。
*   [模 m 的最大子阵和](https://www.geeksforgeeks.org/maximum-subarray-sum-modulo-m/):给定一个 n 元素和一个整数 m 的数组，任务是求其模 m 的子阵和的最大值，即求每个子阵模 m 的和，并打印这个模运算的最大值。
*   [最大子阵列大小，使得该大小的所有子阵列的和小于 k](https://www.geeksforgeeks.org/maximum-subarray-size-subarrays-size-sum-less-k/) :给定 n 个正整数和一个正整数 k 的数组，任务是找到最大子阵列大小，使得该大小的所有子阵列的元素和小于 k
*   [n 个范围内出现的最大整数:](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)给定 L 和 R 形式的 n 个范围，任务是找出所有范围内出现的最大整数。如果存在多个这样的整数，打印最小的一个。
*   [获得所有硬币的最低成本，每枚硬币允许有 k 个额外硬币:](https://www.geeksforgeeks.org/minimum-cost-for-acquiring-all-coins-with-k-extra-coins-allowed-with-every-coin/)您将获得一份不同面值的 N 枚硬币的列表。你可以支付相当于任何一枚硬币的金额，并可以获得该硬币。此外，一旦您支付了一枚硬币，我们最多可以选择 K 枚以上的硬币，并且可以免费获得这些硬币。任务是为给定的 k 值找到获得所有 N 个硬币所需的最小数量。
*   [任意概率分布方式的随机数发生器:](https://www.geeksforgeeks.org/random-number-generator-in-arbitrary-probability-distribution-fashion/)给定 n 个数字，每个数字都有一定的出现频率。返回一个概率与其出现频率成正比的随机数。

**一个示例问题:**
考虑一个大小为 n 的数组，所有初始值都为 0。执行从索引“a”到“b”的给定“m”加法运算，并计算数组中最高的元素。加法运算将从 a 到 b(包括 a 和 b)的所有元素加 100。

**示例:**

```
Input : n = 5 // We consider array {0, 0, 0, 0, 0}
        m = 3.
        a = 2, b = 4.
        a = 1, b = 3.
        a = 1, b = 2.
Output : 300

Explanation : 

After I operation -
A : 0 100 100 100 0

After II operation -
A : 100 200 200 100 0

After III operation -
A : 200 300 200 100 0

Highest element : 300
```

一个简单的方法是运行循环 m 次。输入 a 和 b 并运行从 a 到 b 的循环，将所有元素加 100。
使用**前缀和数组**的有效方法:

```
1 : Run a loop for 'm' times, inputting 'a' and 'b'.
2 : Add 100 at index 'a-1' and subtract 100 from index 'b'.
3 : After completion of 'm' operations, compute the prefix sum array.
4 : Scan the largest element and we're done.
```

我们所做的是在“a”处添加 100，因为这将在获取前缀 sum 数组时向所有元素添加 100。从“b+1”中减去 100 将逆转从“b”开始向元素添加 100 所做的更改。
为了更好地理解:

```
After I operation -
A : 0 100 0 0 -100 
Prefix Sum Array : 0 100 100 100 0

After II operation -
A : 100 100 0 -100 -100
Prefix Sum Array : 100 200 200 100 0

After III operation -
A : 200 100 -100 -100 -100
Prefix Sum Array : 200 300 200 100 0

Final Prefix Sum Array : 200 300 200 100 0 

The required highest element : 300
```

## C++14

```
#include <bits/stdc++.h>
using namespace std;

int find(int m, vector<pair<int,int>> q)
{
    int mx = 0;
    vector<int> pre(5,0);

    for (int i = 0; i < m; i++)
    {   
        // take input a and b
        int a = q[i].first, b = q[i].second;

        // add 100 at first index and
        // subtract 100 from last index

        // pre[1] becomes 100
        pre[a-1] += 100;

        // pre[4] becomes -100 and this
        pre[b] -=100;   
        // continues m times as we input diff. values of a and b
    }
    for (int i = 1; i < 5; i++)
    {
        // add all values in a cumulative way
        pre[i] += pre[i - 1];

        // keep track of max value
        mx = max(mx, pre[i]);
    }

    return mx;
}

// Driver Code
int main()
{

    int m = 3;
    vector<pair<int,int>> q = {{2,4},{1,3},{1,2}};

    // Function call
    cout<< find(m,q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
static int find(int m, pair []q)
{
    int mx = 0;
    int []pre = new int[5];

    for (int i = 0; i < m; i++)
    {   

        // take input a and b
        int a = q[i].first, b = q[i].second;

        // add 100 at first index and
        // subtract 100 from last index

        // pre[1] becomes 100
        pre[a-1] += 100;

        // pre[4] becomes -100 and this
        pre[b] -=100;  

        // continues m times as we input diff. values of a and b
    }
    for (int i = 1; i < 5; i++)
    {

        // add all values in a cumulative way
        pre[i] += pre[i - 1];

        // keep track of max value
        mx = Math.max(mx, pre[i]);
    }

    return mx;
}

// Driver Code
public static void main(String[] args)
{

    int m = 3;
   pair[] q = {new pair(2,4),new pair(1,3), new pair(1,2)};

    // Function call
    System.out.print( find(m,q));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python implementation of the approach
def find( m, q):
    mx = 0
    pre = [0 for i in range(5) ]

    for i in range(m):
        # take input a and b
        a,b = q[i][0], q[i][1]

        # add 100 at first index and
        # subtract 100 from last index

        # pre[1] becomes 100
        pre[a-1] += 100

        # pre[4] becomes -100 and this
        pre[b] -=100; 

        # continues m times as we input diff. values of a and b
    for i in range(1,5):

        # add all values in a cumulative way
        pre[i] += pre[i - 1]

        # keep track of max value
        mx = max(mx, pre[i])                            
    return mx

# Driver Code
m = 3
q = [[2,4],[1,3],[1,2]]

# Function call
print(find(m,q))

# This code is contributed by rohitsingh07052
```

## C#

```
using System;

public class GFG{
   public class pair
    {
       public int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
static int find(int m, pair []q)
{
    int mx = 0;
    int []pre = new int[5];

    for (int i = 0; i < m; i++)
    {   

        // take input a and b
        int a = q[i].first, b = q[i].second;

        // add 100 at first index and
        // subtract 100 from last index

        // pre[1] becomes 100
        pre[a-1] += 100;

        // pre[4] becomes -100 and this
        pre[b] -=100;  

        // continues m times as we input diff. values of a and b
    }
    for (int i = 1; i < 5; i++)
    {

        // add all values in a cumulative way
        pre[i] += pre[i - 1];

        // keep track of max value
        mx = Math.Max(mx, pre[i]);
    }

    return mx;
}

// Driver Code
public static void Main(String[] args)
{
    int m = 3;
   pair[] q = {new pair(2,4),new pair(1,3), new pair(1,2)};

    // Function call
    Console.Write( find(m,q));
}
}

// This code is contributed by gauravrajput1.
```

## java 描述语言

```
<script>

function find( m,q)
{
    let mx = 0;
    let pre = [0,0,0,0,0];

    for (let i = 0; i < m; i++)
    {   
        // take input a and b
        let a = q[i][0], b = q[i][1];

        // add 100 at first index and
        // subtract 100 from last index

        // pre[1] becomes 100
        pre[a-1] += 100;

        // pre[4] becomes -100 and this
        pre[b] -=100;   
        // continues m times as we input diff. values of a and b
    }
    for (let i = 1; i < 5; i++)
    {
        // add all values in a cumulative way
        pre[i] += pre[i - 1];

        // keep track of max value
        mx = Math.max(mx, pre[i]);
    }

    return mx;
}

// Driver Code
let m = 3;
let q = [[2,4],[1,3],[1,2]];

    // Function call
    document.write(find(m,q));

</script>
```

**Output**

```
300
```

[**前缀求和法近期文章**](https://www.geeksforgeeks.org/tag/prefix-sum/)
本文由**罗希特·塔普利亚尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。