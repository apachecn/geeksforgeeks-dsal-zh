# 对于第一个数组中的每个元素，计数小于或等于第二个数组中的元素| 设置 2

给定两个未排序的数组 arr1 []和 arr2 []。 它们可能包含重复项。 对于 arr1 []中的每个元素，计数少于或等于数组 arr2 []中的元素。

**范例**：

> **输入：** arr1 [] = [1、2、3、4、7、9]
> arr2 [] = [0、1、2、1、1、4]
> **输出：** [4、5、5、6、6、6]
> **说明：**第二个数组中小于或等于 1 的 4 个元素，类似地，少 5 个元素 如果第二个数组中的值不等于 2，则对其他元素类似地计算值。
> 
> **输入：** arr1 [] = [5、10、2、6、1、8、6、12]
> arr2 [] = [6、5、11、4、2、3、7 ]
> **输出：** [4、6、1、5、0、6、5、7]
> **说明：**有 4 个小于或等于 5 的元素 在第二个数组中，类似地，有 6 个元素小于第二个数组中的 10 个元素，对其他元素也类似地计算值。

[先前的帖子](https://www.geeksforgeeks.org/element-1st-array-count-elements-less-equal-2nd-array/)中已经讨论了此问题。

**<u>解决方案：</u>** 在本文中，讨论了针对上述问题的更优化的线性时间解决方案。 这里讨论的方法适用于数值范围较小的数组。 可用作数组索引的值的范围。

*   **方法：**
    这个想法是创建一个前缀映射，直到第二个数组的最大元素。 前缀数组将存储最多该索引的元素，例如，prefix [i]将存储最多 i 的元素数。 然后遍历第一个数组，并从前缀数组中找到小于或等于该元素的元素数。
    通过遍历前缀数组并通过添加珍贵元素（即 prefix [i] + = prefix [i-1]）来更新当前元素来创建前缀数组。
*   **算法：**
    1.  创建第二个数组和第一个数组或映射的最大元素大小的额外空间（前缀）。
    2.  遍历第二个数组。
    3.  对于第二个数组的每个元素，增加前缀数组的数量，即 prefix [arr2 [i]] ++
    4.  从 1 到 MAX 遍历前缀数组（第二个数组和第一个数组的最大元素，并通过将第 i-1 个元素的总和相加来更新第 ith 个元素
    5.  现在遍历第一个数组并打印 prefix [arr_1 [i]]的值
*   **实现：**

    ## C++

    ```cpp

    // C++ program for each element in 1st  
    // array count elements less than or equal to it  
    // in 2nd array  

    #include <iostream>  
    using namespace std;  

    #define MAX 100000  

    // Function for each element in 1st  
    // array count elements less than or equal to it  
    // in 2nd array  
    void countEleLessThanOrEqual(int arr1[], int m,  
                                    int arr2[], int n)  
    {  
        // Creating hash array initially  
        // filled with zero  
        int hash[MAX] = {0};  

        // Insert element of arr2[] to hash  
        // such that hash[i] will give count of  
        // element i in arr2[]  
        for (int i = 0; i < n; i++)  
            hash[arr2[i]]++;  

        // Presum of hash array  
        // such that hash[i] will give count of  
        // element less than or equals to i in arr2[]  
        for (int i=1; i<MAX; i++)      
            hash[i] = hash[i] + hash[i-1];  

        // Traverse arr1[] and print hash[arr[i]]  
        for (int i = 0; i < m; i++)  
            cout << hash[arr1[i]] << " ";      
    }  

    // Driver code  
    int main()  
    {  
        int arr1[] = {1, 2, 3, 4, 7, 9};  
        int arr2[] = {0, 1, 2, 1, 1, 4};  
        int m, n;  

        m = sizeof(arr1) / sizeof(arr1[0]);  
        n = sizeof(arr2) / sizeof(arr2[0]);  

        countEleLessThanOrEqual(arr1, m, arr2, n);  

        return 0;  
    }  

    ```

    ## Java

    ```java

    // Java program for each element  
    // in 1st array count elements  
    // less than or equal to it in  
    // 2nd array  
    import java.io.*; 

    class GFG  
    { 
    static int MAX = 100000; 

    // Function for each element  
    // in 1st array count elements  
    // less than or equal to it  
    // in 2nd array  
    static void countEleLessThanOrEqual(int arr1[], int m,  
                                        int arr2[], int n) 
    {  
        // Creating hash array initially 
        // filled with zero 
        int hash[] = new int[MAX]; 

        // Insert element of arr2[] to 
        // hash such that hash[i] will 
        // give count of element i in arr2[] 
        for (int i = 0; i < n; i++) 
            hash[arr2[i]]++; 

        // Presum of hash array 
        // such that hash[i] will  
        // give count of element  
        // less than or equals to  
        // i in arr2[] 
        for(int i = 1; i < MAX; i++) 
        { 
            hash[i] = hash[i] +  
                      hash[i - 1]; 
        } 

        // Traverse arr1[] and  
        // print hash[arr[i]] 
        for (int i = 0; i < m; i++)  
        { 
            System.out.print(hash[arr1[i]] + " "); 
        } 
    } 

    // Driver code 
    public static void main (String[] args)  
    { 
        int arr1[] = {1, 2, 3, 4, 7, 9}; 
        int arr2[] = {0, 1, 2, 1, 1, 4}; 
        int m, n; 

        m = arr1.length; 
        n = arr2.length; 

        countEleLessThanOrEqual(arr1, m, arr2, n); 
    } 
    } 

    // This code is contributed 
    // by inder_verma 

    ```

    ## Python3

    ```py

    # Python 3 program for each element in 1st  
    # array count elements less than or equal  
    # to it in 2nd array  

    MAX = 100000

    # Function for each element in 1st  
    # array count elements less than or  
    # equal to it in 2nd array  
    def countEleLessThanOrEqual(arr1, m, arr2, n): 

        # Creating hash array initially  
        # filled with zero  
        hash = [0 for i in range(MAX)]  

        # Insert element of arr2[] to hash  
        # such that hash[i] will give count  
        # of element i in arr2[]  
        for i in range(n): 
            hash[arr2[i]] += 1

        # Presum of hash array such that  
        # hash[i] will give count of element  
        # less than or equals to i in arr2[]  
        for i in range(1, MAX, 1): 
            hash[i] = hash[i] + hash[i - 1]  

        # Traverse arr1[] and print hash[arr[i]]  
        for i in range(m): 
            print(hash[arr1[i]], end = " ")      

    # Driver code  
    if __name__ == '__main__': 
        arr1 = [1, 2, 3, 4, 7, 9]  
        arr2 = [0, 1, 2, 1, 1, 4]  
        m = len(arr1)  
        n = len(arr2) 

        countEleLessThanOrEqual(arr1, m, arr2, n)  

    # This code is contributed by 
    # Shashank_Sharma 

    ```

    ## C ＃

    ```

    // C# program for each element  
    // in 1st array count elements  
    // less than or equal to it in  
    // 2nd array  
    using System; 
    public class GFG {  

    static int MAX = 100000;  

    // Function for each element  
    // in 1st array count elements  
    // less than or equal to it  
    // in 2nd array  
    static void countEleLessThanOrEqual(int []arr1, int m,  
                                        int []arr2, int n)  
    {  
        // Creating hash array initially  
        // filled with zero  
        int []hash = new int[MAX];  

        // Insert element of arr2[] to  
        // hash such that hash[i] will  
        // give count of element i in arr2[]  
        for (int i = 0; i < n; i++)  
            hash[arr2[i]]++;  

        // Presum of hash array  
        // such that hash[i] will  
        // give count of element  
        // less than or equals to  
        // i in arr2[]  
        for(int i = 1; i < MAX; i++)  
        {  
            hash[i] = hash[i] +  
                    hash[i - 1];  
        }  

        // Traverse arr1[] and  
        // print hash[arr[i]]  
        for (int i = 0; i < m; i++)  
        {  
            Console.Write(hash[arr1[i]] + " ");  
        }  
    }  

    // Driver code  
    public static void Main ()  
    {  
        int []arr1 = {1, 2, 3, 4, 7, 9};  
        int []arr2 = {0, 1, 2, 1, 1, 4};  
        int m, n;  

        m = arr1.Length;  
        n = arr2.Length;  

        countEleLessThanOrEqual(arr1, m, arr2, n);  
    }  
    }  

    // This code is contributed by Shikha Singh.  

    ```

    ## PHP

    ```php

    <?php  
    // PHP program for each element in 1st  
    // array count elements less than or  
    // equal to it in 2nd array  
    $MAX = 100000 ; 

    // Function for each element in 1st  
    // array count elements less than or  
    // equal to it in 2nd array  
    function countEleLessThanOrEqual(&$arr1, $m,  
                                     &$arr2, $n)  
    {  
        global $MAX; 

        // Creating hash array initially  
        // filled with zero  
        $hash = array_fill(0, $MAX, NULL);  

        // Insert element of arr2[] to hash  
        // such that hash[i] will give count of  
        // element i in arr2[]  
        for ($i = 0; $i < $n; $i++)  
            $hash[$arr2[$i]]++;  

        // Presum of hash array such that hash[i]  
        // will give count of element less than  
        // or equals to i in arr2[]  
        for ($i = 1; $i < $MAX; $i++)      
            $hash[$i] = $hash[$i] + $hash[$i - 1];  

        // Traverse arr1[] and print hash[arr[i]]  
        for ($i = 0; $i < $m; $i++)  
            echo $hash[$arr1[$i]] . " ";      
    }  

    // Driver code  
    $arr1 = array(1, 2, 3, 4, 7, 9); 
    $arr2 = array(0, 1, 2, 1, 1, 4);  

    $m = sizeof($arr1);  
    $n = sizeof($arr2);  

    countEleLessThanOrEqual($arr1, $m, $arr2, $n);  

    // This code is contributed  
    // by ChitraNayal 
    ?> 

    ```

    **输出：**

    ```
    4 5 5 6 6 6

    ```

**替代方法：**该方法仅将数组替换为矢量，并且将使用数组生成的哈希图替换为映射。 方法和算法保持不变。

*   **实现：**

    ## C++

    ```cpp

    // C++ program for each element in 1st  
    // array count elements less than or equal to it  
    // in 2nd array  
    #include <iostream> 
    #include <map> 
    #include <vector> 

    // Function for each element in 1st  
    // array count elements less than or equal to it  
    // in 2nd array  
    void countLessThanOrEqual(const std::vector<int>& vec1,  
                            const std::vector<int>& vec2) { 
        std::map<int, unsigned int> countOfVec2; 
        for (const auto& item : vec2) { 
            ++countOfVec2[item]; 
        } 

        unsigned int prev = 0; 
        for (auto& pair : countOfVec2) { 
            pair.second += prev; 
            prev = pair.second; 
        } 
        // Traverse arr1[] and print result  
        for (const auto& item : vec1) { 
            unsigned int result = (--countOfVec2.upper_bound(item))->second; 
            std::cout << result << " "; 
        } 
    } 

    // Driver code 
    int main() 
    { 
        std::vector<int> arr1 = { 1, 2, 3, 4, 7, 9 }; 
        std::vector<int> arr2 = { 0, 1, 2, 1, 1, 4 }; 

        countLessThanOrEqual(arr1, arr2); 

        return 0; 
    } 

    ```

    ## Python3

    ```py

    # Python3 program for each element in 1st  
    # array count elements less than or equal to it  
    # in 2nd array  

    # Function for each element in 1st  
    # array count elements less than or equal to it  
    # in 2nd array  
    def countLessThanOrEqual(vec1, vec2): 

        countOfVec2 = {} 
        for item in vec2: 
            if item not in countOfVec2: 
                countOfVec2[item] = 0
            countOfVec2[item] += 1

        prev = 0
        for pair in countOfVec2: 
            countOfVec2[pair] += prev 
            prev = countOfVec2[pair] 

        val = list(countOfVec2) 

        # Traverse arr1[] and print result  
        for item in vec1: 
            i = 0
            v = 0
            for i in range(len(val)): 
                if item < val[i]: 
                    v = i 
                    break
            v -= 1
            if v == -1: 
                v = val[-1] 
            result = countOfVec2[v] 
            print(result, end = " ") 

    # Driver code 
    arr1 = [1, 2, 3, 4, 7, 9] 
    arr2 = [0, 1, 2, 1, 1, 4] 

    countLessThanOrEqual(arr1, arr2) 

    # This code is contributed by shubhamsingh10 

    ```

    **输出：**

    ```
    4 5 5 6 6 6

    ```

*   **Complexity Analysis:**
    *   **时间复杂度：** O（max + n）其中 max 是两个数组的最大元素，n 是数组的长度。
        需要对数组和前缀数组都进行一次遍历。
    *   **空间复杂度：** O（max）其中 max 是两个数组的最大元素。
        需要大小为 max 的前缀数组。



* * *

* * *



