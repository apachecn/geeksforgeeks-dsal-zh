# 查找所有零和的三元组

> 原文： [https://www.geeksforgeeks.org/find-triplets-array-whose-sum-equal-zero/](https://www.geeksforgeeks.org/find-triplets-array-whose-sum-equal-zero/)

给定一系列不同的元素。 任务是在总和为零的数组中查找三元组。

**示例**：

```
Input : arr[] = {0, -1, 2, -3, 1}
Output : (0 -1 1), (2 -3 1)

Explanation : The triplets with zero sum are
0 + -1 + 1 = 0 and 2 + -3 + 1 = 0  

Input : arr[] = {1, -2, 1, 0, 5}
Output : 1 -2  1
Explanation : The triplets with zero sum is
1 + -2 + 1 = 0   

```



**方法 1**： 这是一种简单的方法，需要`O(n ^ 3)`时间才能得出结果。

*   **方法**：朴素的方法运行三个循环，并一一检查三个元素的总和是否为零。 如果三个元素的总和为零，则打印元素，否则找不到打印。

*   **算法**：

    1.  使用循环计数器`i`，`j`，`k`运行三个嵌套循环。

    2.  这三个循环从 0 到`n-3`，第二个循环从`i + 1`到`n-2`，第三个循环从`j + 1`到`n-1`。 循环计数器代表三元组的三个元素。

    3.  检查第`i`，第`j`，第`k`个元素的总和是否等于零。 如果是，则打印总和，否则继续。

*   **实现**：

    ## C++ 

    ```

    // A simple C++ program to find three elements 
    // whose sum is equal to zero 
    #include<bits/stdc++.h> 
    using namespace std; 

    // Prints all triplets in arr[] with 0 sum 
    void findTriplets(int arr[], int n) 
    { 
        bool found = true; 
        for (int i=0; i<n-2; i++) 
        { 
            for (int j=i+1; j<n-1; j++) 
            { 
                for (int k=j+1; k<n; k++) 
                { 
                    if (arr[i]+arr[j]+arr[k] == 0) 
                    { 
                        cout << arr[i] << " "
                             << arr[j] << " "
                             << arr[k] <<endl; 
                        found = true; 
                    } 
                } 
            } 
        } 

        // If no triplet with 0 sum found in array 
        if (found == false) 
            cout << " not exist "<<endl; 

    } 

    // Driver code 
    int main() 
    { 
        int arr[] = {0, -1, 2, -3, 1}; 
        int n = sizeof(arr)/sizeof(arr[0]); 
        findTriplets(arr, n); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // A simple Java program to find three elements 
    // whose sum is equal to zero 
    class num{ 
    // Prints all triplets in arr[] with 0 sum 
    static void findTriplets(int[] arr, int n) 
    { 
        boolean found = true; 
        for (int i=0; i<n-2; i++) 
        { 
            for (int j=i+1; j<n-1; j++) 
            { 
                for (int k=j+1; k<n; k++) 
                { 
                    if (arr[i]+arr[j]+arr[k] == 0) 
                    { 
                        System.out.print(arr[i]); 
                        System.out.print(" "); 
                        System.out.print(arr[j]); 
                        System.out.print(" "); 
                        System.out.print(arr[k]); 
                        System.out.print("\n"); 
                        found = true; 
                    } 
                } 
            } 
        } 

        // If no triplet with 0 sum found in array 
        if (found == false) 
            System.out.println(" not exist "); 

    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = {0, -1, 2, -3, 1}; 
        int n =arr.length; 
        findTriplets(arr, n); 

    } 
    } 
    //This code is contributed by 
    //Smitha Dinesh Semwal 

    ```

    ## Python3

    ```

    # A simple Python 3 program  
    # to find three elements whose  
    # sum is equal to zero 

    # Prints all triplets in  
    # arr[] with 0 sum 
    def findTriplets(arr, n): 

        found = True
        for i in range(0, n-2): 

            for j in range(i+1, n-1): 

                for k in range(j+1, n): 

                    if (arr[i] + arr[j] + arr[k] == 0): 
                        print(arr[i], arr[j], arr[k]) 
                        found = True

        # If no triplet with 0 sum  
        # found in array 
        if (found == False): 
            print(" not exist ") 

    # Driver code 
    arr = [0, -1, 2, -3, 1] 
    n = len(arr) 
    findTriplets(arr, n) 

    # This code is contributed by Smitha Dinesh Semwal     

    ```

    ## C# 

    ```

    // A simple C# program to find three elements  
    // whose sum is equal to zero 
    using System; 

    class GFG { 

        // Prints all triplets in arr[] with 0 sum 
        static void findTriplets(int []arr, int n) 
        { 
            bool found = true; 
            for (int i = 0; i < n-2; i++) 
            { 
                for (int j = i+1; j < n-1; j++) 
                { 
                    for (int k = j+1; k < n; k++) 
                    { 
                        if (arr[i] + arr[j] + arr[k] 
                                               == 0) 
                        { 
                            Console.Write(arr[i]); 
                            Console.Write(" "); 
                            Console.Write(arr[j]); 
                            Console.Write(" "); 
                            Console.Write(arr[k]); 
                            Console.Write("\n"); 
                            found = true; 
                        } 
                    } 
                } 
            } 

            // If no triplet with 0 sum found in  
            // array 
            if (found == false) 
                Console.Write(" not exist "); 
        } 

        // Driver code 
        public static void Main() 
        { 
            int []arr = {0, -1, 2, -3, 1}; 
            int n = arr.Length; 
            findTriplets(arr, n); 
        } 
    } 

    // This code is contributed by nitin mittal. 

    ```

    ## PHP

    ```

    <?php 
    // A simple PHP program to  
    // find three elements whose  
    // sum is equal to zero 

    // Prints all triplets 
    // in arr[] with 0 sum 
    function findTriplets($arr, $n) 
    { 
        $found = true; 
        for ($i = 0; $i < $n - 2; $i++) 
        { 
            for ($j = $i + 1; $j < $n - 1; $j++) 
            { 
                for ($k = $j + 1; $k < $n; $k++) 
                { 
                    if ($arr[$i] + $arr[$j] +  
                                   $arr[$k] == 0) 
                    { 
                        echo $arr[$i] , " ", 
                             $arr[$j] , " ", 
                             $arr[$k] ,"\n"; 
                        $found = true; 
                    } 
                } 
            } 
        } 

        // If no triplet with 0 
        // sum found in array 
        if ($found == false) 
            echo " not exist ", "\n"; 

    } 

    // Driver Code 
    $arr = array (0, -1, 2, -3, 1); 
    $n = sizeof($arr); 
    findTriplets($arr, $n); 

    // This code is contributed by m_kit 
    ?> 

    ```

    **输出**：

    ```
    0 -1 1
    2 -3 1
    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n ^ 3)`。

        由于需要三个嵌套循环，因此时间复杂度为`O(n ^ 3)`。

    *   **辅助空间**：`O(1)`。

        由于不需要额外的空间，因此时间复杂度是恒定的。

**方法 2**： 第二种方法使用哈希处理来获得结果，并在较短的`O(n^2)`上求解。

*   **方法**：这涉及遍历数组。 对于每个元素`arr[i]`，找到一个总和为`-arr[i]`的对。 这个问题简化为成对和，可以使用哈希在`O(n)`时间内解决。

*   **算法**：

    1.  创建一个哈希来存储键值对。

    2.  运行带有两个循环的嵌套循环，外循环从 0 到`n-2`，内循环从`i + 1`到`n-1`。

    3.  检查哈希映射中是否存在第`i`和`j`元素的总和乘以 -1。

    4.  如果该元素存在于哈希映射中，则打印三元组，否则将第`j`个元素插入哈希映射中。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find triplets in a given 
    // array whose sum is zero 
    #include<bits/stdc++.h> 
    using namespace std; 

    // function to print triplets with 0 sum 
    void findTriplets(int arr[], int n) 
    { 
        bool found = false; 

        for (int i=0; i<n-1; i++) 
        { 
            // Find all pairs with sum equals to 
            // "-arr[i]" 
            unordered_set<int> s; 
            for (int j=i+1; j<n; j++) 
            { 
                int x = -(arr[i] + arr[j]); 
                if (s.find(x) != s.end()) 
                { 
                    printf("%d %d %d\n", x, arr[i], arr[j]); 
                    found = true; 
                } 
                else
                    s.insert(arr[j]); 
            } 
        } 

        if (found == false) 
            cout << " No Triplet Found" << endl; 
    } 

    // Driver code 
    int main() 
    { 
        int arr[] = {0, -1, 2, -3, 1}; 
        int n = sizeof(arr)/sizeof(arr[0]); 
        findTriplets(arr, n); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // Java program to find triplets in a given 
    // array whose sum is zero 
    import java.util.*; 

    class GFG  
    { 

        // function to print triplets with 0 sum 
        static void findTriplets(int arr[], int n)  
        { 
            boolean found = false; 

            for (int i = 0; i < n - 1; i++)  
            { 
                // Find all pairs with sum equals to 
                // "-arr[i]" 
                HashSet<Integer> s = new HashSet<Integer>(); 
                for (int j = i + 1; j < n; j++)  
                { 
                    int x = -(arr[i] + arr[j]); 
                    if (s.contains(x))  
                    { 
                        System.out.printf("%d %d %d\n", x, arr[i], arr[j]); 
                        found = true; 
                    }  
                    else 
                    { 
                        s.add(arr[j]); 
                    } 
                } 
            } 

            if (found == false) 
            { 
                System.out.printf(" No Triplet Found\n"); 
            } 
        } 

        // Driver code 
        public static void main(String[] args)  
        { 
            int arr[] = {0, -1, 2, -3, 1}; 
            int n = arr.length; 
            findTriplets(arr, n); 
        } 
    } 

    // This code contributed by Rajput-Ji 

    ```

    ## Python3

    ```

    # Python3 program to find triplets  
    # in a given array whose sum is zero  

    # function to print triplets with 0 sum  
    def findTriplets(arr, n): 
        found = False
        for i in range(n - 1): 

            # Find all pairs with sum  
            # equals to "-arr[i]"  
            s = set() 
            for j in range(i + 1, n): 
                x = -(arr[i] + arr[j]) 
                if x in s: 
                    print(x, arr[i], arr[j]) 
                    found = True
                else: 
                    s.add(arr[j]) 
        if found == False: 
            print("No Triplet Found") 

    # Driver Code 
    arr = [0, -1, 2, -3, 1] 
    n = len(arr) 
    findTriplets(arr, n) 

    # This code is contributed by Shrikant13 

    ```

    ## C# 

    ```

    // C# program to find triplets in a given 
    // array whose sum is zero 
    using System; 
    using System.Collections.Generic; 

    class GFG  
    { 

        // function to print triplets with 0 sum 
        static void findTriplets(int []arr, int n)  
        { 
            bool found = false; 

            for (int i = 0; i < n - 1; i++)  
            { 
                // Find all pairs with sum equals to 
                // "-arr[i]" 
                HashSet<int> s = new HashSet<int>(); 
                for (int j = i + 1; j < n; j++)  
                { 
                    int x = -(arr[i] + arr[j]); 
                    if (s.Contains(x))  
                    { 
                        Console.Write("{0} {1} {2}\n", x, arr[i], arr[j]); 
                        found = true; 
                    }  
                    else
                    { 
                        s.Add(arr[j]); 
                    } 
                } 
            } 

            if (found == false) 
            { 
                Console.Write(" No Triplet Found\n"); 
            } 
        } 

        // Driver code 
        public static void Main(String[] args)  
        { 
            int []arr = {0, -1, 2, -3, 1}; 
            int n = arr.Length; 
            findTriplets(arr, n); 
        } 
    } 

    // This code has been contributed by 29AjayKumar 

    ```

    **输出**：

    ```
    -1 0 1
    -3 2 1

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n^2)`。

        由于需要两个嵌套循环，因此时间复杂度为 `O(n^2)`。

    *   **辅助空间**：`O(n)`。

        由于需要一个哈希映射，因此时间复杂度是线性的。

**方法 3**： 该方法使用排序来得出正确的结果，并以 `O(n^2)`的时间求解。

*   **方法**：上述方法需要额外的空间。 该想法基于此帖子的[方法 2](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)。 对于每个元素，检查是否存在一对总和等于该元素的负值的对。

*   **算法**：

    1.  以升序对数组进行排序。

    2.  从头到尾遍历数组。

    3.  对于每个索引`i`，创建两个变量`l = i + 1`和`r = n – 1`。

    4.  循环运行直到`l`小`r`，如果`array[l]`，`array[r]`的总和等于零，则打印三元组并中断循环。

    5.  如果总和小于零，则增加`l`的值，通过增加`l`的值，总和将随着数组的排序而增加，因此`array[l + 1] > array[l]`。

    6.  如果总和大于零，则`r`的值递减，通过增加`l`的值，总和将随着对数组进行排序而减小，因此`array[r-1] < array[r]`。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find triplets in a given 
    // array whose sum is zero 
    #include<bits/stdc++.h> 
    using namespace std; 

    // function to print triplets with 0 sum 
    void findTriplets(int arr[], int n) 
    { 
        bool found = false; 

        // sort array elements 
        sort(arr, arr+n); 

        for (int i=0; i<n-1; i++) 
        { 
            // initialize left and right 
            int l = i + 1; 
            int r = n - 1; 
            int x = arr[i]; 
            while (l < r) 
            { 
                if (x + arr[l] + arr[r] == 0) 
                { 
                    // print elements if it's sum is zero 
                    printf("%d %d %d\n", x, arr[l], arr[r]); 
                    l++; 
                    r--; 
                    found = true; 
                } 

                // If sum of three elements is less 
                // than zero then increment in left 
                else if (x + arr[l] + arr[r] < 0) 
                    l++; 

                // if sum is greater than zero than 
                // decrement in right side 
                else
                    r--; 
            } 
        } 

        if (found == false) 
            cout << " No Triplet Found" << endl; 
    } 

    // Driven source 
    int main() 
    { 
        int arr[] = {0, -1, 2, -3, 1}; 
        int n = sizeof(arr)/sizeof(arr[0]); 
        findTriplets(arr, n); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // Java  program to find triplets in a given 
    // array whose sum is zero 
    import java.util.Arrays;  
    import java.io.*; 

    class GFG { 
        // function to print triplets with 0 sum 
    static void findTriplets(int arr[], int n) 
    { 
        boolean found = false; 

        // sort array elements 
        Arrays.sort(arr); 

        for (int i=0; i<n-1; i++) 
        { 
            // initialize left and right 
            int l = i + 1; 
            int r = n - 1; 
            int x = arr[i]; 
            while (l < r) 
            { 
                if (x + arr[l] + arr[r] == 0) 
                { 
                    // print elements if it's sum is zero 
                        System.out.print(x + " "); 
                        System.out.print(arr[l]+ " "); 
                        System.out.println(arr[r]+ " "); 

                    l++; 
                    r--; 
                    found = true; 
                } 

                // If sum of three elements is less 
                // than zero then increment in left 
                else if (x + arr[l] + arr[r] < 0) 
                    l++; 

                // if sum is greater than zero than 
                // decrement in right side 
                else
                    r--; 
            } 
        } 

        if (found == false) 
                System.out.println(" No Triplet Found"); 
    } 

    // Driven source 
        public static void main (String[] args) { 

        int arr[] = {0, -1, 2, -3, 1}; 
        int n =arr.length; 
        findTriplets(arr, n); 
        } 
    //This code is contributed by Tushil..     
    } 

    ```

    ## Python3

    ```

    # python program to find triplets in a given 
    # array whose sum is zero 

    # function to print triplets with 0 sum 
    def findTriplets(arr, n): 

        found = False

        # sort array elements 
        arr.sort() 

        for i in range(0, n-1): 

            # initialize left and right 
            l = i + 1
            r = n - 1
            x = arr[i] 
            while (l < r): 

                if (x + arr[l] + arr[r] == 0): 
                    # print elements if it's sum is zero 
                    print(x, arr[l], arr[r]) 
                    l+=1
                    r-=1
                    found = True

                # If sum of three elements is less 
                # than zero then increment in left 
                elif (x + arr[l] + arr[r] < 0): 
                    l+=1

                # if sum is greater than zero than 
                # decrement in right side 
                else: 
                    r-=1

        if (found == False): 
            print(" No Triplet Found") 

    # Driven source 
    arr = [0, -1, 2, -3, 1] 
    n = len(arr) 
    findTriplets(arr, n) 

    # This code is contributed by Smitha Dinesh Semwal 

    ```

    ## C# 

    ```

    // C#  program to find triplets in a given 
    // array whose sum is zero 
    using System; 

    public class GFG{ 
            // function to print triplets with 0 sum 
    static void findTriplets(int []arr, int n) 
    { 
        bool found = false; 

        // sort array elements 
        Array.Sort(arr); 

        for (int i=0; i<n-1; i++) 
        { 
            // initialize left and right 
            int l = i + 1; 
            int r = n - 1; 
            int x = arr[i]; 
            while (l < r) 
            { 
                if (x + arr[l] + arr[r] == 0) 
                { 
                    // print elements if it's sum is zero 
                        Console.Write(x + " "); 
                        Console.Write(arr[l]+ " "); 
                        Console.WriteLine(arr[r]+ " "); 

                    l++; 
                    r--; 
                    found = true; 
                } 

                // If sum of three elements is less 
                // than zero then increment in left 
                else if (x + arr[l] + arr[r] < 0) 
                    l++; 

                // if sum is greater than zero than 
                // decrement in right side 
                else
                    r--; 
            } 
        } 

        if (found == false) 
                Console.WriteLine(" No Triplet Found"); 
    } 

    // Driven source 
        static public void Main (){ 

        int []arr = {0, -1, 2, -3, 1}; 
        int n =arr.Length; 
        findTriplets(arr, n); 
        } 
    //This code is contributed by akt_mit..  
    } 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find  
    // triplets in a given 
    // array whose sum is zero 

    // function to print  
    // triplets with 0 sum 
    function findTriplets($arr, $n) 
    { 
        $found = false; 

        // sort array elements 
        sort($arr); 

        for ($i = 0; $i < $n - 1; $i++) 
        { 
            // initialize left 
            // and right 
            $l = $i + 1; 
            $r = $n - 1; 
            $x = $arr[$i]; 
            while ($l < $r) 
            { 
                if ($x + $arr[$l] +  
                         $arr[$r] == 0) 
                { 
                    // print elements if  
                    // it's sum is zero 
                    echo $x," ", $arr[$l], 
                            " ", $arr[$r], "\n"; 
                    $l++; 
                    $r--; 
                    $found = true; 
                } 

                // If sum of three elements  
                // is less than zero then  
                // increment in left 
                else if ($x + $arr[$l] +  
                              $arr[$r] < 0) 
                    $l++; 

                // if sum is greater than  
                // zero than decrement 
                // in right side 
                else
                    $r--; 
            } 
        } 

        if ($found == false) 
            echo " No Triplet Found" ,"\n"; 
    } 

    // Driver Code 
    $arr = array (0, -1, 2, -3, 1); 
    $n = sizeof($arr); 
    findTriplets($arr, $n); 

    // This code is contributed by ajit 
    ?> 

    ```

    **输出**：

    ```
    -3 1 2
    -1 0 1

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n^2)`。

        仅需要两个嵌套循环，因此时间复杂度为 `O(n^2)`。

    *   **辅助空间**：`O(1)`，不需要额外的空间，因此时间复杂度是恒定的。

