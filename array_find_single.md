## 从数组中找出只出现一次的数字（其余的都出现两次）

题目描述：

Given an array of integers, every element appears twice except for one. Find that single one.

Note:Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

利用异或：两个相同的数异或结果为0，不同为1

假如数组为［2，3，2，3，4，1，4］

2^3 = 0000 0010 ^ 0000 0011 = 0000 0001   1

1^2 = 0000 0001 ^ 0000 0010 = 0000 0011   3

3^3 = 0000 0011 ^ 0000 0011 = 0000 0000   0

0^4 = 0000 0000 ^ 0000 0100 = 0000 0100   4

4^1 = 0000 0100 ^ 0000 0001 = 0000 0101   5

5^4 = 0000 0101 ^ 0000 0100 = 0000 0001   1

最后的结果为1，也就是数组中单个的1

```java
public int singleNumber(int[] A){
    int val = 0;
    for(int i = 0; i < A.length; i ++){
        val ^=A[i];
    }
    
    reutn val;
}
```
若数组为空，返回0处理。
