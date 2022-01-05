# 打印数组中的中间值

> 原文:[https://www . geesforgeks . org/print-intermediate-values-current-index-element-sequence-next-index-elements-array/](https://www.geeksforgeeks.org/print-intermediate-values-current-index-element-successive-next-index-elements-array/)

给定一个整数数组，打印当前索引元素和数组的后续下一个索引元素之间的中间值。
示例:

```
Input : arr[] = { 4, 2, 7, 5};
Output :
Intermediate elements between 4 and 2
2 3 4
Intermediate elements between 2 and 7
2 3 4 5 6 7
Intermediate elements between 7 and 5
5 6 7
```

## C++

```
// C++ program to print the
// intermediate  value
#include <iostream>
using namespace std;

void inter(int arr[], int n)
    {
        for (int l = 0; l < n - 1; l++)
        {
            // points to first index element
            int i = arr[l];

            // points to preceding index element
            int j = arr[l + 1];

            // Find big element
            // between the above elements
            int big = i > j ? i : j;

            // Find small element
            // between the above elements
            int sml = i < j ? i : j;

            cout<<"Intermediate elements between "<<
                                 i <<" and "<<j<<endl;

            for (int k = sml; k <= big; k++)        
                cout<<k<<" ";

            cout<<endl;
        }
    }

// Driver code
int main() {

    int arr[] = { 4, 2, 7, 5 };

    int n=sizeof(arr)/sizeof(arr[0]);

    inter(arr,n);

    return 0;
}

// this code is contributed by 'vt_m'
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// intermediate  values

public class GFG
{
    static void inter(int[] arr)
    {
        for (int l = 0; l < arr.length - 1; l++)
        {
            // points to first index element
            int i = arr[l];

            //  points to preceding index element
            int j = arr[l + 1];

            // Find big element
            // between the above elements
            int big = i > j ? i : j;

            // Find  small element
            // between the above elements
            int sml = i < j ? i : j;

            System.out.println("Intermediate elements between "
                                + i + " and " + j);
            for (int k = sml; k <= big; k++)            
                System.out.print(k + " ");

            System.out.println();
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 4, 2, 7, 5 };
        inter(arr);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to print the
# intermediate  value

def inter(arr, n) :
    for l in range( 0, n - 1) :

        # points to first index element
        i = arr[l]

        # points to preceding index element
        j = arr[l + 1]

        # Find big element
        # between the above elements
        if(i>j) :
            big = i
        else :
            big = j

        # Find small element
        # between the above elements
        if(i<j) :
            sml =  i
        else :
            sml = j

        print("Intermediate elements between "
             ,i ," and ",j)

        for k in range( sml, big+1) :
            print(k,end = " ")
        print()

# Driver code
arr = [ 4, 2, 7, 5 ]

n= len(arr)

inter(arr,n)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to print the
// intermediate values
using System;

public class GFG
{
    static void inter(int[] arr)
    {
        for (int l = 0; l < arr.Length - 1; l++)
        {
            // points to first index element
            int i = arr[l];

            // points to preceding index element
            int j = arr[l + 1];

            // Find big element
            // between the above elements
            int big = i > j ? i : j;

            // Find small element
            // between the above elements
            int sml = i < j ? i : j;

            Console.WriteLine("Intermediate elements between "
                                + i + " and " + j);
            for (int k = sml; k <= big; k++)        
                Console.Write(k + " ");

            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 4, 2, 7, 5 };
        inter(arr);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the
// intermediate  value

function inter ($arr, $n)
    {
        for ($l = 0; $l < $n - 1; $l++)
        {

            // points to first index element
            $i = $arr[$l];

            // points to preceding index element
            $j = $arr[$l + 1];

            // Find big element
            // between the above elements
            $big = $i > $j ? $i : $j;

            // Find small element
            // between the above elements
            $sml = $i < $j ? $i : $j;

            echo "interermediate elements between ",
                                $i ," and ",$j,"\n";

            for ($k = $sml; $k <= $big; $k++)        
                echo $k," ";

            echo "\n";
        }
    }

    // Driver Code
    $arr = array(4, 2, 7, 5);
    $n=count($arr);
    inter($arr,$n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to print the
// intermediate value

function inter( arr, n)
    {
        for (let l = 0; l < n - 1; l++)
        {
            // points to first index element
            let i = arr[l];

            // points to preceding index element
            let j = arr[l + 1];

            // Find big element
            // between the above elements
            let big = i > j ? i : j;

            // Find small element
            // between the above elements
            let sml = i < j ? i : j;

    document.write("Intermediate elements between " +
                             i + " and "+ j + "</br>");

            for (let k = sml; k <= big; k++)       
                document.write(k + " ");

            document.write("</br>");
        }
    }

    // Driver Code

    let arr = [ 4, 2, 7, 5 ];

    let n= arr.length;

    inter(arr,n);

</script>
```

**输出:**

```
Intermediate elements between 4 and 2
2 3 4
Intermediate elements between 2 and 7
2 3 4 5 6 7 
Intermediate elements between 7 and 5
5 6 7
```