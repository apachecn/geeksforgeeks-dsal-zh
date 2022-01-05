# 求非自相交闭合多边形的质心

> 原文:[https://www . geeksforgeeks . org/find-非自相交闭合多边形的质心/](https://www.geeksforgeeks.org/find-the-centroid-of-a-non-self-intersecting-closed-polygon/)

给定多边形的 N 个顶点，任务是找到多边形的质心
**示例:**

```
Input: ar = {{0, 0}, {0, 8}, {8, 8}, {8, 0}}
Output: {Cx, Cy} = {4, 4}

Input: ar = {{1, 2}, {3, -4}, {6, -7}}
Output: {Cx, Cy} = {3.33, -3}
```

**逼近:**
由 n 个顶点(x0，y0)、(x1，y1)、…、(xn-1，yn-1)定义的非自相交闭合多边形的质心是点(Cx，Cy)，其中:

> ![C_{x}= \frac{1}{6A} \sum_{i=0}^{n-1}(x_{i}+x_{i+1})(x_{i}* y_{i+1}-x_{i+1}*y_{i})](img/c846e6fbbadd94dad7639c0c92ac609e.png "Rendered by QuickLaTeX.com")
> ![C_{y}= \frac{1}{6A} \sum_{i=0}^{n-1}(y_{i}+y_{i+1})(x_{i}* y_{i+1}-x_{i+1}*y_{i})](img/c0debe2c420bc39c03c092fe52c183c7.png "Rendered by QuickLaTeX.com")
> ![A = \frac{1}{2} \sum_{i=0}^{n-1}(x_{i}*y_{i+1}-x_{i+1}*y_{i})](img/a1a94122b9959b822bcd97561232df93.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program to implement the 
// above approach

#include <bits/stdc++.h>
using namespace std;

pair<double, double> find_Centroid(vector<pair<double, double> >& v)
{
    pair<double, double> ans = { 0, 0 };

    int n = v.size();
    double signedArea = 0;

    // For all vertices
    for (int i = 0; i < v.size(); i++) {

        double x0 = v[i].first, y0 = v[i].second;
        double x1 = v[(i + 1) % n].first, y1 = 
                            v[(i + 1) % n].second;

        // Calculate value of A
        // using shoelace formula
        double A = (x0 * y1) - (x1 * y0);
        signedArea += A;

        // Calculating coordinates of
        // centroid of polygon
        ans.first += (x0 + x1) * A;
        ans.second += (y0 + y1) * A;
    }

    signedArea *= 0.5;
    ans.first = (ans.first) / (6 * signedArea);
    ans.second = (ans.second) / (6 * signedArea);

    return ans;
}

// Driver code
int main()
{
    // Coordinate of the vertices
    vector<pair<double, double> > vp = { { 1, 2 }, 
                                         { 3, -4 }, 
                                         { 6, -7 } };

    pair<double, double> ans = find_Centroid(vp);

    cout << setprecision(12) << ans.first << " " 
        << ans.second << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach 
class GFG 
{

    static double[] find_Centroid(double v[][]) 
    { 
        double []ans = new double[2]; 

        int n = v.length; 
        double signedArea = 0; 

        // For all vertices 
        for (int i = 0; i < n; i++)
        { 

            double x0 = v[i][0], y0 = v[i][1]; 
            double x1 = v[(i + 1) % n][0], y1 = v[(i + 1) % n][1]; 

            // Calculate value of A 
            // using shoelace formula 
            double A = (x0 * y1) - (x1 * y0); 
            signedArea += A; 

            // Calculating coordinates of 
            // centroid of polygon 
            ans[0] += (x0 + x1) * A; 
            ans[1] += (y0 + y1) * A; 
        } 

        signedArea *= 0.5; 
        ans[0] = (ans[0]) / (6 * signedArea); 
        ans[1]= (ans[1]) / (6 * signedArea); 

        return ans; 
    } 

    // Driver code 
    public static void main (String[] args)
    { 
        // Coordinate of the vertices 
        double vp[][] = { { 1, 2 }, 
                            { 3, -4 }, 
                            { 6, -7 } }; 

        double []ans = find_Centroid(vp); 

        System.out.println(ans[0] + " " + ans[1]); 
    } 
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach
def find_Centroid(v):
    ans = [0, 0]

    n = len(v)
    signedArea = 0

    # For all vertices
    for i in range(len(v)):

        x0 = v[i][0]
        y0 = v[i][1]
        x1 = v[(i + 1) % n][0]
        y1 =v[(i + 1) % n][1]

        # Calculate value of A
        # using shoelace formula
        A = (x0 * y1) - (x1 * y0)
        signedArea += A

        # Calculating coordinates of
        # centroid of polygon
        ans[0] += (x0 + x1) * A
        ans[1] += (y0 + y1) * A

    signedArea *= 0.5
    ans[0] = (ans[0]) / (6 * signedArea)
    ans[1] = (ans[1]) / (6 * signedArea)

    return ans

# Driver code

# Coordinate of the vertices
vp = [ [ 1, 2 ],
       [ 3, -4 ],
       [ 6, -7 ] ]

ans = find_Centroid(vp)

print(round(ans[0], 12), ans[1])

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach 
using System;

class GFG 
{
    static double[] find_Centroid(double [,]v) 
    { 
        double []ans = new double[2]; 

        int n = v.GetLength(0); 
        double signedArea = 0; 

        // For all vertices 
        for (int i = 0; i < n; i++)
        { 
            double x0 = v[i, 0], y0 = v[i, 1]; 
            double x1 = v[(i + 1) % n, 0], 
                    y1 = v[(i + 1) % n, 1]; 

            // Calculate value of A 
            // using shoelace formula 
            double A = (x0 * y1) - (x1 * y0); 
            signedArea += A; 

            // Calculating coordinates of 
            // centroid of polygon 
            ans[0] += (x0 + x1) * A; 
            ans[1] += (y0 + y1) * A; 
        } 
        signedArea *= 0.5; 
        ans[0] = (ans[0]) / (6 * signedArea); 
        ans[1]= (ans[1]) / (6 * signedArea); 

        return ans; 
    } 

    // Driver code 
    public static void Main (String[] args)
    { 
        // Coordinate of the vertices 
        double [,]vp = { { 1, 2 }, 
                         { 3, -4 }, 
                         { 6, -7 } }; 

        double []ans = find_Centroid(vp); 

        Console.WriteLine(ans[0] + " " + ans[1]); 
    } 
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach 

    function find_Centroid(v) 
    { 
        let ans = new Array(2); 
        ans.fill(0);

        let n = v.length; 
        let signedArea = 0; 

        // For all vertices 
        for (let i = 0; i < n; i++)
        { 

            let x0 = v[i][0], y0 = v[i][1]; 
            let x1 = v[(i + 1) % n][0], y1 = v[(i + 1) % n][1]; 

            // Calculate value of A 
            // using shoelace formula 
            let A = (x0 * y1) - (x1 * y0); 
            signedArea += A; 

            // Calculating coordinates of 
            // centroid of polygon 
            ans[0] += (x0 + x1) * A; 
            ans[1] += (y0 + y1) * A; 
        } 

        signedArea *= 0.5; 
        ans[0] = (ans[0]) / (6 * signedArea); 
        ans[1]= (ans[1]) / (6 * signedArea); 

        return ans; 
    }

    // Coordinate of the vertices 
    let vp = [ [ 1, 2 ], 
                [ 3, -4 ], 
                [ 6, -7 ] ]; 

    let ans = find_Centroid(vp); 

    document.write(ans[0].toFixed(11) + " " + ans[1]); 

 // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3.33333333333 -3
```