# 查找每个雇员下的雇员人数

> 原文：[https://www.geeksforgeeks.org/find-number-of-employees-under-every-manager/](https://www.geeksforgeeks.org/find-number-of-employees-under-every-manager/)

给定一个字典，其中包含员工及其经理作为许多（雇员，经理）对的映射，如下所示。

```
{ "A", "C" },
{ "B", "C" },
{ "C", "F" },
{ "D", "E" },
{ "E", "F" },
{ "F", "F" } 

In this example C is manager of A, 
C is also manager of B, F is manager 
of C and so on.

```

编写一个函数以使层次结构中每个经理下的员工人数不只是他们的直接报表。 可以假设一名员工仅直接向一位经理报告。 在上面的词典中，根节点/ ceo 被列为对自己的报告。

输出应为包含以下内容的字典。

```
A - 0  
B - 0
C - 2
D - 0
E - 1
F - 5 
```

资料来源：微软面试。

这个问题可能会以不同的方式解决，但是我遵循了这个问题，发现很有趣，因此分享：

```
 1\. Create a reverse map with Manager->DirectReportingEmployee 
    combination. Off-course employee will be multiple so Value 
    in Map is List of Strings.
        "C" --> "A", "B",
        "E" --> "D" 
        "F" --> "C", "E", "F"

2\. Now use the given employee-manager map to iterate  and at 
   the same time use newly reverse map to find the count of 
   employees under manager.

   Let the map created in step 2 be 'mngrEmpMap' 
   Do following for every employee 'emp'.
     a) If 'emp' is not present in 'mngrEmpMap' 
          Count under 'emp' is 0 [Nobody reports to 'emp']
     b) If 'emp' is present in 'mngrEmpMap' 
          Use the list of direct reports from map 'mngrEmpMap'
          and recursively calculate number of total employees
          under 'emp'. 
```

步骤 2.b 中的一个技巧是使用记忆（动态规划），同时查找经理下的员工人数，这样我们就无需为任何一名员工再次找到员工人数。 在下面的代码中，`populateResultUtil()`是使用备忘录的递归函数，以避免对相同结果进行重新计算。

以下是上述想法的 Java 实现：

```
// Java program to find number of persons under every employee
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
[
public class NumberEmployeeUnderManager
{
// A hashmap to store result. It stores count of employees
// under every employee, the count may by 0 also
static Map<String,Integer> result =
new HashMap<String, Integer>();
// Driver function
public static void main(String[] args)
{
Map<String, String> dataSet = new HashMap<String, String>();
dataSet.put( "A" , "C" );
dataSet.put( "B" , "C" );
dataSet.put( "C" , "F" );
dataSet.put( "D" , "E" );
dataSet.put( "E" , "F" );
dataSet.put( "F" , "F" );
populateResult(dataSet);
System.out.println( "result = " + result);
}
// This function populates 'result' for given input 'dataset'
private static void populateResult(Map<String, String> dataSet)
{
// To store reverse of original map, each key will have 0
// to multiple values
Map<String, List<String>> mngrEmpMap =
new HashMap<String, List<String>>();
// To fill mngrEmpMap, iterate through the given map
for (Map.Entry<String,String> entry: dataSet.entrySet())
{
String emp = entry.getKey();
String mngr = entry.getValue();
if (!emp.equals(mngr)) // excluding emp-emp entry
[H T G118] {
// Get the previous list of direct reports under
// current 'mgr' and add the current 'emp' to the list
List<String> directReportList = mngrEmpMap.get(mngr);
// If 'emp' is the first employee under 'mgr'
if (directReportList == null )
{
directReportList = new ArrayList<String>();
// add a new entry for the mngr with empty directReportList
mngrEmpMap.put(mngr, directReportList);
}
directReportList.add(emp);
}
}
// Now use manager-Emp map built above to populate result
// with use of populateResultUtil()
// note- we are iterating over original emp-manager map and
// will use mngr-emp map in helper to get the count ]
for (String mngr: dataSet.keySet())
populateResultUtil(mngr, mngrEmpMap);
}
// This is a recursive function to fill count for 'mgr' using
// mngrEmpMap.  This function uses memoization to avoid re-
// computations of subproblems.
private static int populateResultUtil(String mngr,
Map<String, List<String>> mngrEmpMap)
{
int count = 0 ;
// means employee is not a manager of any other employee
if (!mngrEmpMap.containsKey(mngr))
{
result.put(mngr, 0 );
return 0 ;
}
// this employee count has already been done by this
// method, so avoid re-computation
else if (result.containsKey(mngr))
count = result.get(mngr);
else
{
List<String> directReportEmpList = mngrEmpMap.get(mngr);
count = directReportEmpList.size();
for (String directReportEmp: directReportEmpList)
count +=  populateResultUtil(directReportEmp, mngrEmpMap);
result.put(mngr, count);
}
return count;
}
}
```

**输出**：

```
result = {A=0, B=0, C=2, D=0, E=1, F=5}

```

本文由 **Chandan Prakash** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

