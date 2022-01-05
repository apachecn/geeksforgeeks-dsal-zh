# 利用列车速度和长度计算桥梁长度的程序

> 原文:[https://www . geesforgeks . org/program-to-find-长度-桥梁-使用速度和长度-列车/](https://www.geeksforgeeks.org/program-to-find-length-of-bridge-using-speed-and-length-of-train/)

给定火车的长度和速度以及火车通过桥梁或隧道所花费的时间，任务是找到桥梁的长度。
**例:**

> **输入**:列车长度= 120 米，速度= 30 米/秒，时间= 18 秒
> **输出**:桥梁长度= 420 米。
> **输入**:列车长度= 130 米，速度= 25 米/秒，时间= 21 秒
> **输出**:桥梁长度= 395 米。

**进场:**
让桥梁的长度为![x    ](img/bd0dd68c093f19d4b996e479298a7648.png "Rendered by QuickLaTeX.com")。
众所周知**速度=距离/时间**
因此:

> 总距离=(列车长度+桥梁长度)
> = >列车速度=(列车长度+ x) /时间。
> = > x =(列车速度*时间)–列车长度。

**公式:**

> 桥梁长度=(列车速度*过桥时间)-列车长度。

以下是上述方法的实现:

## C++

```
// C++ Program to implement above code.

#include <bits/stdc++.h>
using namespace std;

// function to calculate the length of bridge.
int bridge_length(int trainLength, int Speed, int Time)
{
    return ((Time * Speed) - trainLength);
}

// Driver Code
int main()
{
    // Assuming the input variables
    int trainLength = 120;
    int Speed = 30;
    int Time = 18;

    cout << "Length of bridge = "
         << bridge_length(trainLength, Speed, Time)
         << " meters";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java Program to implement above code.

public class GFG {

    //function to calculate the length of bridge.
    static int bridge_length(int trainLength,
                            int Speed, int Time)
    {
    return ((Time * Speed) - trainLength);
    }

    //Driver Code
    public static void main(String[] args) {

        // Assuming the input variables
        int trainLength = 120;
        int Speed = 30;
        int Time = 18;

        System.out.print("Length of bridge = "+
            bridge_length(trainLength, Speed,Time)
            +" meters");
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to implement above code.

# function to calculate the length of bridge.
def bridge_length(trainLength, Speed, Time) :

    return ((Time * Speed) - trainLength)

# Driver Code
if __name__ == "__main__" :

    # Assuming the input variables
    trainLength = 120
    Speed = 30
    Time = 18

    print("Length of bridge = ",bridge_length
            (trainLength, Speed, Time),"meters")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to implement above code
using System;

class GFG
{

// function to calculate
// the length of bridge
static int bridge_length(int trainLength,
                         int Speed, int Time)
{
    return ((Time * Speed) - trainLength);
}

// Driver Code
static void Main()
{
    // Assuming the input variables
    int trainLength = 120;
    int Speed = 30;
    int Time = 18;

        Console.Write("Length of bridge = " +
        bridge_length(trainLength, Speed, Time) +
                                      " meters");
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to implement
// above code

// function to calculate
// the length of bridge
function bridge_length($trainLength,
                       $Speed, $Time)
{
    return (($Time * $Speed) -
             $trainLength);
}

// Driver Code

// Assuming the input variables
$trainLength = 120;
$Speed = 30;
$Time = 18;

echo "Length of bridge = ".
    bridge_length($trainLength,
                  $Speed, $Time).
                       " meters";

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>

// Javascript program to implement above code.

// Function to calculate the length of bridge.
function bridge_length(trainLength, Speed, Time)
{
    return ((Time * Speed) - trainLength);
}

// Driver code

// Assuming the input variables
var trainLength = 120;
var Speed = 30;
var Time = 18;

document.write("Length of bridge = " +
   bridge_length(trainLength, Speed,Time) +
   " meters");

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Length of bridge = 420 meters
```