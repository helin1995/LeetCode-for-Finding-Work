## 代码
```
class Solution:
    def minNumber(self, nums: List[int]) -> str:
        res = ""
        nums = [str(n) for n in nums]
        for num in sorted(nums, key=cmp_to_key(self.compare)):
            res += num
        return res
    

    def compare(self, s1, s2):
        if s1 + s2 >= s2 + s1:
            return 1  # 升序
        else:
            return -1  # 降序
```