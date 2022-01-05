# 制服二分搜索法

> 原文:[https://www.geeksforgeeks.org/uniform-binary-search/](https://www.geeksforgeeks.org/uniform-binary-search/)

**均匀二分搜索法**是对[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法的优化，在同一个数组或多个大小相同的数组上进行多次搜索。在正常的二分搜索法，我们做算术运算来寻找中点。这里，我们预计算中点，并将其填入查找表。数组查找通常比算术运算(加法和移位)更快找到中点。

**示例:**

```
Input : array={1, 3, 5, 6, 7, 8, 9}, v=3
Output : Position of 3 in array = 2

Input :array={1, 3, 5, 6, 7, 8, 9}, v=7
Output :Position of 7 in array = 5
```

该算法与[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法非常相似，唯一的区别是为一个数组创建了一个查找表，该查找表用于修改数组中指针的索引，从而加快搜索速度。该算法不维护下限和上限，而是维护一个索引，并使用查找表修改该索引。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

const int MAX_SIZE = 1000;

// lookup table
int lookup_table[MAX_SIZE];

// create the lookup table
// for an array of length n
void create_table(int n)
{
    // power and count variable
    int pow = 1;
    int co = 0;
    do {
        // multiply by 2
        pow <<= 1;

        // initialize the lookup table
        lookup_table[co] = (n + (pow >> 1)) / pow;
    } while (lookup_table[co++] != 0);
}

// binary search
int binary(int arr[], int v)
{
    // mid point of the array
    int index = lookup_table[0] - 1;

    // count
    int co = 0;

    while (lookup_table[co] != 0) {

        // if the value is found
        if (v == arr[index])
            return index;

        // if value is less than the mid value
        else if (v < arr[index])
            index -= lookup_table[++co];

        // if value is greater than the mid value
        else
            index += lookup_table[++co];
    }
}

// main function
int main()
{

    int arr[] = { 1, 3, 5, 6, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(int);

    // create the lookup table
    create_table(n);

    // print the position of the array
    cout << "Position of 3 in array = "
         << binary(arr, 3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

    static int MAX_SIZE = 1000;

    // lookup table
    static int lookup_table[] = new int[MAX_SIZE];

    // create the lookup table
    // for an array of length n
    static void create_table(int n)
    {
        // power and count variable
        int pow = 1;
        int co = 0;
        do
        {
            // multiply by 2
            pow <<= 1;

            // initialize the lookup table
            lookup_table[co] = (n + (pow >> 1)) / pow;
        } while (lookup_table[co++] != 0);
    }

    // binary search
    static int binary(int arr[], int v)
    {
        // mid point of the array
        int index = lookup_table[0] - 1;

        // count
        int co = 0;

        while (lookup_table[co] != 0)
        {

            // if the value is found
            if (v == arr[index])
                return index;

            // if value is less than the mid value
            else if (v < arr[index])
            {
                index -= lookup_table[++co];
                return index;
            }

            // if value is greater than the mid value
            else
            {
                index += lookup_table[++co];
                return index;
            }
        }
        return index ;
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr[] = { 1, 3, 5, 6, 7, 8, 9 };
        int n = arr.length;

        // create the lookup table
        create_table(n);

        // print the position of the array
        System.out.println( "Position of 3 in array = " +
                                    binary(arr, 3)) ;

    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of above approach

MAX_SIZE = 1000

# lookup table
lookup_table = [0] * MAX_SIZE

# create the lookup table
# for an array of length n
def create_table(n):

    # power and count variable
    pow = 1
    co = 0
    while True:

        # multiply by 2
        pow <<= 1

        # initialize the lookup table
        lookup_table[co] = (n + (pow >> 1)) // pow
        if lookup_table[co] == 0:
            break
        co += 1

# binary search
def binary(arr, v):

    # mid point of the array
    index = lookup_table[0] - 1

    # count
    co = 0

    while lookup_table[co] != 0:

        # if the value is found
        if v == arr[index]:
            return index

        # if value is less than the mid value
        elif v < arr[index]:
            co += 1
            index -= lookup_table[co]

        # if value is greater than the mid value
        else:
            co += 1
            index += lookup_table[co]

# main function
arr = [1, 3, 5, 6, 7, 8, 9]
n = len(arr)

# create the lookup table
create_table(n)

# print the position of the array
print("Position of 3 in array = ", binary(arr, 3))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    static int MAX_SIZE = 1000;

    // lookup table
    static int []lookup_table = new int[MAX_SIZE];

    // create the lookup table
    // for an array of length n
    static void create_table(int n)
    {
        // power and count variable
        int pow = 1;
        int co = 0;
        do
        {
            // multiply by 2
            pow <<= 1;

            // initialize the lookup table
            lookup_table[co] = (n + (pow >> 1)) / pow;
        } while (lookup_table[co++] != 0);
    }

    // binary search
    static int binary(int []arr, int v)
    {
        // mid point of the array
        int index = lookup_table[0] - 1;

        // count
        int co = 0;

        while (lookup_table[co] != 0)
        {

            // if the value is found
            if (v == arr[index])
                return index;

            // if value is less than the mid value
            else if (v < arr[index])
            {
                index -= lookup_table[++co];
                return index;
            }

            // if value is greater than the mid value
            else
            {
                index += lookup_table[++co];
                return index;
            }
        }
        return index ;
    }

    // Driver code
    public static void Main ()
    {

        int []arr = { 1, 3, 5, 6, 7, 8, 9 };
        int n = arr.GetLength(0);

        // create the lookup table
        create_table(n);

        // print the position of the array
    Console.WriteLine( "Position of 3 in array = " +
                                    binary(arr, 3)) ;

    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
let MAX_SIZE = 1000;

// lookup table
let lookup_table = new Array(MAX_SIZE);
lookup_table.fill(0);

// Create the lookup table
// for an array of length n
function create_table(n)
{

    // Power and count variable
    let pow = 1;
    let co = 0;

    while(true)
    {

        // Multiply by 2
        pow <<= 1;

        // Initialize the lookup table
        lookup_table[co] = parseInt((n + (pow >> 1)) /
                                          pow, 10);

        if (lookup_table[co++] == 0)
        {
            break;
        }
    }
}

// Binary search
function binary(arr, v)
{

    // mid point of the array
    let index = lookup_table[0] - 1;

    // count
    let co = 0;

    while (lookup_table[co] != 0)
    {

        // If the value is found
        if (v == arr[index])
            return index;

        // If value is less than the mid value
        else if (v < arr[index])
        {
            index -= lookup_table[++co];
            return index;
        }

        // If value is greater than the mid value
        else
        {
            index += lookup_table[++co];
            return index;
        }
    }
    return index ;
}

// Driver code
let arr = [ 1, 3, 5, 6, 7, 8, 9 ];
let n = arr.length;

// Create the lookup table
create_table(n);

// Print the position of the array
document.write("Position of 3 in array = " +
               binary(arr, 3));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
Position of 3 in array = 1
```

**参考文献:**T2https://en.wikipedia.org/wiki/Uniform_binary_search