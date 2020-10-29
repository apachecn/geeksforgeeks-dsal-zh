# 平均分为两组，以便一组具有最大不同的元素

> 原文：[https://www.geeksforgeeks.org/equally-divide-into-two-sets-such-that-one-set-has-maximum-distinct-elements/](https://www.geeksforgeeks.org/equally-divide-into-two-sets-such-that-one-set-has-maximum-distinct-elements/)

有两个进程 P1 和 P2，以及 N 个资源，其中 N 是偶数。 有一个大小为 N 的数组，并且 arr [i]表示第 i 种资源的类型。可能有一个以上的资源实例。您将在 P1 和 P2 之间平均分配这些资源，以使最大数量的不同资源数 分配给 P2。 打印分配给 P2 的最大不同资源数。

**示例**：

> 输入：arr [] = [1、2、2、3、3]
> 输出：3
> 说明：
> 有三种不同的资源（1、2 和 3），其中两种 每种。 最佳分配：流程 P1 有资源[1、2、3]，流程 P2 也有礼物[1、2、3]。 进程 p2 具有 3 个不同的资源。
> 
> arr [] = [1，1，2，1，3，4]
> 输出：3
> 说明：
> 存在三种不同类型的资源（1、2、3、4），3 个实例 1 和资源 2、3、4 的单个单个实例。最优分配：进程 P1 具有资源[1、1、1]，进程 P2 具有赠品[2、3、4]。
> 流程 p2 具有 3 个不同的资源。

**方法 1（使用排序）**：

1.对资源数组进行排序。

2.通过比较排序后的数组的相邻元素找出唯一的元素。假设 count 在数组中拥有不同数量的资源。

3.返回最小计数和 N / 2。

时间复杂度-`O(n Log n)`

## C++

```cpp

// C++ program to equally divide n elements 
// into two sets such that second set has 
// maximum distinct elements. 
#include <algorithm> 
#include <iostream> 
using namespace std; 

int distribution(int arr[], int n) 
{ 
    sort(arr, arr + n); 
    int count = 1; 
    for (int i = 1; i < n; i++)  
        if (arr[i] > arr[i - 1]) 
            count++; 

    return min(count, n / 2); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 1, 2, 1, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << distribution(arr, n) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to equally divide n elements 
// into two sets such that second set has 
// maximum distinct elements. 
import java.util.*; 
class Geeks { 

static int distribution(int arr[], int n) 
{ 
    Arrays.sort(arr); 
    int count = 1; 
    for (int i = 1; i < n; i++)  
        if (arr[i] > arr[i - 1]) 
            count++; 

    return Math.min(count, n / 2); 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int arr[] = { 1, 1, 2, 1, 3, 4 }; 
    int n = arr.length; 
    System.out.println(distribution(arr, n)); 
} 
} 

// This code is contributed by ankita_saini 

```

## Python3

```py

# Python 3 program to equally divide n  
# elements into two sets such that second  
# set has maximum distinct elements. 

def distribution(arr, n): 
    arr.sort(reverse = False) 
    count = 1
    for i in range(1, n, 1): 
        if (arr[i] > arr[i - 1]): 
            count += 1

    return min(count, n / 2) 

# Driver code 
if __name__ == '__main__': 
    arr = [1, 1, 2, 1, 3, 4]  
    n = len(arr) 
    print(int(distribution(arr, n))) 

# This code is contributed by 
# Shashank_Sharma 

```

## C#

```cs

// C# program to equally divide  
// n elements into two sets such  
// that second set has maximum 
// distinct elements. 
using System; 

class GFG  
{ 
static int distribution(int []arr, int n) 
{ 
    Array.Sort(arr); 
    int count = 1; 
    for (int i = 1; i < n; i++)  
        if (arr[i] > arr[i - 1]) 
            count++; 

    return Math.Min(count, n / 2); 
} 

// Driver code 
public static void Main(String []args) 
{ 
    int []arr= { 1, 1, 2, 1, 3, 4 }; 
    int n = arr.Length; 
    Console.WriteLine(distribution(arr, n)); 
} 
} 

// This code is contributed  
// by ankita_saini 

```

## PHP

```php

<?php 
// PHP program to equally divide n elements 
// into two sets such that second set has 
// maximum distinct elements. 

function distribution($arr, $n) 
{ 
    sort($arr); 
    $count = 1; 
    for ($i = 1; $i <$n; $i++)  
        if ($arr[$i] > $arr[$i - 1]) 
            $count++; 

    return min($count, $n / 2); 
} 

// Driver code 
$arr = array(1, 1, 2, 1, 3, 4 ); 
$n = count($arr); 
echo(distribution($arr, $n)); 

// This code is contributed  
// by inder_verma 
?> 

```

**输出**：

```
3
```

**方法 2（使用哈希集）**

另一种查找独特元素的方法是，将所有元素插入集合中。 通过集合的属性，它将仅包含唯一元素。 最后，我们可以计算集合中元素的数量，例如 count。 要返回的值将再次由 min（count，n / 2）给出。

## C++

```cpp

// C++ program to equally divide n elements 
// into two sets such that second set has 
// maximum distinct elements. 
#include <bits/stdc++.h> 
using namespace std; 

int distribution(int arr[], int n) 
{ 
    unordered_set<int, greater<int> > resources; 

    // Insert all the resources in the set 
    // There will be unique resources in the set 
    for (int i = 0; i < n; i++)  
        resources.insert(arr[i]);     

    // return minimum of distinct resources 
    // and n/2 
    return min(resources.size(), n / 2); 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 1, 2, 1, 3, 4 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << distribution(arr, n) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to equally divide n elements 
// into two sets such that second set has 
// maximum distinct elements. 
import java.util.*; 

class GFG 
{ 

static int distribution(int arr[], int n) 
{ 
    Set<Integer> resources = new HashSet<Integer>(); 

    // Insert all the resources in the set 
    // There will be unique resources in the set 
    for (int i = 0; i < n; i++)  
        resources.add(arr[i]);  

    // return minimum of distinct resources 
    // and n/2 
    return Math.min(resources.size(), n / 2); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = { 1, 1, 2, 1, 3, 4 }; 
    int n = arr.length; 
    System.out.print(distribution(arr, n) +"\n"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to equally divide n elements 
# into two sets such that second set has 
# maximum distinct elements. 
def distribution(arr, n): 
    resources = set() 

    # Insert all the resources in the set 
    # There will be unique resources in the set 
    for i in range(n): 
        resources.add(arr[i]); 

        # return minimum of distinct resources 
        # and n/2 
    return min(len(resources), n // 2); 

# Driver code 
if __name__ == '__main__': 
    arr = [ 1, 1, 2, 1, 3, 4 ]; 
    n = len(arr); 
    print(distribution(arr, n), ""); 

# This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# program to equally divide n elements 
// into two sets such that second set has 
// maximum distinct elements. 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

static int distribution(int []arr, int n) 
{ 
    HashSet<int> resources = new HashSet<int>(); 

    // Insert all the resources in the set 
    // There will be unique resources in the set 
    for (int i = 0; i < n; i++)  
        resources.Add(arr[i]);  

    // return minimum of distinct resources 
    // and n/2 
    return Math.Min(resources.Count, n / 2); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []arr = { 1, 1, 2, 1, 3, 4 }; 
    int n = arr.Length; 
    Console.Write(distribution(arr, n) +"\n"); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
3
```



* * *

* * *



