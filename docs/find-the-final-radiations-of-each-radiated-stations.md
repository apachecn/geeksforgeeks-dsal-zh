# 找出每个辐射站的最终辐射

> 原文:[https://www . geeksforgeeks . org/find-每个辐射站的最终辐射量/](https://www.geeksforgeeks.org/find-the-final-radiations-of-each-radiated-stations/)

直线上有 **N 个**站，每个站都有一些非负辐射功率。每个站可以通过以下方式增加其相邻站的辐射功率:
站 **i** 用辐射功率 **R** 将增加**(I–1)**站的辐射**R–1**、**(I–2)**站的辐射**R–2**， 以此类推……直到有效辐射功率为正时为止,**(I+1)**站受**R–1**、**(I+2)**站受**R–2**站辐射。
任务是找到每个站的最终辐射。
**举例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 3 4 4
> 新辐射将为{ 1+(2–1)+(3–2)+(1–1)+(3–1)，3+(2–1)}
> 即{3，4，4}
> **输入:** arr[] = {9，87，55，2，1}
> **输出:【T0**

**天真方法:**对于每个站， **i** 如上所述增加相邻站的辐射，直到有效辐射变为负值。
**时间复杂度:** O(n*n)
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the final radiations
void print(int rStation[], int n)
{
    for (int i = 1; i <= n; i++)
        cout << rStation[i] << " ";
    cout << endl;
}

// Function to create the array of the
// resultant radiations
void radiated_Station(int station[], int n)
{

    // Resultant radiations
    int rStation[n + 1];

    // Initialize resultant array with 0
    memset(rStation, 0, sizeof(rStation));

    for (int i = 1; i <= n; i++) {

        // Declaring index counter for left
        // and right radiation
        int li = i - 1, ri = i + 1;

        // Effective radiation for left
        // and right case
        int lRad = station[i] - 1, rRad = station[i] - 1;

        // Radiation for i-th station
        rStation[i] += station[i];

        // Radiation increment for left stations
        while (li >= 1 && lRad >= 1) {
            rStation[li--] += lRad--;
        }

        // Radiation increment for right stations
        while (ri <= n && rRad >= 1) {
            rStation[ri++] += rRad--;
        }
    }

    // Print the resultant radiation
    // for each of the stations
    print(rStation, n);
}

// Driver code
int main()
{

    // 1-based indexing
    int station[] = { 0, 7, 9, 12, 2, 5 };
    int n = (sizeof(station) / sizeof(station[0])) - 1;

    radiated_Station(station, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to print the final radiations
    static void print(int rStation[], int n)
    {
        for (int i = 1; i <= n; i++)
            System.out.print(rStation[i] + " ");
        System.out.println("");
    }

    // Function to create the array of the
    // resultant radiations
    static void radiated_Station(int station[], int n)
    {

        // Resultant radiations
        int rStation[] = new int[n + 1];

        for (int i = 1; i <= n; i++) {

            // Declaring index counter for left
            // and right radiation
            int li = i - 1, ri = i + 1;

            // Effective radiation for left
            // and right case
            int lRad = station[i] - 1, rRad = station[i] - 1;

            // Radiation for i-th station
            rStation[i] += station[i];

            // Radiation increment for left stations
            while (li >= 1 && lRad >= 1) {
                rStation[li--] += lRad--;
            }

            // Radiation increment for right stations
            while (ri <= n && rRad >= 1) {
                rStation[ri++] += rRad--;
            }
        }

        // Print the resultant radiation
        // for each of the stations
        print(rStation, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        // 1-based indexing
        int station[] = { 0, 7, 9, 12, 2, 5 };
        int n = station.length - 1;

        radiated_Station(station, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print the final radiations
def printf(rStation, n):
    for i in range(1, n + 1, 1):
        print(rStation[i], end = " ")
    print("\n", end = " ")

# Function to create the array of the
# resultant radiations
def radiated_Station(station, n):

    # Resultant radiations
    rStation = [0 for i in range(n + 1)]

    for i in range(1, n + 1):
        # Declaring index counter for left
        # and right radiation
        li = i - 1
        ri = i + 1

        # Effective radiation for left
        # and right case
        lRad = station[i] - 1
        rRad = station[i] - 1

        # Radiation for i-th station
        rStation[i] += station[i]

        # Radiation increment for left stations
        while (li >= 1 and lRad >= 1):
            rStation[li] += lRad
            lRad -= 1
            li -= 1

        # Radiation increment for right stations
        while (ri <= n and rRad >= 1):
            rStation[ri] += rRad
            rRad -= 1
            ri += 1

    # Print the resultant radiation
    # for each of the stations
    printf(rStation, n)

# Driver code
if __name__ == '__main__':
    # 1-based indexing
    station = [0, 7, 9, 12, 2, 5]
    n = len(station) - 1

    radiated_Station(station, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to print the final radiations
    static void print(int[] rStation, int n)
    {
        for (int i = 1; i <= n; i++)
            Console.Write(rStation[i] + " ");
        Console.WriteLine("");
    }

    // Function to create the array of the
    // resultant radiations
    static void radiated_Station(int[] station, int n)
    {

        // Resultant radiations
        int[] rStation = new int[n + 1];

        for (int i = 1; i <= n; i++) {

            // Declaring index counter for left
            // and right radiation
            int li = i - 1, ri = i + 1;

            // Effective radiation for left
            // and right case
            int lRad = station[i] - 1, rRad = station[i] - 1;

            // Radiation for i-th station
            rStation[i] += station[i];

            // Radiation increment for left stations
            while (li >= 1 && lRad >= 1) {
                rStation[li--] += lRad--;
            }

            // Radiation increment for right stations
            while (ri <= n && rRad >= 1) {
                rStation[ri++] += rRad--;
            }
        }

        // Print the resultant radiation
        // for each of the stations
        print(rStation, n);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // 1-based indexing
        int[] station = { 0, 7, 9, 12, 2, 5 };
        int n = station.Length - 1;

        radiated_Station(station, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the final radiations

function print_radiation($rStation, $n)
{
    for ($i = 1; $i <= $n; $i++)
    {
        echo $rStation[$i]." ";
    }
    echo "\n";
}

// Function to create the array of the
// resultant radiations
function radiated_Station($station, $n)
{

    // Resultant radiations
    $rStation  = array();

    // Initialize resultant array with 0
    $rStation = array_fill(0, $n+1, 0);

    for ($i = 1; $i <= $n; $i++) {

        // Declaring index counter for left
        // and right radiation
        $li = $i - 1;
        $ri = $i + 1;

        // Effective radiation for left
        // and right case
        $lRad = $station[$i] - 1;
        $rRad = $station[$i] - 1;

        // Radiation for i-th station
        $rStation[$i] += $station[$i];

        // Radiation increment for left stations
        while ($li >= 1 && $lRad >= 1) {
            $rStation[$li--] += $lRad--;
        }

        // Radiation increment for right stations
        while ($ri <= $n && $rRad >= 1) {
            $rStation[$ri++] += $rRad--;
        }
    }

    // Print the resultant radiation
    // for each of the stations
    print_radiation($rStation, $n);
}

// Driver code

// 1-based indexing
$station = array( 0, 7, 9, 12, 2, 5 );
$n = (sizeof($station) / sizeof($station[0])) - 1;

radiated_Station($station, $n);

//code contributed by Shashank_Sharma
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach

    // Function to print the final radiations
    function print( rStation,  n)
    {
        for (var i = 1; i <= n; i++)
            document.write(rStation[i] + " ");
        document.write("<br>");
    }

    // Function to create the array of the
    // resultant radiations
    function radiated_Station(station,  n)
    {
        // Resultant radiations
         var rStation = [] ;
         rStation.length = 6 ;
         rStation.fill(0)

        for (var i = 1; i <= n; i++) {

            // Declaring index counter for left
            // and right radiation
            var li = i - 1, ri = i + 1;

            // Effective radiation for left
            // and right case
            var lRad = station[i] - 1, rRad = station[i] - 1;

            // Radiation for i-th station
            rStation[i] += station[i];

            // Radiation increment for left stations
            while (li >= 1 && lRad >= 1) {
                rStation[li--] += lRad--;
            }

            // Radiation increment for right stations
            while (ri <= n && rRad >= 1) {
                rStation[ri++] += rRad--;
            }
        }

        // Print the resultant radiation
        // for each of the stations
        print(rStation, n);
    }

    // Driver code

        // 1-based indexing
        var station = [ 0, 7, 9, 12, 2, 5 ]
        var n = station.length - 1;

        radiated_Station(station, n);

        // This code is contributed by bunnyram19.

</script>
```

**Output:** 

```
26 28 29 28 25
```