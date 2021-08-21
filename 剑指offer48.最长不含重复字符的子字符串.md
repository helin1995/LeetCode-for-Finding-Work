## 双指针
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:
            return 0
        slow = 0
        record = {s[0]: 0}
        fast = 1
        maxLen = 1
        while fast < len(s):
            if s[fast] in record.keys():
                maxLen = max(maxLen, fast - slow)
                pos = record[s[fast]]
                ## 删除当前左边界到重复元素之间的元素
                for i in range(slow, pos+1):
                    del record[s[i]]
                ## 更新左边界
                slow = pos + 1
            else:
                record[s[fast]] = fast
                fast += 1
        maxLen = max(maxLen, fast - slow)
        return maxLen
```