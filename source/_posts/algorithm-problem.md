---
title: 算法
date: 2018-07-08 22:56:24
categories:
- Algorithm
tags:
- Algorithm Problem
- leetcode
- Python
- JavaScript
copyright: true
---

# 两数之和

给定一个整数数组和一个目标值，找出数组中和为目标值的两个数。

**你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。**

```py

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```
返回的是他们的索引值。

## 解决方案

这里的假设是成立的，所以不用考虑数据是否会重复这些杂七杂八的。

### 暴力法

遍历每个元素` x`，并查找是否存在一个值与 `target - x` 相等的目标元素。

#### Python 实现方式

```py

def twoSum(self, nums, target):
       """
       :type nums: List[int]
       :type target: int
       :rtype: List[int]
       """
       nums_len = len(nums)
        for i in range(nums_len):
            for j in range(i+1, nums_len):
                if nums[i] + nums[j] == target:
                    # l = []
                    # l.append(i)
                    # l.append(j)
                    return [i, j]

```

#### JavaScript 实现方式

```js

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    len = nums.length;
    for(let i = 0; i < len; i++) {

        for(let j = i + 1; j < len; j++){
            if (nums[i] + nums[j] === target) {
                return [i, j];
            }
        }
    }
    return l;
};

// let nums = [2, 7, 11, 15, 3, 6, 4, 5];

// let result = twoSum(nums, 9)

// console.log(result)
```

以上实现过程通过对每一个元素，进行剩余元素进行依依匹配，直到匹配成功的两层循环遍历得已解决。其时间复杂度就是 O(n^2) 不考虑其低阶和常数项的影响。其时间复杂度就不是很可观了。


### 利用哈希表

通过哈希将原数组元素和索引对应关联起来从而达到找到目标元素快速找出他的索引，并且哈希表支持以近似恒定的时间进行快速查找，可以将查找时间从 O(n) 降低到 O(1)。

#### Python

Python 中的字典数据类型就是 Hash 表实现的。

```py
    def twoSum(self, nums, target):
          """
          :type nums: List[int]
          :type target: int
          :rtype: List[int]
          """
          # 创建字典，列表值为key，索引为 value
          nums_dict = { nums[i]: i for i in range(len(nums)) }
          for i in range(len(nums)):
          	   # 更具目标值，求出剩余值
               complement = target - nums[i]
               # 查看字典是否有符合的
               if nums_dict.get(complement) and nums_dict.get(complement) != i:
                   return [i, nums_dict.get(complement)]
```

这里还是使用了两次 for 循环，但却是一维的，时间复杂度也相对变成了 O(n)
