# 查询后缀

中不同整数的个数

> 原文:[https://www . geesforgeks . org/query-for-number-of-distinct-in-integer-in-suffix/](https://www.geeksforgeeks.org/queries-for-number-of-distinct-integers-in-suffix/)

给定一个由 **N** 元素和 **Q** 查询组成的数组，其中每个查询包含一个整数 **K** 。对于每个查询，任务是在从 **K <sup>th</sup>** 元素到 **N <sup>th</sup>** 元素的后缀中找到不同整数的数量。
**举例:**

```
Input :
N=5, Q=3
arr[] = {2, 4, 6, 10, 2}
1
3
2
Output :
4
3
4
```

**方法:**
可以通过预计算从 **N-1** 到 **0** 的所有指标的解来解决问题。想法是在 C++中使用无序集，因为该集不允许重复元素。
从头到尾遍历数组，将当前元素添加到集合中，当前索引的答案就是集合的大小。因此，将当前索引处集合的大小存储在一个辅助数组中，比如后缀 Count。
以下是上述方法的实施:

## C++

```
// C++ program to find distinct
// elements in suffix

#include <bits/stdc++.h>
using namespace std;

// Function to answer queries for distinct
// count in Suffix
void printQueries(int n, int a[], int q, int qry[])
{
    // Set to keep the distinct elements
    unordered_set<int> occ;

    int suffixCount[n + 1];

    // Precompute the answer for each suffix
    for (int i = n - 1; i >= 0; i--) {
        occ.insert(a[i]);
        suffixCount[i + 1] = occ.size();
    }

    // Print the precomputed answers
    for (int i = 0; i < q; i++)
        cout << suffixCount[qry[i]] << endl;
}

// Driver Code
int main()
{
    int n = 5, q = 3;
    int a[n] = { 2, 4, 6, 10, 2 };
    int qry[q] = { 1, 3, 2 };

    printQueries(n, a, q, qry);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find distinct
// elements in suffix
import java.util.*;

class GFG
{

// Function to answer queries for distinct
// count in Suffix
static void printQueries(int n, int a[], int q, int qry[])
{
    // Set to keep the distinct elements
    HashSet<Integer> occ = new HashSet<>();

    int []suffixCount = new int[n + 1];

    // Precompute the answer for each suffix
    for (int i = n - 1; i >= 0; i--)
    {
        occ.add(a[i]);
        suffixCount[i + 1] = occ.size();
    }

    // Print the precomputed answers
    for (int i = 0; i < q; i++)
        System.out.println(suffixCount[qry[i]]);
}

// Driver Code
public static void main(String args[])
{
    int n = 5, q = 3;
    int a[] = { 2, 4, 6, 10, 2 };
    int qry[] = { 1, 3, 2 };

    printQueries(n, a, q, qry);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find distinct
# elements in suffix

# Function to answer queries for distinct
# count in Suffix
def printQueries(n, a, q, qry):

    # Set to keep the distinct elements
    occ = dict()

    suffixCount = [0 for i in range(n + 1)]

    # Precompute the answer for each suffix
    for i in range(n - 1, -1, -1):
        occ[a[i]] = 1
        suffixCount[i + 1] = len(occ)

    # Print the precomputed answers
    for i in range(q):
        print(suffixCount[qry[i]])

# Driver Code
n = 5
q = 3
a = [2, 4, 6, 10, 2]
qry = [1, 3, 2]

printQueries(n, a, q, qry)

# This code is contributed by Mohit Kumar 29
```

## C#

```
// C# program to find distinct
// elements in suffix
using System;
using System.Collections.Generic;

public class GFG
{

// Function to answer queries for distinct
// count in Suffix
static void printQueries(int n, int []a, int q, int []qry)
{
    // Set to keep the distinct elements
    HashSet<int> occ = new HashSet<int>();

    int []suffixCount = new int[n + 1];

    // Precompute the answer for each suffix
    for (int i = n - 1; i >= 0; i--)
    {
        occ.Add(a[i]);
        suffixCount[i + 1] = occ.Count;
    }

    // Print the precomputed answers
    for (int i = 0; i < q; i++)
        Console.WriteLine(suffixCount[qry[i]]);
}

// Driver Code
public static void Main(String []args)
{
    int n = 5, q = 3;
    int []a = { 2, 4, 6, 10, 2 };
    int []qry = { 1, 3, 2 };

    printQueries(n, a, q, qry);
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find distinct
// elements in suffix

// Function to answer queries for distinct
// count in Suffix
function printQueries($n, $a, $q, $qry)
{
    // Set to keep the distinct elements
    $occ = array();

    $suffixCount = array_fill(0, $n + 1, 0);

    // Precompute the answer for each suffix
    for ($i = $n - 1; $i >= 0; $i--)
    {
        array_push($occ, $a[$i]);

        # give array of distinct element
        $occ = array_unique($occ);

        $suffixCount[$i + 1] = sizeof($occ);
    }

    // Print the precomputed answers
    for ($i = 0; $i < $q; $i++)
        echo $suffixCount[$qry[$i]], "\n";
}

// Driver Code
$n = 5;
$q = 3;
$a = array(2, 4, 6, 10, 2);
$qry = array(1, 3, 2);

printQueries($n, $a, $q, $qry);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript program to find distinct
// elements in suffix

// Function to answer queries for distinct
// count in Suffix
function printQueries(n,a,q,qry)
{
    // Set to keep the distinct elements
    let occ = new Set();

    let suffixCount = new Array(n + 1);

    // Precompute the answer for each suffix
    for (let i = n - 1; i >= 0; i--)
    {
        occ.add(a[i]);
        suffixCount[i + 1] = occ.size;
    }

    // Print the precomputed answers
    for (let i = 0; i < q; i++)
        document.write(suffixCount[qry[i]]+"<br>");
}

// Driver Code
let  n = 5, q = 3;
let a=[2, 4, 6, 10, 2];
let qry=[ 1, 3, 2 ];
printQueries(n, a, q, qry);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4
3
4
```

**时间复杂度:** O(N)
**辅助空间** : O(N)
**无 STL 方式:**由于需要处理查询，所以需要做预计算。否则，简单遍历后缀就足够了。
辅助阵列**辅助[]** 从阵列右侧保持。数组**标记[]** 存储一个元素是否已经出现在已经遍历的后缀中。如果元素没有出现，则更新 **aux[i] = aux[i+1] + 1** 。否则**辅助[i] =辅助[i+1]** 。
每个查询的答案都是 **aux[q[i]]** 。
以下是上述办法的实施情况。

## C++

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>

#define MAX 100002
using namespace std;

// Function to print no of unique elements
// in specified suffix for each query.
void printUniqueElementsInSuffix(const int* arr,
                                 int n, const int* q, int m)
{

    // aux[i] stores no of unique elements in arr[i..n]
    int aux[MAX];

    // mark[i] = 1 if i has occurred in the suffix at least once.
    int mark[MAX];
    memset(mark, 0, sizeof(mark));

    // Initialization for the last element.
    aux[n - 1] = 1;
    mark[arr[n - 1]] = 1;

    for (int i = n - 2; i >= 0; i--) {
        if (mark[arr[i]] == 0) {
            aux[i] = aux[i + 1] + 1;
            mark[arr[i]] = 1;
        }
        else {
            aux[i] = aux[i + 1];
        }
    }

    for (int i = 0; i < m; i++) {
        cout << aux[q[i] - 1] << "\n";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 1, 2, 3, 4, 10000, 999 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int q[] = { 1, 3, 6 };
    int m = sizeof(q) / sizeof(q[0]);
    printUniqueElementsInSuffix(arr, n, q, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

static int MAX = 100002;

// Function to print no of unique elements
// in specified suffix for each query.
static void printUniqueElementsInSuffix(int[] arr,
                                int n, int[] q, int m)
{

    // aux[i] stores no of unique elements in arr[i..n]
    int []aux = new int[MAX];

    // mark[i] = 1 if i has occurred
    // in the suffix at least once.
    int []mark = new int[MAX];

    // Initialization for the last element.
    aux[n - 1] = 1;
    mark[arr[n - 1]] = 1;

    for (int i = n - 2; i >= 0; i--)
    {
        if (mark[arr[i]] == 0)
        {
            aux[i] = aux[i + 1] + 1;
            mark[arr[i]] = 1;
        }
        else
        {
            aux[i] = aux[i + 1];
        }
    }

    for (int i = 0; i < m; i++)
    {
        System.out.println(aux[q[i] - 1] );
    }
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 1, 2, 3, 4, 1, 2, 3, 4, 10000, 999 };
    int n = arr.length;
    int q[] = { 1, 3, 6 };
    int m = q.length;
    printUniqueElementsInSuffix(arr, n, q, m);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of the above approach.
MAX = 100002;

# Function to prno of unique elements
# in specified suffix for each query.
def printUniqueElementsInSuffix(arr, n, q, m):

    # aux[i] stores no of unique elements in arr[i..n]
    aux = [0] * MAX;

    # mark[i] = 1 if i has occurred
    # in the suffix at least once.
    mark = [0] * MAX;

    # Initialization for the last element.
    aux[n - 1] = 1;
    mark[arr[n - 1]] = 1;

    for i in range(n - 2, -1, -1):
        if (mark[arr[i]] == 0):
            aux[i] = aux[i + 1] + 1;
            mark[arr[i]] = 1;
        else:
            aux[i] = aux[i + 1];

    for i in range(m):
        print(aux[q[i] - 1]);

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 1, 2, 3, 4, 10000, 999];
    n = len(arr);
    q = [1, 3, 6];
    m = len(q);
    printUniqueElementsInSuffix(arr, n, q, m);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{
    static int MAX = 100002;

    // Function to print no of unique elements
    // in specified suffix for each query.
    static void printUniqueElementsInSuffix(int[] arr,
                                    int n, int[] q, int m)
    {

        // aux[i] stores no of unique elements in arr[i..n]
        int []aux = new int[MAX];

        // mark[i] = 1 if i has occurred
        // in the suffix at least once.
        int []mark = new int[MAX];

        // Initialization for the last element.
        aux[n - 1] = 1;
        mark[arr[n - 1]] = 1;

        for (int i = n - 2; i >= 0; i--)
        {
            if (mark[arr[i]] == 0)
            {
                aux[i] = aux[i + 1] + 1;
                mark[arr[i]] = 1;
            }
            else
            {
                aux[i] = aux[i + 1];
            }
        }

        for (int i = 0; i < m; i++)
        {
            Console.WriteLine(aux[q[i] - 1] );
        }
    }

    // Driver code
    static public void Main ()
    {

        int []arr = { 1, 2, 3, 4, 1, 2, 3, 4, 10000, 999 };
        int n = arr.Length;
        int []q = { 1, 3, 6 };
        int m = q.Length;
        printUniqueElementsInSuffix(arr, n, q, m);
    }
}

// This code is contributed by Sachin.
```

## java 描述语言

```
<script>

// javascript implementation of the above approach.

     var MAX = 100002;

    // Function to print no of unique elements
    // in specified suffix for each query.
    function printUniqueElementsInSuffix(arr, n,  q,  m)
    {

        // aux[i] stores no of unique elements in arr[i..n]
        var aux =[] ;
        var mark = [];
        aux.length = MAX ;
        mark.length = MAX ;
        aux.fill(0);
        mark.fill(0);

        // Initialization for the last element.
        aux[n - 1] = 1;
        mark[arr[n - 1]] = 1;

        for (var i = n - 2; i >= 0; i--)
        {
            if (mark[arr[i]] == 0)
            {
                aux[i] = aux[i + 1] + 1;
                mark[arr[i]] = 1;
            }
            else
            {
                aux[i] = aux[i + 1];
            }
        }

        for (var i = 0; i < m; i++)
        {
            document.write(aux[q[i] - 1] , "<br>" );
        }
    }

    // Driver code

        var arr = [ 1, 2, 3, 4, 1, 2, 3, 4, 10000, 999 ]
        var n = arr.length;
        var q = [ 1, 3, 6 ];
        var m = q.length;
        printUniqueElementsInSuffix(arr, n, q, m);

        // This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
6
6
5
```