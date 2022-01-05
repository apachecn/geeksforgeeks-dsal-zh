# 排列产品查询范围

> 原文:[https://www . geesforgeks . org/range-product-query-in-a-array/](https://www.geeksforgeeks.org/range-product-queries-in-an-array/)

我们有一个整数数组和一组范围查询。对于每个查询，我们需要找到给定范围内元素的乘积。
**例:**

```
Input : arr[] = {5, 10, 15, 20, 25}   
        queries[] = {(3, 5), (2, 2), (2, 3)}
Output : 7500, 10, 150
7500 = 15 x 20 x 25
10 = 10
150 = 10 x 15
```

一种简单的方法是从下到上遍历数组中的每个元素，并将所有元素相乘以找到乘积。每个查询的时间复杂度为 0(n)。
一种有效的**方法是获取另一个数组，并将所有元素的乘积存储到数组第 I 个索引中索引为 I 的元素。但是这里有个问题。如果数组中的任何元素为 0，则 dp 数组从那时起将包含 0。因此，我们应该得到 0 作为我们的答案，即使 0 不在下限和上限之间。
为了解决这种情况，我们使用了另一个名为 countZeros 的数组，该数组将包含“0”的数字，该数组包含直到索引 i.
现在，如果**count zeros[upper]-count zeros[lower]>0**，则表示该范围内有 0，因此答案将是 0。否则我们将照此进行。** 

## **C++**

```
// C++ program for array
// range product queries
#include<bits/stdc++.h>
using namespace std;

// Answers product queries
// given as two arrays
// lower[] and upper[].
void findProduct(long arr[], int lower[],
                 int upper[], int n, int n1)
{
    long preProd[n];
    int countZeros[n];

    long prod = 1; // stores the product

    // keeps count of zeros
    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // if arr[i] is 0, we increment
        // count and do not multiply
        // it with the product
        if (arr[i] == 0)
            count++;
        else
            prod *= arr[i];

        // store the value of prod in dp
        preProd[i] = prod;

        // store the value of
        // count in countZeros
        countZeros[i] = count;
    }

    // We have preprocessed
    // the array, let us
    // answer queries now.
    for (int i = 0; i < n1; i++)
    {
        int l = lower[i];
        int u = upper[i];

        // range starts from
        // first element
        if (l == 1)
        {
            // range does not
            // contain any zero
            if (countZeros[u - 1] == 0)
                cout << (preProd[u - 1]) << endl;
            else
                cout<<0<<endl;
        }

        else // range starts from
             // any other index
        {
            // no difference in countZeros
            // indicates that there are no
            // zeros in the range
            if (countZeros[u - 1] -
                countZeros[l - 2] == 0)
                cout << (preProd[u - 1] /
                         preProd[l - 2]) << endl;

            else // zeros are present in the range
                cout << 0 << endl;
        }
    }
}

// Driver code
int main()
{
    long arr[] ={ 0, 2, 3, 4, 5 };
    int lower[] = {1, 2};
    int upper[] = {3, 2};    
    findProduct(arr, lower, upper,5,2);
    return 0;
}

// This code is contributed
// by Arnab Kundu
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for array range product queries
class Product {

    // Answers product queries given as two arrays
    // lower[] and upper[].   
    static void findProduct(long[] arr, int[] lower,
                                        int[] upper)
    {
        int n = arr.length;
        long[] preProd = new long[n];
        int[] countZeros = new int[n];

        long prod = 1; // stores the product

        // keeps count of zeros
        int count = 0;
        for (int i = 0; i < n; i++) {

            // if arr[i] is 0, we increment count and
            // do not multiply it with the product
            if (arr[i] == 0)
                count++;
            else
                prod *= arr[i];

            // store the value of prod in dp
            preProd[i] = prod;

            // store the value of count in countZeros
            countZeros[i] = count;
        }

        // We have preprocessed the array, let us
        // answer queries now.
        for (int i = 0; i < lower.length; i++) {
            int l = lower[i];
            int u = upper[i];

            // range starts from first element
            if (l == 1)
            {
                // range does not contain any zero
                if (countZeros[u - 1] == 0)
                    System.out.println(preProd[u - 1]);
                else
                    System.out.println(0);
            }

            else // range starts from any other index
            {
                // no difference in countZeros indicates that
                // there are no zeros in the range
                if (countZeros[u - 1] - countZeros[l - 2] == 0)
                    System.out.println(preProd[u - 1] / preProd[l - 2]);

                else // zeros are present in the range
                    System.out.println(0);
            }
        }
    }

    public static void main(String[] args)
    {
        long[] arr = new long[] { 0, 2, 3, 4, 5 };
        int[] lower = {1, 2};
        int[] upper = {3, 2};    
        findProduct(arr, lower, upper);
    }
}
```

## **蟒蛇 3**

```
# Python 3 program for array range
# product queries

# Answers product queries given as
# lower[] and upper[].
def findProduct(arr,lower, upper, n, n1):
    preProd = [0 for i in range(n)]
    countZeros = [0 for i in range(n)]

    prod = 1

    # stores the product

    # keeps count of zeros
    count = 0
    for i in range(0, n, 1):

        # if arr[i] is 0, we increment
        # count and do not multiply
        # it with the product
        if (arr[i] == 0):
            count += 1
        else:
            prod *= arr[i]

        # store the value of prod in dp
        preProd[i] = prod

        # store the value of count
        # in countZeros
        countZeros[i] = count

    # We have preprocessed the array,
    # let us answer queries now.
    for i in range(0, n1, 1):
        l = lower[i]
        u = upper[i]

        # range starts from first element
        if (l == 1):

            # range does not contain any zero
            if (countZeros[u - 1] == 0):
                print(int(preProd[u - 1]))
            else:
                print(0)

        else:

            # range starts from any other index
            # no difference in countZeros indicates
            # that there are no zeros in the range
            if (countZeros[u - 1] -
                countZeros[l - 2] == 0):
                print(int(preProd[u - 1] /
                          preProd[l - 2]))

            else:

                # zeros are present in the range
                print(0)

# Driver code
if __name__ == '__main__':
    arr = [0, 2, 3, 4, 5]
    lower = [1, 2]
    upper = [3, 2]
    findProduct(arr, lower, upper,5, 2)

# This code is contributed by
# Sahil_Shelangia
```

## **C#**

```
// C# program for array
// range product queries
using System;

class GFG
{

// Answers product queries
// given as two arrays
// lower[] and upper[].
static void findProduct(long[] arr,
                        int[] lower,
                        int[] upper)
{
    int n = arr.Length;
    long[] preProd = new long[n];
    int[] countZeros = new int[n];

    long prod = 1; // stores the product

    // keeps count of zeros
    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // if arr[i] is 0, we increment
        // count and do not multiply it
        // with the product
        if (arr[i] == 0)
            count++;
        else
            prod *= arr[i];

        // store the value
        // of prod in dp
        preProd[i] = prod;

        // store the value of
        // count in countZeros
        countZeros[i] = count;
    }

    // We have preprocessed
    // the array, let us
    // answer queries now.
    for (int i = 0;
             i < lower.Length; i++)
    {
        int l = lower[i];
        int u = upper[i];

        // range starts from
        // first element
        if (l == 1)
        {
            // range does not
            // contain any zero
            if (countZeros[u - 1] == 0)
                Console.WriteLine(preProd[u - 1]);
            else
                Console.WriteLine(0);
        }

        // range starts from
        // any other index
        else
        {
            // no difference in countZeros
            // indicates that there are no
            // zeros in the range
            if (countZeros[u - 1] -
                countZeros[l - 2] == 0)
                Console.WriteLine(preProd[u - 1] /
                                  preProd[l - 2]);

            // zeros are present
            // in the range
            else
                Console.WriteLine(0);
        }
    }
}

// Driver Code
public static void Main()
{
    long[] arr = {0, 2, 3, 4, 5};
    int[] lower = {1, 2};
    int[] upper = {3, 2};
    findProduct(arr, lower, upper);
}
}

// This code is contributed
// by chandan_jnu.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program for array range product queries
// Answers product queries given as two arrays
// lower[] and upper[].
function findProduct( $arr, $lower,$upper)
{
    $n = sizeof($arr);
    $preProd = array($n);
    $countZeros = array($n);

    $prod = 1; // stores the product

    // keeps count of zeros
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // if arr[i] is 0, we increment count and
        // do not multiply it with the product
        if ($arr[$i] == 0)
            $count++;
        else
            $prod *= $arr[$i];

        // store the value of prod in dp
        $preProd[$i] = $prod;

        // store the value of count in countZeros
        $countZeros[$i] = $count;
    }

    // We have preprocessed the array, let us
    // answer queries now.
    for ($i = 0; $i < sizeof($lower); $i++) {
        $l = $lower[$i];
        $u = $upper[$i];

        // range starts from first element
        if ($l == 1)
        {
            // range does not contain any zero
            if ($countZeros[$u - 1] == 0)
                echo($preProd[$u - 1] );
            else
                echo(0);
        }

        else // range starts from any other index
        {
            // no difference in countZeros indicates that
            // there are no zeros in the range
            if ($countZeros[$u - 1] - $countZeros[$l - 2] == 0)
                echo ($preProd[$u - 1] / $preProd[$l - 2]);

            else // zeros are present in the range
                echo(0);
        }
        echo "\n";
    }
}

// Driver Code
$arr = array(0, 2, 3, 4, 5 );
$lower =array (1, 2);
$upper =array (3, 2);    
findProduct($arr, $lower, $upper);

// This code is contributed
// by Mukul Singh
```

## **java 描述语言**

```
<script>

    // JavaScript program for array
    // range product queries

    // Answers product queries
    // given as two arrays
    // lower[] and upper[].
    function findProduct(arr, lower, upper)
    {
        let n = arr.length;
        let preProd = new Array(n);
        preProd.fill(0);
        let countZeros = new Array(n);
        countZeros.fill(0);

        let prod = 1; // stores the product

        // keeps count of zeros
        let count = 0;
        for (let i = 0; i < n; i++)
        {

            // if arr[i] is 0, we increment
            // count and do not multiply it
            // with the product
            if (arr[i] == 0)
                count++;
            else
                prod *= arr[i];

            // store the value
            // of prod in dp
            preProd[i] = prod;

            // store the value of
            // count in countZeros
            countZeros[i] = count;
        }

        // We have preprocessed
        // the array, let us
        // answer queries now.
        for (let i = 0;
                 i < lower.length; i++)
        {
            let l = lower[i];
            let u = upper[i];

            // range starts from
            // first element
            if (l == 1)
            {
                // range does not
                // contain any zero
                if (countZeros[u - 1] == 0)
                    document.write(preProd[u - 1] + "</br>");
                else
                    document.write(0 + "</br>");
            }

            // range starts from
            // any other index
            else
            {
                // no difference in countZeros
                // indicates that there are no
                // zeros in the range
                if (countZeros[u - 1] -
                    countZeros[l - 2] == 0)
                    document.write(
                    (preProd[u - 1] / preProd[l - 2]) +
                    "</br>");

                // zeros are present
                // in the range
                else
                    document.write(0 + "</br>");
            }
        }
    }

    let arr = [0, 2, 3, 4, 5];
    let lower = [1, 2];
    let upper = [3, 2];
    findProduct(arr, lower, upper);

</script>
```

****Output:** 

```
0
2
```** 

****时间复杂度:****0(n)**在创建 dp 数组期间和**0(1)**每个查询**