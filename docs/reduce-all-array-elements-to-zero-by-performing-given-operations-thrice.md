# 通过执行三次给定操作将所有数组元素减少到零

> 原文:[https://www . geesforgeks . org/通过三次执行给定操作将所有数组元素减少到零/](https://www.geeksforgeeks.org/reduce-all-array-elements-to-zero-by-performing-given-operations-thrice/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过应用以下操作恰好三次将每个数组元素转换为 **0** :

*   选择一个[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。
*   将子阵列的每个元素增加其长度的整数倍。

最后，打印所涉及的子阵列的第一个和最后一个索引，以及在每个步骤中添加到子阵列的每个索引中的元素。

**示例:**

> **输入:**arr【】**= { 1，3，2，4}
> **输出:**
> 操作 1: 1 1
> 添加元素:1
> 操作 2: 3 4
> 添加元素:4 2
> 操作 3: 2 4
> 添加元素:-3 -6 -6
> **解释:**
> 步骤 1:选择子阵列{arr[1]}并将-1 添加到中唯一的元素因此，数组 arr[]修改为{0，3，2，4}。
> 步骤 2:选择子阵列{arr[3]，arr[4]}并分别向子阵列元素添加{4，2}。因此，数组 arr[]修改为{0，3，6，6}。
> 步骤 3:选择子阵列{arr[2]、arr[4]}并分别向子阵列元素添加{-3、-6、-6}。因此，数组 arr[]修改为{0，0，0，0}**
> 
>  ****输入:** arr[] = { 5 }
> **输出:**
> 操作 1 : 1 1
> 添加元素:-5
> 操作 2 : 1 1
> 添加元素:5
> 操作 3 : 1 1
> 添加元素:-5**

****方法:** 给定的问题可以基于以下观察来解决:**

> ****操作 1:** 选择子阵列{arr[1]，..，arr[N]}。设置 A[I]= A[I]–N * A[I]=(N–1)*(-A[I])。
> 操作 1 后，每个元素都是(N–1)的倍数。
> **操作 2:** 选择子阵列{arr[1]，..arr[N-1]}。将子阵列的所有值加/减(N–1)的倍数，直到它们减少到 0。
> **操作 3:** 选择尺寸为 1 的子阵列{arr[N]}。加/减 1 的倍数使 A[N] = 0。**

**按照以下步骤解决问题:**

*   **如果 **N** 等于 **1** ，则分三步分别打印 **-arr[0]、+arr[0]、-arr[0]** 。**
*   **否则，执行以下操作:

    *   打印 **1 N** 。从数组的每个元素中减去**N * arr【I】**打印减去的元素。
    *   打印**1N–1**。S 子矩阵T5(N–1)*从子矩阵和的每个元素中获取【I】并打印减去的值。
    *   最后打印 **N** 。subtractT5】arr【I–1】来自元素。打印**arr[I–1]**。** 

**以下是上述方法的实现:**

## **C++**

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to reduce all
// array elements to zero
void ConvertArray(int arr[], int N)
{
    // If size of array is 1
    if (N == 1) {

        // First operation
        cout << "Operation 1 : " << 1
             << " " << 1 << endl;
        cout << "Added elements: "
             << -1 * arr[0] << endl;
        cout << endl;

        // 2nd Operation
        cout << "Operation 2 : "
             << 1 << " " << 1 << endl;
        cout << "Added elements: "
             << 1 * arr[0] << endl;
        cout << endl;

        // 3rd Operation
        cout << "Operation 3 : "
             << 1 << " " << 1 << endl;
        cout << "Added elements: "
             << -1 * arr[0] << endl;
    }

    // Otherwise
    else {

        // 1st Operation
        cout << "Operation 1 : "
             << 1 << " " << N << endl;
        cout << "Added elements: ";
        for (int i = 0; i < N; i++) {
            cout << -1 * arr[i] * N << " ";
        }
        cout << endl;
        cout << endl;

        // 2nd Operation
        cout << "Operation 2 : "
             << 1 << " " << N - 1 << endl;
        cout << "Added elements: ";
        for (int i = 0; i < N - 1; i++) {
            cout << arr[i] * (N - 1) << " ";
        }
        cout << endl;
        cout << endl;

        // 3rd Operation
        cout << "Operation 3 : " << N
             << " " << N << endl;
        cout << "Added elements: ";
        cout << arr[N - 1] * (N - 1) << endl;
    }
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 3, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to make all
    // array elements equal to 0
    ConvertArray(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

  // Function to reduce all
  // array elements to zero
  static void ConvertArray(int arr[], int N)
  {

    // If size of array is 1
    if (N == 1) {

      // First operation
      System.out.println("Operation 1 : " + 1
                         + " " + 1 );
      System.out.println("Added elements: "
                         + -1 * arr[0] );
      System.out.println();

      // 2nd Operation
      System.out.println("Operation 2 : "
                         + 1 + " " + 1 );
      System.out.println("Added elements: "
                         + 1 * arr[0] );
      System.out.println();

      // 3rd Operation
      System.out.println("Operation 3 : "
                         + 1 + " " + 1 );
      System.out.println("Added elements: "
                         + -1 * arr[0] );
    }

    // Otherwise
    else {

      // 1st Operation
      System.out.println("Operation 1 : "
                         + 1 + " " + N );
      System.out.print("Added elements: ");
      for (int i = 0; i < N; i++) {
        System.out.print(-1 * arr[i] * N + " ");
      }
      System.out.println();
      System.out.println();

      // 2nd Operation
      System.out.println("Operation 2 : "
                         + 1 + " " + (N - 1) );
      System.out.print("Added elements: ");
      for (int i = 0; i < N - 1; i++) {
        System.out.print(arr[i] * (N - 1) + " ");
      }
      System.out.println();
      System.out.println();

      // 3rd Operation
      System.out.println("Operation 3 : " + N
                         + " " + N );
      System.out.print("Added elements: ");
      System.out.println(arr[N - 1] * (N - 1) );
    }
  }

  // Driver code
  public static void main(String[] args)
  {

    // Input
    int arr[] = { 1, 3, 2, 4 };
    int N = arr.length;

    // Function call to make all
    // array elements equal to 0
    ConvertArray(arr, N);
  }
}

// This code is contributed by souravghosh0416.
```

## **蟒蛇 3**

```
# Python 3 program of the above approach

# Function to reduce all
# array elements to zero
def ConvertArray(arr, N):

    # If size of array is 1
    if (N == 1):

        # First operation
        print("Operation 1 :",1,1)
        print("Added elements:",-1 * arr[0])
        print("\n",end = "")

        # 2nd Operation
        print("Operation 2 :",1,1)
        print("Added elements:",1 * arr[0])
        print("\n",end = "")

        # 3rd Operation
        print("Operation 3 :",1,1)
        print("Added elements:",-1 * arr[0])
        print("\n",end = "")

    # Otherwise
    else:

        # 1st Operation
        print("Operation 1 :",1,N)
        print("Added elements:",end = " ")
        for i in range(N):
            print(-1 * arr[i] * N,end = " ")
        print("\n")

        # 2nd Operation
        print("Operation 2 :",1,N - 1)
        print("Added elements:",end = " ")
        for i in range(N - 1):
            print(arr[i] * (N - 1),end = " ")
        print("\n")

        # 3rd Operation
        print("Operation 3 : ",N,N)
        print("Added elements:",end = " ")
        print(arr[N - 1] * (N - 1))

# Driver Code
if __name__ == '__main__':

    # Input
    arr =  [1, 3, 2, 4]
    N =  len(arr)

    # Function call to make all
    # array elements equal to 0
    ConvertArray(arr, N)

    # This code is contributed by ipg2016107.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG{

  // Function to reduce all
  // array elements to zero
  static void ConvertArray(int[] arr, int N)
  {

    // If size of array is 1
    if (N == 1) {

      // First operation
      Console.WriteLine("Operation 1 : " + 1
                         + " " + 1 );
      Console.WriteLine("Added elements: "
                         + -1 * arr[0] );
      Console.WriteLine();

      // 2nd Operation
      Console.WriteLine("Operation 2 : "
                         + 1 + " " + 1 );
      Console.WriteLine("Added elements: "
                         + 1 * arr[0] );
      Console.WriteLine();

      // 3rd Operation
      Console.WriteLine("Operation 3 : "
                         + 1 + " " + 1 );
      Console.WriteLine("Added elements: "
                         + -1 * arr[0] );
    }

    // Otherwise
    else {

      // 1st Operation
      Console.WriteLine("Operation 1 : "
                         + 1 + " " + N );
      Console.Write("Added elements: ");
      for (int i = 0; i < N; i++) {
        Console.Write(-1 * arr[i] * N + " ");
      }
      Console.WriteLine();
      Console.WriteLine();

      // 2nd Operation
      Console.WriteLine("Operation 2 : "
                         + 1 + " " + (N - 1) );
      Console.Write("Added elements: ");
      for (int i = 0; i < N - 1; i++) {
        Console.Write(arr[i] * (N - 1) + " ");
      }
      Console.WriteLine();
      Console.WriteLine();

      // 3rd Operation
      Console.WriteLine("Operation 3 : " + N
                         + " " + N );
      Console.Write("Added elements: ");
      Console.WriteLine(arr[N - 1] * (N - 1) );
    }
  }

// Driver Code
public static void Main(string[] args)
{

    // Input
    int[] arr = { 1, 3, 2, 4 };
    int N = arr.Length;

    // Function call to make all
    // array elements equal to 0
    ConvertArray(arr, N);
}
}

// This code is contributed by code_hunt.
```

## **java 描述语言**

```
<script>
// javascript program for the above approach

    // Function to reduce all
    // array elements to zero
    function ConvertArray(arr, N)
    {

        // If size of array is 1
        if (N == 1)
        {

            // First operation
            document.write("Operation 1 : " + 1 + " " + 1+ "<br/>");
            document.write("Added elements: " + -1 * arr[0]+"<br/>");
            document.write("<br/>");

            // 2nd Operation
            document.write("Operation 2 : " + 1 + " " + 1+"<br/>");
            document.write("Added elements: " + 1 * arr[0]+"<br/>");
            document.write("<br/>");

            // 3rd Operation
            document.write("Operation 3 : " + 1 + " " + 1+"<br/>");
            document.write("Added elements: " + -1 * arr[0]+"<br/>");
        }

        // Otherwise
        else
        {

            // 1st Operation
            document.write("Operation 1 : " + 1 + " " + N+"<br/>");
            document.write("Added elements: ");
            for (i = 0; i < N; i++) {
                document.write(-1 * arr[i] * N + " ");
            }
            document.write("<br/>");
            document.write("<br/>");

            // 2nd Operation
            document.write("Operation 2 : " + 1 + " " + (N - 1)+"<br/>");
            document.write("Added elements: ");
            for (i = 0; i < N - 1; i++) {
                document.write(arr[i] * (N - 1) + " ");
            }
            document.write("<br/>");
            document.write("<br/>");

            // 3rd Operation
            document.write("Operation 3 : " + N + " " + N+"<br/>");
            document.write("Added elements: ");
            document.write(arr[N - 1] * (N - 1)+"<br/>");
        }
    }

    // Driver code

        // Input
        var arr = [ 1, 3, 2, 4 ];
        var N = arr.length;

        // Function call to make all
        // array elements equal to 0
        ConvertArray(arr, N);

// This code is contributed by todaysgaurav.
</script>
```

****Output:** 

```
Operation 1 : 1 4
Added elements: -4 -12 -8 -16 

Operation 2 : 1 3
Added elements: 3 9 6 

Operation 3 : 4 4
Added elements: 12
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**