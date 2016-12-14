题目描述


Given an array of integers, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.

You may assume that each input would have exactly one solution.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2

借助HashMap遍历一次，HashMap相当于python中的dictionary

HashMap方法汇总
```java
// 创建HashMap对象
HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();

// 判断是否包含某个key
map.containsKey(key);

// 增加一个键值对
map.put(key, value);

// 输出键为key的value
map.get(key);

//删除键为key的键值对
map.remove(key);

// 判断HashMap是否为空
map.empty();

// HashMap的键集合
map.keySet();

// 采用Iterator遍历HashMap
Iterator it = hashMap.keySet().iterator();
while(it.hasNext()){
    int key = it.next();
    int val = map.get(key);
}
```


```java
import java.util.HashMap;
public class solution{
    public int[] twoSum(int[] numbers, int target){
        int n = numbers.length;
        int[] result = new int[2];
        
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i = 0; i < n; i ++){
            if(map.containsKey(target - numbers[i])){
                result[0] = map.get(target - numbers[i]) + 1;
                result[1] = i + 1;
                break;
            }else{
                map.put(numbers[i], i);
            }
        }
        return result;
    }
}
```
