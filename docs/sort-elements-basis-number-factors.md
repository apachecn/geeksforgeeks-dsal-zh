# 根据因子数量对元素进行排序

> 原文:[https://www . geesforgeks . org/sort-elements-basis-number-factors/](https://www.geeksforgeeks.org/sort-elements-basis-number-factors/)

给定一个正整数数组。按照每个元素的因子数递减的顺序对给定的数组进行排序，即因子数最多的元素应该是第一个显示的元素，因子数最少的元素应该是最后一个显示的元素。因子数量相等的两个元素应该与原始数组中的元素顺序相同。
示例:

```
Input : {5, 11, 10, 20, 9, 16, 23}
Output : 20 16 10 9 5 11 23
Number of distinct factors:
For 20 = 6, 16 = 5, 10 = 4, 9 = 3
and for 5, 11, 23 = 2 (same number of factors
therefore sorted in increasing order of index)

Input : {104, 210, 315, 166, 441, 180}
Output : 180 210 315 441 104 166
```

以下步骤按照因子计数的递减顺序对数字进行排序。

1.  计算每个元素的不同因子数。参见[本](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)。
2.  您可以为每个元素使用一个结构来存储其原始索引和因子计数。创建此类结构的数组来存储所有元素的此类信息。
3.  使用任何排序算法根据问题陈述对这一组结构进行排序。
4.  从头开始遍历这个结构数组，并借助存储在已排序的结构数组的每个元素的结构中的索引，从原始数组中获取数字。

## C++

```
// C++ implementation to sort numbers on
// the basis of factors
#include <bits/stdc++.h>

using namespace std;

// structure of each element having its index
// in the input array and number of factors
struct element
{
    int index, no_of_fact;
};

// function to count factors for
// a given number n
int countFactors(int n)
{
    int count = 0;
    int sq = sqrt(n);

    // if the number is a perfect square
    if (sq * sq == n)
        count++;

    // count all other factors
    for (int i=1; i<sqrt(n); i++)
    {
        // if i is a factor then n/i will be
        // another factor. So increment by 2
        if (n % i == 0)   
            count += 2;
    }       

    return count;
}

// comparison function for the elements
// of the structure
bool compare(struct element e1, struct element e2)
{
    // if two elements have the same number
    // of factors then sort them in increasing
    // order of their index in the input array
    if (e1.no_of_fact == e2.no_of_fact)
        return e1.index < e2.index;

    // sort in decreasing order of number of factors
    return e1.no_of_fact > e2.no_of_fact;   
}

// function to print numbers after sorting them in
// decreasing order of number of factors
void printOnBasisOfFactors(int arr[], int n)
{   
    struct element num[n];

    // for each element of input array create a
    // structure element to store its index and
    // factors count
    for (int i=0; i<n; i++)
    {
        num[i].index = i;
        num[i].no_of_fact = countFactors(arr[i]);       
    }

    // sort the array of structures as defined
    sort(num, num+n, compare);

    // access index from the structure element and corresponding
    // to that index access the element from arr
    for (int i=0; i<n; i++)
        cout << arr[num[i].index] << " ";
}

// Driver program to test above
int main()
{
    int arr[] = {5, 11, 10, 20, 9, 16, 23};
    int n = sizeof(arr) / sizeof(arr[0]);
    printOnBasisOfFactors(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort numbers on
// the basis of factors

import java.util.Arrays;
import java.util.Comparator;

class Element
{
    //each element having its index
    // in the input array and number of factors
    int index, no_of_fact;

    public Element(int i, int countFactors)
    {
        index = i;
        no_of_fact = countFactors;
    }

    // method to count factors for
    // a given number n
    static int countFactors(int n)
    {
        int count = 0;
        int sq = (int)Math.sqrt(n);

        // if the number is a perfect square
        if (sq * sq == n)
            count++;

        // count all other factors
        for (int i=1; i<Math.sqrt(n); i++)
        {
            // if i is a factor then n/i will be
            // another factor. So increment by 2
            if (n % i == 0)   
                count += 2;
        }       

        return count;
    }

    // function to print numbers after sorting them in
    // decreasing order of number of factors
    static void printOnBasisOfFactors(int arr[], int n)
    {   
        Element num[] = new Element[n];

        // for each element of input array create a
        // structure element to store its index and
        // factors count
        for (int i=0; i<n; i++)
        {
            num[i] = new Element(i,countFactors(arr[i]));
        }

        // sort the array of structures as defined
        Arrays.sort(num,new Comparator<Element>() {

            @Override
            // compare method for the elements
            // of the structure
            public int compare(Element e1, Element e2) {
                // if two elements have the same number
                // of factors then sort them in increasing
                // order of their index in the input array
                if (e1.no_of_fact == e2.no_of_fact)
                 return e1.index < e2.index ? -1 : 1;

                // sort in decreasing order of number of factors
                return e1.no_of_fact > e2.no_of_fact ? -1 : 1; 
            }

        });

        // access index from the structure element and corresponding
        // to that index access the element from arr
        for (int i=0; i<n; i++)
            System.out.print(arr[num[i].index]+" ");
    }

    // Driver program to test above
    public static void main(String[] args)
    {

        int arr[] = {5, 11, 10, 20, 9, 16, 23};

        printOnBasisOfFactors(arr, arr.length);

    }
}
// This code is contributed by Gaurav Miglani
```

输出:

```
20 16 10 9 5 11 23
```

时间复杂度:O(n √n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。