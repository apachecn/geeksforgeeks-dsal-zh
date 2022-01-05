# 数组中的平均数

> 原文:[https://www.geeksforgeeks.org/average-numbers-array/](https://www.geeksforgeeks.org/average-numbers-array/)

给定一系列正整数 a1，a2，…，an。找到所有这样的索引 I，使得第 I 个元素等于所有其他元素的算术平均值(即除了这个元素之外的所有元素)。
**例:**

```
Input : 5
        1 2 3 4 5
Output : 1 no. of elements
         2 index of element
Average of 1, 2, 4 & 5 is 3 so the 
output is single index i.e. 3.

Input : 4
        50 50 50 50
Output : 4 no. of elements
         0 1 2 3 index of element
Average of 50, 50, 50 & 50 is 50 and 
all the indexes has the same i.e. 50
so the output is indexes 1, 2, 3 & 4.
```

## C++

```
// CPP program to print all such indices such
// that the i-th element equals the arithmetic
// mean of all other elements
#include <bits/stdc++.h>
using namespace std;

// function to find number of elements
// satisfying condition and their indexes
void averageNumbers(int arr[], int n, int sum)
{

    int cnt = 0;

    // calculating average
    sum /= (double)n;

    // counting how many elements
    // satisfies the condition.
    cout << count(arr, arr + n, sum)
         << endl;
    for (int i = 0; i < n; i++) {
        if ((double)arr[i] == sum) {

            // output the indices.
            cout << i << " ";
            cnt++;
        }
    }
}

// Driver code
int main()
{
    int n;
    int arr[] = { 1, 2, 3, 4, 5 };
    n = sizeof(arr) / sizeof(arr[0]);
    double sum = 0;
    int cnt = 0;

    // sum of the elements of the array
    for (int i = 0; i < n; i++) {
        sum += (double)arr[i];
    }
    averageNumbers(arr, n, sum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all such indices such
// that the i-th element equals the arithmetic
// mean of all other elements
public class GFG {

// function to find number of elements
// satisfying condition and their indexes
    static void averageNumbers(int arr[], int n, int sum) {

        int cnt = 0;

        // calculating average
        sum /= (double) n;

        // counting how many elements
        // satisfies the condition.
        System.out.println(count(arr, sum));
        for (int i = 0; i < n; i++) {
            if ((double) arr[i] == sum) {

                // output the indices.
                System.out.print(i + " ");
                cnt++;
            }
        }
    }

    static int count(int[] array, int sum) {
        int count = 0;
        for (int i = 0; i < array.length; i++) {
            if (array[i] == sum) {
                count++;
            }
        }
        return count;
    }
// Driver code

    public static void main(String[] args) {
        int n;
        int arr[] = {1, 2, 3, 4, 5};
        n = arr.length;
        int sum = 0;
        int cnt = 0;

        // sum of the elements of the array
        for (int i = 0; i < n; i++) {
            sum += (double) arr[i];
        }
        averageNumbers(arr, n, sum);

    }

}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to print all such indices
# such that the i-th element equals the
# arithmetic mean of all other elements

# Function to find number of elements
# satisfying condition and their indexes
def averageNumbers(arr, n, sum):
    cnt = 0

    # calculating average
    sum /= n

    # counting how many elements
    # satisfies the condition.
    print(count(arr, sum))
    for i in range(0, n):
        if (arr[i] == sum):

            # output the indices.
            print(i, " ")
            cnt += 1

def count(array, sum):
    count = 0
    for i in range(0, len(array)):
        if (array[i] == sum):
            count += 1
    return count

# Driver code
if __name__ == '__main__':
    n = 0
    arr = [ 1, 2, 3, 4, 5 ]
    n = len(arr)
    sum = 0
    cnt = 0

    # sum of the elements of the array
    for i in range(0, n):
        sum += arr[i]
    averageNumbers(arr, n, sum)

# This code contributed by 29AjayKumar
```

## C#

```

// C# program to print all such indices such
// that the i-th element equals the arithmetic
// mean of all other elements
using System;
public class GFG {

// function to find number of elements
// satisfying condition and their indexes
    static void averageNumbers(int []arr, int n, int sum) {

        int cnt = 0;

        // calculating average
        sum /=  n;

        // counting how many elements
        // satisfies the condition.
        Console.WriteLine(count(arr, sum));
        for (int i = 0; i < n; i++) {
            if ((double) arr[i] == sum) {

                // output the indices.
                Console.Write(i + " ");
                cnt++;
            }
        }
    }

    static int count(int[] array, int sum) {
        int count = 0;
        for (int i = 0; i < array.Length; i++) {
            if (array[i] == sum) {
                count++;
            }
        }
        return count;
    }
// Driver code

    public static void Main() {
        int n;
        int []arr = {1, 2, 3, 4, 5};
        n = arr.Length;
        int sum = 0;

        // sum of the elements of the array
        for (int i = 0; i < n; i++) {
            sum += arr[i];
        }
        averageNumbers(arr, n, sum);

    }

}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all such indices
// such that the i-th element equals the
// arithmetic mean of all other elements

// counting how many elements
// satisfies the condition.
function coun_t($arr, $sum)
{
    $cnt = 0;
    for ( $i = 0; $i < count($arr); $i++)
    {
        if ($arr[$i] == $sum)
        {
            $cnt++;
        }
    }
    return $cnt;
}

// function to find number of elements
// satisfying condition and their indexes
function averageNumbers($arr, $n, $sum)
{

    $cnt = 0;

    // calculating average
    $sum /= $n;

    // counting how many elements
    // satisfies the condition.
    echo coun_t($arr, $sum) . "\n";

    for ( $i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == $sum)
        {

            // output the indices.
            echo $i . " ";
            $cnt++;
        }
    }
}

// Driver Code
$n = 0;
$arr = array( 1, 2, 3, 4, 5 );
$n = count($arr);
$sum = 0;
$cnt = 0;

// sum of the elements of the array
for ($i = 0; $i < $n; $i++)
{
    $sum += $arr[$i];
}
averageNumbers($arr, $n, $sum);

// This code is contributed by
// Rajput-Ji
?>
```

## java 描述语言

```
<script>
    // Javascript program to print all such indices such
    // that the i-th element equals the arithmetic
    // mean of all other elements

    // function to find number of elements
    // satisfying condition and their indexes
    function averageNumbers(arr, n, sum) {

        let cnt = 0;

        // calculating average
        sum /=  n;

        // counting how many elements
        // satisfies the condition.
        document.write(count(arr, sum) + "</br>");
        for (let i = 0; i < n; i++) {
            if (arr[i] == sum) {

                // output the indices.
                document.write(i + " ");
                cnt++;
            }
        }
    }

    function count(array, sum) {
        let count = 0;
        for (let i = 0; i < array.length; i++) {
            if (array[i] == sum) {
                count++;
            }
        }
        return count;
    }

    // Driver code
    let n;
    let arr = [1, 2, 3, 4, 5];
    n = arr.length;
    let sum = 0;

    // sum of the elements of the array
    for (let i = 0; i < n; i++) {
      sum += arr[i];
    }
    averageNumbers(arr, n, sum);

    // This code is contributed by mukesh07.
</script>
```

**输出:**

```
1
2 
```

**时间复杂度:** O(n)
本文由 [**萨加尔·舒克拉**](https://auth.geeksforgeeks.org/profile.php?user=Sagar Shukla) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。