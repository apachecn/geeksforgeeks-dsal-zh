# 大小为 2 的分组之间的最小差异

> 原文： [https://www.geeksforgeeks.org/minimum-difference-between-groups-of-size-two/](https://www.geeksforgeeks.org/minimum-difference-between-groups-of-size-two/)

给定一个偶数个元素的数组，请使用这些数组元素形成 2 个组，以使总和最高的组与总和最低的组之间的差异最小。

**注意**：一个元素只能是一个组的一部分，并且必须是至少一个组的一部分。

**示例**：

```
Input : arr[] = {2, 6, 4, 3}
Output : 1
Groups formed will be (2, 6) and (4, 3), 
the difference between highest sum group
(2, 6) i.e 8 and lowest sum group (3, 4)
i.e 7 is 1.

Input : arr[] = {11, 4, 3, 5, 7, 1}
Output : 3
Groups formed will be (1, 11), (4, 5) and
(3, 7), the difference between highest 
sum group (1, 11) i.e 12 and lowest sum 
group (4, 5) i.e 9 is 3.

```



**简单方法**：一种简单方法是尝试对数组元素的所有组合进行检查，并检查总和最高的组和总和最低的组之间组合差异的每组。 总共将形成`n * (n-1) / 2`个这样的基团`C(n, 2)`。

时间复杂度：`O(n ^ 3)`要生成组，需要进行`n ^ 2`次迭代，并针对每个组进行`n`次迭代，因此在最坏的情况下，需要`n ^ 3`次迭代。

**有效方法**：有效方法是使用贪婪方法。 通过从数组的开头选择一个元素，然后从结尾选择一个元素，对整个数组进行排序并生成组。

## C++ 

```cpp

// CPP program to find minimum difference 
// between groups of highest and lowest 
// sums. 
#include <bits/stdc++.h> 
#define ll long long int 
using namespace std; 

ll calculate(ll a[], ll n) 
{ 
    // Sorting the whole array. 
    sort(a, a + n);  

    // Generating sum groups. 
    vector<ll> s; 
    for (int i = 0, j = n - 1; i < j; i++, j--)  
       s.push_back(a[i] + a[j]); 

    ll mini = *min_element(s.begin(), s.end());  
    ll maxi = *max_element(s.begin(), s.end());  

    return abs(maxi - mini); 
} 

int main() 
{ 
    ll a[] = { 2, 6, 4, 3 }; 
    int n = sizeof(a) / (sizeof(a[0])); 
    cout << calculate(a, n) << endl; 
    return 0; 
} 

```

## Java

```java
// Java program to find minimum 
// difference between groups of  
// highest and lowest sums. 
import java.util.Arrays; 
import java.util.Collections; 
import java.util.Vector; 
  
  
class GFG { 
  
static long calculate(long a[], int n) 
{ 
    // Sorting the whole array. 
    Arrays.sort(a);  
    int i,j; 
      
    // Generating sum groups. 
    Vector<Long> s = new Vector<>(); 
    for (i = 0, j = n - 1; i < j; i++, j--)  
        s.add((a[i] + a[j])); 
          
    long mini = Collections.min(s); 
    long maxi = Collections.max(s);  
    return Math.abs(maxi - mini); 
} 
  
// Driver code 
public static void main(String[] args)  
{ 
    long a[] = { 2, 6, 4, 3 }; 
    int n = a.length; 
    System.out.println(calculate(a, n)); 
    } 
}  
// This code is contributed by 29AjayKumar
```

## Python3

```py
# Python3 program to find minimum  
# difference between groups of  
# highest and lowest sums. 
def calculate(a, n): 
      
    # Sorting the whole array. 
    a.sort();  
  
    # Generating sum groups. 
    s = []; 
    i = 0; 
    j = n - 1; 
    while(i < j): 
        s.append((a[i] + a[j])); 
        i += 1; 
        j -= 1; 
  
    mini = min(s);  
    maxi = max(s);  
  
    return abs(maxi - mini); 
  
# Driver Code 
a = [ 2, 6, 4, 3 ]; 
n = len(a); 
print(calculate(a, n)); 
  
# This is contributed by mits
```

## C#

```cs
// C# program to find minimum 
// difference between groups of  
// highest and lowest sums. 
using System; 
using System.Linq; 
using System.Collections.Generic; 
  
class GFG  
{ 
  
    static long calculate(long []a, int n) 
    { 
        // Sorting the whole array. 
        Array.Sort(a);  
        int i, j; 
  
        // Generating sum groups. 
        List<long> s = new List<long>(); 
        for (i = 0, j = n - 1; i < j; i++, j--)  
            s.Add((a[i] + a[j])); 
  
        long mini = s.Min(); 
        long maxi = s.Max();  
        return Math.Abs(maxi - mini); 
    } 
  
    // Driver code 
    public static void Main()  
    { 
        long []a = { 2, 6, 4, 3 }; 
        int n = a.Length; 
        Console.WriteLine(calculate(a, n)); 
    } 
} 
  
//This code is contributed by Rajput-Ji
```

## PHP

```php
<?php 
// PHP program to find minimum  
// difference between groups of  
// highest and lowest sums. 
  
function calculate($a, $n) 
{ 
    // Sorting the whole array. 
    sort($a);  
  
    // Generating sum groups. 
    $s = array(); 
    for ($i = 0, $j = $n - 1;  
         $i < $j; $i++, $j--)  
    array_push($s, ($a[$i] + $a[$j])); 
  
    $mini = min($s);  
    $maxi = max($s);  
  
    return abs($maxi - $mini); 
} 
  
// Driver Code 
$a = array( 2, 6, 4, 3 ); 
$n = sizeof($a); 
echo calculate($a, $n); 
  
// This is contributed by mits  
?>
```

输出：

```
1
```

时间复杂度：`O (n * log n)`。