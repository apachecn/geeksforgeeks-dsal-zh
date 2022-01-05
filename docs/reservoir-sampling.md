# 油藏取样

> 原文:[https://www.geeksforgeeks.org/reservoir-sampling/](https://www.geeksforgeeks.org/reservoir-sampling/)

[储层采样](http://en.wikipedia.org/wiki/Reservoir_sampling)是一系列随机算法，用于从 *n* 项列表中随机选择 *k* 个样本，其中 *n* 是一个非常大或未知的数字。通常 *n* 足够大，以至于列表不适合主内存。例如，谷歌和脸书的搜索查询列表。
所以给我们一个大的数字数组(或流)(为了简化)，我们需要写一个高效的函数来随机选择 *k* 个数字，其中 *1 < = k < = n* 。让输入数组成为*流[]。*

一个**简单的解决方案**是创建一个最大尺寸 *k* 的阵列*水库【】*。逐一从*流中随机选择一个项目[0..n-1]* 。如果选择的项目不是先前选择的，则将其放入*储槽[]* 。要检查一个项目之前是否被选中，我们需要在*蓄水池[]* 中搜索该项目。这个算法的时间复杂度将是 *O(k^2)* 。如果 *k* 很大，这可能会很昂贵。此外，如果输入是流的形式，这也是无效的。

它**可以在** ***O(n)*** **时间**内解决。该解决方案也非常适合流形式的输入。想法和[这个](https://www.geeksforgeeks.org/shuffle-a-given-array/)帖子差不多。以下是步骤。
**1)** 创建阵列*储层【0..k-1]* 并将*流[]* 的第一个 *k* 项复制到其中。
**2)** 现在逐一考虑从 *(k+1)* 项到 *n* 项的所有项目。
… **a)** 生成一个从 0 到 *i* 的随机数，其中 *i* 是*流中当前项目的索引【】*。让生成的随机数为 *j* 。
……**b)**如果 *j* 在 0 到 *k-1* 的范围内，用水流*【I】*替换*蓄水池【j】*

下面是上述算法的实现。

## C++

```
// An efficient program to randomly select
// k items from a stream of items
#include <bits/stdc++.h>
#include <time.h>
using namespace std;

// A utility function to print an array
void printArray(int stream[], int n)
{
    for (int i = 0; i < n; i++)
        cout << stream[i] << " ";
    cout << endl;
}

// A function to randomly select
// k items from stream[0..n-1].
void selectKItems(int stream[], int n, int k)
{
    int i; // index for elements in stream[]

    // reservoir[] is the output array. Initialize
    // it with first k elements from stream[]
    int reservoir[k];
    for (i = 0; i < k; i++)
        reservoir[i] = stream[i];

    // Use a different seed value so that we don't get
    // same result each time we run this program
    srand(time(NULL));

    // Iterate from the (k+1)th element to nth element
    for (; i < n; i++)
    {
        // Pick a random index from 0 to i.
        int j = rand() % (i + 1);

        // If the randomly picked index is smaller than k,
        // then replace the element present at the index
        // with new element from stream
        if (j < k)
        reservoir[j] = stream[i];
    }

    cout << "Following are k randomly selected items \n";
    printArray(reservoir, k);
}

// Driver Code
int main()
{
    int stream[] = {1, 2, 3, 4, 5, 6,
                    7, 8, 9, 10, 11, 12};
    int n = sizeof(stream)/sizeof(stream[0]);
    int k = 5;
    selectKItems(stream, n, k);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// An efficient program to randomly select k items from a stream of items

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// A utility function to print an array
void printArray(int stream[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", stream[i]);
    printf("\n");
}

// A function to randomly select k items from stream[0..n-1].
void selectKItems(int stream[], int n, int k)
{
    int i;  // index for elements in stream[]

    // reservoir[] is the output array. Initialize it with
    // first k elements from stream[]
    int reservoir[k];
    for (i = 0; i < k; i++)
        reservoir[i] = stream[i];

    // Use a different seed value so that we don't get
    // same result each time we run this program
    srand(time(NULL));

    // Iterate from the (k+1)th element to nth element
    for (; i < n; i++)
    {
        // Pick a random index from 0 to i.
        int j = rand() % (i+1);

        // If the randomly  picked index is smaller than k, then replace
        // the element present at the index with new element from stream
        if (j < k)
          reservoir[j] = stream[i];
    }

    printf("Following are k randomly selected items \n");
    printArray(reservoir, k);
}

// Driver program to test above function.
int main()
{
    int stream[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
    int n = sizeof(stream)/sizeof(stream[0]);
    int k = 5;
    selectKItems(stream, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An efficient Java program to randomly
// select k items from a stream of items
import java.util.Arrays;
import java.util.Random;
public class ReservoirSampling {

    // A function to randomly select k items from
    // stream[0..n-1].
    static void selectKItems(int stream[], int n, int k)
    {
        int i; // index for elements in stream[]

        // reservoir[] is the output array. Initialize it
        // with first k elements from stream[]
        int reservoir[] = new int[k];
        for (i = 0; i < k; i++)
            reservoir[i] = stream[i];

        Random r = new Random();

        // Iterate from the (k+1)th element to nth element
        for (; i < n; i++) {
            // Pick a random index from 0 to i.
            int j = r.nextInt(i + 1);

            // If the randomly  picked index is smaller than
            // k, then replace the element present at the
            // index with new element from stream
            if (j < k)
                reservoir[j] = stream[i];
        }

        System.out.println(
            "Following are k randomly selected items");
        System.out.println(Arrays.toString(reservoir));
    }

    // Driver Program to test above method
    public static void main(String[] args)
    {
        int stream[]
            = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 };
        int n = stream.length;
        int k = 5;
        selectKItems(stream, n, k);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# An efficient Python3 program
# to randomly select k items
# from a stream of items
import random
# A utility function
# to print an array
def printArray(stream,n):
    for i in range(n):
        print(stream[i],end=" ");
    print();

# A function to randomly select
# k items from stream[0..n-1].
def selectKItems(stream, n, k):
        i=0;
        # index for elements
        # in stream[]

        # reservoir[] is the output
        # array. Initialize it with
        # first k elements from stream[]
        reservoir = [0]*k;
        for i in range(k):
            reservoir[i] = stream[i];

        # Iterate from the (k+1)th
        # element to nth element
        while(i < n):
            # Pick a random index
            # from 0 to i.
            j = random.randrange(i+1);

            # If the randomly picked
            # index is smaller than k,
            # then replace the element
            # present at the index
            # with new element from stream
            if(j < k):
                reservoir[j] = stream[i];
            i+=1;

        print("Following are k randomly selected items");
        printArray(reservoir, k);

# Driver Code

if __name__ == "__main__":
    stream = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
    n = len(stream);
    k = 5;
    selectKItems(stream, n, k);

# This code is contributed by mits
```

## C#

```
// An efficient C# program to randomly
// select k items from a stream of items
using System;
using System.Collections;

public class ReservoirSampling
{
    // A function to randomly select k
    // items from stream[0..n-1].
    static void selectKItems(int []stream,
                            int n, int k)
    {
        // index for elements in stream[]
        int i;

        // reservoir[] is the output array.
        // Initialize it with first k
        //  elements from stream[]
        int[] reservoir = new int[k];
        for (i = 0; i < k; i++)
            reservoir[i] = stream[i];

        Random r = new Random();

        // Iterate from the (k+1)th
        // element to nth element
        for (; i < n; i++)
        {
            // Pick a random index from 0 to i.
            int j = r.Next(i + 1);

            // If the randomly picked index
            // is smaller than k, then replace
            // the element present at the index
            // with new element from stream
            if(j < k)
                reservoir[j] = stream[i];        
        }

        Console.WriteLine("Following are k " +
                    "randomly selected items");
        for (i = 0; i < k; i++)
        Console.Write(reservoir[i]+" ");
    }

    //Driver code
    static void Main()
    {
        int []stream = {1, 2, 3, 4, 5, 6, 7,
                        8, 9, 10, 11, 12};
        int n = stream.Length;
        int k = 5;
        selectKItems(stream, n, k);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// An efficient PHP program
// to randomly select k items
// from a stream of items

// A utility function
// to print an array
function printArray($stream,$n)
{
    for ($i = 0; $i < $n; $i++)
        echo $stream[$i]." ";
    echo "\n";
}

// A function to randomly select
// k items from stream[0..n-1].
function selectKItems($stream, $n, $k)
    {
        $i; // index for elements
            // in stream[]

        // reservoir[] is the output
        // array. Initialize it with
        // first k elements from stream[]
        $reservoir = array_fill(0, $k, 0);
        for ($i = 0; $i < $k; $i++)
            $reservoir[$i] = $stream[$i];

        // Iterate from the (k+1)th
        // element to nth element
        for (; $i < $n; $i++)
        {
            // Pick a random index
            // from 0 to i.
            $j = rand(0,$i + 1);

            // If the randomly picked
            // index is smaller than k,
            // then replace the element
            // present at the index
            // with new element from stream
            if($j < $k)
                $reservoir[$j] = $stream[$i];    
        }

        echo "Following are k randomly ".
                      "selected items\n";
        printArray($reservoir, $k);
    }

// Driver Code
$stream = array(1, 2, 3, 4, 5, 6, 7,
                8, 9, 10, 11, 12);
$n = count($stream);
$k = 5;
selectKItems($stream, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// An efficient program to randomly select
// k items from a stream of items

// A utility function to print an array
function printArray(stream, n)
{
    for(let i = 0; i < n; i++)
        document.write(stream[i] + " ");

    document.write('\n');
}

// A function to randomly select
// k items from stream[0..n-1].
function selectKItems(stream, n, k)
{

    // Index for elements in stream[]
    let i;

    // reservoir[] is the output array. Initialize
    // it with first k elements from stream[]
    let reservoir = [];
    for(i = 0; i < k; i++)
        reservoir[i] = stream[i];

    // Use a different seed value so that
    // we don't get same result each time
    // we run this program

    // Iterate from the (k+1)th element
    // to nth element
    for(; i < n; i++)
    {
        // Pick a random index from 0 to i.
        let j = (Math.floor(Math.random() *
                 100000000) % (i + 1));

        // If the randomly picked index is
        // smaller than k, then replace the
        // element present at the index
        // with new element from stream
        if (j < k)
            reservoir[j] = stream[i];
    }

    document.write("Following are k randomly " +
                   "selected items \n");
    printArray(reservoir, k);
}

// Driver Code
let stream = [ 1, 2, 3, 4, 5, 6,
               7, 8, 9, 10, 11, 12 ];
let n = stream.length;
let k = 5;

selectKItems(stream, n, k);

// This code is contributed by rohan07

</script>
```

**输出:**

```
Following are k randomly selected items
6 2 11 8 12
Note: Output will differ every time as it selects and prints random elements
```

**时间复杂度:** O(n)

***辅助空间:** O(k)*

**这是如何工作的？**
为了证明这个解决方案是完美的，我们必须证明*流【I】*中 *0 < = i < n* 的任何一个项目在最终*水库【】*中的概率是 *k/n* 。让我们将证明分为两种情况，首先 *k* 项被区别对待。

**情况 1:对于最后一个** ***n-k*** **流项目，即对于** ***流【I】*****其中*****k<= I<n*** **对于每一个这样的流项目*流【I】*，我们从 0 到*随机选取一个索引最后一个项目在最终库的概率=第一个 *k* 指标中的一个被选中作为最后一个项目的概率= *k/n* (从尺寸列表 *n* 中选择一个 *k* 项目的概率)
现在让我们考虑第二个最后一个项目*。第二个最后一项在最终*储层【】* =【迭代中为*流【n-2】*选取第一个 *k* 指标之一的概率】X【迭代中为*流【n-1】*选取的指标与为*流【n-2】*选取的指标不相同的概率】=【*k/(n-1)】*[(n-1)/n【T55
同样，对于*流【n-1】*到*流【k】*的所有流项，我们可以考虑其他项，并对证明进行推广。*****

****情况 2:对于第一个** ***k*** **流项目，即对于** ***流【I】*****其中*****0<= I<k***
第一个 *k* 项目最初被复制到*水库【】*并可能在后面的*流的迭代中被移除
来自*的项目流[0..k-1]* 在最终数组中=当物品*流[k]，流[k+1]，…，物品未被拾取的概率。流[n-1]* 被认为=*[k/(k+1)]×x[(k+1)/(k+2)]×x[(k+2)/(k+3)]x…x[(n-1)/n]= k/n****

**参考文献:
[【http://en.wikipedia.org/wiki/Reservoir_sampling】](http://en.wikipedia.org/wiki/Reservoir_sampling)
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。**