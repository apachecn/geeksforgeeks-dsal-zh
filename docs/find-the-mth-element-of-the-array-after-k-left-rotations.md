# 在左旋转 K 次后找到数组的第 m 个元素

> 原文:[https://www . geeksforgeeks . org/find-the-mth-element-of-the-array-after-k-left-rotations/](https://www.geeksforgeeks.org/find-the-mth-element-of-the-array-after-k-left-rotations/)

给定非负整数 **K** 、 **M** 和带有 **N** 元素的数组**arr【】**在 **K** 左旋转后找到数组的 **M <sup>第</sup>个**元素。

**示例:**

> **输入:** arr[] = {3，4，5，23}，K = 2，M = 1
> **输出:** 5
> **解释:**
> 第一次左旋转后的数组 a <sub>1</sub> [ ] = {4，5，23，3}
> 第二次左旋转后的数组 a <sub>2</sub> [ ] = {5，23，3，4}
> st 元素左旋转 2 次后为 5。
> 
> **输入:** arr[] = {1，2，3，4，5}，K = 3，M = 2
> **输出:** 5
> **说明:**
> 左旋转 3 圈后的阵列第二个位置有 5 个。

**天真法:**思路是[执行左旋转](https://www.geeksforgeeks.org/print-left-rotation-array/)操作 **K** 次，然后找到最终阵的 **M <sup>第</sup>个元素**。

***时间复杂度:** O(N * K)*
***辅助空间:** O(N)*

**高效方法:**要优化问题，请注意以下几点:

2.  If the array is rotated **N** times it returns the initial array again.

    > 例如，a[ ] = {1，2，3，4，5}，K=5 那么数组经过 5 次左旋转 a <sub>5</sub> [ ] = {1，2，3，4，5}。

    因此， **Kth 旋转**后数组中的元素与原数组中索引 **K%N** 处的元素相同。

3.  The Mth element of the array after K left rotations is

    > **{(K+M–1)% N }第**

    元素。

    下面是上述方法的实现:

    ## C++

    ```
    // C++ program for the above approach 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to return Mth element of 
    // array after k left rotations 
    int getFirstElement(int a[], int N, 
                        int K, int M) 
    { 
        // The array comes to original state 
        // after N rotations 
        K %= N; 

        // Mth element after k left rotations 
        // is (K+M-1)%N th element of the 
        // original array 
        int index = (K + M - 1) % N; 

        int result = a[index]; 

        // Return the result 
        return result; 
    } 

    // Driver Code 
    int main() 
    { 
        // Array initialization 
        int a[] = { 3, 4, 5, 23 }; 

        // Size of the array 
        int N = sizeof(a) / sizeof(a[0]); 

        // Given K rotation and Mth element 
        // to be found after K rotation 
        int K = 2, M = 1; 

        // Function call 
        cout << getFirstElement(a, N, K, M); 
        return 0; 
    } 
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program for the above approach 
    import java.util.*; 
    class GFG{ 

    // Function to return Mth element of 
    // array after k left rotations 
    public static int getFirstElement(int[] a, int N, 
                                      int K, int M) 
    { 

        // The array comes to original state 
        // after N rotations 
        K %= N; 

        // Mth element after k left rotations 
        // is (K+M-1)%N th element of the 
        // original array 
        int index = (K + M - 1) % N; 

        int result = a[index]; 

        // Return the result 
        return result; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        // Array initialization 
        int a[] = { 3, 4, 5, 23 }; 

        // Size of the array 
        int N = a.length; 

        // Given K rotation and Mth element 
        // to be found after K rotation 
        int K = 2, M = 1; 

        // Function call 
        System.out.println(getFirstElement(a, N, K, M)); 
    } 
    } 

    // This code is contributed by divyeshrabadiya07 
    ```

    ## 蟒蛇 3

    ```
    # Python3 program for the above approach 

    # Function to return Mth element of 
    # array after k left rotations 
    def getFirstElement(a, N, K, M): 

        # The array comes to original state 
        # after N rotations 
        K %= N 

        # Mth element after k left rotations 
        # is (K+M-1)%N th element of the 
        # original array 
        index = (K + M - 1) % N 

        result = a[index] 

        # Return the result 
        return result 

    # Driver Code 
    if __name__ == '__main__': 

        # Array initialization 
        a = [ 3, 4, 5, 23 ] 

        # Size of the array 
        N = len(a) 

        # Given K rotation and Mth element 
        # to be found after K rotation 
        K = 2
        M = 1

        # Function call 
        print(getFirstElement(a, N, K, M)) 

    # This code is contributed by mohit kumar 29 
    ```

    ## C#

    ```
    // C# program for the above approach 
    using System;

    class GFG{

    // Function to return Mth element of 
    // array after k left rotations 
    public static int getFirstElement(int[] a, int N, 
                                      int K, int M) 
    { 

        // The array comes to original state 
        // after N rotations 
        K %= N; 

        // Mth element after k left rotations 
        // is (K+M-1)%N th element of the 
        // original array 
        int index = (K + M - 1) % N; 

        int result = a[index]; 

        // Return the result 
        return result; 
    } 

    // Driver code
    public static void Main(string[] args) 
    {

        // Array initialization 
        int []a = { 3, 4, 5, 23 }; 

        // Size of the array 
        int N = a.Length; 

        // Given K rotation and Mth element 
        // to be found after K rotation 
        int K = 2, M = 1; 

        // Function call 
        Console.Write(getFirstElement(a, N, K, M));
    }
    }

    // This code is contributed by rutvik_56
    ```

    ## java 描述语言

    ```
    <script>

    // Javascript program for the above approach 

        // Function to return Mth element of
        // array after k left rotations
        function getFirstElement(a , N , K , M) {

            // The array comes to original state
            // after N rotations
            K %= N;

            // Mth element after k left rotations
            // is (K+M-1)%N th element of the
            // original array
            var index = (K + M - 1) % N;

            var result = a[index];

            // Return the result
            return result;
        }

        // Driver code

            // Array initialization
            var a = [ 3, 4, 5, 23 ];

            // Size of the array
            var N = a.length;

            // Given K rotation and Mth element
            // to be found after K rotation
            var K = 2, M = 1;

            // Function call
            document.write(getFirstElement(a, N, K, M));

    // This code contributed by gauravrajput1 

    </script>
    ```

    **Output:** 

    ```
    5
    ```

    ***时间复杂度:**O(1)*
    T5**辅助空间:** O(1)