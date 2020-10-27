# 查找范围为

的缺失元素

给定一个由不同元素组成的数组 arr [0..n-1]和一个范围[low，high]，找到所有在范围内但不在数组中的数字。 缺少的元素应按排序顺序打印。

**示例：**

```
Input: arr[] = {10, 12, 11, 15}, 
       low = 10, hight = 15
Output: 13, 14

Input: arr[] = {1, 14, 11, 51, 15}, 
       low = 50, hight = 55
Output: 50, 52, 53, 54

```

可以采用以下两种方法来解决该问题。

1.  **Use Sorting :** Sort the array, then do binary search for ‘low’. Once location of low is find, start traversing array from that location and keep printing all missing numbers.

    ## C ++

    ```

    // A sorting based C++ program to find missing 
    // elements from an array 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Print all elements of range [low, high] that 
    // are not present in arr[0..n-1] 
    void printMissing(int arr[], int n, int low, 
                      int high) 
    { 
        // Sort the array 
        sort(arr, arr + n); 

        // Do binary search for 'low' in sorted 
        // array and find index of first element 
        // which either equal to or greater than 
        // low. 
        int* ptr = lower_bound(arr, arr + n, low); 
        int index = ptr - arr; 

        // Start from the found index and linearly 
        // search every range element x after this 
        // index in arr[] 
        int i = index, x = low; 
        while (i < n && x <= high) { 
            // If x doesn't math with current element 
            // print it 
            if (arr[i] != x) 
                cout << x << " "; 

            // If x matches, move to next element in arr[] 
            else
                i++; 

            // Move to next element in range [low, high] 
            x++; 
        } 

        // Print range elements thar are greater than the 
        // last element of sorted array. 
        while (x <= high) 
            cout << x++ << " "; 
    } 

    // Driver program 
    int main() 
    { 
        int arr[] = { 1, 3, 5, 4 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        int low = 1, high = 10; 
        printMissing(arr, n, low, high); 
        return 0; 
    } 

    ```

    ## 爪哇

    ```

    // A sorting based Java program to find missing 
    // elements from an array 

    import java.util.Arrays; 

    public class PrintMissing { 
        // Print all elements of range [low, high] that 
        // are not present in arr[0..n-1] 
        static void printMissing(int ar[], int low, int high) 
        { 
            Arrays.sort(ar); 
            // Do binary search for 'low' in sorted 
            // array and find index of first element 
            // which either equal to or greater than 
            // low. 
            int index = ceilindex(ar, low, 0, ar.length - 1); 
            int x = low; 

            // Start from the found index and linearly 
            // search every range element x after this 
            // index in arr[] 
            while (index < ar.length && x <= high) { 
                // If x doesn't math with current element 
                // print it 
                if (ar[index] != x) { 
                    System.out.print(x + " "); 
                } 

                // If x matches, move to next element in arr[] 
                else
                    index++; 
                // Move to next element in range [low, high] 
                x++; 
            } 

            // Print range elements thar are greater than the 
            // last element of sorted array. 
            while (x <= high) { 
                System.out.print(x + " "); 
                x++; 
            } 
        } 

        // Utility function to find ceil index of given element 
        static int ceilindex(int ar[], int val, int low, int high) 
        { 

            if (val < ar[0]) 
                return 0; 
            if (val > ar[ar.length - 1]) 
                return ar.length; 

            int mid = (low + high) / 2; 
            if (ar[mid] == val) 
                return mid; 
            if (ar[mid] < val) { 
                if (mid + 1 < high && ar[mid + 1] >= val) 
                    return mid + 1; 
                return ceilindex(ar, val, mid + 1, high); 
            } 
            else { 
                if (mid - 1 >= low && ar[mid - 1] < val) 
                    return mid; 
                return ceilindex(ar, val, low, mid - 1); 
            } 
        } 

        // Driver program to test above function 
        public static void main(String[] args) 
        { 
            int arr[] = { 1, 3, 5, 4 }; 
            int low = 1, high = 10; 
            printMissing(arr, low, high); 
        } 
    } 

    // This code is contributed by Rishabh Mahrsee 

    ```

    ## 蟒蛇

    ```

    # Python library for binary search  
    from bisect import bisect_left  

    # A sorting based C++ program to find missing  
    # elements from an array  

    # Print all elements of range [low, high] that  
    # are not present in arr[0..n-1]  

    def printMissing(arr, n, low, high): 

        # Sort the array 
        arr.sort() 

        # Do binary search for 'low' in sorted  
        # array and find index of first element  
        # which either equal to or greater than  
        # low.  
        ptr = bisect_left(arr, low) 
        index = ptr 

        # Start from the found index and linearly  
        # search every range element x after this  
        # index in arr[]  
        i = index 
        x = low 
        while (i < n and x <= high): 
        # If x doesn't math with current element  
        # print it  
            if(arr[i] != x): 
                print(x, end =" ") 

        # If x matches, move to next element in arr[]  
            else: 
                i = i + 1
        # Move to next element in range [low, high]  
            x = x + 1

        # Print range elements thar are greater than the  
        # last element of sorted array.  
        while (x <= high):  
            print(x, end =" ") 
            x = x + 1

    # Driver code  

    arr = [1, 3, 5, 4]  
    n = len(arr) 
    low = 1
    high = 10
    printMissing(arr, n, low, high);  

    # This code is contributed by YatinGupta 

    ```

    ## C＃

    ```

    // A sorting based Java program to 
    // find missing elements from an array 
    using System; 

    class GFG { 

        // Print all elements of range 
        // [low, high] that are not 
        // present in arr[0..n-1] 
        static void printMissing(int[] ar, 
                                 int low, int high) 
        { 
            Array.Sort(ar); 

            // Do binary search for 'low' in sorted 
            // array and find index of first element 
            // which either equal to or greater than 
            // low. 
            int index = ceilindex(ar, low, 0, 
                                  ar.Length - 1); 
            int x = low; 

            // Start from the found index and linearly 
            // search every range element x after this 
            // index in arr[] 
            while (index < ar.Length && x <= high) { 
                // If x doesn't math with current 
                // element print it 
                if (ar[index] != x) { 
                    Console.Write(x + " "); 
                } 

                // If x matches, move to next 
                // element in arr[] 
                else
                    index++; 

                // Move to next element in 
                // range [low, high] 
                x++; 
            } 

            // Print range elements thar 
            // are greater than the 
            // last element of sorted array. 
            while (x <= high) { 
                Console.Write(x + " "); 
                x++; 
            } 
        } 

        // Utility function to find 
        // ceil index of given element 
        static int ceilindex(int[] ar, int val, 
                             int low, int high) 
        { 
            if (val < ar[0]) 
                return 0; 
            if (val > ar[ar.Length - 1]) 
                return ar.Length; 

            int mid = (low + high) / 2; 
            if (ar[mid] == val) 
                return mid; 
            if (ar[mid] < val) { 
                if (mid + 1 < high && ar[mid + 1] >= val) 
                    return mid + 1; 
                return ceilindex(ar, val, mid + 1, high); 
            } 
            else { 
                if (mid - 1 >= low && ar[mid - 1] < val) 
                    return mid; 
                return ceilindex(ar, val, low, mid - 1); 
            } 
        } 

        // Driver Code 
        static public void Main() 
        { 
            int[] arr = { 1, 3, 5, 4 }; 
            int low = 1, high = 10; 
            printMissing(arr, low, high); 
        } 
    } 

    // This code is contributed 
    // by Sach_Code 

    ```

    **Output:**

    ```
    2 6 7 8 9 10 
    ```

2.  **Using Arrays :** Create a boolean array, where each index will represent wether the (i+low)th element is present in array or not. Mark all those elements which are in the given range and are present in the array. Once all array items, present in given range have been marked true in the array we traverse through the boolean array and print all elements whose value is false.

    ## C ++

    ```

    // An array based C++ program 
    // to find missing elements from 
    // an array 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Print all elements of range 
    // [low, high] that are not present 
    // in arr[0..n-1] 
    void printMissing( 
        int arr[], int n, 
        int low, int high) 
    { 
        // Create boolean array of size 
        // high-low+1, each index i representing 
        // wether (i+low)th element found or not. 
        bool points_of_range[high - low + 1] = { false }; 

        for (int i = 0; i < n; i++) { 
            // if ith element of arr is in 
            // range low to high then mark 
            // corresponding index as true in array 
            if (low <= arr[i] && arr[i] <= high) 
                points_of_range[arr[i] - low] = true; 
        } 

        // Traverse through the range and 
        // print all elements  whose value 
        // is false 
        for (int x = 0; x <= high - low; x++) { 
            if (points_of_range[x] == false) 
                cout << low + x << " "; 
        } 
    } 

    // Driver program 
    int main() 
    { 
        int arr[] = { 1, 3, 5, 4 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        int low = 1, high = 10; 
        printMissing(arr, n, low, high); 
        return 0; 
    } 

    // This code is contributed by Shubh Bansal 

    ```

    ## 爪哇

    ```

    // An array based Java program 
    // to find missing elements from 
    // an array 

    import java.util.Arrays; 

    public class Print { 
        // Print all elements of range 
        // [low, high] that are not present 
        // in arr[0..n-1] 
        static void printMissing( 
            int arr[], int low, 
            int high) 
        { 
            // Create boolean array of 
            // size high-low+1, each index i 
            // representing wether (i+low)th 
            // element found or not. 
            boolean[] points_of_range = new boolean
                [high - low + 1]; 

            for (int i = 0; i < arr.length; i++) { 
                // if ith element of arr is in 
                // range low to high then mark 
                // corresponding index as true in array 
                if (low <= arr[i] && arr[i] <= high) 
                    points_of_range[arr[i] - low] = true; 
            } 

            // Traverse through the range and print all 
            // elements whose value is false 
            for (int x = 0; x <= high - low; x++) { 
                if (points_of_range[x] == false) 
                    System.out.print((low + x) + " "); 
            } 
        } 

        // Driver program to test above function 
        public static void main(String[] args) 
        { 
            int arr[] = { 1, 3, 5, 4 }; 
            int low = 1, high = 10; 
            printMissing(arr, low, high); 
        } 
    } 

    // This code is contributed by Shubh Bansal 

    ```

    ## Python3

    ```

    # n array-based Python 3 program to  
    # find missing elements from an array  

    # Print all elements of range  
    # [low, high] that are not 
    # present in arr[0..n-1]  
    def printMissing(arr, n, low, high): 

        # Create boolean list of size  
        # high-low+1, each index i  
        # representing wether (i+low)th 
        # element found or not. 
        points_of_range = [False] * (high-low+1)  

        for i in range(n) : 
            # if ith element of arr is in range 
            # low to high then mark corresponding 
            # index as true in array 
            if ( low <= arr[i] and arr[i] <= high ) :  
                points_of_range[arr[i]-low] = True

        # Traverse through the range  
        # and print all elements  whose value 
        # is false 
        for x in range(high-low+1) : 
            if (points_of_range[x]==False) :  
                print(low+x, end = " ") 

    # Driver Code  
    arr = [1, 3, 5, 4] 
    n = len(arr) 
    low, high = 1, 10
    printMissing(arr, n, low, high) 

    # This code is contributed  
    # by Shubh Bansal 

    ```

    **输出：**

    ```
    2 6 7 8 9 10 
    ```

3.  **Use Hashing :** Create a hash table and insert all array items into the hash table. Once all items are in hash table, traverse through the range and print all missing elements.

    ## C ++

    ```

    // A hashing based C++ program to find missing 
    // elements from an array 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Print all elements of range [low, high] that 
    // are not present in arr[0..n-1] 
    void printMissing(int arr[], int n, int low, 
                      int high) 
    { 
        // Insert all elements of arr[] in set 
        unordered_set<int> s; 
        for (int i = 0; i < n; i++) 
            s.insert(arr[i]); 

        // Traverse throught the range an print all 
        // missing elements 
        for (int x = low; x <= high; x++) 
            if (s.find(x) == s.end()) 
                cout << x << " "; 
    } 

    // Driver program 
    int main() 
    { 
        int arr[] = { 1, 3, 5, 4 }; 
        int n = sizeof(arr) / sizeof(arr[0]); 
        int low = 1, high = 10; 
        printMissing(arr, n, low, high); 
        return 0; 
    } 

    ```

    ## 爪哇

    ```

    // A hashing based Java program to find missing 
    // elements from an array 

    import java.util.Arrays; 
    import java.util.HashSet; 

    public class Print { 
        // Print all elements of range [low, high] that 
        // are not present in arr[0..n-1] 
        static void printMissing(int ar[], int low, int high) 
        { 
            HashSet<Integer> hs = new HashSet<>(); 

            // Insert all elements of arr[] in set 
            for (int i = 0; i < ar.length; i++) 
                hs.add(ar[i]); 

            // Traverse throught the range an print all 
            // missing elements 
            for (int i = low; i <= high; i++) { 
                if (!hs.contains(i)) { 
                    System.out.print(i + " "); 
                } 
            } 
        } 

        // Driver program to test above function 
        public static void main(String[] args) 
        { 
            int arr[] = { 1, 3, 5, 4 }; 
            int low = 1, high = 10; 
            printMissing(arr, low, high); 
        } 
    } 

    // This code is contributed by Rishabh Mahrsee 

    ```

    ## Python3

    ```

    # A hashing based Python 3 program to  
    # find missing elements from an array  

    # Print all elements of range  
    # [low, high] that are not 
    # present in arr[0..n-1]  
    def printMissing(arr, n, low, high): 

        # Insert all elements of  
        # arr[] in set  
        s = set(arr) 

        # Traverse through the range  
        # and print all missing elements  
        for x in range(low, high + 1): 
            if x not in s: 
                print(x, end = ' ') 

    # Driver Code  
    arr = [1, 3, 5, 4] 
    n = len(arr) 
    low, high = 1, 10
    printMissing(arr, n, low, high) 

    # This code is contributed  
    # by SamyuktaSHegde  

    ```

    ## C＃

    ```

    // A hashing based C# program to 
    // find missing elements from an array 
    using System; 
    using System.Collections.Generic; 

    class GFG { 

        // Print all elements of range 
        // [low, high] that are not 
        // present in arr[0..n-1] 
        static void printMissing(int[] arr, int n, 
                                 int low, int high) 
        { 
            // Insert all elements of arr[] in set 
            HashSet<int> s = new HashSet<int>(); 
            for (int i = 0; i < n; i++) { 
                s.Add(arr[i]); 
            } 

            // Traverse throught the range 
            // an print all missing elements 
            for (int x = low; x <= high; x++) 
                if (!s.Contains(x)) 
                    Console.Write(x + " "); 
        } 

        // Driver Code 
        public static void Main() 
        { 
            int[] arr = { 1, 3, 5, 4 }; 
            int n = arr.Length; 
            int low = 1, high = 10; 
            printMissing(arr, n, low, high); 
        } 
    } 

    // This code is contributed by ihritik 

    ```

    **Output:**

    ```
    2 6 7 8 9 10 
    ```

**哪种方法更好？**
第一种方法的时间复杂度为 O（nLogn + k），其中 k 是丢失元素的数量（请注意，如果数组较小且范围较大，则 k 可能大于 nLogn）

第二个和第三个解决方案的时间复杂度为 O（n +（high-low + 1））。

如果给定的数组几乎具有范围内的元素，即 n 接近（high-low + 1）的值，则第二和第三种方法肯定更好，因为没有 Log n 因子。 但是，如果 n 小于范围，则第一种方法会更好，因为它不需要用于散列的额外空间。 我们还可以修改第一种方法以将相邻的缺失元素打印为范围以节省时间。 例如，如果缺少 50、51、52、53、54、59，我们可以在第一种方法中将它们打印为 50-54、59。 如果允许以这种方式打印，则第一种方法仅需要 O（n Log n）时间。

在第二和第三解决方案之外，第二解决方案更好，因为第二种解决方案在最坏情况下的时间复杂度要比第三种更好。

本文由 **Piyush Gupta** 和 **Shubh Bansal** 贡献。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。