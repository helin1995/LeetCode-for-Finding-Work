## 题目描述：
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每
个数字重复了几次。请找出数组中任意一个重复的数字。

## 示例1：
```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：
2 或 3
```

## 方法1：先排序，然后遍历数组，找出重复的数字（判断相邻两个数字是否相等），O(nlogn)、O(1)
## 代码：
```
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        # 方法1：先排序，然后遍历数组，找出重复的数字（判断相邻两个数字是否相等），O(nlogn)、O(1)
        nums.sort()  # 快速排序
        for i in range(len(nums)-1):
            if nums[i] == nums[i+1]:
                return nums[i]
        return -1
```
## 方法2：哈希表，遍历数组，如果当前数字在哈希表中，那么返回这个数字，否则就将这个数字加入哈希表。O(n)、O(n)
## 代码：
```
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        d = {}
        for n in nums:
            if n in d.keys():
                return n
            else:
                d[n] = 1
        return -1
```
## 方法3：O(n)、O(1)
根据题目给的信息：长度为n的数组，其中元素的范围是0~n-1，那么当数组中没有重复的元素时，对数组进行排序，结果就是数组下标
i和该下标对应的元素相等，即i=num[i]。所以，我们可以对数组进行排列，就是将nums[i]进行调整，将其放在i位置上。当i=nums[i]
时，就遍历下一个元素；如果i!=num[i]，就先检查下标为nums[i]的元素是否等于nums[nums[i]]，如果相等，则nums[i]重复，返回
nums[i]；如果不等，就交换下标为i和下标为nums[i]对应的元素。这种方法相当于对数组进行排序。
## 代码：
```
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        i = 0
        while i < len(nums):
            if i == nums[i]:
                i += 1
                continue
            if nums[nums[i]] == nums[i]:
                return nums[i]
            else:
                j = nums[i]
                nums[i], nums[j] = nums[j], nums[i]
        return -1
```