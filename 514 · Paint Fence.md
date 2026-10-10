514 · Paint Fence
問題: https://www.lintcode.com/problem/514/
（leetcodeの代替）

You are painting a fence of n posts with k different colors. You must paint the posts following these rules:

Every post must be painted exactly one color.
There cannot be three or more consecutive posts with the same color.
Given the two integers n and k, return the number of ways you can paint the fence.

Example 1:
Input: n = 3, k = 2
Output: 6
Explanation: All the possibilities are shown.
Note that painting all the posts red or all the posts green is invalid because there cannot be three posts in a row with the same color.

Example 2:
Input: n = 1, k = 1
Output: 1

Example 3:
Input: n = 7, k = 2
Output: 42

Constraints:

1 <= n <= 50
1 <= k <= 10^5
The testcases are generated such that the answer is in the range [0, 2^31 - 1] for the given n and k.

---
https://github.com/olsen-blue/Arai60/pull/30/changes
を読んで真似した。

step3 pass
```py
def num_ways(self, n: int, k: int) -> int:
        if n == 1:
            return k
        if n == 2:
            return k * k
        
        num_ways = [0] * n
        num_ways[0] = k
        num_ways[1] = k * k
        for i in range(2, n):
            num_ways[i] = (k - 1) * (num_ways[i - 1] + num_ways[i - 2])
        return num_ways[n - 1]
```
for文で回しているので時間計算量O(n)、n <= 50なので時間は問題ない。
空間計算量もO(n)

最初、最後2つが同じ状態のときと、異なる色の状態の2つの状態を定義して考えたが、
olsen-blueさんのように一気に総数から直接考えた方が早いしコードも簡潔なのでこのやり方にした。

キャッシュを用いたやり方とキャッシュ自作は今度やりたい

