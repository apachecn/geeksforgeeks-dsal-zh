# 按照乘法持久性的递增顺序对数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-a-array-in-递增顺序-它们的乘法-持久性/](https://www.geeksforgeeks.org/sort-an-array-in-increasing-order-of-their-multiplicative-persistence/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是[按照递增顺序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组进行排序，通过对每个数组元素递归地乘以其位数来获得一个一位数所需的步数。如果任意两个数字的步数相同，则先打印较小的数字。

**示例**:

> **输入:** arr[] = {39，999，4，9876}
> **输出:** 4 9876 39 999
> **解释:**
> 以下是将每个数组元素减少到 0 所需的步数:
> 
> *   **对于 arr[0] (= 39):** 元素 39 将减少为 39 → 27 → 14 → 4。因此，所需的步骤数为 3。
> *   **对于 arr[1] (= 999):** 元素 999 将减少为 999 → 729 → 126 → 12 → 2。因此，所需的步骤数为 4。
> *   **对于 arr[2] (= 4):** 元素 4 已经是一个一位数。因此，所需的步骤数为 0。
> *   **对于 arr[3] (= 9876):** 元素 9876 将减少为 9876 → 3024 → 0。因此，所需的步骤数为 2。
> 
> 根据给定的标准，将元素减少到一位数所需的步骤数递增顺序为{4，9876，29，999}
> 
> **输入:** arr[] = {1，27，90}
> **输出:** 1 90 27

**方法:**通过对每个数组元素递归地乘以其位数，然后[使用](https://www.geeksforgeeks.org/sort-first-k-values-in-ascending-order-and-remaining-n-k-values-in-descending-order/)[比较器功能](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)以递增顺序对数组进行排序，找到获得一个一位数所需的步数，就可以解决给定的问题。按照以下步骤解决问题:

*   声明一个比较器函数， **cmp(X，Y)** ，该函数以两个元素作为参数，并执行以下步骤:
    *   重复一个循环，直到 **X** 变成一位数，并将 **X** 的值更新为其位数的乘积。
    *   对数值 **Y** 重复上述步骤。
    *   如果 **X** 的值小于 **Y** ，则返回**真**。否则，返回**假**。
*   [使用上述比较器功能作为**排序(arr，arr + N，cmp)** ，对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 进行排序。
*   完成以上步骤后，[打印数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/) **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// steps required to reduce a given
// number to a single-digit number
int countReduction(int num)
{
    // Stores the required result
    int ans = 0;

    // Iterate until a single digit
    // number is not obtained
    while (num >= 10) {

        // Store the number in a
        // temporary variable
        int temp = num;
        num = 1;

        // Iterate over all digits and
        // store their product in num
        while (temp > 0) {
            int digit = temp % 10;
            temp = temp / 10;
            num *= digit;
        }

        // Increment the answer
        // by 1
        ans++;
    }

    // Return the result
    return ans;
}

// Comparator function to sort the array
bool compare(int x, int y)
{
    // Count number of steps required
    // to reduce X and Y into single
    // digits integer
    int x1 = countReduction(x);
    int y1 = countReduction(y);

    // Return true
    if (x1 < y1)
        return true;

    return false;
}

// Function to sort the array according
// to the number of steps required to
// reduce a given number into a single
// digit number
void sortArray(int a[], int n)
{
    // Sort the array using the
    // comparator function
    sort(a, a + n, compare);

    // Print the array after sorting
    for (int i = 0; i < n; i++) {
        cout << a[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 39, 999, 4, 9876 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
class GFG
{

// Function to find the number of
// steps required to reduce a given
// number to a single-digit number
static int countReduction(int num)
{

    // Stores the required result
    int ans = 0;

    // Iterate until a single digit
    // number is not obtained
    while (num >= 10)
    {

        // Store the number in a
        // temporary variable
        int temp = num;
        num = 1;

        // Iterate over all digits and
        // store their product in num
        while (temp > 0) {
            int digit = temp % 10;
            temp = temp / 10;
            num *= digit;
        }

        // Increment the answer
        // by 1
        ans++;
    }

    // Return the result
    return ans;
}

// Function to sort the array according
// to the number of steps required to
// reduce a given number into a single
// digit number
static void sortArray(Integer a[], int n)
{

    // Sort the array using the
    // comparator function
    Arrays.sort(a,new Comparator<Integer>(){
        public int compare(Integer x, Integer y)
   {

            // Count number of steps required
    // to reduce X and Y into single
    // digits integer
    int x1 = countReduction(x);
    int y1 = countReduction(y);

    // Return true
    if (x1 < y1)
        return -1;

    return 1;
        }
    });

    // Print the array after sorting
    for (int i = 0; i < n; i++)
    {
        System.out.print(a[i] + " ");
    }
}

  // Driver code
public static void main (String[] args)
{
     Integer arr[] = { 39, 999, 4, 9876 };
    int N = arr.length;

    // Function Call
    sortArray(arr, N);
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the number of
// steps required to reduce a given
// number to a single-digit number
function countReduction(num) {
    // Stores the required result
    let ans = 0;

    // Iterate until a single digit
    // number is not obtained
    while (num >= 10) {

        // Store the number in a
        // temporary variable
        let temp = num;
        num = 1;

        // Iterate over all digits and
        // store their product in num
        while (temp > 0) {
            let digit = temp % 10;
            temp = Math.floor(temp / 10);
            num *= digit;
        }

        // Increment the answer
        // by 1
        ans++;
    }

    // Return the result
    return ans;
}

// Comparator function to sort the array
function compare(x, y) {
    // Count number of steps required
    // to reduce X and Y into single
    // digits integer
    let x1 = countReduction(x);
    let y1 = countReduction(y);

    // Return true
    if (x1 < y1)
        return -1;

    return 1;
}

// Function to sort the array according
// to the number of steps required to
// reduce a given number into a single
// digit number
function sortArray(a, n) {
    // Sort the array using the
    // comparator function
    a.sort(compare);

    // Print the array after sorting
    for (let i = 0; i < n; i++) {
        document.write(a[i] + " ");
    }
}

// Driver Code

let arr = [39, 999, 4, 9876];
let N = arr.length;

// Function Call
sortArray(arr, N);

</script>
```

**Output:** 

```
4 9876 39 999
```

***时间复杂度:** O(N * log(N) * log(X))，其中 X 是数组中最大的* [*元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *，arr【】*
***辅助空间:** O(1)*