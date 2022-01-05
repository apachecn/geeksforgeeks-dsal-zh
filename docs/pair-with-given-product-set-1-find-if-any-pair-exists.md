# 与给定产品配对|集合 1(查找是否存在配对)

> 原文:[https://www . geesforgeks . org/pair-with-给定产品-set-1-find-if-any-pair-exists/](https://www.geeksforgeeks.org/pair-with-given-product-set-1-find-if-any-pair-exists/)

给定一组不同的元素和一个数字 x，找出是否有乘积等于 x 的对。

**示例:**

```
Input : arr[] = {10, 20, 9, 40};
        int x = 400;
Output : Yes

Input : arr[] = {10, 20, 9, 40};
        int x = 190;
Output : No

Input : arr[] = {-10, 20, 9, -40};
        int x = 400;
Output : Yes

Input : arr[] = {-10, 20, 9, 40};
        int x = -400;
Output : Yes

Input : arr[] = {0, 20, 9, 40};
        int x = 0;
Output : Yes
```

**天真的方法(O(n<sup>2</sup>)**是运行两个循环来考虑所有可能的对。对于每一对，检查乘积是否等于 x。

## C++

```
// A simple C++ program to find if there is a pair
// with given product.
#include<bits/stdc++.h>
using namespace std;

// Returns true if there is a pair in arr[0..n-1]
// with product equal to x.
bool isProduct(int arr[], int n, int x)
{
    // Consider all possible pairs and check for
    // every pair.
    for (int i=0; i<n-1; i++)
       for (int j=i+1; i<n; i++)
          if (arr[i] * arr[j] == x)
              return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = {10, 20, 9, 40};
    int x = 400;
    int n = sizeof(arr)/sizeof(arr[0]);
    isProduct(arr, n, x)? cout << "Yesn"
                        : cout << "Non";
    x = 190;
    isProduct(arr, n, x)? cout << "Yesn"
                        : cout << "Non";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there is a pair
// with given product.
class GFG
{   
    // Returns true if there is a pair in
    // arr[0..n-1] with product equal to x. 
    boolean isProduct(int arr[], int n, int x)
    {
        for (int i=0; i<n-1; i++)
            for (int j=i+1; j<n; j++)
                if (arr[i]*arr[j] == x)
                    return true;
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        GFG g = new GFG();
        int arr[] = {10, 20, 9, 40};
        int x = 400;
        int n = arr.length;
        if (g.isProduct(arr, n, x))
            System.out.println("Yes");
        else
            System.out.println("No");

        x = 190;
        if (g.isProduct(arr, n, x))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}
// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to find if there
# is a pair with given product.

# Returns true if there is a
# pair in arr[0..n-1] with
# product equal to x
def isProduct(arr, n, x):
    for i in arr:
        for j in arr:
            if i * j == x:
                return True
    return False

# Driver code    
arr = [10, 20, 9, 40]
x = 400
n = len(arr)
if(isProduct(arr,n, x) == True):
    print ("Yes")

else:
    print("No")

x = 900
if(isProduct(arr, n, x)):
    print("Yes")

else:
    print("No")

# This code is contributed
# by prerna saini

```

## C#

```
// C# program to find
// if there is a pair
// with given product.
using System;

class GFG
{

// Returns true if there
// is a pair in arr[0..n-1]
// with product equal to x.
static bool isProduct(int []arr,
                      int n, int x)
{
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (arr[i] * arr[j] == x)
                return true;
    return false;
}

// Driver Code
static void Main()
{
    int []arr = {10, 20, 9, 40};
    int x = 400;
    int n = arr.Length;
    if (isProduct(arr, n, x))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    x = 190;
    if (isProduct(arr, n, x))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed
// by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple php program to
// find if there is a pair
// with given product.

// Returns true if there
// is a pair in arr[0..n-1]
// with product equal to x.
function isProduct($arr, $n, $x)
{
    // Consider all possible
    // pairs and check for
    // every pair.
    for ($i = 0;
         $i < $n - 1; $i++)
    for ($j = $i + 1;
         $i < $n; $i++)
        if ($arr[$i] *
            $arr[$j] == $x)
            return true;

    return false;
}

// Driver code
$arr = array(10, 20, 9, 40);
$x = 400;
$n = count($arr);
if(isProduct($arr, $n, $x))
echo "Yes\n";
else
echo "No\n";

$x = 190;
if(isProduct($arr, $n, $x))
echo "Yes\n";
else
echo "No\n";

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to find if there is a pair
// with given product.

// Returns true if there is a pair in arr[0..n-1]
// with product equal to x.
function isProduct(arr, n, x)
{
    // Consider all possible pairs and check for
    // every pair.
    for (var i=0; i<n-1; i++)
    for (var j=i+1; i<n; i++)
        if (arr[i] * arr[j] == x)
            return true;

    return false;
}

// Driver code
var arr = [10, 20, 9, 40];
var x = 400;
var n = arr.length;
isProduct(arr, n, x)? document.write("Yes<br>")
                    : document.write("No<br>");
x = 190;
isProduct(arr, n, x)? document.write("Yes")
                    : document.write("No");

</script>
```

**输出:**

```
Yes
No
```

**更好的解(O(n Log n) :** 我们对给定的数组进行排序。排序后，我们遍历数组，对于 arr[i]的每个元素，我们在 arr[i]右边的子数组中，即在子数组 arr[I+1]中，对 x/arr[i]进行二分搜索法运算..n-1]

**高效解决方案(O(n) ):** 我们可以使用[哈希](http://geeksquiz.com/hashing-set-1-introduction/)将时间复杂度提高到 O(n)。以下是步骤。

1.  创建一个空哈希表
2.  遍历数组元素，并对每个元素 arr[i]执行以下操作。
    *   如果 arr[i]为 0，x 也为 0，则返回 true，否则忽略 arr[i]。
    *   如果 x % arr[i]为 0，并且表中存在 x/arr[i]，则返回 true。
    *   将 arr[i]插入哈希表。
3.  返回 false

以下是上述想法的实现。

## C++

```
// C++ program to find if there is a pair
// with given product.
#include<bits/stdc++.h>
using namespace std;

// Returns true if there is a pair in arr[0..n-1]
// with product equal to x.
bool isProduct(int arr[], int n, int x)
{
    if (n < 2)
        return false;

    // Create an empty set and insert first
    // element into it
    unordered_set<int> s;

    // Traverse remaining elements
    for (int i=0; i<n; i++)
    {
        // 0 case must be handles explicitly as
        // x % 0 is undefined behaviour in C++
        if (arr[i] == 0)
        {
           if (x == 0)
               return true;
           else
               continue;
        }

        // x/arr[i] exists in hash, then we
        // found a pair
        if (x%arr[i] == 0)
        {
            if (s.find(x/arr[i]) != s.end())
               return true;

            // Insert arr[i]
            s.insert(arr[i]);
        }
    }
    return false;
}

// Driver code
int main()
{
    int arr[] = {10, 20, 9, 40};
    int x = 400;

    int n = sizeof(arr)/sizeof(arr[0]);
    isProduct(arr, n, x)? cout << "Yes\n"
                       : cout << "Non";

    x = 190;
    isProduct(arr, n, x)? cout << "Yes\n"
                        : cout << "Non";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program if there exists a pair for given product
import java.util.HashSet;

class GFG
{
    // Returns true if there is a pair in arr[0..n-1]
    // with product equal to x.
    static boolean isProduct(int arr[], int n, int x)
    {
        // Create an empty set and insert first
        // element into it
        HashSet<Integer> hset = new HashSet<>();

        if(n < 2)
            return false;

        // Traverse remaining elements
        for(int i = 0; i < n; i++)
        {
            // 0 case must be handles explicitly as
            // x % 0 is undefined
            if(arr[i] == 0)
            {
                if(x == 0)
                    return true;
                else
                    continue;
            }

            // x/arr[i] exists in hash, then we
            // found a pair
            if(x % arr[i] == 0)
            {
                if(hset.contains(x / arr[i]))
                    return true;

            // Insert arr[i]
            hset.add(arr[i]);
            }
        }
        return false;
    }

    // driver code
    public static void main(String[] args)
    {
        int arr[] = {10, 20, 9, 40};
        int x = 400;
        int n = arr.length;

        if(isProduct(arr, arr.length, x))
        System.out.println("Yes");
        else
        System.out.println("No");

        x = 190;

        if(isProduct(arr, arr.length, x))
        System.out.println("Yes");
        else
        System.out.println("No");
    }
}

// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to find if there
# is a pair with the given product.

# Returns true if there is a pair in
# arr[0..n-1] with product equal to x.
def isProduct(arr, n, x):

    if n < 2:
        return False

    # Create an empty set and insert
    # first element into it
    s = set()

    # Traverse remaining elements
    for i in range(0, n):

        # 0 case must be handles explicitly as
        # x % 0 is undefined behaviour in C++
        if arr[i] == 0:

            if x == 0:
                return True
            else:
                continue

        # x/arr[i] exists in hash, then
        # we found a pair
        if x % arr[i] == 0:

            if x // arr[i] in s:
                return True

            # Insert arr[i]
            s.add(arr[i])

    return False

# Driver code
if __name__ == "__main__":

    arr = [10, 20, 9, 40]
    x = 400

    n = len(arr)
    if isProduct(arr, n, x):
        print("Yes")
    else:
        print("No")

    x = 190
    if isProduct(arr, n, x):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# program if there exists a
// pair for given product
using System;
using System.Collections.Generic;

class GFG
{
// Returns true if there is a pair
// in arr[0..n-1] with product equal to x.
public static bool isProduct(int[] arr,
                             int n, int x)
{
    // Create an empty set and insert
    // first element into it
    HashSet<int> hset = new HashSet<int>();

    if (n < 2)
    {
        return false;
    }

    // Traverse remaining elements
    for (int i = 0; i < n; i++)
    {
        // 0 case must be handles explicitly
        // as x % 0 is undefined
        if (arr[i] == 0)
        {
            if (x == 0)
            {
                return true;
            }
            else
            {
                continue;
            }
        }

        // x/arr[i] exists in hash, then
        // we found a pair
        if (x % arr[i] == 0)
        {
            if (hset.Contains(x / arr[i]))
            {
                return true;
            }

        // Insert arr[i]
        hset.Add(arr[i]);
        }
    }
    return false;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {10, 20, 9, 40};
    int x = 400;
    int n = arr.Length;

    if (isProduct(arr, arr.Length, x))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }

    x = 190;

    if (isProduct(arr, arr.Length, x))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program if there exists a pair for given product

// Returns true if there is a pair in arr[0..n-1]
    // with product equal to x.
    function isProduct(arr, n, x)
    {
        // Create an empty set and insert first
        // element into it
        let hset = new Set();

        if(n < 2)
            return false;

        // Traverse remaining elements
        for(let i = 0; i < n; i++)
        {
            // 0 case must be handles explicitly as
            // x % 0 is undefined
            if(arr[i] == 0)
            {
                if(x == 0)
                    return true;
                else
                    continue;
            }

            // x/arr[i] exists in hash, then we
            // found a pair
            if(x % arr[i] == 0)
            {
                if(hset.has(x / arr[i]))
                    return true;

            // Insert arr[i]
            hset.add(arr[i]);
            }
        }
        return false;
    }

// Driver program

         let arr = [10, 20, 9, 40];
        let x = 400;
        let n = arr.length;

        if(isProduct(arr, arr.length, x))
            document.write("Yes" + "<br/>");
        else
            document.write("No" + "<br/>");

        x = 190;

        if(isProduct(arr, arr.length, x))
            document.write("Yes" + "<br/>");
        else
            document.write("No" + "<br/>");

</script>
```

**输出:**

```
Yes
No
```

在下一集，我们将讨论打印所有产品等于 0 的对的方法。
本文由**舒巴姆·戈亚尔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息