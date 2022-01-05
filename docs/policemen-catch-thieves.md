# 警察抓小偷

> 原文:[https://www.geeksforgeeks.org/policemen-catch-thieves/](https://www.geeksforgeeks.org/policemen-catch-thieves/)

给定大小为 n 的数组，该数组具有以下规格:

1.  数组中的每个元素要么包含一个警察，要么包含一个小偷。
2.  每个警察只能抓一个小偷。
3.  警察抓不到离警察超过 K 个单位的小偷。

我们需要找到最多能抓到多少小偷。
示例:

```
Input : arr[] = {'P', 'T', 'T', 'P', 'T'},
            k = 1.
Output : 2.
Here maximum 2 thieves can be caught, first
policeman catches first thief and second police-
man can catch either second or third thief.

Input : arr[] = {'T', 'T', 'P', 'P', 'T', 'P'}, 
            k = 2.
Output : 3.

Input : arr[] = {'P', 'T', 'P', 'T', 'T', 'P'},
            k = 3.
Output : 3.
```

一种**蛮力**方法是检查所有可行的警察和小偷组合集，并返回其中的最大大小集。它的时间复杂度是指数的，如果我们观察到一个重要的性质，它可以被优化。
一个**高效的**解决方案是使用贪婪算法。但是使用哪个贪婪属性
可能很棘手。我们可以试着用:“每个警察从左边抓住最近的小偷。”这对于上面给出的示例三有效，但是对于示例二无效，因为它输出 2，这是不正确的。
**我们也可以试试**:“对于每一个从左边抓住最远的小偷的警察”。这对于上面给出的示例 2 有效，但是对于示例 3 无效，因为它输出 2，这是不正确的。可以应用一个对称参数来显示从数组的右侧遍历这些数组也失败了。我们可以观察到，思维不考虑
警察，只关注分配工作:
1。获取警察 p 和小偷 t 的最低指数，如果|p-t| < = k，则进行分配
，并递增到找到的下一个 p 和 t。
2。否则，将最小值(p，t)增加到找到的下一个 p 或 t。
3。重复以上两个步骤，直到找到下一个 p 和 t。
4。返回分配的数量。
下面是上述算法的实现。它使用向量
将警察和小偷的索引存储在数组中并进行处理。

## C++

```
// C++ program to find maximum number of thieves
// caught
#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// Returns maximum number of thieves that can
// be caught.
int policeThief(char arr[], int n, int k)
{
    int res = 0;
    vector<int> thi;
    vector<int> pol;

    // store indices in the vector
    for (int i = 0; i < n; i++) {
        if (arr[i] == 'P')
            pol.push_back(i);
        else if (arr[i] == 'T')
            thi.push_back(i);
    }  

    // track lowest current indices of
    // thief: thi[l], police: pol[r]
    int l = 0, r = 0;
    while (l < thi.size() && r < pol.size()) {

        // can be caught
        if (abs(thi[l] - pol[r]) <= k) {
            res++;
            l++;
            r++;
        }

        // increment the minimum index
        else if (thi[l] < pol[r])
            l++;
        else
            r++;
    }

    return res;
}

// Driver program
int main()
{
    int k, n;

    char arr1[] = { 'P', 'T', 'T', 'P', 'T' };
    k = 2;
    n = sizeof(arr1) / sizeof(arr1[0]);
    cout << "Maximum thieves caught: "
         << policeThief(arr1, n, k) << endl;

    char arr2[] = { 'T', 'T', 'P', 'P', 'T', 'P' };
    k = 2;
    n = sizeof(arr2) / sizeof(arr2[0]);
    cout << "Maximum thieves caught: "
         << policeThief(arr2, n, k) << endl;

    char arr3[] = { 'P', 'T', 'P', 'T', 'T', 'P' };
    k = 3;
    n = sizeof(arr3) / sizeof(arr3[0]);
    cout << "Maximum thieves caught: "
         << policeThief(arr3, n, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of
// thieves caught
import java.util.*;
import java.io.*;

class GFG
{
    // Returns maximum number of thieves
    // that can be caught.
    static int policeThief(char arr[], int n, int k)
    {
        int res = 0;
        ArrayList<Integer> thi = new ArrayList<Integer>();
        ArrayList<Integer> pol = new ArrayList<Integer>();

        // store indices in the ArrayList
        for (int i = 0; i < n; i++) {
            if (arr[i] == 'P')
            pol.add(i);
            else if (arr[i] == 'T')
            thi.add(i);
        }

        // track lowest current indices of
        // thief: thi[l], police: pol[r]
        int l = 0, r = 0;
        while (l < thi.size() && r < pol.size()) {

            // can be caught
            if (Math.abs(thi.get(l) - pol.get(r)) <= k) {
            res++;
            l++;
            r++;
            }

            // increment the minimum index
            else if (thi.get(l) < pol.get(r))
                l++;
            else
                r++;
        }
        return res;
    }

    // Driver program
    public static void main(String args[])
    {
        int k, n;
        char arr1[] =new char[] { 'P', 'T', 'T',
                                  'P', 'T' };
        k = 2;
        n = arr1.length;
        System.out.println("Maximum thieves caught: "
                            +policeThief(arr1, n, k));

        char arr2[] =new char[] { 'T', 'T', 'P', 'P',
                                  'T', 'P' };
        k = 2;
        n = arr2.length;
        System.out.println("Maximum thieves caught: "
                            +policeThief(arr2, n, k));

        char arr3[] = new char[]{ 'P', 'T', 'P', 'T',
                                  'T', 'P' };
        k = 3;
        n = arr3.length;
        System.out.println("Maximum thieves caught: "
                            +policeThief(arr3, n, k));
    }
}

/* This code is contributed by Danish kaleem */
```

## 蟒蛇 3

```
# Python3 program to find maximum
# number of thieves caught

# Returns maximum number of thieves
# that can be caught.
def policeThief(arr, n, k):
    i = 0
    l = 0
    r = 0
    res = 0
    thi = []
    pol = []

    # store indices in list
    while i < n:
        if arr[i] == 'P':
            pol.append(i)
        elif arr[i] == 'T':
            thi.append(i)
        i += 1

    # track lowest current indices of
    # thief: thi[l], police: pol[r]
    while l < len(thi) and r < len(pol):

        # can be caught
        if (abs( thi[l] - pol[r] ) <= k):
            res += 1
            l += 1
            r += 1

        # increment the minimum index
        elif thi[l] < pol[r]:
            l += 1
        else:
            r += 1

    return res

# Driver program
if __name__=='__main__':
    arr1 = ['P', 'T', 'T', 'P', 'T']
    k = 2
    n = len(arr1)
    print(("Maximum thieves caught: {}".
         format(policeThief(arr1, n, k))))

    arr2 = ['T', 'T', 'P', 'P', 'T', 'P']
    k = 2
    n = len(arr2)
    print(("Maximum thieves caught: {}".
          format(policeThief(arr2, n, k))))

    arr3 = ['P', 'T', 'P', 'T', 'T', 'P']
    k = 3
    n = len(arr3)
    print(("Maximum thieves caught: {}".
          format(policeThief(arr3, n, k))))

# This code is contributed by `jahid_nadim`
```

**Output**

```
Maximum thieves caught: 2
Maximum thieves caught: 3
Maximum thieves caught: 3
```