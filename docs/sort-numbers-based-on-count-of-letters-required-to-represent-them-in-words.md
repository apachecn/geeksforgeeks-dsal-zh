# 根据单词中表示数字所需的字母数量对数字进行排序

> 原文:[https://www . geesforgeks . org/sort-numbers-based-on-count-of-letters-required-to-presentation-in-words/](https://www.geeksforgeeks.org/sort-numbers-based-on-count-of-letters-required-to-represent-them-in-words/)

给定一个包含非负整数 **N** 的数组 **arr[]** ，任务是根据表示这些整数所需的字母数量之和对它们进行排序。

**示例:**

> **输入:** arr[] = {12，10，31，18}
> **输出:** 12 31 10 18
> **解释:**
> 12->1+2->3+3 = 6
> 31->3+1->4+3 = 7
> 10->1+0->3+4 = 7【T11
> 
> **输入:** arr[] = {12，10}
> **输出:** 12 10
> **解释:**
> 12->1+2->3+3 = 6
> 10->1+0->3+4 = 7

**进场:**

*   最初，定义了一个大小为十的数组，其中包含表示每个数字所需的字母数量。
*   现在，给定的数组被迭代，对于每个数字，表示它们所需的字母数被找到。
*   现在，这个字符总数和数字被加到一个[向量对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)中。
*   最后，这个向量对按升序排序。

下面是上述方法的实现:

## C++

```
// C++ program to sort the strings
// based on the numbers of letters
// required to represent them

#include <bits/stdc++.h>
using namespace std;

// letters[i] stores the count of letters
// required to represent the digit i
const int letters[] = { 4, 3, 3, 3, 4,
                        4, 3, 5, 5, 4 };

// Function to return the sum of
// letters required to represent N
int sumOfLetters(int n)
{
    int sum = 0;
    while (n > 0) {
        sum += letters[n % 10];
        n = n / 10;
    }
    return sum;
}

// Function to sort the array according to
// the sum of letters to represent n
void sortArr(int arr[], int n)
{
    // Vector to store the digit sum
    // with respective elements
    vector<pair<int, int> > vp;

    // Inserting digit sum with elements
    // in the vector pair
    for (int i = 0; i < n; i++) {

        // Making the vector pair
        vp.push_back(
            make_pair(
                sumOfLetters(
                    arr[i]),
                arr[i]));
    }

    // Sort the vector, this will sort the
    // pair according to the sum of
    // letters to represent n
    sort(vp.begin(), vp.end());

    // Print the sorted vector content
    for (int i = 0; i < vp.size(); i++)
        cout << vp[i].second << " ";
}

// Driver code
int main()
{
    int arr[] = { 12, 10, 31, 18 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort the strings
// based on the numbers of letters
// required to represent them
import java.util.*;
import java.lang.*;

class GFG{

// letters[i] stores the count of letters
// required to represent the digit i
static int letters[] = { 4, 3, 3, 3, 4,
                         4, 3, 5, 5, 4 };

// Function to return the sum of
// letters required to represent N
static int sumOfLetters(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += letters[n % 10];
        n = n / 10;
    }
    return sum;
}

// Function to sort the array according to
// the sum of letters to represent n
static void sortArr(int arr[], int n)
{

    // Vector to store the digit sum
    // with respective elements
    ArrayList<int[]> vp = new ArrayList<>();

    // Inserting digit sum with elements
    // in the vector pair
    for(int i = 0; i < n; i++)
    {

        // Making the vector pair
        vp.add(new int[]{sumOfLetters(arr[i]),
                                      arr[i]});
    }

    // Sort the vector, this will sort the
    // pair according to the sum of
    // letters to represent n
    Collections.sort(vp, (a, b) -> a[0] - b[0]);

    // Print the sorted vector content
    for(int i = 0; i < vp.size(); i++)
        System.out.print(vp.get(i)[1] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 12, 10, 31, 18 };
    int n = arr.length;

    sortArr(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to sort the strings
# based on the numbers of letters
# required to represent them

# letters[i] stores the count of letters
# required to represent the digit i
letters = [4, 3, 3, 3, 4,
           4, 3, 5, 5, 4]

# Function to return the sum of
# letters required to represent N
def sumOfLetters(n):

    sum = 0
    while (n > 0):
        sum += letters[n % 10]
        n = n // 10

    return sum

# Function to sort the array according to
# the sum of letters to represent n
def sortArr(arr, n):

    # List to store the digit sum
    # with respective elements
    vp = []

    # Inserting digit sum with elements
    # in the list pair
    for i in range(n):
        vp.append([sumOfLetters(arr[i]), arr[i]])

    # Sort the list, this will sort the
    # pair according to the sum of
    # letters to represent n
    vp.sort(key = lambda x : x[0])

    # Print the sorted list content
    for i in vp:
        print(i[1], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [ 12, 10, 31, 18 ]
    n = len(arr)

    sortArr(arr, n)

# This code is contributed by Shivam Singh
```

## java 描述语言

```
<script>

// Javascript program to sort the strings
// based on the numbers of letters
// required to represent them

// letters[i] stores the count of letters
// required to represent the digit i
let letters = [ 4, 3, 3, 3, 4,
                         4, 3, 5, 5, 4 ];

// Function to return the sum of
// letters required to represent N
function sumOfLetters( n)
{
    let sum = 0;
    while (n > 0)
    {
        sum += letters[n % 10];
        n = Math.floor(n / 10);
    }
    return sum;
}

// Function to sort the array according to
// the sum of letters to represent n
function sortArr(arr, n)
{

    // Vector to store the digit sum
    // with respective elements
    let vp = [];

    // Inserting digit sum with elements
    // in the vector pair
    for(let i = 0; i < n; i++)
    {

        // Making the vector pair
        vp.push([sumOfLetters(arr[i]),
                                      arr[i]]);
    }

    // Sort the vector, this will sort the
    // pair according to the sum of
    // letters to represent n
    vp.sort((a, b) => a[0] - b[0]);

    // Prlet the sorted vector content
    for(let i = 0; i < vp.length; i++)
        document.write(vp[i][1] + " ");
}

  // Driver Code

    let arr = [ 12, 10, 31, 18 ];
    let n = arr.length;

    sortArr(arr, n);

</script>
```

**Output:** 

```
12 31 10 18
```

**时间复杂度:** *O(N * log(N))* ，其中 N 是数组的大小。