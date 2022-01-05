# 根据给定条件对给定数组进行排序

> 原文:[https://www . geesforgeks . org/按给定条件对给定数组进行排序/](https://www.geeksforgeeks.org/sort-the-given-array-as-per-given-conditions/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，使得–

*   所有偶数必须在所有奇数之前。
*   所有能被 5 整除的偶数必须排在不能被 5 整除的偶数之前。
*   如果两个偶数能被 5 整除，那么具有较大值的数字将排在第一位
*   如果两个偶数不能被 5 整除，那么数组中索引较大的数字将排在第一位。
*   所有奇数必须以相对顺序出现，因为它们存在于数组中。

**示例:**

> **输入:** arr[] = {5，10，30，7}
> **输出:** 30 10 5 7
> **解释:**偶数=【10，30】。奇数= [5，7]。偶数排序后，偶数= [30，10]，因为 10 和 30 都可以被 5 整除，但 30 的值更大，所以它会在 10 之前。
> 排序后 A = [30，10，5，7]因为所有偶数必须排在所有奇数之前。

**方法:**这个问题可以通过使用排序来解决。按照以下步骤解决问题:

*   创建三个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)表示 **v1** 、 **v2** 、 **v3** ，其中 **v1** 存储偶数且可被 **5** 、 **v2** 存储偶数但不可被 **5** 整除的数字， **v3** 存储奇数。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤-
    *   如果 **arr[i]%2 = 0** 和 **arr[i]%5=0** ，则在 **v1** 中插入 **arr[i]** 。
    *   如果 **arr[i]%2 = 0** 和 **arr[i]%5！= 0，**然后在 **v2** 中插入**arr【I】**。
    *   如果 **arr[i]%2** ，则在 **v3** 中插入 **arr[i]** 。
*   [按降序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **v1** 。
*   执行上述步骤后，打印[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **v1** 然后打印向量 **v2** 然后 **v3** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to sort array in the way
// mentioned above
void AwesomeSort(vector<int> m, int n)
{
    // Create three vectors
    vector<int> v1, v2, v3;

    int i;

    // Traverse through the elements
    // of the array
    for (i = 0; i < n; i++) {

        // If elements are even and
        // divisible by 10
        if (m[i] % 10 == 0)
            v1.push_back(m[i]);

        // If number is even but not divisible
        // by 5
        else if (m[i] % 2 == 0)
            v2.push_back(m[i]);
        else
            // If number is odd
            v3.push_back(m[i]);
    }

    // Sort  v1 in descending orde
    sort(v1.begin(), v1.end(), greater<int>());

    for (int i = 0; i < v1.size(); i++) {
        cout << v1[i] << " ";
    }
    for (int i = 0; i < v2.size(); i++) {
        cout << v2[i] << " ";
    }
    for (int i = 0; i < v3.size(); i++) {
        cout << v3[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    vector<int> arr{ 5, 10, 30, 7 };
    int N = arr.size();

    // FunctionCall
    AwesomeSort(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Collections;
import java.util.Vector;

public class GFG_JAVA {

    // Function to sort array in the way
    // mentioned above
    static void AwesomeSort(Vector<Integer> m, int n)
    {
        // Create three vectors
        Vector<Integer> v1 = new Vector<>();
        Vector<Integer> v2 = new Vector<>();
        Vector<Integer> v3 = new Vector<>();

        int i;

        // Traverse through the elements
        // of the array
        for (i = 0; i < n; i++) {

            // If elements are even and
            // divisible by 10
            if (m.get(i) % 10 == 0)
                v1.add(m.get(i));

            // If number is even but not divisible
            // by 5
            else if (m.get(i) % 2 == 0)
                v2.add(m.get(i));
            else
                // If number is odd
                v3.add(m.get(i));
        }

        // Sort  v1 in descending orde
        Collections.sort(v1, Collections.reverseOrder());

        for (int ii = 0; ii < v1.size(); ii++) {
            System.out.print(v1.get(ii) + " ");
        }
        for (int ii = 0; ii < v2.size(); ii++) {
            System.out.print(v2.get(ii) + " ");
        }
        for (int ii = 0; ii < v3.size(); ii++) {
            System.out.print(v3.get(ii) + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        Vector<Integer> arr = new Vector<>();
        arr.add(5);
        arr.add(10);
        arr.add(30);
        arr.add(7);

        int N = arr.size();

        // FunctionCall
        AwesomeSort(arr, N);
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to sort array in the way
# mentioned above
def AwesomeSort(m, n):

    # Create three vectors
    v1, v2, v3 = [],[],[]

    # Traverse through the elements
    # of the array
    for i in range(n):

        # If elements are even and
        # divisible by 10
        if (m[i] % 10 == 0):
            v1.append(m[i])

        # If number is even but not divisible
        # by 5
        elif (m[i] % 2 == 0):
            v2.append(m[i])
        else:
            # If number is odd
            v3.append(m[i])

    # Sort  v1 in descending orde
    v1 = sorted(v1)[::-1]

    for i in range(len(v1)):
        print(v1[i], end = " ")

    for i in range(len(v2)):
        print(v2[i], end = " ")

    for i in range(len(v3)):
        print (v3[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [5, 10, 30, 7]
    N = len(arr)

    # FunctionCall
    AwesomeSort(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to sort array in the way
    // mentioned above
    static void AwesomeSort(List<int> m, int n)
    {

        // Create three vectors
        List<int> v1 = new List<int>();
        List<int> v2 = new List<int>();
        List<int> v3 = new List<int>();

        int i;

        // Traverse through the elements
        // of the array
        for (i = 0; i < n; i++) {

            // If elements are even and
            // divisible by 10
            if (m[i] % 10 == 0)
                v1.Add(m[i]);

            // If number is even but not divisible
            // by 5
            else if (m[i] % 2 == 0)
                v2.Add(m[i]);
            else
                // If number is odd
                v3.Add(m[i]);
        }

        // Sort  v1 in descending orde
        v1.Sort();
        v1.Reverse();

        for (int ii = 0; ii < v1.Count; ii++) {
            Console.Write(v1[ii] + " ");
        }
        for (int ii = 0; ii < v2.Count; ii++) {
            Console.Write(v2[ii] + " ");
        }
        for (int ii = 0; ii < v3.Count; ii++) {
            Console.Write(v3[ii] + " ");
        }
    }

  static void Main()
  {

    // Given Input
    List<int> arr = new List<int>();
    arr.Add(5);
    arr.Add(10);
    arr.Add(30);
    arr.Add(7);

    int N = arr.Count;

    // FunctionCall
    AwesomeSort(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to sort array in the way
// mentioned above
function AwesomeSort(m, n)
{
    // Create three vectors
    let v1 = [];
    let v2 = [];
    let v3 = [];

    let i;

    // Traverse through the elements
    // of the array
    for (i = 0; i < n; i++) {

        // If elements are even and
        // divisible by 10
        if (m[i] % 10 == 0)
            v1.push(m[i]);

        // If number is even but not divisible
        // by 5
        else if (m[i] % 2 == 0)
            v2.push(m[i]);
        else
            // If number is odd
            v3.push(m[i]);
    }

    // Sort  v1 in descending orde
    v1.sort((a, b) => b - a);

    for (let i = 0; i < v1.length; i++) {
        document.write(v1[i] + " ");
    }
    for (let i = 0; i < v2.length; i++) {
        document.write(v2[i] + " ");
    }
    for (let i = 0; i < v3.length; i++) {
        document.write(v3[i] + " ");
    }
}

// Driver Code

// Given Input
let arr = [5, 10, 30, 7];
let N = arr.length;

// FunctionCall
AwesomeSort(arr, N);

</script>
```

**Output**

```
30 10 5 7 
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*