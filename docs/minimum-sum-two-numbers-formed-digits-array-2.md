# 由一个数组的数字组成的两个数的最小和

> 原文:[https://www . geesforgeks . org/minimum-sum-two-numbers-formed-digits-array-2/](https://www.geeksforgeeks.org/minimum-sum-two-numbers-formed-digits-array-2/)

给定一个数字数组(值从 0 到 9)，求由数组的数字组成的两个数字的最小可能和。给定数组的所有数字都必须用来构成这两个数字。

**示例:**

```
Input: [6, 8, 4, 5, 2, 3]
Output: 604
The minimum sum is formed by numbers 
358 and 246

Input: [5, 3, 0, 7, 4]
Output: 82
The minimum sum is formed by numbers 
35 and 047 
```

既然我们想最小化要形成的两个数的和，我们就必须把所有的数字分成两半，并给它们分配半个数字。我们还需要确保前导数字较小。

我们用给定数组的元素构建一个最小堆，这需要 O(n)个最差的时间。现在，我们通过从优先级队列中轮询来检索数组的最小值(一次 2 个)，并将这两个最小值附加到我们的数字中，直到堆变空，即数组的所有元素耗尽。我们返回两个形成的数的和，这是我们需要的答案。整体复杂性为 0(nlogn)，因为 push()操作需要 0(logn)，并且重复 n 次。

## C++

```
// C++ program to find minimum sum of two numbers
// formed from all digits in a given array.
#include<bits/stdc++.h>
using namespace std;

// Returns sum of two numbers formed
// from all digits in a[]
int minSum(int arr[], int n)
{
    // min Heap
    priority_queue <int, vector<int>, greater<int> > pq;

    // to store the 2 numbers formed by array elements to
    // minimize the required sum
    string num1, num2;

    // Adding elements in Priority Queue
    for(int i=0; i<n; i++)
        pq.push(arr[i]);

    // checking if the priority queue is non empty
    while(!pq.empty())
    {
        // appending top of the queue to the string
        num1+=(48 + pq.top());
        pq.pop();
        if(!pq.empty())
        {
            num2+=(48 + pq.top());
            pq.pop();
        }
    }

    // converting string to integer
    int a = atoi(num1.c_str());
    int b = atoi(num2.c_str());

    // returning the sum
    return a+b;
}

int main()
{
    int arr[] = {6, 8, 4, 5, 2, 3};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout<<minSum(arr, n)<<endl;
    return 0;
}
// Contributed By: Harshit Sidhwa
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum sum of two numbers
// formed from all digits in a given array.
import java.util.PriorityQueue;

class MinSum
{
    // Returns sum of two numbers formed
    // from all digits in a[]
    public static long solve(int[] a)
    {
        // min Heap
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

        // to store the 2 numbers formed by array elements to
        // minimize the required sum
        StringBuilder num1 = new StringBuilder();
        StringBuilder num2 = new StringBuilder();

        // Adding elements in Priority Queue
        for (int x : a)
            pq.add(x);

        // checking if the priority queue is non empty
        while (!pq.isEmpty())
        {
            num1.append(pq.poll()+ "");
            if (!pq.isEmpty())
                num2.append(pq.poll()+ "");
        }

        // the required sum calculated
        long sum = Long.parseLong(num1.toString()) +
                   Long.parseLong(num2.toString());

        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {6, 8, 4, 5, 2, 3};
        System.out.println("The required sum is "+ solve(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find minimum
# sum of two numbers formed from
# all digits in a given array.
from queue import PriorityQueue

# Returns sum of two numbers formed
# from all digits in a[]
def solve(a):

    # min Heap
    pq = PriorityQueue()

    # To store the 2 numbers
    # formed by array elements to
    # minimize the required sum
    num1 = ""
    num2 = ""

    # Adding elements in
    # Priority Queue
    for x in a:
        pq.put(x)

    # Checking if the priority
    # queue is non empty
    while not pq.empty():
        num1 += str(pq.get())
        if not pq.empty():
            num2 += str(pq.get())   

    # The required sum calculated
    sum = int(num1) + int(num2)

    return sum

# Driver code
if __name__=="__main__":

    arr = [ 6, 8, 4, 5, 2, 3 ]
    print("The required sum is ", solve(arr))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find minimum sum of two numbers
// formed from all digits in a given array.
using System;
using System.Collections.Generic;
class GFG
{

    // Returns sum of two numbers formed
    // from all digits in a[]
    public static long solve(int[] a)
    {

        // min Heap
        List<int> pq = new List<int>();

        // to store the 2 numbers formed by array elements to
        // minimize the required sum
        string num1 = "";
        string num2 = "";

        // Adding elements in Priority Queue
        foreach(int x in a)
            pq.Add(x);

        pq.Sort();

        // checking if the priority queue is non empty
        while (pq.Count > 0)
        {
            num1 = num1 + pq[0];
            pq.RemoveAt(0);
            if (pq.Count > 0)
            {
                num2 = num2 + pq[0];
                pq.RemoveAt(0);
            }
        }

        // the required sum calculated
        int sum = Int32.Parse(num1) + Int32.Parse(num2);

        return sum;
    }

  // Driver code
  static void Main()
  {
    int[] arr = {6, 8, 4, 5, 2, 3};
    Console.WriteLine("The required sum is "+ solve(arr));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript program to find minimum sum of two numbers
// formed from all digits in a given array.

    // Returns sum of two numbers formed
    // from all digits in a[]
    function solve(a)
    {
        // min Heap
        pq=[];
        // to store the 2 numbers formed by array elements to
        // minimize the required sum
        let num1="";
        let num2="";

        // Adding elements in Priority Queue
        for(let x=0;x<a.length;x++)
        {
            pq.push(a[x]);
        }
        pq.sort(function(a,b){return b-a;});

        // checking if the priority queue is non empty
        while(pq.length!=0)
        {
            num1+=pq.pop();
            if(pq.length!=0)
            {
                num2+=pq.pop();
            }
        }
        // the required sum calculated
        let sum=parseInt(num1)+parseInt(num2);
        return sum;
    }
    // Driver code
    let arr=[6, 8, 4, 5, 2, 3];
    document.write("The required sum is "+ solve(arr));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
The required sum is 604
```

**另一种方法:**
我们可以遵循另一种方法，也像这样，因为我们需要两个数字，这样它们的和是最小的，那么我们也需要两个最小的数字。如果我们以升序排列我们的数组，那么我们可以得到两个数字，这将形成最小的数字，
例如，2 3 4 5 6 8，现在我们可以得到从 2 和 3 开始的两个数字。第一部分现在完成了。继续前进，我们必须形成这样的形式，它们将包含小数字，即从数组中交替选择数字扩展你的两个数字。
即 246，358。如果我们看到分析这个，那么我们可以为 num1 选择偶数索引，为 num2 选择奇数索引。

下面是实现:

## C++

```
// C++ program to find minimum sum of two numbers
// formed from all digits in a given array.
#include<bits/stdc++.h>
using namespace std;

// Returns sum of two numbers formed
// from all digits in a[]
int minSum(int a[], int n){

    // sort the elements
    sort(a,a+n);

    int num1 = 0;
    int num2 = 0;
    for(int i = 0;i<n;i++){
        if(i%2==0)
            num1 = num1*10+a[i];
        else num2 = num2*10+a[i];
    }
    return num2+num1;
}

// Driver code
int main()
{
    int arr[] = {5, 3, 0, 7, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout<<"The required sum is  "<<minSum(arr, n)<<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
//Java program to find minimum sum of two numbers
//formed from all digits in a given array.
public class AQRQ {

    //Returns sum of two numbers formed
    //from all digits in a[]
    static int minSum(int a[], int n){

     // sort the elements
     Arrays.sort(a);

     int num1 = 0;
     int num2 = 0;
     for(int i = 0;i<n;i++){
         if(i%2==0)
             num1 = num1*10+a[i];
         else num2 = num2*10+a[i];
     }
     return num2+num1;
    }

    //Driver code
    public static void main(String[] args) {

         int arr[] = {5, 3, 0, 7, 4};
         int n = arr.length;
         System.out.println("The required sum is  " + minSum(arr, n));

    }

}
```

## 蟒蛇 3

```
# Python 3 program to find minimum
# sum of two numbers formed
# from all digits in an given array

# Returns sum of two numbers formed
# from all digits in a[]
def minSum(a, n):

    # sorted the elements
    a = sorted(a)
    num1, num2 = 0, 0

    for i in range(n):
        if i % 2 == 0:
            num1 = num1 * 10 + a[i]
        else:
            num2 = num2 * 10 + a[i]

    return num2 + num1    

# Driver code
arr = [5, 3, 0, 7, 4]
n = len(arr)
print("The required sum is",
             minSum(arr, n))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# a program to find minimum sum of two numbers
//formed from all digits in a given array.

using System;

public class GFG{

    //Returns sum of two numbers formed
    //from all digits in a[]
    static int minSum(int []a, int n){

    // sort the elements
    Array.Sort(a);

    int num1 = 0;
    int num2 = 0;
    for(int i = 0;i<n;i++){
        if(i%2==0)
            num1 = num1*10+a[i];
        else num2 = num2*10+a[i];
    }
    return num2+num1;
    }

    //Driver code
    static public void Main (){
        int []arr = {5, 3, 0, 7, 4};
        int n = arr.Length;
        Console.WriteLine("The required sum is " + minSum(arr, n));
    }
//This code is contributed by ajit.   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum sum
// of two numbers formed from all
// digits in a given array.

// Returns sum of two numbers formed
// from all digits in a[]
function minSum($a, $n)
{

    // sort the elements
    sort($a);

    $num1 = 0;
    $num2 = 0;
    for($i = 0; $i < $n; $i++)
    {
        if($i % 2 == 0)
            $num1 = $num1 * 10 + $a[$i];
        else $num2 = $num2 * 10 + $a[$i];
    }
    return ($num2 + $num1);
}

// Driver code
$arr = array(5, 3, 0, 7, 4);
$n = sizeof($arr);
echo "The required sum is ",
     minSum($arr, $n), "\n";

// This Code is Contributed by ajit
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find minimum sum of two numbers
    // formed from all digits in a given array.

    // Returns sum of two numbers formed
    // from all digits in a[]
    function minSum(a, n){

        // sort the elements
        a.sort();

        let num1 = 0;
        let num2 = 0;
        for(let i = 0;i<n;i++){
            if(i%2==0)
                num1 = num1*10+a[i];
            else num2 = num2*10+a[i];
        }
        return num2+num1;
    }

    let arr = [5, 3, 0, 7, 4];
    let n = arr.length;
    document.write("The required sum is  " + minSum(arr, n));

</script>
```

**输出:**

```
The required sum is 82
```

**时间复杂度:** O(nLogN)

本文由**普拉哈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。