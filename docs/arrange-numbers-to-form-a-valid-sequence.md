# 排列数字形成有效序列

> 原文:[https://www . geesforgeks . org/array-numbers-to-form-a-valid-sequence/](https://www.geeksforgeeks.org/arrange-numbers-to-form-a-valid-sequence/)

给定一个具有 N 个不同数字的数组 **arr[]** 和另一个具有 N-1 个运算符(或者是<或者是>)的数组 **arr1[]** ，任务是将这些数字组织成一个有效的序列，该序列遵守与所提供的运算符相关的关系运算符规则。

**示例:**

> **输入:** arr[] = {3，12，7，8，5 }；arr 1 = {“<”、“>”、“>”、“<”}
> **输出:** {3、12、8、5、7}
> **说明:**
> 3<12>8>5<7
> 这样的组合还可以有更多。任务是返回其中一个组合。
> 
> **输入:** arr[] = {8，2，7，1，5，9 }；arr 1[]= {“>”、“>”、“<”、“>”、“<”}
> **输出:** {9、8、1、7、2、5}
> **解释:**
> 9>8>1<7>2<5

**天真的方法:**
天真的方法是尝试[所有不同可能的数字排列方式](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)，并检查序列是否有效。
**时间复杂度:** O(2 <sup>N</sup> )。

**高效方法:**其思想是首先按升序对给定的数字数组进行排序。然后用[两指技术](https://www.geeksforgeeks.org/two-pointers-technique/)解决问题:一指前面，一指后面。

1.  取一个与给定数组大小相同的结果数组。
2.  如果当前操作符是'
3.  如果当前操作符是“>”，则在结果数组中包含最后一个指针指向的元素，并将其减 1。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to organize the given numbers
// to form a valid sequence.
vector<int> orgazineInOrder(vector<int> vec,
                            vector<int> op, int n)
{
    vector<int> result(n);
    // Sorting the array
    sort(vec.begin(), vec.end());

    int i = 0, j = n - 1, k = 0;
    while (i <= j && k <= n - 2) {
        // Two pointer technique
        // to organize the numbers
        if (op[k] == '<') {
            result[k] = vec[i++];
        }
        else {
            result[k] = vec[j--];
        }
        k++;
    }
    result[n - 1] = vec[i];

    return result;
}

// Driver code
int main()
{
    vector<int> vec({ 8, 2, 7, 1, 5, 9 });

    vector<int> op({ '>', '>', '<',
                     '>', '<' });

    vector<int> result
        = orgazineInOrder(vec,
                          op, vec.size());

    for (int i = 0; i < result.size(); i++) {
        cout << result[i] << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to organize the given numbers
// to form a valid sequence.
static int[] orgazineInOrder(int []vec,int[] op, int n)
{
    int []result = new int[n];

    // Sorting the array
    Arrays.sort(vec);

    int i = 0, j = n - 1, k = 0;
    while (i <= j && k <= n - 2)
    {
        // Two pointer technique
        // to organize the numbers
        if (op[k] == '<')
        {
            result[k] = vec[i++];
        }
        else
        {
            result[k] = vec[j--];
        }
        k++;
    }
    result[n - 1] = vec[i];

    return result;
}

// Driver code
public static void main(String[] args)
{
    int []vec ={ 8, 2, 7, 1, 5, 9 };

    int[] op ={ '>', '>', '<',
                    '>', '<' };

    int []result = orgazineInOrder(vec,
                        op, vec.length);

    for (int i = 0; i < result.length; i++)
    {
        System.out.print(result[i]+ " ");
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to organize the given numbers
# to form a valid sequence.
def orgazineInOrder(vec, op, n) :

    result = [0] * n;

    # Sorting the array
    vec.sort();
    i = 0;
    j = n - 1;
    k = 0;

    while (i <= j and k <= n - 2) :

        # Two pointer technique
        # to organize the numbers
        if (op[k] == '<') :
            result[k] = vec[i];
            i += 1;

        else :
            result[k] = vec[j];
            j -= 1;

        k += 1;

    result[n - 1] = vec[i];

    return result;

# Driver code
if __name__ == "__main__" :

    vec = [ 8, 2, 7, 1, 5, 9 ];
    op = [ '>', '>', '<', '>', '<' ];

    result = orgazineInOrder(vec, op, len(vec));

    for i in range(len(result)) :
        print(result[i], end = " ");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to organize the given numbers
    // to form a valid sequence.
    static int[] orgazineInOrder(int []vec,int[] op, int n)
    {
        int []result = new int[n];

        // Sorting the array
        Array.Sort(vec);

        int i = 0, j = n - 1, k = 0;
        while (i <= j && k <= n - 2)
        {
            // Two pointer technique
            // to organize the numbers
            if (op[k] == '<')
            {
                result[k] = vec[i++];
            }
            else
            {
                result[k] = vec[j--];
            }
            k++;
        }
        result[n - 1] = vec[i];

        return result;
    }

    // Driver code
    public static void Main()
    {
        int []vec ={ 8, 2, 7, 1, 5, 9 };

        int[] op ={ '>', '>', '<',
                        '>', '<' };

        int []result = orgazineInOrder(vec,
                            op, vec.Length);

        for (int i = 0; i < result.Length; i++)
        {
            Console.Write(result[i] + " ");
        }
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to organize the given numbers
// to form a valid sequence.
function orgazineInOrder(vec, op, n)
{
    let result = [n];

    // Sorting the array
    vec.sort();

    let i = 0, j = n - 1, k = 0;

    while (i <= j && k <= n - 2)
    {

        // Two pointer technique
        // to organize the numbers
        if (op[k] == '<')
        {
            result[k] = vec[i++];
        }
        else
        {
            result[k] = vec[j--];
        }
        k++;
    }
    result[n - 1] = vec[i];

    return result;
}

// Driver code
let vec = [ 8, 2, 7, 1, 5, 9 ];
let op = [ '>', '>', '<', '>', '<' ];

let result = orgazineInOrder(vec,
                             op, vec.length);

for(let i = 0; i < result.length; i++)
{
   document.write(result[i] + " ");
}

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
9 8 1 7 2 5
```

**时间复杂度:** O(NlogN)