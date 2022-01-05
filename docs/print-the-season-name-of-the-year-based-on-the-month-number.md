# 根据月号

打印一年的季节名称

> 原文:[https://www . geesforgeks . org/print-基于月数的年度季名/](https://www.geeksforgeeks.org/print-the-season-name-of-the-year-based-on-the-month-number/)

给定月号 M，任务是根据月号打印一年的季节名称。
**例:**

```
Input: M = 5
Output: SPRING

Input: M = 1
Output: WINTER
```

**进场:**

*   一年有四个主要季节，即夏、秋、冬、春。
*   冬天的月份是在十二月，一月和二月。
*   三月、四月和五月是春天。
*   六月、七月和八月的夏季。
*   九月、十月和十一月是秋天。
*   所以把月份分别映射到特定的季节并打印出来。

以下是上述方法的实现:

## C++

```
// C++ program to print the season
// name based on the month number
#include <bits/stdc++.h>
using namespace std;

void findSeason(int M)
{

    // Checks out the season according
    // to the month number entered by the user
    switch (M)
    {
        case 12:
        case 1:
        case 2:
            cout << ("\nWINTER");
            break;
        case 3:
        case 4:
        case 5:
            cout << ("\nSPRING");
            break;
        case 6:
        case 7:
        case 8:
            cout << ("\nSUMMER");
            break;
        case 9:
        case 10:
        case 11:
            cout << ("\nAUTUMN");
            break;
        default:

            // Handles the condition if number entered
            // is not among the valid 12 months
            cout << ("\nInvalid Month number");
            break;
    }
}

// Driver code
int main()
{
    int M = 5;
    cout << "For Month number: " << M;
    findSeason(M);

    M = 10;
    cout << "\nFor Month number: " << M;
    findSeason(M);
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the season
// name based on the month number

import java.util.*;
public class Seasons {

    public static void findSeason(int M)
    {

        // Checks out the season according
        // to the month number entered by the user
        switch (M) {
        case 12:
        case 1:
        case 2:
            System.out.println("WINTER");
            break;
        case 3:
        case 4:
        case 5:
            System.out.println("SPRING");
            break;
        case 6:
        case 7:
        case 8:
            System.out.println("SUMMER");
            break;
        case 9:
        case 10:
        case 11:
            System.out.println("AUTUMN");
            break;
        default:
            // Handles the condition if number entered
            // is not among the valid 12 months
            System.out.println("Invalid Month number");
            break;
        }
    }

    // Driver Code
    public static void main(String abc[])
    {
        int M = 5;
        System.out.println("For Month number: "
                           + M);
        findSeason(M);

        M = 10;
        System.out.println("For Month number: "
                           + M);
        findSeason(M);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print the season
# name based on the month number
def findseason (M) :

    # Taken all the possible
    # month numbers in the list.
    list1 = [[12 , 1 , 2], [3 , 4 , 5],
             [6 , 7 , 8], [9 , 10 , 11]]

    # Matching the month number
    # with the above list entries
    if M in list1[0] :
        print ( "WINTER" )
    elif M in list1[1] :
        print ( "SPRING" )
    elif M in list1[2] :
        print ( "SUMMER" )
    elif M in list1[3] :
        print ( "AUTUMN" )
    else :
        print ( "Invalid Month Number" )

# Driver Code
M = 5
print("For Month number:", M);
findseason ( M )

M = 10
print("For Month number:", M);
findseason ( M )

# This code is contributed by Abhishek
```

## C#

```
// C# program to print the season
// name based on the month number
using System;

class GFG
{
public static void findSeason(int M)
{

    // Checks out the season according
    // to the month number entered by the user
    switch (M)
    {
        case 12:
        case 1:
        case 2:
            Console.WriteLine("WINTER");
            break;
        case 3:
        case 4:
        case 5:
            Console.WriteLine("SPRING");
            break;
        case 6:
        case 7:
        case 8:
            Console.WriteLine("SUMMER");
            break;
        case 9:
        case 10:
        case 11:
            Console.WriteLine("AUTUMN");
            break;
        default:
            // Handles the condition if number entered
            // is not among the valid 12 months
            Console.WriteLine("Invalid Month number");
            break;
    }
}

// Driver Code
public static void Main()
{
    int M = 5;
    Console.WriteLine("For Month number: " + M);
    findSeason(M);

    M = 10;
    Console.WriteLine("For Month number: " + M);
    findSeason(M);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // Javascript program to print the season
// name based on the month number

    function findSeason(M)
    {

        // Checks out the season according
        // to the month number entered by the user
        switch (M) {
        case 12:
        case 1:
        case 2:
            document.write("WLETER" + "<br/>");
            break;
        case 3:
        case 4:
        case 5:
            document.write("SPRING" + "<br/>");
            break;
        case 6:
        case 7:
        case 8:
            document.write("SUMMER"  + "<br/>");
            break;
        case 9:
        case 10:
        case 11:
            document.write("AUTUMN" + "<br/>");
            break;
        default:
            // Handles the condition if number entered
            // is not among the valid 12 months
            document.write("Invalid Month number");
            break;
        }
    }

    // Driver code

        let M = 5;
        document.write("For Month number: "
                           + M + "<br/>");
        findSeason(M);

        M = 10;
        document.write("For Month number: "
                           + M + "<br/>");
        findSeason(M);

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
For Month number: 5
SPRING
For Month number: 10
AUTUMN
```

**时间复杂度:** O(1)

**辅助空间:** O(1)