## 代码
```
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.bigheap = []
        self.smallheap = []
        heapq.heapify(self.bigheap)
        heapq.heapify(self.smallheap)


    def addNum(self, num: int) -> None:
        # 初始化
        if len(self.bigheap) == 0:
            heapq.heappush(self.bigheap, -num)
        else:
            # 如果当前的数小于等于大根堆的堆顶，则入大根堆；否则入小根堆
            if num <= -self.bigheap[0]:
                heapq.heappush(self.bigheap, -num)
            else:
                heapq.heappush(self.smallheap, num)
        # 比较两个堆的大小是否相差超过或等于2，则将较大堆的堆顶弹出，放入较小的堆
        if len(self.bigheap) - len(self.smallheap) >= 2:
            heapq.heappush(self.smallheap, -heapq.heappop(self.bigheap))
        if len(self.smallheap) - len(self.bigheap) >= 2:
            heapq.heappush(self.bigheap, -heapq.heappop(self.smallheap))


    def findMedian(self) -> float:
        if len(self.bigheap) > len(self.smallheap):
            return -self.bigheap[0]
        elif len(self.bigheap) < len(self.smallheap):
            return self.smallheap[0]
        else:
            return (-self.bigheap[0] + self.smallheap[0]) / 2



# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```