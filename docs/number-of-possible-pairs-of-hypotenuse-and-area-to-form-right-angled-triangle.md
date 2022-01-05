# 形成直角三角形的可能斜边对的数量和面积

> 原文:[https://www . geeksforgeeks . org/可能的直角三角形斜边和面积对数量/](https://www.geeksforgeeks.org/number-of-possible-pairs-of-hypotenuse-and-area-to-form-right-angled-triangle/)

给定两个数组 H 和 S，数组 H[]包含斜边的长度，数组 S[]包含直角三角形的面积。任务是找到所有可能的(H，S)对，这样我们就可以构造一个斜边为 H、面积为 S 的直角三角形
**例** :

```
Input : H[] = {1, 6, 4}  ;  S[] = {23, 3, 42, 14}
Output : 2 
Possible pairs are {6, 3} {4, 3}

Input : H[] = {1, 6, 4, 3}  ;  S[] = {23, 3, 42, 5}
Output : 3
Possible pairs are {6, 3} {6, 5} {4, 3}
```

说
![a     ](img/dad1f7e479eb136e5f42993179fc50ca.png "Rendered by QuickLaTeX.com") =直角三角形的底
![b     ](img/a8e8fb4fd9a17331255f4c4900f83ab4.png "Rendered by QuickLaTeX.com") =直角三角形的高
所以，

```
area S = (a*b)/2
or, 4*S*S=a*a*b*b
```

还有，

```
a2 + b2 = H2
```

因此，

```
4*S2 = a2(H2-a2)
```

在 a <sup>2</sup> 中求解这个二次方程，放入判别式>= 0(a 存在的条件)。我们会得到，

```
H<sup>2 >= 4*S</sup> 

For a right-angled triangle to exist with 
hypotenuse H and area S.
```

**天真法**:天真法是找到所有可能的(H，S)对，检查它们是否满足条件，*H<sup>2</sup>T8】= 4 * S*。计算满足此条件的对的数量，并打印计数。
下面是天真方法的实现:

## C++

```
#include <iostream>
using namespace std;

// Function to check the condition
bool check(int H, int S)
{
    // Condition for triangle to exist
    return H * H >= 4 * S;
}

// Function to find all pairs
int findPairs(int H[], int n, int S[], int m)
{
    int count = 0;

    // Checking all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (check(H[i], S[j]))
                count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int H[] = { 1, 6, 4 };
    int n = sizeof(H)/sizeof(H[0]);

    int S[] = { 23, 3, 42, 14 };
    int m = sizeof(S)/sizeof(S[0]);

    cout<<findPairs(H, n, S, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{

// Function to check the condition
static boolean check(int H, int S)
{
    // Condition for triangle to exist
    return H * H >= 4 * S;
}

// Function to find all pairs
static int findPairs(int H[], int n,
                     int S[], int m)
{
    int count = 0;

    // Checkinag all possible pairs
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (check(H[i], S[j]))
                count++;
        }
    }

    return count;
}

// Driver code
public static void main(String args[])
{
    int H[] = { 1, 6, 4 };
    int n = H.length;

    int S[] = { 23, 3, 42, 14 };
    int m = S.length;

    System.out.println(findPairs(H, n, S, m));
}
}

// This code is contributed
// by ankita_saini
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach

# Function to check the condition
def check(H, S) :

    # Condition for triangle to exist
    return H * H >= 4 * S

# Function to find all pairs
def findPairs(H, n, S, m):

    count = 0

    # Checking all possible pairs
    for i in range(n) :
        for j in range(m) :
            if check(H[i], S[j]) :
                count += 1

    return count

# Driver Code
if __name__ == "__main__" :

    H = [ 1, 6, 4]
    n = len(H)

    S = [ 23, 3, 42, 14]
    m = len(S)

    # function calling
    print(findPairs(H, n, S,m))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to check the condition
static bool check(int H, int S)
{
    // Condition for triangle to exist
    return H * H >= 4 * S;
}

// Function to find all pairs
static int findPairs(int[] H, int n,
                      int[] S, int m)
{
    int count = 0;

    // Checkinag all possible pairs
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {
            if (check(H[i], S[j]))
                count++;
        }
    }

    return count;
}

// Driver code
public static void Main()
{
    int[] H = { 1, 6, 4 };
    int n = H.Length;

    int[] S = { 23, 3, 42, 14 };
    int m = S.Length;

    Console.Write(findPairs(H, n, S, m));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check the condition
function check($H, $S)
{
    // Condition for triangle to exist
    return $H * $H >= 4 * $S;
}

// Function to find all pairs
function findPairs($H, $n, $S, $m)
{
    $count = 0;

    // Checking all possible pairs
    for ($i = 0; $i < $n; $i++)
    {
        for ($j = 0; $j < $m; $j++)
        {
            if (check($H[$i], $S[$j]))
                $count++;
        }
    }

    return $count;
}

// Driver code
$H = array( 1, 6, 4 );
$n = count($H);

$S = array( 23, 3, 42, 14 );
$m = count($S);

echo findPairs($H, $n, $S, $m);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Function to check the condition
    function check(H , S)
    {

        // Condition for triangle to exist
        return H * H >= 4 * S;
    }

    // Function to find all pairs
    function findPairs(H , n , S , m)
    {
        var count = 0;

        // Checkinag all possible pairs
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                if (check(H[i], S[j]))
                    count++;
            }
        }

        return count;
    }

    // Driver code

    var H = [ 1, 6, 4 ];
    var n = H.length;

    var S = [ 23, 3, 42, 14 ];
    var m = S.length;

    document.write(findPairs(H, n, S, m));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
2
```

**有效方法**:一种有效的方法是以递增的顺序对可用的两个数组进行排序。然后，对于斜边的每一个可能的长度，应用二分搜索法来寻找满足必要条件的最大面积。
比方说，在二分搜索法之后，最大可能区域在数组 S[]的索引 4 处可用。那么我们可以形成 4 个这样的可能对，因为所有小于索引 4 的区域也将满足条件。
以下是高效方法的实施:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check the condition
bool check(int H, int S)
{
    // Condition for triangle to exist
    return H * H >= 4 * S;
}

// Function to find all pairs
int findPairs(int H[], int n, int S[], int m)
{
    int count = 0;

    // Sort both the arrays
    sort(H, H + n);
    sort(S, S + m);

    // To keep track of last possible Area
    int index = -1;

    for (int i = 0; i < n; i++) {
        // Apply Binary Search for
        // each Hypotenuse Length
        int start = 0;
        int end = m - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (check(H[i], S[mid])) {
                index = mid;
                start = mid + 1;
            }
            else {
                end = mid - 1;
            }
        }

        // Check if we get any
        // possible Area or Not
        if (index != -1) {
            // All area less than area[index]
            // satisfy property
            count += index + 1;
        }
    }

    return count;
}

// Driver code
int main()
{
    int H[] = { 1, 6, 4 };
    int n = sizeof(H)/sizeof(H[0]);

    int S[] = { 23, 3, 42, 14 };
    int m = sizeof(S)/sizeof(S[0]);

    cout<<findPairs(H, n, S, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.util.Arrays;
import java.io.*;

class GFG {

// Function to check the condition
static boolean check(int H, int S)
{
    // Condition for triangle to exist
    return H * H >= 4 * S;
}

// Function to find all pairs
static int findPairs(int H[], int n, int S[], int m)
{
    int count = 0;

    // Sort both the arrays
    Arrays.sort(H);
    Arrays.sort(S);

    // To keep track of last possible Area
    int index = -1;

    for (int i = 0; i < n; i++) {
        // Apply Binary Search for
        // each Hypotenuse Length
        int start = 0;
        int end = m - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (check(H[i], S[mid])) {
                index = mid;
                start = mid + 1;
            }
            else {
                end = mid - 1;
            }
        }

        // Check if we get any
        // possible Area or Not
        if (index != -1) {
            // All area less than area[index]
            // satisfy property
            count += index + 1;
        }
    }

    return count;
}

// Driver code
    public static void main (String[] args) {

    int H[] = { 1, 6, 4 };
    int n = H.length;

    int S[] = { 23, 3, 42, 14 };
    int m = S.length;

    System.out.println(findPairs(H, n, S, m));
    }

// This code is contributed
// by ajit...
}
```

## 蟒蛇 3

```
# Function to check the condition
def check(H, S):

    # Condition for triangle to exist
    return H * H >= 4 * S;

# Function to find all pairs
def findPairs(H, n, S, m):
    count = 0;

    # Sort both the arrays
    H.sort();
    S.sort();

    # To keep track of last possible Area
    index = -1;

    for i in range(n):

        # Apply Binary Search for
        # each Hypotenuse Length
        start = 0;
        end = m - 1;

        while (start <= end):
            mid = int(start + (end - start) / 2);
            if (check(H[i], S[mid])):
                index = mid;
                start = mid + 1;
            else:
                end = mid - 1;

        # Check if we get any possible
        # Area or Not
        if (index != -1):

            # All area less than area[index]
            # satisfy property
            count += index + 1;

    return count;

# Driver code
H = [ 1, 6, 4 ];
n = len(H);

S= [ 23, 3, 42, 14 ];
m = len(S);

print(findPairs(H, n, S, m));

# This code is contributed by mits
```

## C#

```
/*package whatever //do not write package name here */

using System;

public class GFG{

// Function to check the condition
static bool check(int H, int S)
{
    // Condition for triangle to exist
    return H * H >= 4 * S;
}

// Function to find all pairs
static int findPairs(int []H, int n, int []S, int m)
{
    int count = 0;

    // Sort both the arrays
    Array.Sort(H);
    Array.Sort(S);

    // To keep track of last possible Area
    int index = -1;

    for (int i = 0; i < n; i++) {
        // Apply Binary Search for
        // each Hypotenuse Length
        int start = 0;
        int end = m - 1;

        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (check(H[i], S[mid])) {
                index = mid;
                start = mid + 1;
            }
            else {
                end = mid - 1;
            }
        }

        // Check if we get any
        // possible Area or Not
        if (index != -1) {
            // All area less than area[index]
            // satisfy property
            count += index + 1;
        }
    }

    return count;
}

// Driver code
    static public void Main (){
        int []H = { 1, 6, 4 };
    int n = H.Length;

    int []S = { 23, 3, 42, 14 };
    int m = S.Length;

    Console.WriteLine(findPairs(H, n, S, m));
    }

// This code is contributed
// by  akt_mit...
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to check the condition
function check($H, $S)
{
    // Condition for triangle to exist
    return $H * $H >= 4 * $S;
}

// Function to find all pairs
function findPairs($H, $n, $S, $m)
{
    $count = 0;

    // Sort both the arrays
    sort($H);
    sort($S);

    // To keep track of last possible Area
    $index = -1;

    for ($i = 0; $i < $n; $i++)
    {

        // Apply Binary Search for
        // each Hypotenuse Length
        $start = 0;
        $end = $m - 1;

        while ($start <= $end)
        {
            $mid = $start + (int)($end - $start) / 2;
            if (check($H[$i], $S[$mid]))
            {
                $index = $mid;
                $start = $mid + 1;
            }
            else
            {
                $end = $mid - 1;
            }
        }

        // Check if we get any possible
        // Area or Not
        if ($index != -1)
        {
            // All area less than area[index]
            // satisfy property
            $count += $index + 1;
        }
    }

    return $count;
}

// Driver code
$H = array( 1, 6, 4 );
$n = sizeof($H);

$S = array(23, 3, 42, 14 );
$m = sizeof($S);

echo findPairs($H, $n, $S, $m);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

    // Function to check the condition
    function check(H, S)
    {
        // Condition for triangle to exist
        return H * H >= 4 * S;
    }

    // Function to find all pairs
    function findPairs(H, n, S, m)
    {
        let count = 0;

        // Sort both the arrays
        H.sort(function(a, b){return a - b});
        S.sort(function(a, b){return a - b});

        // To keep track of last possible Area
        let index = -1;

        for (let i = 0; i < n; i++) {
            // Apply Binary Search for
            // each Hypotenuse Length
            let start = 0;
            let end = m - 1;

            while (start <= end) {
                let mid = start +
                parseInt((end - start) / 2, 10);
                if (check(H[i], S[mid])) {
                    index = mid;
                    start = mid + 1;
                }
                else {
                    end = mid - 1;
                }
            }

            // Check if we get any
            // possible Area or Not
            if (index != -1) {
                // All area less than area[index]
                // satisfy property
                count += index + 1;
            }
        }

        return count;
    }

    let H = [ 1, 6, 4 ];
    let n = H.length;

    let S = [ 23, 3, 42, 14 ];
    let m = S.length;

    document.write(findPairs(H, n, S, m));

</script>
```

**Output:** 

```
2
```