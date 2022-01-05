# 箱柜包装问题(尽量减少使用的箱柜数量)

> 原文:[https://www . geesforgeks . org/bin-packing-problem-minimum-of-used-bin/](https://www.geeksforgeeks.org/bin-packing-problem-minimize-number-of-used-bins/)

给定 n 个不同重量的物品和每个容量为 c 的箱子，将每个物品分配给一个箱子，使得总使用箱子的数量最小化。可以假设所有物品的重量都小于箱容量。
**例:**

```
Input:  weight[]       = {4, 8, 1, 4, 2, 1}
        Bin Capacity c = 10
Output: 2
We need minimum 2 bins to accommodate all items
First bin contains {4, 4, 2} and second bin {8, 1, 1}

Input:  weight[]       = {9, 8, 2, 2, 5, 4}
        Bin Capacity c = 10
Output: 4
We need minimum 4 bins to accommodate all items.  

Input:  weight[]       = {2, 5, 4, 7, 1, 3, 8}; 
        Bin Capacity c = 10
Output: 3
```

**下限**
我们总能找到所需最小箱数的下限。下限可由下式给出:

```
   Min no. of bins  >=  Ceil ((Total Weight) / (Bin Capacity))
```

在上面的例子中，第一个例子的下限是“ceil(4+8+1+4+2+1)/10”= 2，第二个例子的下限是“ceil(9+8+2+2+5+4)/10”= 3。
这个问题是一个 NP 难问题，找到精确的最小箱数需要指数时间。下面是这个问题的近似算法。
**应用**

1.  像卡车一样装载集装箱。
2.  将数据放在多个磁盘上。
3.  作业调度。
4.  在固定长度的广播/电视台休息时间包装广告。
5.  将大量音乐储存在磁带/光盘等上。

**在线算法**
这些算法是针对装箱问题的，物品一次到达一个(顺序未知)，每个必须放入一个箱子，然后再考虑下一个物品。
**1。下一个符合:**
处理下一个项目时，检查它是否符合最后一个项目的相同箱。只有在没有的情况下才使用新的垃圾箱。
下面是这个算法的 C++实现。

## C++

```
// C++ program to find number of bins required using
// next fit algorithm.
#include <bits/stdc++.h>
using namespace std;

// Returns number of bins required using next fit
// online algorithm
int nextFit(int weight[], int n, int c)
{
    // Initialize result (Count of bins) and remaining
    // capacity in current bin.
    int res = 0, bin_rem = c;

    // Place items one by one
    for (int i = 0; i < n; i++) {
        // If this item can't fit in current bin
        if (weight[i] > bin_rem) {
            res++; // Use a new bin
            bin_rem = c - weight[i];
        }
        else
            bin_rem -= weight[i];
    }
    return res;
}

// Driver program
int main()
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = sizeof(weight) / sizeof(weight[0]);
    cout << "Number of bins required in Next Fit : "
         << nextFit(weight, n, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of bins required using
// next fit algorithm.
class GFG {

    // Returns number of bins required
    // using next fit online algorithm
    static int nextFit(int weight[], int n, int c)
    {

        // Initialize result (Count of bins) and remaining
        // capacity in current bin.
        int res = 0, bin_rem = c;

        // Place items one by one
        for (int i = 0; i < n; i++) {
            // If this item can't fit in current bin
            if (weight[i] > bin_rem) {
                res++; // Use a new bin
                bin_rem = c - weight[i];
            }
            else
                bin_rem -= weight[i];
        }
        return res;
    }

    // Driver program
    public static void main(String[] args)
    {
        int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
        int c = 10;
        int n = weight.length;
        System.out.println("Number of bins required in Next Fit : " + nextFit(weight, n, c));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation for above approach
def nextfit(weight, c):
    res = 0
    rem = c
    for _ in range(len(weight)):
        if rem >= weight[_]:
            rem = rem - weight[_]
        else:
            res += 1
            rem = c - weight[_]
    return res

# Driver Code
weight = [2, 5, 4, 7, 1, 3, 8]
c = 10

print("Number of bins required in Next Fit :",
                           nextfit(weight, c))

# This code is contributed by code_freak
```

## C#

```

// C# program to find number
// of bins required using
// next fit algorithm.
using System;

class GFG
{

    // Returns number of bins required
    // using next fit online algorithm
    static int nextFit(int []weight, int n, int c)
    {

        // Initialize result (Count of bins) and remaining
        // capacity in current bin.
        int res = 0, bin_rem = c;

        // Place items one by one
        for (int i = 0; i < n; i++)
        {
            // If this item can't fit in current bin
            if (weight[i] > bin_rem)
            {
                res++; // Use a new bin
                bin_rem = c - weight[i];
            }
            else
                bin_rem -= weight[i];
        }
        return res;
    }

    // Driver program
    public static void Main(String[] args)
    {
        int []weight = { 2, 5, 4, 7, 1, 3, 8 };
        int c = 10;
        int n = weight.Length;
        Console.WriteLine("Number of bins required" +
                " in Next Fit : " + nextFit(weight, n, c));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find number
// of bins required using
// next fit algorithm.

    // Returns number of bins required
    // using next fit online algorithm
    function nextFit(weight, n, c)
    {

        // Initialize result (Count of bins) and remaining
        // capacity in current bin.
        let res = 0, bin_rem = c;

        // Place items one by one
        for (let i = 0; i < n; i++)
        {

            // If this item can't fit in current bin
            if (weight[i] > bin_rem)
            {
                res++; // Use a new bin
                bin_rem = c - weight[i];
            }
            else
                bin_rem -= weight[i];
        }
        return res;
    }

// Driver Code

        let weight = [ 2, 5, 4, 7, 1, 3, 8 ];
        let c = 10;
        let n = weight.length;
        document.write("Number of bins required in Next Fit : " + nextFit(weight, n, c));

    // This code is contributed by target_2.
</script>
```

**输出:**

```
Number of bins required in Next Fit : 4
```

Next Fit 是一个简单的算法。处理 n 个项目只需要 O(n)个时间和 O(1)个额外空间。
Next Fit 是 2 个近似值，即该算法使用的箱数以最优的两倍为界。考虑任何两个相邻的箱子。这两个箱子里的物品总和必须是>c；否则，NextFit 会将第二个箱的所有项目放入第一个箱。所有其他垃圾箱也是如此。因此，最多浪费一半的空间，因此如果 M 是最优的，Next Fit 最多使用 2M 箱。
**2。第一个符合:**
处理下一个物品时，按顺序扫描前面的箱子，并将物品放入第一个符合的箱子中。仅当新箱不适合任何现有箱时，才启动新箱。

## C++

```
// C++ program to find number of bins required using
// First Fit algorithm.
#include <bits/stdc++.h>
using namespace std;

// Returns number of bins required using first fit
// online algorithm
int firstFit(int weight[], int n, int c)
{
    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    int bin_rem[n];

    // Place items one by one
    for (int i = 0; i < n; i++) {
        // Find the first bin that can accommodate
        // weight[i]
        int j;
        for (j = 0; j < res; j++) {
            if (bin_rem[j] >= weight[i]) {
                bin_rem[j] = bin_rem[j] - weight[i];

                break;
            }
        }

        // If no bin could accommodate weight[i]
        if (j == res) {
            bin_rem[res] = c - weight[i];
            res++;
        }

    }
    return res;
}

// Driver program
int main()
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = sizeof(weight) / sizeof(weight[0]);
    cout << "Number of bins required in First Fit : "
         << firstFit(weight, n, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of bins required using
// First Fit algorithm.
class GFG
{

// Returns number of bins required using first fit
// online algorithm
static int firstFit(int weight[], int n, int c)
{
    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    int []bin_rem = new int[n];

    // Place items one by one
    for (int i = 0; i < n; i++)
    {
        // Find the first bin that can accommodate
        // weight[i]
        int j;
        for (j = 0; j < res; j++)
        {
            if (bin_rem[j] >= weight[i])
            {
                bin_rem[j] = bin_rem[j] - weight[i];
                break;
            }
        }

        // If no bin could accommodate weight[i]
        if (j == res)
        {
            bin_rem[res] = c - weight[i];
            res++;
        }
    }
    return res;
}

// Driver program
public static void main(String[] args)
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = weight.length;
    System.out.print("Number of bins required in First Fit : "
                    + firstFit(weight, n, c));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find number of bins required using
# First Fit algorithm.

# Returns number of bins required using first fit
# online algorithm
def firstFit(weight, n, c):

    # Initialize result (Count of bins)
    res = 0

    # Create an array to store remaining space in bins
    # there can be at most n bins
    bin_rem = [0]*n

    # Place items one by one
    for i in range(n):

        # Find the first bin that can accommodate
        # weight[i]
        j = 0
        while( j < res):
            if (bin_rem[j] >= weight[i]):
                bin_rem[j] = bin_rem[j] - weight[i]
                break
            j+=1

        # If no bin could accommodate weight[i]
        if (j == res):
            bin_rem[res] = c - weight[i]
            res= res+1
    return res

# Driver program
weight = [2, 5, 4, 7, 1, 3, 8]
c = 10
n = len(weight)
print("Number of bins required in First Fit : ",firstFit(weight, n, c))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to find number of bins required using
// First Fit algorithm.
using System;

class GFG
{

// Returns number of bins required using first fit
// online algorithm
static int firstFit(int []weight, int n, int c)
{
    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    int []bin_rem = new int[n];

    // Place items one by one
    for (int i = 0; i < n; i++)
    {
        // Find the first bin that can accommodate
        // weight[i]
        int j;
        for (j = 0; j < res; j++)
        {
            if (bin_rem[j] >= weight[i])
            {
                bin_rem[j] = bin_rem[j] - weight[i];
                break;
            }
        }

        // If no bin could accommodate weight[i]
        if (j == res)
        {
            bin_rem[res] = c - weight[i];
            res++;
        }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int []weight = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = weight.Length;
    Console.Write("Number of bins required in First Fit : "
                    + firstFit(weight, n, c));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find number of bins required using
// First Fit algorithm.

// Returns number of bins required using first fit
// online algorithm
function firstFit(weight,n,c)
{
    // Initialize result (Count of bins)
    let res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    let bin_rem = new Array(n);

    // Place items one by one
    for (let i = 0; i < n; i++)
    {
        // Find the first bin that can accommodate
        // weight[i]
        let j;
        for (j = 0; j < res; j++)
        {
            if (bin_rem[j] >= weight[i])
            {
                bin_rem[j] = bin_rem[j] - weight[i];
                break;
            }
        }

        // If no bin could accommodate weight[i]
        if (j == res)
        {
            bin_rem[res] = c - weight[i];
            res++;
        }
    }
    return res;
}

// Driver program
let weight=[ 2, 5, 4, 7, 1, 3, 8];
let c = 10;
let n = weight.length;
document.write("Number of bins required in First Fit : "
                    + firstFit(weight, n, c));

// This code is contributed by patel2127
</script>
```

**输出:**

```
Number of bins required in First Fit : 4
```

上述首次拟合的实现需要 O(n <sup>2</sup> )个时间，但是首次拟合可以使用自平衡二分搜索法树在 O(n Log n)个时间内实现。
如果 M 是最佳箱数，那么 First Fit 使用的箱数不会超过 1.7M。因此，就箱数上限而言，第一次拟合优于下一次拟合。
T4【3】。最佳匹配:
想法是将下一个项目放在最紧的地方。也就是说，把它放在垃圾箱里，以便留下最小的空白空间。

## C++

```
// C++ program to find number
// of bins required using
// Best fit algorithm.
#include <bits/stdc++.h>
using namespace std;

// Returns number of bins required using best fit
// online algorithm
int bestFit(int weight[], int n, int c)
{
    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store
    // remaining space in bins
    // there can be at most n bins
    int bin_rem[n];

    // Place items one by one
    for (int i = 0; i < n; i++) {

        // Find the best bin that can accommodate
        // weight[i]
        int j;

        // Initialize minimum space left and index
        // of best bin
        int min = c + 1, bi = 0;

        for (j = 0; j < res; j++) {
            if (bin_rem[j] >= weight[i] && bin_rem[j] -
                                     weight[i] < min) {
                bi = j;
                min = bin_rem[j] - weight[i];
            }
        }

        // If no bin could accommodate weight[i],
        // create a new bin
        if (min == c + 1) {
            bin_rem[res] = c - weight[i];
            res++;
        }
        else // Assign the item to best bin
            bin_rem[bi] -= weight[i];
    }
    return res;
}

// Driver program
int main()
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = sizeof(weight) / sizeof(weight[0]);
    cout << "Number of bins required in Best Fit : "
         << bestFit(weight, n, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of bins required using
// Best fit algorithm.
class GFG
{

// Returns number of bins
// required using best fit
// online algorithm
static int bestFit(int weight[], int n, int c)
{

    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store
    // remaining space in bins
    // there can be at most n bins
    int []bin_rem = new int[n];

    // Place items one by one
    for (int i = 0; i < n; i++)
    {

        // Find the best bin that
        // can accommodate
        // weight[i]
        int j;

        // Initialize minimum space
        // left and index
        // of best bin
        int min = c + 1, bi = 0;

        for (j = 0; j < res; j++)
        {
            if (bin_rem[j] >= weight[i] &&
                bin_rem[j] - weight[i] < min)
            {
                bi = j;
                min = bin_rem[j] - weight[i];
            }
        }

        // If no bin could accommodate weight[i],
        // create a new bin
        if (min == c + 1)
        {
            bin_rem[res] = c - weight[i];
            res++;
        }
        else // Assign the item to best bin
            bin_rem[bi] -= weight[i];
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int []weight = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = weight.length;
    System.out.print("Number of bins required in Best Fit : "
                        + bestFit(weight, n, c));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find number
# of bins required using
# First Fit algorithm.

# Returns number of bins required
# using first fit
# online algorithm
def firstFit(weight, n, c):

    # Initialize result (Count of bins)
    res = 0;

    # Create an array to store
    # remaining space in bins
    # there can be at most n bins
    bin_rem = [0]*n;

    # Place items one by one
    for i in range(n):

        # Find the first bin that
        # can accommodate
        # weight[i]
        j = 0;

        # Initialize minimum space
        # left and index
        # of best bin
        min = c + 1;
        bi = 0;

        for j in range(res):
            if (bin_rem[j] >= weight[i] and bin_rem[j] -
                                       weight[i] < min):
                bi = j;
                min = bin_rem[j] - weight[i];

        # If no bin could accommodate weight[i],
        # create a new bin
        if (min == c + 1):
            bin_rem[res] = c - weight[i];
            res += 1;
        else: # Assign the item to best bin
            bin_rem[bi] -= weight[i];
    return res;

# Driver code
if __name__ == '__main__':
    weight = [ 2, 5, 4, 7, 1, 3, 8 ];
    c = 10;
    n = len(weight);
    print("Number of bins required in First Fit : ",
                             firstFit(weight, n, c));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find number
// of bins required using
// Best fit algorithm.
using System;

class GFG {

    // Returns number of bins
    // required using best fit
    // online algorithm
    static int bestFit(int[] weight, int n, int c)
    {

        // Initialize result (Count of bins)
        int res = 0;

        // Create an array to store
        // remaining space in bins
        // there can be at most n bins
        int[] bin_rem = new int[n];

        // Place items one by one
        for (int i = 0; i < n; i++) {

            // Find the best bin that
            // can accommodate
            // weight[i]
            int j;

            // Initialize minimum space
            // left and index
            // of best bin
            int min = c + 1, bi = 0;

            for (j = 0; j < res; j++) {
                if (bin_rem[j] >= weight[i]
                    && bin_rem[j] - weight[i] < min) {
                    bi = j;
                    min = bin_rem[j] - weight[i];
                }
            }

            // If no bin could accommodate weight[i],
            // create a new bin
            if (min == c + 1) {
                bin_rem[res] = c - weight[i];
                res++;
            }

            // Assign the item to best bin
            else
                bin_rem[bi] -= weight[i];
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] weight = { 2, 5, 4, 7, 1, 3, 8 };
        int c = 10;
        int n = weight.Length;
        Console.Write(
            "Number of bins required in Best Fit : "
            + bestFit(weight, n, c));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to find number
// of bins required using
// Best fit algorithm.
// Returns number of bins
    // required using best fit
    // online algorithm
    function bestFit(weight , n , c) {

        // Initialize result (Count of bins)
        var res = 0;

        // Create an array to store
        // remaining space in bins
        // there can be at most n bins
        var bin_rem = Array(n).fill(0);

        // Place items one by one
        for (i = 0; i < n; i++) {

            // Find the best bin that
            // can accommodate
            // weight[i]
            var j;

            // Initialize minimum space
            // left and index
            // of best bin
            var min = c + 1, bi = 0;

            for (j = 0; j < res; j++) {
                if (bin_rem[j] >= weight[i] && bin_rem[j] - weight[i] < min) {
                    bi = j;
                    min = bin_rem[j] - weight[i];
                }
            }

            // If no bin could accommodate weight[i],
            // create a new bin
            if (min == c + 1) {
                bin_rem[res] = c - weight[i];
                res++;
            } else // Assign the item to best bin
                bin_rem[bi] -= weight[i];
        }
        return res;
    }

    // Driver code

        var weight = [ 2, 5, 4, 7, 1, 3, 8 ];
        var c = 10;
        var n = weight.length;
        document.write("Number of bins required in Best Fit : " + bestFit(weight, n, c));

// This code contributed by gauravrajput1
</script>
```

**输出:**

```
Number of bins required in Best Fit : 4
```

最佳拟合也可以使用自平衡二分搜索法树在 0(n 乘 n)时间内实现。
如果 M 是最佳箱数，那么最佳拟合使用的箱数不会超过 1.7M。因此，最佳拟合与第一次拟合相同，在箱数上限方面优于下一次拟合。
**4。最不合适:**
这个想法是把下一件物品放在最不紧的地方，以平衡垃圾箱。也就是说，把它放在垃圾箱里，这样就剩下了大部分的空白空间。

## C++

```
// C++ program to find number of bins required using
// Worst fit algorithm.
#include <bits/stdc++.h>
using namespace std;

// Returns number of bins required using worst fit
// online algorithm
int worstFit(int weight[], int n, int c)
{
    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    int bin_rem[n];

    // Place items one by one
    for (int i = 0; i < n; i++) {
        // Find the best bin that ca\n accommodate
        // weight[i]
        int j;

        // Initialize maximum space left and index
        // of worst bin
        int mx = -1, wi = 0;

        for (j = 0; j < res; j++) {
            if (bin_rem[j] >= weight[i] && bin_rem[j] - weight[i] > mx) {
                wi = j;
                mx = bin_rem[j] - weight[i];
            }
        }

        // If no bin could accommodate weight[i],
        // create a new bin
        if (mx == -1) {
            bin_rem[res] = c - weight[i];
            res++;
        }
        else // Assign the item to best bin
            bin_rem[wi] -= weight[i];
    }
    return res;
}

// Driver program
int main()
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = sizeof(weight) / sizeof(weight[0]);
    cout << "Number of bins required in Worst Fit : "
         << worstFit(weight, n, c);
    return 0;
}

// This code is contributed by gromperen
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of bins required using
// Worst fit algorithm.
class GFG
{

// Returns number of bins required using worst fit
// online algorithm
static int worstFit(int weight[], int n, int c)
{

    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    int bin_rem[]= new int[n];

    // Place items one by one
    for (int i = 0; i < n; i++)
    {

        // Find the best bin that ca\n accommodate
        // weight[i]
        int j;

        // Initialize maximum space left and index
        // of worst bin
        int mx = -1, wi = 0;

        for (j = 0; j < res; j++) {
            if (bin_rem[j] >= weight[i] && bin_rem[j] - weight[i] > mx) {
                wi = j;
                mx = bin_rem[j] - weight[i];
            }
        }

        // If no bin could accommodate weight[i],
        // create a new bin
        if (mx == -1) {
            bin_rem[res] = c - weight[i];
            res++;
        }
        else // Assign the item to best bin
            bin_rem[wi] -= weight[i];
    }
    return res;
}

// Driver program
public static void main(String[] args)
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = weight.length;
    System.out.print("Number of bins required in Worst Fit : " +worstFit(weight, n, c));
}
}

// This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to find number of bins required using
// Worst fit algorithm.
using System;
class GFG
{

// Returns number of bins required using worst fit
// online algorithm
static int worstFit(int []weight, int n, int c)
{

    // Initialize result (Count of bins)
    int res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    int []bin_rem= new int[n];

    // Place items one by one
    for (int i = 0; i < n; i++)
    {

        // Find the best bin that ca\n accommodate
        // weight[i]
        int j;

        // Initialize maximum space left and index
        // of worst bin
        int mx = -1, wi = 0;

        for (j = 0; j < res; j++) {
            if (bin_rem[j] >= weight[i] && bin_rem[j] - weight[i] > mx) {
                wi = j;
                mx = bin_rem[j] - weight[i];
            }
        }

        // If no bin could accommodate weight[i],
        // create a new bin
        if (mx == -1) {
            bin_rem[res] = c - weight[i];
            res++;
        }
        else // Assign the item to best bin
            bin_rem[wi] -= weight[i];
    }
    return res;
}

// Driver program
public static void Main(String[] args)
{
    int []weight = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = weight.Length;
    Console.Write("Number of bins required in Worst Fit : " +worstFit(weight, n, c));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// javascript program to find number of bins required using
// Worst fit algorithm.
// Returns number of bins required using worst fit
// online algorithm
function worstFit( weight,  n,  c)
{

    // Initialize result (Count of bins)
    var res = 0;

    // Create an array to store remaining space in bins
    // there can be at most n bins
    var bin_rem = Array(n).fill(0);

    // Place items one by one
    for (var i = 0; i < n; i++)
    {

        // Find the best bin that ca\n accommodate
        // weight[i]
        var j;

        // Initialize maximum space left and index
        // of worst bin
        var mx = -1, wi = 0;

        for (j = 0; j < res; j++) {
            if (bin_rem[j] >= weight[i] && bin_rem[j] - weight[i] > mx) {
                wi = j;
                mx = bin_rem[j] - weight[i];
            }
        }

        // If no bin could accommodate weight[i],
        // create a new bin
        if (mx == -1) {
            bin_rem[res] = c - weight[i];
            res++;
        }
        else // Assign the item to best bin
            bin_rem[wi] -= weight[i];
    }
    return res;
}

// Driver program
    var weight = [ 2, 5, 4, 7, 1, 3, 8 ];
    var c = 10;
    var n = weight.length;
    document.write("Number of bins required in Worst Fit : " +worstFit(weight, n, c));

// This code is contributed by shivanisinghss2110

</script>
```

**输出:**

```
Number of bins required in Worst Fit : 4
```

最差拟合也可以使用自平衡二分搜索法树在 0(n 乘 n)时间内实现。
如果 M 是最佳箱数，那么最佳拟合使用的箱数不会超过 2M-2。因此，就箱数上限而言，最差拟合与下一次拟合相同。

**离线算法**
在离线版本中，我们有所有的前期项目。不幸的是，离线版本也是 NP 完全的，但是我们有一个更好的近似算法。如果最佳值为 M.
**4，第一次拟合递减最多使用(4M + 1)/3 个面元。第一个适合度递减:**
在线算法的一个问题是打包大项目很困难，尤其是如果它们出现在序列的后期。我们可以通过对输入序列进行排序，并将大项目放在第一位来避免这种情况。通过排序，我们得到第一次拟合递减和最佳拟合递减，作为在线第一次拟合和最佳拟合的离线模拟。

## C++

```
// C++ program to find number of bins required using
// First Fit Decreasing algorithm.
#include <bits/stdc++.h>
using namespace std;

/* Copy firstFit() from above */

// Returns number of bins required using first fit
// decreasing offline algorithm
int firstFitDec(int weight[], int n, int c)
{
    // First sort all weights in decreasing order
    sort(weight, weight + n, std::greater<int>());

    // Now call first fit for sorted items
    return firstFit(weight, n, c);
}

// Driver program
int main()
{
    int weight[] = { 2, 5, 4, 7, 1, 3, 8 };
    int c = 10;
    int n = sizeof(weight) / sizeof(weight[0]);
    cout << "Number of bins required in First Fit "
         << "Decreasing : " << firstFitDec(weight, n, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of bins required using
// First Fit Decreasing algorithm.
import java.util.*;

class GFG
{

    /* Copy firstFit() from above */

    // Returns number of bins required using first fit
    // decreasing offline algorithm
    static int firstFitDec(Integer weight[], int n, int c)
    {

        // First sort all weights in decreasing order
        Arrays.sort(weight, Collections.reverseOrder());

        // Now call first fit for sorted items
        return firstFit(weight, n, c);
    }

    // Driver code
    public static void main(String[] args)
    {
        Integer weight[] = { 2, 5, 4, 7, 1, 3, 8 };
        int c = 10;
        int n = weight.length;
        System.out.print("Number of bins required in First Fit " + "Decreasing : "
        + firstFitDec(weight, n, c));
    }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find number of bins required using
// First Fit Decreasing algorithm.
using System;

public class GFG
{

    /* Copy firstFit() from above */

    // Returns number of bins required using first fit
    // decreasing offline algorithm
    static int firstFitDec(int []weight, int n, int c)
    {

        // First sort all weights in decreasing order
        Array.Sort(weight);
        Array.Reverse(weight);

        // Now call first fit for sorted items
        return firstFit(weight, n, c);
    }
    static int firstFit(int []weight, int n, int c)
    {
        // Initialize result (Count of bins)
        int res = 0;

        // Create an array to store remaining space in bins
        // there can be at most n bins
        int []bin_rem = new int[n];

        // Place items one by one
        for (int i = 0; i < n; i++)
        {
            // Find the first bin that can accommodate
            // weight[i]
            int j;
            for (j = 0; j < res; j++)
            {
                if (bin_rem[j] >= weight[i])
                {
                    bin_rem[j] = bin_rem[j] - weight[i];
                    break;
                }
            }

            // If no bin could accommodate weight[i]
            if (j == res)
            {
                bin_rem[res] = c - weight[i];
                res++;
            }
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []weight = { 2, 5, 4, 7, 1, 3, 8 };
        int c = 10;
        int n = weight.Length;
        Console.Write("Number of bins required in First Fit " + "Decreasing : "
        + firstFitDec(weight, n, c));
    }
}

// This code is contributed by 29AjayKumar
```

**输出:**

```
Number of bins required in First Fit Decreasing : 3
```

第一次拟合递减为样本输入产生最佳结果，因为项目是先排序的。
首次拟合递减也可以使用自平衡二分搜索法树在 O(n Log n)时间内实现。
本文由**泽拉杰·古普塔**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论