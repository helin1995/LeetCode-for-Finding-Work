## 题目描述
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的
数组的一个旋转，输出旋转数组的最小元素。例如，数组[3,4,5,1,2] 为 [1,2,3,4,5] 的
一个旋转，该数组的最小值为1。
## 示例1
```
输入：[3,4,5,1,2]
输出：1
```
```
输入：[2,2,2,0,1]
输出：0
```
## 思路
根据题意，旋转之后的数组分为两部分，第一部分是递增的，第二部分也是递增的，而且第一部分
的值都大于等于第二部分的值。所以，我们可以采用二分法的思路来解。这里有一个特例，就是将
0个元素旋转，那么整个数组整体是有序的。因此，最小值就是数组的第一个元素。
设p1和p2分别指向数组的两端，mid数组的中间元素。如果numbers[mid]>=numbers[p1]，
那么mid处于第一部分，此时最小值一定在mid的右边；
如果numbers[mid]<=numbers[p1]， 那么mid处于第二部分，此时最小值一定在mid的
左边。以上两种方法就可以缩小查找范围。然后继续执行上述过程，最后，p1会指向第一部分
最后一个元素，p2会指向第二部分的第一个元素，而且p1、p2紧挨着，p2指向的元素就是最小值。


但是，当p1、mid、p2指向的元素都相等时，就无法 判断最小值在哪一部分，所以此时只能
采用顺序查找，找出最小值。

## 代码
```
class Solution:
    def minArray(self, numbers: List[int]) -> int:
        if numbers == []:
            return None
        if numbers[0] < numbers[-1]:
            return numbers[0]
        p1, p2 = 0, len(numbers) - 1
        while (p2 - p1) != 1:
            mid = p1 + ((p2 - p1) >> 1)
            if numbers[mid] == numbers[p1] and numbers[mid] == numbers[p2]:
                return self.find_min(numbers, p1, p2)
            if numbers[mid] >= numbers[p1]:
                p1 = mid
                continue
            if numbers[mid] <= numbers[p2]:
                p2 = mid
                continue
        return numbers[p2]
    
    def find_min(self, numbers, p1, p2):
        min_val = numbers[p1]
        idx = p1
        while idx <= p2:
            if numbers[idx] < min_val:
                min_val = numbers[idx]
            idx += 1
        return min_val
```
