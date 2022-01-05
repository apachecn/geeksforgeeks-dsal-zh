# 斯特恩-布罗克序列

> 原文:[https://www.geeksforgeeks.org/stern-brocot-sequence/](https://www.geeksforgeeks.org/stern-brocot-sequence/)

**Stern Brocot 序列**与斐波那契序列相似，但生成斐波那契序列的方式不同。
**代斯特布罗克序列:**

> 1.序列的第一个和第二个元素是 1 和 1。
> 2。考虑序列的第二个成员。然后，将所考虑的序列成员和它的先例(即 1 + 1 = 2)相加。现在 2 是我们系列的下一个元素。顺序将是**【1，1，2】**
> 3。在这个元素之后，我们序列的下一个元素将是我们第二步考虑的元素。现在的顺序将是**【1，1，2，1】**
> 4。我们再次执行步骤 2，但是现在考虑的元素将是 2(第三个元素)。因此，序列的下一个数字将是考虑的数字和它的先例(2 + 1 = 3)的和。序列现在将是**【1，1，2，1，3】**
> 5。与步骤 3 一样，下一个元素将是考虑的元素，即 2。这样顺序将是**【1，1，2，1，3，2】**
> 6。因此这个过程继续，现在下一个考虑的元素将是 1(第 4 个元素)。

下面是打印斯特恩·布罗克序列的简单程序。

## C++

```
// CPP program to print Brocot Sequence
#include <bits/stdc++.h>
using namespace std;

void SternSequenceFunc(vector<int>& BrocotSequence, int n)
{
    // loop to create sequence
    for (int i = 1; BrocotSequence.size() < n; i++)
    {
        int considered_element = BrocotSequence[i];
        int precedent = BrocotSequence[i - 1];

        // adding sum of considered element and it's precedent
        BrocotSequence.push_back(considered_element + precedent);

        // adding next considered element
        BrocotSequence.push_back(considered_element);
    }

    // printing sequence..
    for (int i = 0; i < 15; ++i)
        cout << BrocotSequence[i] << " ";
}

int main()
{
    int n = 15;
    vector<int> BrocotSequence;

    // adding first two element
    // in the sequence
    BrocotSequence.push_back(1);
    BrocotSequence.push_back(1);

    SternSequenceFunc(BrocotSequence, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// Brocot Sequence
import java.io.*;
import java.util.*;

class GFG {

static void SternSequenceFunc(Vector<Integer>
                         BrocotSequence, int n)
{
    // loop to create sequence
    for (int i = 1; BrocotSequence.size() < n; i++)
    {
        int considered_element = BrocotSequence.get(i);
        int precedent = BrocotSequence.get(i-1);

        // adding sum of considered element and it's precedent
        BrocotSequence.add(considered_element + precedent);

        // adding next considered element
        BrocotSequence.add(considered_element);
    }

    // printing sequence..
    for (int i = 0; i < 15; ++i)
        System.out.print(BrocotSequence.get(i) + " ");
}
    // Driver code
    public static void main (String[] args) {

        int n = 15;
        Vector<Integer> BrocotSequence = new Vector<Integer>();

        // adding first two element
        // in the sequence
        BrocotSequence.add(1);
        BrocotSequence.add(1);

        SternSequenceFunc(BrocotSequence, n);

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python program to print
# Brocot Sequence
import math

def SternSequenceFunc(BrocotSequence, n):

    # loop to create sequence
    for i in range(1,  n):

        considered_element = BrocotSequence[i]
        precedent = BrocotSequence[i-1]

        # adding sum of considered
        # element and it's precedent
        BrocotSequence.append(considered_element + precedent)

        # adding next considered element
        BrocotSequence.append(considered_element)

    # printing sequence..
    for i in range(0, 15):
        print(BrocotSequence[i] , end=" ")

# Driver code
n = 15
BrocotSequence = []

# adding first two element
# in the sequence
BrocotSequence.append(1)
BrocotSequence.append(1)

SternSequenceFunc(BrocotSequence, n)

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to print
// Brocot Sequence
using System;
using System.Collections.Generic;

class GFG
{
static void SternSequenceFunc(List<int>
                 BrocotSequence, int n)
{
    // loop to create sequence
    for (int i = 1;
             BrocotSequence.Count < n; i++)
    {
        int considered_element =
                       BrocotSequence[i];
        int precedent =
                   BrocotSequence[i - 1];

        // adding sum of considered
        // element and it's precedent
        BrocotSequence.Add(considered_element +
                                    precedent);

        // adding next
        // considered element
        BrocotSequence.Add(
                       considered_element);
    }

    // printing sequence..
    for (int i = 0; i < 15; ++i)
        Console.Write(
                BrocotSequence[i] + " ");
}
// Driver code
static void Main ()
{

    int n = 15;
    List<int> BrocotSequence =
                    new List<int>();

    // adding first two element
    // in the sequence
    BrocotSequence.Add(1);
    BrocotSequence.Add(1);

    SternSequenceFunc(BrocotSequence, n);
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to
// print Brocot Sequence

function SternSequenceFunc(&$BrocotSequence, $n)
{
    // loop to create sequence
    for ($i = 1;
         count($BrocotSequence) < $n;
         $i++)
    {
        $considered_element =
                    $BrocotSequence[$i];
        $precedent = $BrocotSequence[$i - 1];

        // adding sum of considered
        // element and it's precedent
        array_push($BrocotSequence,
                   $considered_element +
                   $precedent);

        // adding next
        // considered element
        array_push($BrocotSequence,
                   $considered_element);
    }

    // printing sequence..
    for ($i = 0; $i < 15; ++$i)
        echo ($BrocotSequence[$i]." ");
}

// Driver code
$n = 15;
$BrocotSequence = array();

// adding first two element
// in the sequence
array_push($BrocotSequence, 1);
array_push($BrocotSequence, 1);

SternSequenceFunc($BrocotSequence, $n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to print Brocot Sequence

function SternSequenceFunc( BrocotSequence, n)
{
    // loop to create sequence
    for (var i = 1; BrocotSequence.length < n; i++)
    {
        var considered_element = BrocotSequence[i];
        var precedent = BrocotSequence[i - 1];

        // adding sum of considered element and it's precedent
        BrocotSequence.push(considered_element + precedent);

        // adding next considered element
        BrocotSequence.push(considered_element);
    }

    // printing sequence..
    for (var i = 0; i < 15; ++i)
        document.write( BrocotSequence[i] + " ");
}

var n = 15;
var BrocotSequence = [];

// adding first two element
// in the sequence
BrocotSequence.push(1);
BrocotSequence.push(1);

SternSequenceFunc(BrocotSequence, n);

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
1 1 2 1 3 2 3 1 4 3 5 2 5 3 4
```

**参考文献:**
[【吉图布】](https://github.com/rhdunn/stern-brocot)T5】