## 题目描述
给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），
每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大
乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的
最大乘积是18。
## 示例1
```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```
## 示例2
```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```
## 方法1：数学方法推导
每一段绳子被切分成3的时候，每段绳子的长度乘积最大。
## 代码：
```
# # 数学方法推导
class Solution:
    def cuttingRope(self, n: int) -> int:
        if n == 2:
            return 1
        if n == 3:
            return 2
        m = n // 3
        s = n % 3
        if s == 0:
            return  int(math.pow(3, m))
        elif s == 1:
            return  int(math.pow(3, m-1) * 4)
        else:
            return int(math.pow(3, m) * 2)
```
## 方法2：动态规划
1、我们想要求长度为n的绳子剪掉后的最大乘积，可以从前面比n小的绳子转移而来
2、用一个dp数组记录从0到n长度的绳子剪掉后的最大乘积，也就是dp[i]表示长度为i的绳子
剪成m段后的最大乘积，初始化dp[2] = 1
3、我们先把绳子剪掉第一段（长度为j），如果只剪掉长度为1，对最后的乘积无任何增益，
所以从长度为2开始剪
4、剪了第一段后，剩下(i - j)长度可以剪也可以不剪。如果不剪的话长度乘积即为
j * (i - j)；如果剪的话长度乘积即为j * dp[i - j]。取两者最大值max(j * (i - j), j * dp[i - j])
5、第一段长度j可以取的区间为[2,i)，对所有j不同的情况取最大值，因此最终dp[i]的转
移方程为 dp[i] = max(dp[i], max(j * (i - j), j * dp[i - j]))
6、最后返回dp[n]即可
## 代码
```
class Solution:
    def cuttingRope(self, n: int) -> int:
        ## 动态规划
        dp = [0] * (n+1)
        dp[2] = 1
        for i in range(3, n+1):
            temp = 0
            for j in range(2, i):
                temp = max(temp, max(j * (i-j), j * dp[i-j]))
            dp[i] = temp
        return dp[n]
```