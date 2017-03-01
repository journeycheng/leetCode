# leetCode

## 数组

[1. 快排](https://github.com/journeycheng/leetCode/blob/master/array_quick_sort.md)

[2. 归并排序](https://github.com/journeycheng/leetCode/blob/master/array_merge_sort.md)

[3. 堆排序](https://github.com/journeycheng/leetCode/blob/master/array_heap_sort.md)

[4. 二分查找](https://github.com/journeycheng/leetCode/blob/master/array_binary_search.md)

[5. 找出唯一的单个元素](https://github.com/journeycheng/leetCode/blob/master/array_find_single.md)

[6. two sum](https://github.com/journeycheng/leetCode/blob/master/array_two_sum.md)


## 链表

[1. 链表的插入排序](https://github.com/journeycheng/leetCode/blob/master/linkedList_insertion_sort.md)

[2. 链表的归并排序](https://github.com/journeycheng/leetCode/blob/master/linkedList_merge_sort.md)

[3. 链表的快速排序](https://github.com/journeycheng/leetCode/blob/master/linkedList_quick_sort.md)

[4. 合并有序链表](https://github.com/journeycheng/leetCode/blob/master/merge_sorted_linkedLists.md)

[5. 反转链表](https://github.com/journeycheng/leetCode/blob/master/reverse_linkedList.md)

[6. 判断链表中是否有环](https://github.com/journeycheng/leetCode/blob/master/judge_cycle_in_linkedList.md)


## 二叉树

[1. 二叉树的遍历打印](https://github.com/journeycheng/leetCode/blob/master/tree_print.md)

[2. 二叉树的遍历列表返回](https://github.com/journeycheng/leetCode/blob/master/tree_return.md)

[3. 二叉树的根节点到叶子节点的最少层数](https://github.com/journeycheng/leetCode/blob/master/tree_minimun_nodes_between_root_and_leaf.md)

[4. 数组转换为二叉树](https://github.com/journeycheng/leetCode/blob/master/array_to_tree.md)

[5. 二叉树是否存在根节点到叶子节点的和等于某个值](https://github.com/journeycheng/leetCode/blob/master/tree_path_sum.md)

[6. 平衡二叉树的判断](https://github.com/journeycheng/leetCode/blob/master/is_balanced_tree.md)

[7. 有序链表转换为二叉搜索树](https://github.com/journeycheng/leetCode/blob/master/sorted_linkedlist_2_BST.md)

[8. 有序数组转换为二叉搜索树](https://github.com/journeycheng/leetCode/blob/master/sorted_array_2_BST.md)



## 判断字符串的乱序排列

Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 

```java
public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if(strs == null || strs.length == 0) return null;
        
        Map<String, List<String>> map = new HashMap<String, List<String>>();
        Arrays.sort(strs);
        for(String s: strs){
            char[] cs = s.toCharArray();
            Arrays.sort(cs);
            String keyStr = String.valueOf(cs);
            
            if(!map.containsKey(keyStr)){
                map.put(keyStr,new ArrayList<String>());
            }
            map.get(keyStr).add(s);
        }
        
        return new ArrayList<List<String>>(map.values());
    }
}
```

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,

s = "anagram", t = "nagaram", return true.

s = "rat", t = "car", return false.

Note:You may assume the string contains only lowercase alphabets.

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] alphabet_count = new int[26];
        for(int i=0; i<s.length(); i++) alphabet_count[s.charAt(i) - 'a']++;
        for(int i=0; i<t.length(); i++) alphabet_count[t.charAt(i) - 'a']--;
        for(int i: alphabet_count){
            if(i != 0) return false;
        }
        return true;
    }
}
```

## 数值计算
#### pow(x,n) tag: 二分搜索、数学

```java
public class Solution {
    public double myPow(double x, int n) {
        if(n==0) return 1;
        if(n<0){
            return 1/(x * myPow(x, -(n+1))); 
        }
        return n%2==0 ? myPow(x*x, n/2) : x*myPow(x*x, n/2);
    }
}
```
int的范围是(-2^32, 2^32-1)，也就是(-2147483648, 2147483647)。如果是INT_MIN直接取反的话，会出现溢出的情况。

#### sqrt(int x) tag: 二分搜索、数学

{\mbox{isqrt}}(n)=\lfloor {\sqrt  n}\rfloor .

root^2 <= x < (root+1)^2

```java
public class Solution {
    public int mySqrt(int x) {
        if(x == 0) return 0;
        int left = 1, right = x;
        while(true){
            int mid = (left + right)/2;
            if(mid > x/mid){
                right = mid - 1;
            }else{
                if(mid+1 > x/(mid+1)){
                    return mid;
                }
                left = mid + 1;
            }
        }
    }
}
```

#### valid Perfect Square, tag: 二分搜索、数学

Given a positive integer num, write a function which returns True if num is a perfect square else False.

16-> true, 14-> false

This is a math problem：

1 = 1

4 = 1 + 3

9 = 1 + 3 + 5

16 = 1 + 3 + 5 + 7

so 1+3+...+(2n-1) = (2n-1 + 1)n/2 = nn

```java
public class Solution {
    public boolean isPerfectSquare(int num) {
        if(num == 0) return false;
        
        int i = 1;
        while(num > 0){
            num -= i;
            i += 2;
        }
        return num == 0;
    }
}
```
时间复杂度为O(sqrt(n))



## 动态规划

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];   //dp[i] means the maximum subarray ending with A[i]
        dp[0] = nums[0];
        int max = dp[0];
        
        for(int i=1; i<n; i++){
            dp[i] = nums[i] + (dp[i-1]>0? dp[i-1]:0);
            max = Math.max(max, dp[i]);
        }
        
        return max;
    }
}
```


## 矩阵顺时针螺旋读取

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

return [1,2,3,6,9,8,7,4,5].

```java
public class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> result = new ArrayList<>();
        
        if (matrix == null || matrix.length == 0) return result;
        
        int top = 0;
        int botton = matrix.length - 1;
        int left = 0;
        int right  = matrix[0].length - 1;
        
        while(true){
            for(int i=left; i<=right; i++){
                result.add(matrix[top][i]);
            }
            if (check_finish(top, botton, left, right)){
                break;
            }
            top ++;
            
            for(int i=top; i<=botton; i++){
                result.add(matrix[i][right]);
            }
            if (check_finish(top, botton, left, right)){
                break;
            }
            right --;
            
            for(int i=right; i>=left; i--){
                result.add(matrix[botton][i]);
            }
            if (check_finish(top, botton, left, right)){
                break;
            }
            botton --;
            
            for(int i=botton; i>=top; i--){
                result.add(matrix[i][left]);
            }
            if (check_finish(top, botton, left, right)){
                break;
            }
            left ++;
        }
        
        return result;
    }
    
    public boolean check_finish(int top, int botton, int left, int right){
        if(top > botton || left > right){
            return true;
        }else{
            return false;
        }
    }
}
```

