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
pow(x,n) tag：二分搜索、数学

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
int的范围是
