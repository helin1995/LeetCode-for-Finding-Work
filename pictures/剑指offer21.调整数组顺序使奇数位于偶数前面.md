## 题目描述
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部
分，所有偶数位于数组的后半部分。
## 示例
```
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```
## 方法：双指针
```
class Solution:
    def exchange(self, nums: List[int]) -> List[int]:
        if nums == []:
            return []
        lp, rp = -1, len(nums)
        cur = 0
        while cur < rp:
            if nums[cur] & 1:  # 等价于nums[cur] % 2 == 1，即判断nums[cur]是否为奇数
                lp += 1
                cur += 1
            else:
                self.swap(nums, cur, rp-1)
                rp -= 1
        return nums
    
    def swap(self, nums, i, j):
        temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp
```