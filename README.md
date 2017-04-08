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

[7. 链表的相交起始点](https://github.com/journeycheng/leetCode/blob/master/intersection_of_2_linkedLists.md)


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

#### nuique paths

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

```java
public class Solution {
    public int uniquePaths(int m, int n) {
        Integer[][] map = new Integer[m][n];
        // 到达第一行或者第一列的任何位置都只有一种可能
        for(int i=0; i<m; i++){
            map[i][0] = 1;
        }
        for(int i=0; i<n; i++){
            map[0][i] = 1;
        }
        for(int i=1;i<m; i++){
            for(int j=1;j<n; j++){
                map[i][j] = map[i-1][j]+map[i][j-1];
            }
        }
        return map[m-1][n-1];
    }
}
```
#### unique path with obstacle

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```


```java
public class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        Integer[][] map = new Integer[m][n];
        int i = 0;
        for(; i<m; i++){
            if(obstacleGrid[i][0] == 1){
                break; 
            }
            map[i][0] = 1;
        }
        for(; i<m; i++){
            map[i][0] = 0;
        }
        
        i = 0;
        for(; i<n; i++){
            if(obstacleGrid[0][i] == 1){
                break;
            }
            map[0][i] = 1;
        }
        for(; i<n; i++){
            map[0][i] = 0;
        }
        
        for(i=1; i<m; i++){
            for(int j=1; j<n; j++){
                if(obstacleGrid[i][j] == 1){
                    map[i][j] = 0;
                }else{
                    map[i][j] = map[i-1][j] + map[i][j-1];
                }
            }
        }
        
        return map[m-1][n-1];
        
    }
}
```

#### miminum path sum
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

```java
public class Solution {
    public int minPathSum(int[][] grid) {
        if(grid == null || grid.length == 0) return 0;
        Integer[][] map = new Integer[grid.length][grid[0].length];
        map[0][0] = grid[0][0];
        
        for(int i=1; i<grid.length; i++){
            map[i][0] = map[i-1][0] + grid[i][0];
        }
        for(int i=1; i<grid[0].length; i++){
            map[0][i] = map[0][i-1] + grid[0][i];
        }
        
        for(int i=1; i<grid.length; i++){
            for(int j=1; j<grid[0].length; j++){
                map[i][j] = Math.min(map[i-1][j], map[i][j-1]) + grid[i][j];
            }
        }
        
        return map[grid.length-1][grid[0].length-1];
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

## 贪心

#### jump game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:

A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

```java
public class Solution {
    public boolean canJump(int[] nums) {
        int max = 0;
        for(int i=0; i<nums.length; i++){
            if(i>max) return false;
            max = Math.max(max, i+nums[i]);
        }
        return true;
    }
}
```

## 数组旋转

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

空间复杂度O(1)
```java
public class Solution {
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length-1);
        reverse(nums, 0, k-1);
        reverse(nums, k, nums.length-1);
    }
    
    public void reverse(int[] nums, int start, int end){
        while(start < end){
            int tmp = nums[start];
            nums[start] = nums[end];
            nums[end] = tmp;
            start ++;
            end --;
        }
    }
}
```

## 二进制相加

#### Add Binary

Given two binary strings, return their sum (also a binary string).

```java
public class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();
        int i = a.length() - 1, j = b.length() - 1, carry = 0;
        while(i>=0 || j>=0){
            int sum = carry;
            if(j >= 0) sum += b.charAt(j--) - '0';
            if(i >= 0) sum += a.charAt(i--) - '0';
            sb.append(sum%2);
            carry = sum/2;
        }
        
        if(carry != 0) sb.append(carry);
        return sb.reverse().toString();
    }
}
```
- StringBuilder用于构建字符串，append(), reverse(), toString()
- 字符串中的某个字符，charAt()

## 斐波那契数列

#### Climbing Stairs
You are climbing a stair case. It takes n(n>0) steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

```java
public class Solution {
    public int climbStairs(int n) {
        if(n == 1){
            return 1;
        }
        if(n == 2){
            return 2;
        }
        int[] result = new int[n];
        result[0] = 1;
        result[1] = 2;
        for(int i=2; i<n; i++){
            result[i] = result[i-1] + result[i-2];
        }
        return result[n-1];
    }
}
```

## 栈、队列
#### Simplify Path

Given an absolute path for a file (Unix-style), simplify it.

For example,
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"

```java
public class Solution {
    public String simplifyPath(String path) {
        Deque<String> stack = new LinkedList<>();
        Set<String> skip = new HashSet<>(Arrays.asList("..", ".", ""));
        for(String dir: path.split("/")){
            if(dir.equals("..") && !stack.isEmpty()) stack.pop();
            else if(!skip.contains(dir)) stack.push(dir);
        }
        String res = "";
        for(String dir: stack){
            res = "/" + dir + res;
        }
        
        return res.isEmpty()? "/" : res;
    }
}
```

- split将path分割，灵活的for循环
- 栈的pop(), push()，for遍历




