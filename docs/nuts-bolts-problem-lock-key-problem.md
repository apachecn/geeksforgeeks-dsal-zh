# 螺母&螺栓问题(锁&钥匙问题)|设置 1

> 原文:[https://www . geesforgeks . org/nuts-bolts-problem-lock-key-problem/](https://www.geeksforgeeks.org/nuts-bolts-problem-lock-key-problem/)

给定一套 n 个不同尺寸的螺母和 n 个不同尺寸的螺栓。螺母和螺栓之间是一一对应的。高效匹配螺母和螺栓。
**约束:**不允许将一个螺母与另一个螺母或螺栓与另一个螺栓进行比较。意思是螺母只能和螺栓比较，螺栓只能和螺母比较，看哪个大/小。
问这个问题的另一种方法是，给定一个有锁和钥匙的盒子，盒子里的一把钥匙可以打开一把锁。我们需要配对。

**蛮力方式:**先从第一个螺栓开始，和每个螺母对比，直到找到匹配。在最坏的情况下，我们需要 n 次比较。对所有螺栓都这样做给了我们 O(n^2)复杂性。
**快速排序方式:**我们可以使用快速排序技术来解决这个问题。为了理解逻辑，我们用字符数组表示具体细节。
表示为字符数组的坚果
字符坚果[] = {'@ '，' # '，' { content } ' 2019；，' % '，'^'，'& '}
螺栓表示为字符数组
char bolt[]= { ' { content } }。、“%”、“&”、'^'、“@”、“#”}
该算法首先通过选取螺栓数组的最后一个元素作为枢轴来执行分区，重新排列螺母数组并返回分区索引“I ”,使得小于螺母[i]的所有螺母都在左侧，大于螺母[i]的所有螺母都在右侧。接下来，使用螺母[i]，我们可以分割螺栓阵列。分区操作可以很容易地在 O(n)中实现。这一操作也使得螺母和螺栓阵列被很好地分割。现在，我们将这种划分递归地应用于螺母和螺栓的左右子阵列。
当我们在螺母和螺栓上应用分区时，总的时间复杂度是多少？(2*nlogn) =？平均来说。
这里为了简单起见，我们选择了最后一个元素始终作为枢轴。我们也可以做随机快速排序。
以下是上述思路的实现:

## C++

```
// C++ program to solve nut and bolt
// problem using Quick Sort.
#include <iostream>
using namespace std;

// Method to print the array
void printArray(char arr[])
{
    for(int i = 0; i < 6; i++)
    {
        cout << " " <<  arr[i];
    }
    cout << "\n";
}

// Similar to standard partition method.
// Here we pass the pivot element too
// instead of choosing it inside the method.
int partition(char arr[], int low,
            int high, char pivot)
{
    int i = low;
    char temp1, temp2;

    for(int j = low; j < high; j++)
    {
        if (arr[j] < pivot)
        {
            temp1 = arr[i];
            arr[i] = arr[j];
            arr[j] = temp1;
            i++;
        }
        else if(arr[j] == pivot)
        {
            temp1 = arr[j];
            arr[j] = arr[high];
            arr[high] = temp1;
            j--;
        }
    }
    temp2 = arr[i];
    arr[i] = arr[high];
    arr[high] = temp2;

    // Return the partition index of
    // an array based on the pivot
    // element of other array.
    return i;
}

// Function which works just like quick sort
void matchPairs(char nuts[], char bolts[],
                int low, int high)
{
    if (low < high)
    {

        // Choose last character of bolts
        // array for nuts partition.
        int pivot = partition(nuts, low,
                            high, bolts[high]);

        // Now using the partition of nuts
        // choose that for bolts partition.
        partition(bolts, low, high, nuts[pivot]);

        // Recur for [low...pivot-1] &
        // [pivot+1...high] for nuts and
        // bolts array.
        matchPairs(nuts, bolts, low, pivot - 1);
        matchPairs(nuts, bolts, pivot + 1, high);
    }
}

// Driver code
int main()
{

    // Nuts and bolts are represented
    // as array of characters
    char nuts[] = {'@', '#', '{content}apos;, '%', '^', '&'};
    char bolts[] = {'{content}apos;, '%', '&', '^', '@', '#'};

    // Method based on quick sort which
    // matches nuts and bolts
    matchPairs(nuts, bolts, 0, 5);

    cout <<"Matched nuts and bolts are : \n";

    printArray(nuts);
    printArray(bolts);
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to solve nut and bolt
// problem using Quick Sort.
#include<stdio.h>

// Method to print the array
void printArray(char arr[])
{
    for(int i = 0; i < 6; i++)
    {
        printf("%c ", arr[i]);
    }
    printf("\n");
}

// Similar to standard partition method.
// Here we pass the pivot element too
// instead of choosing it inside the method.
int partition(char arr[], int low,
              int high, char pivot)
{
    int i = low;
    char temp1, temp2;

    for(int j = low; j < high; j++)
    {
        if (arr[j] < pivot)
        {
            temp1 = arr[i];
            arr[i] = arr[j];
            arr[j] = temp1;
            i++;
        }
        else if(arr[j] == pivot)
        {
            temp1 = arr[j];
            arr[j] = arr[high];
            arr[high] = temp1;
            j--;
        }
    }
    temp2 = arr[i];
    arr[i] = arr[high];
    arr[high] = temp2;

    // Return the partition index of
    // an array based on the pivot
    // element of other array.
    return i;
}

// Function which works just like quick sort
void matchPairs(char nuts[], char bolts[],
                int low, int high)
{
    if (low < high)
    {

        // Choose last character of bolts
        // array for nuts partition.
        int pivot = partition(nuts, low,
                              high, bolts[high]);

        // Now using the partition of nuts
        // choose that for bolts partition.
        partition(bolts, low, high, nuts[pivot]);

        // Recur for [low...pivot-1] &
        // [pivot+1...high] for nuts and
        // bolts array.
        matchPairs(nuts, bolts, low, pivot - 1);
        matchPairs(nuts, bolts, pivot + 1, high);
    }
}

// Driver code
int main()
{

    // Nuts and bolts are represented
    // as array of characters
    char nuts[] = {'@', '#', '{content}apos;, '%', '^', '&'};
    char bolts[] = {'{content}apos;, '%', '&', '^', '@', '#'};

    // Method based on quick sort which
    // matches nuts and bolts
    matchPairs(nuts, bolts, 0, 5);

    printf("Matched nuts and bolts are : \n");

    printArray(nuts);
    printArray(bolts);
}

// This code is contributed by Amit Mangal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve nut and bolt problem using Quick Sort
public class NutsAndBoltsMatch
{
    //Driver method
    public static void main(String[] args)
    {
        // Nuts and bolts are represented as array of characters
        char nuts[] = {'@', '#', '{content}apos;, '%', '^', '&'};
        char bolts[] = {'{content}apos;, '%', '&', '^', '@', '#'};

        // Method based on quick sort which matches nuts and bolts
        matchPairs(nuts, bolts, 0, 5);

        System.out.println("Matched nuts and bolts are : ");
        printArray(nuts);
        printArray(bolts);
    }

    // Method to print the array
    private static void printArray(char[] arr) {
        for (char ch : arr){
            System.out.print(ch + " ");
        }
        System.out.print("\n");
    }

    // Method which works just like quick sort
    private static void matchPairs(char[] nuts, char[] bolts, int low,
                                                              int high)
    {
        if (low < high)
        {
            // Choose last character of bolts array for nuts partition.
            int pivot = partition(nuts, low, high, bolts[high]);

            // Now using the partition of nuts choose that for bolts
            // partition.
            partition(bolts, low, high, nuts[pivot]);

            // Recur for [low...pivot-1] & [pivot+1...high] for nuts and
            // bolts array.
            matchPairs(nuts, bolts, low, pivot-1);
            matchPairs(nuts, bolts, pivot+1, high);
        }
    }

    // Similar to standard partition method. Here we pass the pivot element
    // too instead of choosing it inside the method.
    private static int partition(char[] arr, int low, int high, char pivot)
    {
        int i = low;
        char temp1, temp2;
        for (int j = low; j < high; j++)
        {
            if (arr[j] < pivot){
                temp1 = arr[i];
                arr[i] = arr[j];
                arr[j] = temp1;
                i++;
            } else if(arr[j] == pivot){
                temp1 = arr[j];
                arr[j] = arr[high];
                arr[high] = temp1;
                j--;
            }
        }
        temp2 = arr[i];
        arr[i] = arr[high];
        arr[high] = temp2;

        // Return the partition index of an array based on the pivot
        // element of other array.
        return i;
    }
}
```

## 蟒蛇 3

```
# Python program to solve nut and bolt
# problem using Quick Sort.
from typing import List

# Method to print the array
def printArray(arr: List[str]) -> None:
    for i in range(6):
        print(" {}".format(arr[i]), end=" ")
    print()

# Similar to standard partition method.
# Here we pass the pivot element too
# instead of choosing it inside the method.
def partition(arr: List[str], low: int, high: int, pivot: str) -> int:
    i = low
    j = low
    while j < high:
        if (arr[j] < pivot):
            arr[i], arr[j] = arr[j], arr[i]
            i += 1
        elif (arr[j] == pivot):
            arr[j], arr[high] = arr[high], arr[j]
            j -= 1
        j += 1
    arr[i], arr[high] = arr[high], arr[i]

    # Return the partition index of
    # an array based on the pivot
    # element of other array.
    return i

# Function which works just like quick sort
def matchPairs(nuts: List[str], bolts: List[str], low: int, high: int) -> None:
    if (low < high):

        # Choose last character of bolts
        # array for nuts partition.
        pivot = partition(nuts, low, high, bolts[high])

        # Now using the partition of nuts
        # choose that for bolts partition.
        partition(bolts, low, high, nuts[pivot])

        # Recur for [low...pivot-1] &
        # [pivot+1...high] for nuts and
        # bolts array.
        matchPairs(nuts, bolts, low, pivot - 1)
        matchPairs(nuts, bolts, pivot + 1, high)

# Driver code
if __name__ == "__main__":

    # Nuts and bolts are represented
    # as array of characters
    nuts = ['@', '#', '{content}apos;, '%', '^', '&']
    bolts = ['{content}apos;, '%', '&', '^', '@', '#']

    # Method based on quick sort which
    # matches nuts and bolts
    matchPairs(nuts, bolts, 0, 5)
    print("Matched nuts and bolts are : ")
    printArray(nuts)
    printArray(bolts)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to solve nut and
// bolt problem using Quick Sort
using System;
using System.Collections.Generic;

class GFG
{
    // Driver Code
    public static void Main(String[] args)
    {
        // Nuts and bolts are represented
        // as array of characters
        char []nuts = {'@', '#', '{content}apos;, '%', '^', '&'};
        char []bolts = {'{content}apos;, '%', '&', '^', '@', '#'};

        // Method based on quick sort
        // which matches nuts and bolts
        matchPairs(nuts, bolts, 0, 5);

        Console.WriteLine("Matched nuts and bolts are : ");
        printArray(nuts);
        printArray(bolts);
    }

    // Method to print the array
    private static void printArray(char[] arr)
    {
        foreach (char ch in arr)
        {
            Console.Write(ch + " ");
        }
        Console.Write("\n");
    }

    // Method which works just like quick sort
    private static void matchPairs(char[] nuts,
                                   char[] bolts,
                                   int low, int high)
    {
        if (low < high)
        {
            // Choose last character of
            // bolts array for nuts partition.
            int pivot = partition(nuts, low,
                                  high, bolts[high]);

            // Now using the partition of nuts
            // choose that for bolts partition.
            partition(bolts, low, high, nuts[pivot]);

            // Recur for [low...pivot-1] &
            // [pivot+1...high] for nuts
            // and bolts array.
            matchPairs(nuts, bolts, low, pivot - 1);
            matchPairs(nuts, bolts, pivot + 1, high);
        }
    }

    // Similar to standard partition method.
    // Here we pass the pivot element too
    // instead of choosing it inside the method.
    private static int partition(char[] arr, int low,
                                 int high, char pivot)
    {
        int i = low;
        char temp1, temp2;
        for (int j = low; j < high; j++)
        {
            if (arr[j] < pivot)
            {
                temp1 = arr[i];
                arr[i] = arr[j];
                arr[j] = temp1;
                i++;
            }
            else if(arr[j] == pivot)
            {
                temp1 = arr[j];
                arr[j] = arr[high];
                arr[high] = temp1;
                j--;
            }
        }
        temp2 = arr[i];
        arr[i] = arr[high];
        arr[high] = temp2;

        // Return the partition index of an array
        // based on the pivot element of other array.
        return i;
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to solve nut and
// bolt problem using Quick Sort

    // Method to print the array
    function printArray(arr)
    {
        for (let ch = 0 ; ch < arr.length ; ch++)
        {
            document.write(arr[ch] + " ");
        }
        document.write("<br>");
    }

    // Method which works just like quick sort
    function matchPairs( nuts, bolts, low,  high)
    {
        if (low < high)
        {
            // Choose last character of
            // bolts array for nuts partition.
            var pivot = partition(nuts, low,
                                  high, bolts[high]);

            // Now using the partition of nuts
            // choose that for bolts partition.
            partition(bolts, low, high, nuts[pivot]);

            // Recur for [low...pivot-1] &
            // [pivot+1...high] for nuts
            // and bolts array.
            matchPairs(nuts, bolts, low, pivot - 1);
            matchPairs(nuts, bolts, pivot + 1, high);
        }
    }

    // Similar to standard partition method.
    // Here we pass the pivot element too
    // instead of choosing it inside the method.
    function partition( arr,  low, high,  pivot)
    {
        var i = low;
        var temp1, temp2;
        for (var j = low; j < high; j++)
        {
            if (arr[j] < pivot)
            {
                temp1 = arr[i];
                arr[i] = arr[j];
                arr[j] = temp1;
                i++;
            }
            else if(arr[j] == pivot)
            {
                temp1 = arr[j];
                arr[j] = arr[high];
                arr[high] = temp1;
                j--;
            }
        }
        temp2 = arr[i];
        arr[i] = arr[high];
        arr[high] = temp2;

        // Return the partition index of an array
        // based on the pivot element of other array.
        return i;
    }

        // Driver Code

        // Nuts and bolts are represented
        // as array of characters
        var nuts = ['@', '#', '{content}apos;, '%', '^', '&'];
        var bolts = ['{content}apos;, '%', '&', '^', '@', '#'];

        // Method based on quick sort
        // which matches nuts and bolts
        matchPairs(nuts, bolts, 0, 5);

        document.write(
        "Matched nuts and bolts are : " + "<br>"
        );
        printArray(nuts);
        printArray(bolts);

</script>
```

**输出:**

```
Matched nuts and bolts are :
# $ % & @ ^
# $ % & @ ^
```

[螺母&螺栓问题(锁&钥匙问题)|第二集(Hashmap)](https://www.geeksforgeeks.org/nuts-bolts-problem-lock-key-problem-set-2-hashmap/)
本文由**库马尔·高塔姆**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息