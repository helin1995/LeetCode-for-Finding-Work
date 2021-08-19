## 方法1：暴力解法，但是超时了
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # 暴力解法，超时了
        if nums == []:
            return 0
        res = -float(inf)
        for i in range(len(nums)):
            maxSum = nums[i]
            if maxSum > res:
                res = maxSum
            for j in range(i+1, len(nums)):
                maxSum += nums[j]
                if maxSum > res:
                    res = maxSum 
        return res
```

## 方法2：动态规划
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        if not nums:
            return 0
        dp = [-float(inf)] * len(nums)
        dp[0] = nums[0]
        for i in range(1, len(nums)):
            if dp[i-1] > 0:
                dp[i] = dp[i-1] + nums[i]
            else:
                dp[i] = nums[i]
        return max(dp)
```