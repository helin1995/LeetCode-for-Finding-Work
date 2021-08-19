## 代码
```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        if nums == []:
            return None
        n = 1
        record = nums[0]
        for i in range(1, len(nums)):
            if n == 0:
                record = nums[i]
            if nums[i] != record:
                n -= 1
            else:
                n += 1
        return record
        # times = 0
        # for num in nums:
        #     if num == record:
        #         times += 1
        # if times > (len(nums) >> 1):
        #     return record
```