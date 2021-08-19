## 方法1：基于快速排序中的partition
```
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        if arr == [] or k == 0:
            return []
        if k == len(arr):
            return arr
        # m = self.partition(arr, 0, len(arr))
        # return m, arr
        self.quickSelect(arr, 0, len(arr), k)
        return arr[:k]

    def  quickSelect(self, arr, low, high, k):
        m = self.partition(arr, low, high)
        if m == k:
            return 
        elif m > k:
            self.quickSelect(arr, low, m, k)
        else:
            self.quickSelect(arr, m+1, high, k)

    
    def partition(self, arr, low, high):
        target = arr[high-1]
        lb, rb, i = low-1, high, low
        while i < rb:
            if arr[i] > target:
                self.swap(arr, i, rb-1)
                rb -= 1
            elif arr[i] == target:
                i += 1
            else:
                self.swap(arr, lb+1, i)
                lb += 1
                i += 1
        return i-1

    
    def swap(self, arr, i, j):
        temp = arr[i]
        arr[i] = arr[j]
        arr[j] = temp
```

## 方法2：堆
```
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        if arr == [] or k == 0:
            return []
        if k == len(arr):
            return arr
        res = [-x for x in arr[:k]]
        heapq.heapify(res)
        for n in range(k, len(arr)):
            if -res[0] > arr[n]:
                heapq.heappop(res)
                heapq.heappush(res, -arr[n])
        return [-x for x in res]
```