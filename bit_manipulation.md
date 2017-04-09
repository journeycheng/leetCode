### 191.二进制中1的个数

- 问题描述：给定一个非负整数(32bit)，返回这个数的二进制中1的个数（也称作"汉明权重"）。

```python
def hammingWeight(n):
    result = 0
    while n != 0:
        if n & 1:
            result += 1
        n = n>> 1
    return result
```

- 主要思想：
  - 整数和1进行"与"操作，如果等于0，说明最后一位是0，反之，说明最后一位是1。
  - 整数右移一位
  
  
### 190.二进制数反转

- 问题描述：给定一个无符号整数(32bit)，转换为二进制表示，将该二进制数反转，返回二进制数反转后表示的整数。

```python
def reverseBits(n):
    if n == 0:
        return 0
    result = 0
    for i in range(0, 32):
        result <<= 1
        result += (n & 1)
        n >>= 1
    return result
```

- 主要思想：
  - result左移一位用来加上整数的最后一位
  - 整数右移一位
  
  
### 136.单独出现的数

- 问题描述：给定一个整数数组，除了一个元素，其他的都出现两次。找出那个单独出现的数。

```python
def singleNumber(nums):
    return reduce(lambda x, y: x ^ y, nums)
```
- 主要思想：
  - 利用异或的性质，相同为0，不同为1
  - 相同的数异或结果为0，0与任何数异或等于该数本身
  
### 268.缺失的数

- 问题描述：给定一个数组[0, 1, 2,..., n]。找出0-n中缺失的数。例如nums = [0, 1, 3]，缺失的数是2

```python
def missingNumber(nums):
    result = 0
    for i in range(len(nums)):
        result = result ^ i ^ nums[i]
    return result ^ len(nums)
```

- 主要思想：利用索引值、原数组和数组长度，将这个问题转化为“单独出现的数”问题

### 338.统计连续数值的数组中各个元素二进制的个数

- 问题描述：给定一个非负整数num，计算i（0 <=i<=num）的二进制中1的个数，结果以数组形式返回

```python
def countBits(num):
    result = [0] * num
    for i in range(1, num+1):
        result[i] = result[i >> 1] + (i & 1)
    return result
```
- 主要思想：
  - 找出规律，类似于斐波那契数列的非递归实现
  - 位操作的优先级低于四则运算

### 421.数组两个元素异或的最大值

- 问题描述：给定一个非空数组，里面的元素是非负整数，找出其中两个元素异或的最大值






