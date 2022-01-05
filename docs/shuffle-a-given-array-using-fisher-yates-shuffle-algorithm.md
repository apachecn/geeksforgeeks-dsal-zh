# 使用费希尔-耶茨混洗算法混洗给定的数组

> 原文:[https://www . geeksforgeeks . org/shuffle-给定数组-使用-fisher-Yates-shuffle-algorithm/](https://www.geeksforgeeks.org/shuffle-a-given-array-using-fisher-yates-shuffle-algorithm/)

给定一个数组，编写一个程序来生成数组元素的随机排列。这个问题也被称为“洗牌”或“随机化给定的阵列”。这里 shuffle 意味着数组元素的每个排列都应该同样可能。

![shuffle-array](img/59ddf5216a59d4898c9e512c0da3cca6.png)

假设给定的数组是 *arr[]* 。一个简单的解决方案是创建一个辅助数组 *temp[]* ，它最初是 *arr[]* 的副本。从*temp【】*中随机选择一个元素，将随机选择的元素复制到*arr【0】*中，并从*temp【】*中移除所选元素。重复相同的过程 n 次，并继续将元素复制到 *arr[1]，arr[2]，…。*这个解决方案的时间复杂度将是 O(n^2).
[费希尔-耶茨混洗算法](http://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle#The_modern_algorithm)在 O(n)时间复杂度下工作。这里的假设是，给我们一个函数 rand()，它在 O(1)时间内生成随机数。
思路是从最后一个元素开始，用整个数组(包括最后一个)中随机选择的元素进行交换。现在考虑从 0 到 n-2(大小减少 1)的数组，重复这个过程，直到我们遇到第一个元素。
以下是详细算法

```
To shuffle an array a of n elements (indices 0..n-1):
  for i from n - 1 downto 1 do
       j = random integer with 0 <= j <= i
       exchange a[j] and a[i]
```

下面是该算法的实现。

## C++

```
// C++ Program to shuffle a given array
#include<bits/stdc++.h>
#include <stdlib.h>
#include <time.h>
using namespace std;

// A utility function to swap to integers
void swap (int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// A utility function to print an array
void printArray (int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << "\n";
}

// A function to generate a random
// permutation of arr[]
void randomize (int arr[], int n)
{
    // Use a different seed value so that
    // we don't get same result each time
    // we run this program
    srand (time(NULL));

    // Start from the last element and swap
    // one by one. We don't need to run for
    // the first element that's why i > 0
    for (int i = n - 1; i > 0; i--)
    {
        // Pick a random index from 0 to i
        int j = rand() % (i + 1);

        // Swap arr[i] with the element
        // at random index
        swap(&arr[i], &arr[j]);
    }
}

// Driver Code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8};
    int n = sizeof(arr) / sizeof(arr[0]);
    randomize (arr, n);
    printArray(arr, n);

    return 0;
}

// This code is contributed by
// rathbhupendra
```

## C

```
// C Program to shuffle a given array

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// A utility function to swap to integers
void swap (int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// A utility function to print an array
void printArray (int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// A function to generate a random permutation of arr[]
void randomize ( int arr[], int n )
{
    // Use a different seed value so that we don't get same
    // result each time we run this program
    srand ( time(NULL) );

    // Start from the last element and swap one by one. We don't
    // need to run for the first element that's why i > 0
    for (int i = n-1; i > 0; i--)
    {
        // Pick a random index from 0 to i
        int j = rand() % (i+1);

        // Swap arr[i] with the element at random index
        swap(&arr[i], &arr[j]);
    }
}

// Driver program to test above function.
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8};
    int n = sizeof(arr)/ sizeof(arr[0]);
    randomize (arr, n);
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to shuffle a given array
import java.util.Random;
import java.util.Arrays;
public class ShuffleRand
{
    // A Function to generate a random permutation of arr[]
    static void randomize( int arr[], int n)
    {
        // Creating a object for Random class
        Random r = new Random();

        // Start from the last element and swap one by one. We don't
        // need to run for the first element that's why i > 0
        for (int i = n-1; i > 0; i--) {

            // Pick a random index from 0 to i
            int j = r.nextInt(i+1);

            // Swap arr[i] with the element at random index
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
        // Prints the random array
        System.out.println(Arrays.toString(arr));
    }

    // Driver Program to test above function
    public static void main(String[] args)
    {

         int[] arr = {1, 2, 3, 4, 5, 6, 7, 8};
         int n = arr.length;
         randomize (arr, n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python Program to shuffle a given array
import random

# A function to generate a random permutation of arr[]
def randomize (arr, n):
    # Start from the last element and swap one by one. We don't
    # need to run for the first element that's why i > 0
    for i in range(n-1,0,-1):
        # Pick a random index from 0 to i
        j = random.randint(0,i+1)

        # Swap arr[i] with the element at random index
        arr[i],arr[j] = arr[j],arr[i]
    return arr

# Driver program to test above function.
arr = [1, 2, 3, 4, 5, 6, 7, 8]
n = len(arr)
print(randomize(arr, n))

# This code is contributed by Pratik Chhajer
```

## C#

```
// C# Code for Number of digits
// in the product of two numbers
using System;

class GFG
{
// A Function to generate a
// random permutation of arr[]
    static void randomize(int []arr, int n)
    {
        // Creating a object
        // for Random class
        Random r = new Random();

        // Start from the last element and
        // swap one by one. We don't need to
        // run for the first element
        // that's why i > 0
        for (int i = n - 1; i > 0; i--)
        {

            // Pick a random index
            // from 0 to i
            int j = r.Next(0, i+1);

            // Swap arr[i] with the
            // element at random index
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
        // Prints the random array
        for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
    }

// Driver Code
static void Main()
{
    int[] arr = {1, 2, 3, 4,
                 5, 6, 7, 8};
    int n = arr.Length;
    randomize (arr, n);
}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to shuffle
// a given array

// A function to generate
// a random permutation of arr[]
function randomize ($arr, $n)
{
    // Start from the last element
    // and swap one by one. We
    // don't need to run for the
    // first element that's why i > 0
    for($i = $n - 1; $i >= 0; $i--)
    {
        // Pick a random index
        // from 0 to i
        $j = rand(0, $i+1);

        // Swap arr[i] with the
        // element at random index
        $tmp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $tmp;
    }
    for($i = 0; $i < $n; $i++)
    echo $arr[$i]." ";
}

// Driver Code
$arr = array(1, 2, 3, 4,
             5, 6, 7, 8);
$n = count($arr);
randomize($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// JavaScript Program to shuffle a given array

// A function to print an array
let printArray = (arr, n)=>
{
    ans = '';
    for (let i = 0; i < n; i++)
    {
        ans += arr[i] + " ";
    }
    console.log(ans);
}

// A function to generate a random
// permutation of arr
let randomize = (arr, n) =>
{

    // Start from the last element and swap
    // one by one. We don't need to run for
    // the first element that's why i > 0
    for (let i = n - 1; i > 0; i--)
    {

        // Pick a random index from 0 to i inclusive
        let j = Math.floor(Math.random() * (i + 1));

        // Swap arr[i] with the element
        // at random index
        [arr[i], arr[j]] = [arr[j], arr[i]];
    }
}

// Driver Code
let arr = [1, 2, 3, 4, 5, 6, 7, 8];
let n = arr.length;
randomize (arr, n);
printArray(arr, n);

// This code is contributed by rohitsingh07052.
</script>
```

**输出:**

```
7 8 4 6 3 1 2 5
```

上面的函数假设 rand()生成一个随机数。
**时间复杂度:** O(n)，假设函数 rand()花费 O(1)时间。

***辅助空间:**O(1)*
T5】这是怎么工作的？
第 I 个元素(包括最后一个)走到最后一个位置的概率是 1/n，因为我们在第一次迭代中随机选取了一个元素。
通过两种情况下的除法，可以证明 ith 元素到倒数第二位的概率为 1/n。
*情况 1: i = n-1(最后一个元素的索引)* :
最后一个元素转到第二个最后位置的概率为=(最后一个元素没有停留在原来位置的概率)x(上一步拾取的索引再次被拾取从而最后一个元素被交换的概率)
所以概率=((n-1)/n)x(1/(n-1))= 1/n
*情况 2: 0 < i < n-1* :
ith 元素到第二个位置的概率=(上一次迭代中 ith 元素没有被拾取的概率)x(本次迭代中 ith 元素被拾取的概率)
所以概率= ((n-1)/n) x (1/(n-1)) = 1/n
我们可以很容易地将以上证明推广到任何其他位置。

？list = plqm7 alhxfyseqd k2mdfbwedd2s vvjh9p
如果发现有不正确的地方，或者想分享更多关于上面讨论的话题的信息，请写评论。