# 给定数组奇数索引的所有合成数之和

> 原文:[https://www . geeksforgeeks . org/给定数组奇数索引的所有组合数之和/](https://www.geeksforgeeks.org/sum-of-all-the-composite-numbers-from-odd-indices-of-the-given-array/)

给定一个大小为 N 的**数组 arr[]** ，该数组包含至少一个复合数。任务是找出数组中奇数索引处的所有复合数的和(其中索引基于 1)。
**例:**

> **输入:** arr = [13，5，8，16，25]
> **输出:** 33
> **解释:**
> 奇数索引中的数字是 13，8，25，因为我们遵循基于 1 的索引。
> 这 3 个数中，组合数是 8 和 25，加起来是 33。
> **输入:** arr = [9，7，14，10，34]
> **输出:** 57
> **解释:**
> 奇数索引中的数字是 9，14，34，因为我们遵循基于 1 的索引。
> 三个数都是复合数，加起来是 57。

**方法:**
解决上述问题的主要思路是**检查复合数**也就是说，如果一个整数有 2 个以上的因子，那么它就是一个复合数，否则就不是。然后我们将迭代并检查数组奇数索引中的复合数。如果它是一个复合数，那么我们将把它加到**和**变量中，否则跳过它，直到数组的末尾。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the sum of all the
// composite numbers from odd indices of the given array
#include<bits/stdc++.h>
using namespace std;

// Function to check for composite numbers
int composite(int n){
    int flag = 0;

    int c = 0;

    // Check if the factors are greater than 2
    for (int j = 1; j <= n; j++){
      if (n % j == 0){
            c += 1; 
      }   
    }        

    // Check if the number is composite or not
    if (c >= 3)
      flag = 1;

    return flag;
}

// Function to print the sum of all
// composite numbers in the array
void odd_indices(int arr[],int n){

int sum = 0;

// Iterate for odd indices in the array
for (int k = 0; k < n; k += 2){
    int check = composite(arr[k]);

    // Check if the number is composite
    // then add it to sum
    if (check == 1)
        sum += arr[k];
}

    // return the sum
    cout << sum << endl;
}

// Driver code
int main(){
    int arr[] = {13, 5, 8, 16, 25};
    int n = sizeof(arr)/sizeof(arr[0]);
    odd_indices(arr,n);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the sum of all the
// composite numbers from odd indices of the given array

class GFG{

// Function to check for composite numbers
static int composite(int n){
    int flag = 0;

    int c = 0;

    // Check if the factors are greater than 2
    for (int j = 1; j <= n; j++){
    if (n % j == 0){
            c += 1;
    }
    }        

    // Check if the number is composite or not
    if (c >= 3)
    flag = 1;

    return flag;
}

// Function to print the sum of all
// composite numbers in the array
static void odd_indices(int arr[],int n){

int sum = 0;

// Iterate for odd indices in the array
for (int k = 0; k < n; k += 2){
    int check = composite(arr[k]);

    // Check if the number is composite
    // then add it to sum
    if (check == 1)
        sum += arr[k];
}

    // return the sum
    System.out.print(sum +"\n");
}

// Driver code
public static void main(String[] args){

    int arr[] = {13, 5, 8, 16, 25};
    int n = arr.length;
    odd_indices(arr,n);
}
}
// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to find the sum of all the
# composite numbers from odd indices of the given array

# Function to print the sum of all
# composite numbers in the array
def odd_indices(arr):

    sum = 0

    # Iterate for odd indices in the array
    for k in range (0, len(arr), 2):

        check = composite (arr[k])

        # Check if the number is composite
        # then add it to sum
        sum += arr[k] if check == 1 else 0

    # return the sum
    print (sum)

# Function to check for composite numbers
def composite(n):

    flag = 0

    c = 0

    # Check if the factors are greater than 2
    for j in range (1, n + 1):

        if (n % j == 0):

            c += 1

    # Check if the number is composite or not
    if (c >= 3):
        flag = 1

    return flag

# Driver code
if __name__ == "__main__":

    arr = [13, 5, 8, 16, 25]

    odd_indices(arr)
```

## C#

```
// C# implementation to find the sum
// of all the composite numbers from
// odd indices of the given array
using System;

class GFG{

// Function to check for composite numbers
static int composite(int n)
{
    int flag = 0;
    int c = 0;

    // Check if the factors are greater than 2
    for(int j = 1; j <= n; j++)
    {
       if (n % j == 0)
       {
           c += 1;
       }
    }        

    // Check if the number is composite or not
    if (c >= 3)
        flag = 1;
    return flag;
}

// Function to print the sum of all
// composite numbers in the array
static void odd_indices(int []arr,int n)
{
    int sum = 0;

    // Iterate for odd indices in the array
    for(int k = 0; k < n; k += 2)
    {
       int check = composite(arr[k]);

       // Check if the number is composite
       // then add it to sum
       if (check == 1)
           sum += arr[k];
    }

    // return the sum
    Console.Write(sum + "\n");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 13, 5, 8, 16, 25 };
    int n = arr.Length;

    odd_indices(arr, n);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript implementation to find the sum of all the
// composite numbers from odd indices of the given array

// Function to check for composite numbers
function composite(n){
    let flag = 0;

    let c = 0;

    // Check if the factors are greater than 2
    for (let j = 1; j <= n; j++){
      if (n % j == 0){
            c += 1; 
      }   
    }        

    // Check if the number is composite or not
    if (c >= 3)
      flag = 1;

    return flag;
}

// Function to print the sum of all
// composite numbers in the array
function odd_indices(arr, n){

let sum = 0;

// Iterate for odd indices in the array
for (let k = 0; k < n; k += 2){
    let check = composite(arr[k]);

    // Check if the number is composite
    // then add it to sum
    if (check == 1)
        sum += arr[k];
}

    // return the sum
    document.write(sum + "<br>");
}

// Driver code
    let arr = [13, 5, 8, 16, 25];
    let n = arr.length
    odd_indices(arr,n);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
33
```