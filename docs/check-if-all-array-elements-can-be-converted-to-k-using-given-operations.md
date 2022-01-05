# 检查是否所有数组元素都可以用给定的操作转换成 K

> 原文:[https://www . geesforgeks . org/check-if-all-array-elements-can-convert-to-k-use-given-operations/](https://www.geeksforgeeks.org/check-if-all-array-elements-can-be-converted-to-k-using-given-operations/)

给定一个大小为 **N** 的整数数组 **arr** 和一个整数 **K** ，任务是使用以下操作使数组的所有元素等于**K【T7:** 

*   选择任意的**子阵列【l…】。输入数组的**
*   替换该子阵列中等于排序子阵列[l…r]中第**[(r–l)+2)/2]<sup>个</sup>** 值的所有值

**例:**

> **输入:** arr [ ] = {5，4，3，1，2，6，7，8，9，10}，K = 3
> **输出:** YES
> **解释:**
> 选择前五个元素并用 3 替换所有元素:arr = {3，3，3，3，3，3，6，7，8，9，10}
> 现在取第四至第六个元素，用 3 替换所有元素:arr = {3，3，3，3，3，3，3，3，3 10}
> 通过应用相同的操作，我们可以使 arr 的所有元素等于 K: arr = {3，3，3，3，3，3，3，3，3，3}
> **输入:** arr [ ] = {3，1，2，3}，K = 4
> **输出:**否

**进场:**

*   我们可以观察到，只有满足以下两个条件，才有可能使数组的所有元素都等于 **K** :
    1.  必须至少有一个元素等于 **K** 。
    2.  必须存在一个连续的三元组，使得该三元组的任何两个值都大于或等于 k
*   为了解决这个问题，我们需要创建一个辅助数组，比如 **aux[]** ，它包含三个值 0，1，2。
*   最后的任务是检查是否有可能使 **aux** 数组的所有元素都等于 1。如果**aux【】**中三个连续元素中的两个大于 0，那么我们可以取一个大小为 3 的子阵列，并使该子阵列的所有元素等于 1。然后我们将这个逻辑扩展到整个数组。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function that prints
// whether is to possible
// to make all elements
// of the array equal to K
void makeAllK(int a[], int k, int n)
{
    vector<int> aux;

    bool one_found = false;

    // Fill vector aux
    // according to the
    // above approach
    for (int i = 0; i < n; i++) {

        if (a[i] < k)
            aux.push_back(0);

        else if (a[i] == k) {
            aux.push_back(1);
            one_found = true;
        }

        else
            aux.push_back(2);
    }

    // Condition if K
    // does not exist in
    // the given array
    if (one_found == false) {
        cout << "NO"
             << "\n";
        return;
    }

    bool ans = false;

    if (n == 1
        && aux[0] == 1)
        ans = true;

    if (n == 2
        && aux[0] > 0
        && aux[1] > 1)
        ans = true;

    for (int i = 0; i < n - 2; i++) {

        // Condition for minimum
        // two elements is
        // greater than 0 in
        // pair of three elements
        if (aux[i] > 0
            && aux[i + 1] > 0) {

            ans = true;
            break;
        }

        else if (aux[i] > 0
                 && aux[i + 2] > 0) {
            ans = true;
            break;
        }

        else if (aux[i + 2] > 0
                 && aux[i + 1] > 0) {
            ans = true;
            break;
        }
    }

    if (ans == true)
        cout << "YES"
             << "\n";
    else
        cout << "NO"
             << "\n";
}

// Driver Code
int main()
{
    int arr[]
        = { 1, 2, 3,
            4, 5, 6,
            7, 8, 9, 10 };

    int K = 3;

    int size = sizeof(arr)
               / sizeof(arr[0]);

    makeAllK(arr, K, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function that prints
// whether is to possible
// to make all elements
// of the array equal to K
static void makeAllK(int a[], int k, int n)
{
    Vector<Integer> aux = new Vector<Integer>();

    boolean one_found = false;

    // Fill vector aux according
    // to the above approach
    for(int i = 0; i < n; i++)
    {
       if (a[i] < k)
           aux.add(0);

       else if (a[i] == k)
       {
           aux.add(1);
           one_found = true;
       }
       else
           aux.add(2);
    }

    // Condition if K does not 
    // exist in the given array
    if (one_found == false)
    {
        System.out.print("NO" + "\n");
        return;
    }

    boolean ans = false;

    if (n == 1 && aux.get(0) == 1)
        ans = true;

    if (n == 2 && aux.get(0) > 0 &&
                  aux.get(1) > 1)
        ans = true;

    for(int i = 0; i < n - 2; i++)
    {

       // Condition for minimum
       // two elements is
       // greater than 0 in
       // pair of three elements
       if (aux.get(i) > 0 &&
           aux.get(i + 1) > 0)
       {
           ans = true;
           break;
       }
       else if (aux.get(i) > 0 &&
                aux.get(i + 2) > 0)
       {
           ans = true;
           break;
       }
       else if (aux.get(i + 2) > 0 &&
                aux.get(i + 1) > 0)
       {
           ans = true;
           break;
       }
    }

    if (ans == true)
        System.out.print("YES" + "\n");
    else
        System.out.print("NO" + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 };
    int K = 3;
    int size = arr.length;

    makeAllK(arr, K, size);

}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function that prints whether is
# to possible to make all elements
# of the array equal to K
def makeAllK(a, k, n):

    aux = []
    one_found = False

    # Fill vector aux according
    # to the above approach
    for i in range(n):
        if (a[i] < k):
            aux.append(0)

        elif (a[i] == k):
            aux.append(1)
            one_found = True

        else:
            aux.append(2)

    # Condition if K does
    # not exist in the given
    # array
    if (one_found == False):
        print("NO")
        return

    ans = False

    if (n == 1 and aux[0] == 1):
        ans = True

    if (n == 2 and aux[0] > 0 and aux[1] > 1):
        ans = True

    for i in range(n - 2):

        # Condition for minimum two
        # elements is greater than
        # 0 in pair of three elements
        if (aux[i] > 0 and aux[i + 1] > 0):
            ans = True
            break

        elif (aux[i] > 0 and aux[i + 2] > 0):
            ans = True
            break

        elif (aux[i + 2] > 0 and aux[i + 1] > 0):
            ans = True
            break

    if (ans == True):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
    K = 3
    size = len(arr)

    makeAllK(arr, K, size)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that prints
// whether is to possible
// to make all elements
// of the array equal to K
static void makeAllK(int []a, int k, int n)
{
    List<int> aux = new List<int>();

    bool one_found = false;

    // Fill vector aux according
    // to the above approach
    for(int i = 0; i < n; i++)
    {
       if (a[i] < k)
       {
           aux.Add(0);
       }
       else if (a[i] == k)
       {
           aux.Add(1);
           one_found = true;
       }
       else
           aux.Add(2);
    }

    // Condition if K does not
    // exist in the given array
    if (one_found == false)
    {
        Console.Write("NO" + "\n");
        return;
    }

    bool ans = false;
    if (n == 1 && aux[0] == 1)
        ans = true;

    if (n == 2 && aux[0] > 0 &&
                  aux[1] > 1)
        ans = true;

    for(int i = 0; i < n - 2; i++)
    {

       // Condition for minimum
       // two elements is
       // greater than 0 in
       // pair of three elements
       if (aux[i] > 0 &&
           aux[i + 1] > 0)
       {
           ans = true;
           break;
       }
       else if (aux[i] > 0 &&
                aux[i + 2] > 0)
       {
           ans = true;
           break;
       }
       else if (aux[i + 2] > 0 &&
                aux[i + 1] > 0)
       {
           ans = true;
           break;
       }
    }
    if (ans == true)
        Console.Write("YES" + "\n");
    else
        Console.Write("NO" + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10 };
    int K = 3;
    int size = arr.Length;

    makeAllK(arr, K, size);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that prints
// whether is to possible
// to make all elements
// of the array equal to K
function makeAllK(a, k, n)
{
    var aux = [];

    var one_found = false;

    // Fill vector aux
    // according to the
    // above approach
    for (var i = 0; i < n; i++) {

        if (a[i] < k)
            aux.push(0);

        else if (a[i] == k) {
            aux.push(1);
            one_found = true;
        }

        else
            aux.push(2);
    }

    // Condition if K
    // does not exist in
    // the given array
    if (one_found == false) {
        document.write( "NO" + "<br>");
        return;
    }

    var ans = false;

    if (n == 1
        && aux[0] == 1)
        ans = true;

    if (n == 2
        && aux[0] > 0
        && aux[1] > 1)
        ans = true;

    for (var i = 0; i < n - 2; i++) {

        // Condition for minimum
        // two elements is
        // greater than 0 in
        // pair of three elements
        if (aux[i] > 0
            && aux[i + 1] > 0) {

            ans = true;
            break;
        }

        else if (aux[i] > 0
                 && aux[i + 2] > 0) {
            ans = true;
            break;
        }

        else if (aux[i + 2] > 0
                 && aux[i + 1] > 0) {
            ans = true;
            break;
        }
    }

    if (ans == true)
        document.write( "YES"+ "<br>")
    else
        document.write( "NO"+ "<br>")
}

// Driver Code
var arr
    = [1, 2, 3,
        4, 5, 6,
        7, 8, 9, 10];
var K = 3;
var size = arr.length;
makeAllK(arr, K, size);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:O(N)***
***辅助空间:O(N)***