# 数组的 GCD 大于 1

> 原文:[https://www.geeksforgeeks.org/gcd-array-greater-one/](https://www.geeksforgeeks.org/gcd-array-greater-one/)

给定 n 个整数的数组。如果数组所有元素的 GCD 大于 1，则认为该数组是最佳的。如果数组不是最好的，我们可以通过 a<sub>I</sub>–a<sub>I+1</sub>和 a <sub>i</sub> + a <sub>i + 1</sub> 分别选择一个索引 i (1 <= i < n) and replace numbers a <sub>i</sub> 和一个 <sub>i + 1</sub> 。找到要在阵列上完成的最小操作数，使其达到最佳状态。
示例:

```
Input : n = 2
        a[] = [1, 1]
Output : 1
Explanation:
Here, gcd(1,1) = 1\. So, to make 
it best we have to replace array 
by [(1-1), (1+1)] = [0, 2]. Now, 
gcd(0, 2) > 1\. Hence, in one
operation array become best.

Input : n = 3
        a[] = [6, 2, 4]
Output :0
Explanation:
Here, gcd(6,2,4) > 1.
Hence, no operation is required. 
```

我们首先计算 gcd(数组)并检查它是否大于 1。如果是，那么这个数组已经是最好的了，否则我们贪婪地检查需要多少次移动来完成所有的移动，方法是当有两个奇数时，你可以在一次移动中使它们变成偶数，否则如果有一个奇数和一个偶数，那么你需要两次移动。
以下是上述方法的实现:

## C++

```
// CPP program to find bestArray
#include<bits/stdc++.h>
using namespace std;

// Calculating gcd of two numbers
int gcd(int a, int b){
        if (a == 0)
            return b;
        return gcd(b%a, a);
}

void bestArray(int arr[], int n){
        bool even[n] = {false};
        int ans = 0;

        // calculating gcd and
        // counting the even numbers
        for(int i = 0; i < n; i++){
            ans = gcd(ans, arr[i]);
            if(arr[i] % 2 == 0)
                even[i] = true;
        }

        // check array is already best
        if(ans > 1)
            cout << 0 << endl;
        else{

            // counting the number
            // of operations required.
            ans = 0;
            for(int i = 0; i < n-1; i++){
                if(!even[i]){
                    even[i] = true;
                    even[i+1] = true;
                    if(arr[i+1]%2 != 0){
                        ans+=1;
                    }
                    else
                        ans+=2;
                }
            }
            if(!even[n-1]){
                ans+=2;
            }
            cout << ans << endl;
        }
}

// driver code
int main(){

        int arr[] = {57, 30, 28, 81, 88, 32, 3, 42, 25};
        int n = 9;
        bestArray(arr, n);

        int arr1[] = {1, 1};
        n = 2;
        bestArray(arr1, n);

        int arr2[] = {6, 2, 4};
        n = 3;
        bestArray(arr2, n);
}

/*This code is contributed by Sagar Shukla.*/
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find best array
import java.util.*;
import java.lang.*;

public class GeeksforGeeks{

    // function to calculate gcd of two numbers.
    public static int gcd(int a, int b){
        if (a == 0)
            return b;
        return gcd(b%a, a);
    }

    public static void bestArray(int arr[], int n){
        boolean even[] = new boolean[n];
        int ans = 0;
        for(int i=0; i<n; i++)
            even[i] = false;

        // calculating gcd and
        // counting the even numbers
        for(int i=0; i<n; i++){
            ans = gcd(ans, arr[i]);
            if(arr[i]%2 == 0)
                even[i] = true;
        }

        // check array is already best
        if(ans > 1)
            System.out.println(0);
        else{

            // counting the number of operations required.
            ans = 0;
            for(int i=0; i<n-1; i++){
                if(!even[i]){
                    even[i] = true;
                    even[i+1] = true;
                    if(arr[i+1]%2 != 0){
                        ans+=1;
                    }
                    else
                        ans+=2;
                }
            }
            if(!even[n-1]){
                ans+=2;
            }
            System.out.println(ans);
        }
    }

    // driver code
    public static void main(String argc[]){

        int arr[] = {57, 30, 28, 81, 88, 32, 3, 42, 25};
        int n = 9;
        bestArray(arr, n);

        int arr1[] = {1, 1};
        n = 2;
        bestArray(arr1, n);

        int arr2[] = {6, 2, 4};
        n = 3;
        bestArray(arr2, n);
    }
}

/*This code is contributed by Sagar Shukla.*/
```

## 计算机编程语言

```
# code to find the best array
from fractions import gcd

def bestArray(a,n):

    even = [False]*n
    ans = 0

    # calculating the gcd and
    # counting the even numbers
    for i in xrange(n):
        ans = gcd(ans, a[i])
        if a[i]%2 == 0:
            even[i] = True

    # check if array is already best.
    if ans > 1:
        print (0)
    else:      

        # calculating the no of
        # operations required.
        ans = 0
        for i in xrange(n-1):
            if not even[i]:
                even[i] = True
                even[i+1] = True
                if a[i+1]%2 != 0:
                    ans += 1
                else:
                    ans += 2
        if not even[n-1]:
            ans += 2
        print (ans)

# driver code
n = 9
a = [57, 30, 28, 81, 88, 32, 3, 42, 25]
bestArray(a,n)
n = 2
a = [1, 1]
bestArray(a,n)
n = 3
a = [6, 2, 4]
bestArray(a,n)
```

## C#

```
// C# code to find best array
using System;

public class GFG {

    // function to calculate gcd
    // of two numbers.
    public static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    public static void bestArray(int []arr, int n)
    {
        bool []even = new bool[n];
        int ans = 0;

        for(int i = 0; i < n; i++)
            even[i] = false;

        // calculating gcd and
        // counting the even numbers
        for(int i = 0; i < n; i++)
        {
            ans = gcd(ans, arr[i]);

            if(arr[i] % 2 == 0)
                even[i] = true;
        }

        // check array is already best
        if(ans > 1)
            Console.WriteLine(0);
        else
        {

            // counting the number of
            // operations required.
            ans = 0;
            for(int i = 0; i < n-1; i++)
            {
                if(!even[i])
                {
                    even[i] = true;
                    even[i+1] = true;
                    if(arr[i+1] % 2 != 0)
                        ans += 1;
                    else
                        ans += 2;
                }
            }
            if(!even[n-1])
                ans += 2;

            Console.WriteLine(ans);
        }
    }

    // driver code
    public static void Main()
    {

        int []arr = {57, 30, 28, 81, 88,
                            32, 3, 42, 25};
        int n = 9;
        bestArray(arr, n);

        int []arr1 = {1, 1};
        n = 2;
        bestArray(arr1, n);

        int []arr2 = {6, 2, 4};
        n = 3;
        bestArray(arr2, n);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript code to find best array

    // function to calculate gcd
    // of two numbers.
    function gcd( a,  b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    function bestArray(arr,  n)
    {
        var even = new Array(n);
        var ans = 0;

        for(var i = 0; i < n; i++)
            even[i] = false;

        // calculating gcd and
        // counting the even numbers
        for(var i = 0; i < n; i++)
        {
            ans = gcd(ans, arr[i]);

            if(arr[i] % 2 == 0)
                even[i] = true;
        }

        // check array is already best
        if(ans > 1)
            document.write(0);
        else
        {

            // counting the number of
            // operations required.
            ans = 0;
            for(var i = 0; i < n-1; i++)
            {
                if(!even[i])
                {
                    even[i] = true;
                    even[i+1] = true;
                    if(arr[i+1] % 2 != 0)
                        ans += 1;
                    else
                        ans += 2;
                }
            }
            if(!even[n-1])
                ans += 2;

            document.write(ans + "<br>");
        }
    }

    // driver code

         var arr = [57, 30, 28, 81, 88,
                            32, 3, 42, 25];
        var n = 9;
        bestArray(arr, n);

        var arr1 = [1, 1];
        n = 2;
        bestArray(arr1, n);

        var arr2 = [6, 2, 4];
        n = 3;
        bestArray(arr2, n);

</script>
```

**输出:**

```
8
1
0
```