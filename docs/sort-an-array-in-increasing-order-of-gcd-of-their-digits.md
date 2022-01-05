# 按照数字的 GCD 递增顺序对数组进行排序

> 原文:[https://www . geeksforgeeks . org/按数字的 gcd 递增顺序对数组进行排序/](https://www.geeksforgeeks.org/sort-an-array-in-increasing-order-of-gcd-of-their-digits/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是[按照每个元素](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)位数的 [GCD 递增顺序对数组 **arr[]**](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 进行排序。如果两个或多个元素的 **GCD** 相同，则根据它们的值进行排序。

**示例:**

> **输入:** arr[] = {555，363，488，244}
> **输出:** 244 363 488 555
> **解释:**
> 跟随每个数字的数字的 GCD:
> 
> 1.  555: GCD(5，5，5) = 5。
> 2.  363: GCD(3，6，3) = 3。
> 3.  488: GCD(4，8，8) = 4。
> 4.  244: GCD(2，4，4) = 2。
> 
> 根据给定标准排序后，元素的顺序为{244，363，488，555}。
> 
> **输入:** arr[] = {555，363，488，244，444，5 }
> T3】输出: 244 363 444 488 5 555

**方法:**使用[比较器功能](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)和[排序()功能](https://www.geeksforgeeks.org/sort-c-stl/)可以解决给定的问题。比较器功能定义为:

*   它一次接受两个参数，如果第一个参数的 GCD 小于第二个参数，则返回 **true** 。
*   如果 **GCD** 值相同，那么如果第一个参数小于第二个参数，则返回**真**。否则，退回**假**。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate GCD of two integers
int gcd(int a, int b)
{

    // Base case
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to calculate GCD of
// digits of array elements
int keyFunc(int n)
{
    int getGCD = 0;

    while (n > 0)
    {
        getGCD = gcd(n % 10, getGCD);

        // If at point GCD becomes 1,
        // return it
        if (getGCD == 1)
            return 1;

        n = n / 10;
    }
    return getGCD;
}

// Comparator function that compares 
// elements according to their gcd value.
bool compare(int o1, int o2)
{
    int x = keyFunc(o1);
    int y = keyFunc(o2);

    if(x == y)
    {
        return o1 < o2;
    }
    return x < y;
}

// Function to sort an array in according
// to GCD of digits of array elements
void sortArrayByGCD(vector<int>arr)
{
    vector<int>list;
    for(int i : arr)
    {
        list.push_back(i);
    }

    // Sort the array according to gcd of
    // digits using comparator function
    sort(list.begin(), list.end(), compare);

    // Print the resultant array
    for(int i : list)
    {
        cout << i << " ";
    }
}

// Driver code
int main()
{
    vector<int>arr = { 555, 363, 488, 244 };;
    sortArrayByGCD(arr);
}

// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG{

// Function to calculate GCD of two integers
static int gcd(int a, int b)
{

    // Base case
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to calculate GCD of
// digits of array elements
static int keyFunc(int n)
{
    int getGCD = 0;

    while (n > 0)
    {
        getGCD = gcd(n % 10, getGCD);

        // If at point GCD becomes 1,
        // return it
        if (getGCD == 1)
            return 1;

        n = n / 10;
    }
    return getGCD;
}

// Function to sort an array in according
// to GCD of digits of array elements
public static void sortArrayByGCD(int[] arr)
{
    ArrayList<Integer> list = new ArrayList<Integer>();
    for(int i : arr)
    {
        list.add(i);
    }

    // Sort the array according to gcd of
    // digits using comparator function
    Collections.sort(list, new Comparator<Integer>()
    {
        @Override
        public int compare(Integer o1, Integer o2)
        {
            int x = keyFunc(o1) - keyFunc(o2);
            if (x == 0)
            {
                if (o1 > o2)
                    x = 1;
                else
                    x = -1;
            }
            return x;
        }
    });

    // Print the resultant array
    for(int i : list)
    {
        System.out.print(i + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 555, 363, 488, 244 };
    sortArrayByGCD(arr);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate
# GCD of two integers
def gcd(a, b):

    # Base Case
    if not b:
        return a

    # Recursively calculate GCD
    return gcd(b, a % b)

# Function to calculate GCD
# of two array elements
def keyFunc(n):
    getGCD = int(str(n)[0])

    # Update the getGCD
    for i in str(n):
        getGCD = gcd(getGCD, int(i))

    # Return the resultant GCD
    return getGCD

# Function to sort an array by
# increasing order of GCD of
# digits of array elements
def sortArrayByGCD(arr):

    # Sort the array
    arr.sort()

    # Sort the array according to gcd of
    # digits using comparator function
    arr = sorted(arr, key = keyFunc)

    # Print the resultant array
    print(*arr)

# Driver Code

# Given array
arr = [555, 363, 488, 244]
sortArrayByGCD(arr)
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to calculate GCD of two integers
function gcd(a, b) {

    // Base case
    if (b == 0)
        return a;

    // Recursively calculate GCD
    return gcd(b, a % b);
}

// Function to calculate GCD of
// digits of array elements
function keyFunc(n) {
    let getGCD = String(n)[0]

    // Update the getGCD
    for (let i = 0; i < n; i++)
        getGCD = gcd(getGCD, i)

    // Return the resultant GCD
    return getGCD
}

// Function to sort an array in according
// to GCD of digits of array elements
function sortArrayByGCD(arr) {
    // Sort the array
    arr.sort()

    // Sort the array according to gcd of
    // digits using comparator function
    arr = arr.sort(keyFunc)

    // Print the resultant array
    for (let i of arr) {
        document.write(i + " ")
    }
}

// Driver code
let arr = [555, 363, 488, 244];
sortArrayByGCD(arr);

</script>
```

**Output:** 

```
244 363 488 555
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(1)