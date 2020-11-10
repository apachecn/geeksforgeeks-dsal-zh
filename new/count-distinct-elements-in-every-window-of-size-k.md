# 在每个大小为`k`的窗口中计数不同的元素

> 原文：[https://www.geeksforgeeks.org/count-distinct-elements-in-every-window-of-size-k/](https://www.geeksforgeeks.org/count-distinct-elements-in-every-window-of-size-k/)

给定大小为`n`的数组和整数`k`，返回所有大小为`k`的窗口中不同数字的计数。

**示例**：

```
Input: arr[] = {1, 2, 1, 3, 4, 2, 3};
       k = 4
Output: 3 4 4 3

Explanation:
First window is {1, 2, 1, 3}, count of distinct numbers is 3
Second window is {2, 1, 3, 4} count of distinct numbers is 4
Third window is {1, 3, 4, 2} count of distinct numbers is 4
Fourth window is {3, 4, 2, 3} count of distinct numbers is 3

Input: arr[] = {1, 2, 4, 4};
       k = 2
Output: 2 2 1

Explanation:
First window is {1, 2}, count of distinct numbers is 2
First window is {2, 4}, count of distinct numbers is 2
First window is {4, 4}, count of distinct numbers is 1

```

**来源**：[Microsoft 面试问题中已出现此问题。](http://qa.geeksforgeeks.org/1137/counting-factorial-numbers-in-c)

**朴素的方法**：朴素的解决方案是遍历给定数组，考虑其中的每个窗口，并对窗口的不同元素进行计数。

*   **算法**：

    1.  对于从 0 到`len_array(n) – k`的每个索引`i`，即`n – k`，从`i`到`i + k`遍历数组。 这是窗口。

    2.  从`i`到该索引遍历窗口，然后检查元素是否存在。

    3.  如果元素不存在于数组的前缀中，即从`i`到`index-1`不存在重复元素，则增加计数。

    4.  打印计数。

*   **实现**；

    ## C++

    ```cpp

    // Simple C++ program to count distinct 
    // elements in every window of size k 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Counts distinct elements in window of size k 
    int countWindowDistinct(int win[], int k) 
    { 
        int dist_count = 0; 

        // Traverse the window 
        for (int i = 0; i < k; i++) { 
            // Check if element arr[i] exists in arr[0..i-1] 
            int j; 
            for (j = 0; j < i; j++) 
                if (win[i] == win[j]) 
                    break; 
            if (j == i) 
                dist_count++; 
        } 
        return dist_count; 
    } 

    // Counts distinct elements in all windows of size k 
    void countDistinct(int arr[], int n, int k) 
    { 
        // Traverse through every window 
        for (int i = 0; i <= n - k; i++) 
            cout << countWindowDistinct(arr + i, k) << endl; 
    } 

    // Driver program 
    int main() 
    { 
        int arr[] = { 1, 2, 1, 3, 4, 2, 3 }, k = 4; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        countDistinct(arr, n, k); 
        return 0; 
    } 

    ```

    ## Java

    ```java

    // Simple Java program to count distinct elements in every 
    // window of size k 

    import java.util.Arrays; 

    class Test { 
        // Counts distinct elements in window of size k 
        static int countWindowDistinct(int win[], int k) 
        { 
            int dist_count = 0; 

            // Traverse the window 
            for (int i = 0; i < k; i++) { 
                // Check if element arr[i] exists in arr[0..i-1] 
                int j; 
                for (j = 0; j < i; j++) 
                    if (win[i] == win[j]) 
                        break; 
                if (j == i) 
                    dist_count++; 
            } 
            return dist_count; 
        } 

        // Counts distinct elements in all windows of size k 
        static void countDistinct(int arr[], int n, int k) 
        { 
            // Traverse through every window 
            for (int i = 0; i <= n - k; i++) 
                System.out.println(countWindowDistinct(Arrays.copyOfRange(arr, i, arr.length), k)); 
        } 

        // Driver method 
        public static void main(String args[]) 
        { 
            int arr[] = { 1, 2, 1, 3, 4, 2, 3 }, k = 4; 

            countDistinct(arr, arr.length, k); 
        } 
    } 

    ```

    ## Python3

    ```py

    # Simple Python3 program to count distinct  
    # elements in every window of size k 
    import math as mt  

    # Counts distinct elements in window 
    # of size k 
    def countWindowDistinct(win, k): 

        dist_count = 0

        # Traverse the window 
        for i in range(k): 

            # Check if element arr[i] exists 
            # in arr[0..i-1] 
            j = 0
            while j < i: 
                if (win[i] == win[j]): 
                    break
                else: 
                    j += 1
            if (j == i): 
                dist_count += 1

        return dist_count 

    # Counts distinct elements in all  
    # windows of size k 
    def countDistinct(arr, n, k): 

        # Traverse through every window 
        for i in range(n - k + 1): 
            print(countWindowDistinct(arr[i:k + i], k)) 

    # Driver Code 
    arr = [1, 2, 1, 3, 4, 2, 3] 
    k = 4
    n = len(arr) 
    countDistinct(arr, n, k) 

    # This code is contributed by  
    # Mohit kumar 29 

    ```

    ## C#

    ```cs

    // Simple C# program to count distinct 
    // elements in every window of size k 
    using System; 
    using System.Collections.Generic; 

    class GFG { 
        // Counts distinct elements in 
        // window of size k 
        static int countWindowDistinct(int[] win, 
                                       int k) 
        { 
            int dist_count = 0; 

            // Traverse the window 
            for (int i = 0; i < k; i++) { 
                // Check if element arr[i] 
                // exists in arr[0..i-1] 
                int j; 
                for (j = 0; j < i; j++) 
                    if (win[i] == win[j]) 
                        break; 
                if (j == i) 
                    dist_count++; 
            } 
            return dist_count; 
        } 

        // Counts distinct elements in 
        // all windows of size k 
        static void countDistinct(int[] arr, 
                                  int n, int k) 
        { 
            // Traverse through every window 
            for (int i = 0; i <= n - k; i++) { 
                int[] newArr = new int[k]; 
                Array.Copy(arr, i, newArr, 0, k); 
                Console.WriteLine(countWindowDistinct(newArr, k)); 
            } 
        } 

        // Driver Code 
        public static void Main(String[] args) 
        { 
            int[] arr = { 1, 2, 1, 3, 4, 2, 3 }; 
            int k = 4; 

            countDistinct(arr, arr.Length, k); 
        } 
    } 

    // This code is contributed by Princi Singh 

    ```

*   **输出**：

    ```
    3
    4
    4
    3
    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(nk ^ 2)`。

        通过使用排序修改`countWindowDistinct()`，可以将时间复杂度提高到`O(n * k * log k)`。 可以进一步优化该功能以使用[哈希](http://geeksquiz.com/print-distinct-elements-given-integer-array/)在窗口中查找不同的元素。 通过散列，时间复杂度变为`O(n * k)`。

    *   **空间复杂度**：`O(1)`，我们不需要任何额外的空间。

**高效方法**：因此，尽管散列需要额外的`O(n)`空间，但存在使用散列的有效解决方案，但时间复杂度将提高。 诀窍是在滑动窗口时使用上一个窗口的计数。 为此，可以使用散列图来存储当前窗口的元素。 哈希映射还可以通过同时添加和删除元素，同时跟踪不同元素来进行操作。 该问题涉及在长度为`k`的窗口中查找不同元素的数量，尽管`k - 1`个元素与先前的相邻窗口相同。 例如，假设从索引`i`到`i + k – 1`的元素作为元素频率对存储在哈希映射中。 因此，在将`i + 1`到`i + k`范围内的哈希映射更新时，将第`i`个元素的频率降低 1 并将第`i + k`个元素的频率增加 1。

从`HashMap`插入和删除需要固定的时间。

*   **算法**：

    1.  创建一个空的哈希映射。 令哈希映射为`hM`。

    2.  将`dist_count`的不重复元素的计数初始化为 0。

    3.  遍历第一个窗口并将第一个窗口的元素插入到`hM`中。 这些元素用作键，其计数作为`hM`中的值。 另外，请继续更新`dist_count`。

    4.  打印第一个窗口的不重复计数。

    5.  遍历其余数组（或其他窗口）。

    6.  删除上一个窗口的第一个元素。

        *   如果删除的元素仅出现一次，则将其从`hM`中删除并减少不重复计数，即`dist_count– -`

        *   否则（以`hM`出现多次），然后以`hM`为单位递减计数

    7.  添加当前元素（新窗口的最后一个元素）

        *   如果添加的元素不在`hM`中存在，请将其添加到`hM`中并增加不重复计数，即`dist_count++`

        *   否则（添加的元素出现多次），以`hM`递增其计数

*   **以下是上述方法的模拟**：

    ![](img/3a18bec756059e94265d825bf8cb3b9e.png)

*   **实现**：

    ## C++

    ```cpp

    // An efficient C++ program to 
    // count distinct elements in 
    // every window of size k 
    #include <iostream> 
    #include <map> 
    using namespace std; 

    void countDistinct(int arr[], int k, int n) 
    { 
        // Creates an empty hashmap hm 
        map<int, int> hm; 

        // initialize distinct element count for current window 
        int dist_count = 0; 

        // Traverse the first window and store count 
        // of every element in hash map 
        for (int i = 0; i < k; i++) { 
            if (hm[arr[i]] == 0) { 
                dist_count++; 
            } 
            hm[arr[i]] += 1; 
        } 

        // Print count of first window 
        cout << dist_count << endl; 

        // Traverse through the remaining array 
        for (int i = k; i < n; i++) { 
            // Remove first element of previous window 
            // If there was only one occurrence, then reduce distinct count. 
            if (hm[arr[i - k]] == 1) { 
                dist_count--; 
            } 
            // reduce count of the removed element 
            hm[arr[i - k]] -= 1; 

            // Add new element of current window 
            // If this element appears first time, 
            // increment distinct element count 

            if (hm[arr[i]] == 0) { 
                dist_count++; 
            } 
            hm[arr[i]] += 1; 

            // Print count of current window 
            cout << dist_count << endl; 
        } 
    } 

    int main() 
    { 
        int arr[] = { 1, 2, 1, 3, 4, 2, 3 }; 
        int size = sizeof(arr) / sizeof(arr[0]); 
        int k = 4; 
        countDistinct(arr, k, size); 

        return 0; 
    } 
    // This solution is contributed by Aditya Goel 

    ```

    ## Java

    ```java

    // An efficient Java program to count distinct elements in 
    // every window of size k 
    import java.util.HashMap; 

    class CountDistinctWindow { 
        static void countDistinct(int arr[], int k) 
        { 
            // Creates an empty hashMap hM 
            HashMap<Integer, Integer> hM = new HashMap<Integer, Integer>(); 

            // Traverse the first window and store count 
            // of every element in hash map 
            for (int i = 0; i < k; i++) 
                hM.put(arr[i], hM.getOrDefault(arr[i], 0) + 1); 

            // Print count of first window 
            System.out.println(hM.size()); 

            // Traverse through the remaining array 
            for (int i = k; i < arr.length; i++) { 

                // Remove first element of previous window 
                // If there was only one occurrence 
                if (hM.get(arr[i - k]) == 1) { 
                    hM.remove(arr[i - k]); 
                } 

                else // reduce count of the removed element 
                    hM.put(arr[i - k],  hM.get(arr[i - k]) - 1);             

                // Add new element of current window 
                // If this element appears first time, 
                // set its count as 1, 
                hM.put(arr[i], hM.getOrDefault(arr[i], 0) + 1); 

                // Print count of current window 
                System.out.println(hM.size()); 
            } 
        } 

        // Driver method 
        public static void main(String arg[]) 
        { 
            int arr[] = { 1, 2, 1, 3, 4, 2, 3 }; 
            int k = 4; 
            countDistinct(arr, k); 
        } 
    } 

    ```

    ## Python3

    ```py

    # An efficient Python program to 
    # count distinct elements in 
    # every window of size k 
    from collections import defaultdict 

    def countDistinct(arr, k, n): 

        # Creates an empty hashmap hm  
        mp = defaultdict(lambda:0) 

        # initialize distinct element  
        # count for current window  
        dist_count = 0

        # Traverse the first window and store count  
        # of every element in hash map  
        for i in range(k): 
            if mp[arr[i]] == 0: 
                dist_count += 1
            mp[arr[i]] += 1

        # Print count of first window  
        print(dist_count) 

        # Traverse through the remaining array  
        for i in range(k, n): 

            # Remove first element of previous window  
            # If there was only one occurrence,  
            # then reduce distinct count.  
            if mp[arr[i - k]] == 1: 
                dist_count -= 1
            mp[arr[i - k]] -= 1

        # Add new element of current window  
        # If this element appears first time,  
        # increment distinct element count  
            if mp[arr[i]] == 0: 
                dist_count += 1
            mp[arr[i]] += 1

            # Print count of current window  
            print(dist_count) 

    arr = [1, 2, 1, 3, 4, 2, 3] 
    n = len(arr) 
    k = 4
    countDistinct(arr, k, n) 

    # This code is contributed by Shrikant13 

    ```

    ## C#

    ```cs

    // An efficient C# program to count 
    // distinct elements in every window of size k 
    using System; 
    using System.Collections.Generic; 

    public class CountDistinctWindow { 
        static void countDistinct(int[] arr, int k) 
        { 
            // Creates an empty hashMap hM 
            Dictionary<int, int> hM = new Dictionary<int, int>(); 

            // initialize distinct element count for 
            // current window 
            int dist_count = 0; 

            // Traverse the first window and store count 
            // of every element in hash map 
            for (int i = 0; i < k; i++) { 
                if (!hM.ContainsKey(arr[i])) { 
                    hM.Add(arr[i], 1); 
                    dist_count++; 
                } 
                else { 
                    int count = hM[arr[i]]; 
                    hM.Remove(arr[i]); 
                    hM.Add(arr[i], count + 1); 
                } 
            } 

            // Print count of first window 
            Console.WriteLine(dist_count); 

            // Traverse through the remaining array 
            for (int i = k; i < arr.Length; i++) { 

                // Remove first element of previous window 
                // If there was only one occurrence, then 
                // reduce distinct count. 
                if (hM[arr[i - k]] == 1) { 
                    hM.Remove(arr[i - k]); 
                    dist_count--; 
                } 
                else // reduce count of the removed element 
                { 
                    int count = hM[arr[i - k]]; 
                    hM.Remove(arr[i - k]); 
                    hM.Add(arr[i - k], count - 1); 
                } 

                // Add new element of current window 
                // If this element appears first time, 
                // increment distinct element count 
                if (!hM.ContainsKey(arr[i])) { 
                    hM.Add(arr[i], 1); 
                    dist_count++; 
                } 
                else // Increment distinct element count 
                { 
                    int count = hM[arr[i]]; 
                    hM.Remove(arr[i]); 
                    hM.Add(arr[i], count + 1); 
                } 

                // Print count of current window 
                Console.WriteLine(dist_count); 
            } 
        } 

        // Driver method 
        public static void Main(String[] arg) 
        { 
            int[] arr = { 1, 2, 1, 3, 4, 2, 3 }; 
            int k = 4; 
            countDistinct(arr, k); 
        } 
    } 

    // This code contributed by Rajput-Ji 

    ```

*   **输出**：

    ```
    3
    4
    4
    3

    ```

*   **Complexity Analysis:**

    *   **时间复杂度**`O(n)`。 由于需要单遍遍数组。

    *   **空间复杂度**`O(n)`。 因为，哈希映射需要线性空间。

本文由 **Piyush** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

