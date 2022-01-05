# 找出矩形区域的百分比变化

> 原文:[https://www . geeksforgeeks . org/find-矩形面积变化百分比/](https://www.geeksforgeeks.org/find-the-percentage-change-in-the-area-of-a-rectangle/)

给定两个整数 **P** 和 **Q** ，表示矩形的**长度和宽度的百分比变化，任务是在矩形的[区域打印百分比变化。](https://www.geeksforgeeks.org/program-area-perimeter-rectangle/)**

**示例:**

> **输入:** P = 10，Q = 20
> **输出:** 32
> **说明:**
> 让矩形的初始长度为 100，宽度为 80。
> 初始面积= 8000。
> 新长度= 110，新宽度= 96。因此，新面积= 10560。
> 面积变化百分比=((10560–8000)/8000)* 100 = 32。
> 
> **输入:** P = 20，Q =-10
> T3】输出: 8
> 让矩形的初始长度为 100，宽度为 80。
> 初始面积= 8000。
> 新长度= 120，新宽度= 72。因此，新面积= 8640。
> 面积变化百分比=((8640–8000)/8000)* 100 = 8。

**进场:**

*   由于矩形的[面积由公式

    ```
    area = length * breadth

    ```

    给出](https://www.geeksforgeeks.org/program-area-perimeter-rectangle/)
*   假设矩形的初始长度为 **L** ，矩形的宽度为 **B** 。因此，初始面积由 **L * B** 给出。
*   因此，新的长度和宽度给出为:

    ```
    L' = L + ((P/100)*L)
    B' = B + ((Q/100)*B)

    ```

*   因此，新的长度和宽度给出为:

    > **新增面积=[L+((C/100)* L)]*[B+((D/100)* B)]**

*   The percentage change in the area is given by the formula:

    > **%变化=((新区-旧区)/旧区)*100**

    下面是上述方法的实现:

    ## C++

    ```
    // CPP implementation to find the percentage
    #include <bits/stdc++.h>
    using namespace std;

    // change in the area when the percentage change
    // in the length and breadth is given

    // Function to calculate percentage
    // change in area of rectangle
    int calculate_change(int length, int breadth){
        int change = 0;
        change = length + breadth+((length * breadth)/100);
        return change;
      }

    // Driver code
    int main()
    {
      int cL = 20;
      int cB = -10;
      int cA = calculate_change(cL, cB);

      printf("%d",cA);
      return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation to find the percentage
    import java.util.*;

    class GFG{

        // change in the area when the percentage change
        // in the length and breadth is given

        // Function to calculate percentage
        // change in area of rectangle
        static int calculate_change(int length, int breadth){
            int change = 0;
            change = length + breadth+((length * breadth)/100);
            return change;
        }

        // Driver code
        public static void main(String args[])
        {
            int cL = 20;
            int cB = -10;
            int cA = calculate_change(cL, cB);

            System.out.println(+ cA);

        }
    }

    // This code is contributed by AbhiThakur

    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation to find the percentage
    # change in the area when the percentage change
    # in the length and breadth is given

    # Function to calculate percentage 
    # change in area of rectangle
    def calculate_change(length, breadth):
        change = 0
        change = length + breadth+((length * breadth)//100)
        return change

    # Driver code
    if __name__ == "__main__":
        cL = 20
        cB = -10
        cA = calculate_change(cL, cB)

        print(cA)

    # This code is contributed by mohit kumar 29
    ```

    ## C#

    ```
    // C# implementation to find the percentage
    using System;
    using System.Collections.Generic;
    using System.Linq;

    class GFG 
    {

    // change in the area when the percentage change
    // in the length and breadth is given

    // Function to calculate percentage
    // change in area of rectangle
    static int calculate_change(int length, int breadth){
        int change = 0;
        change = length + breadth + ((length * breadth)/100);
        return change;
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        int cL = 20;
        int cB = -10;
        int cA = calculate_change(cL, cB);

        Console.Write(cA);
    }
    }

    // This code is contributed by shivanisinghss2110
    ```

    **Output:**

    ```
    8

    ```

    **时间复杂度:** O(1)