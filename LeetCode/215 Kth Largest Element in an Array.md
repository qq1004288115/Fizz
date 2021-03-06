```
from random import randint
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        n = len(nums)
        l, r = 0, n - 1
        while l <= r:
            index = self.partition(l, r, nums)
            if index == n - k:
                return nums[index]
            elif index < n - k:
                l = index + 1
            else:
                r = index - 1       
    def partition(self, l, r, nums):
        ind = randint(l, r)
        val = nums[ind]
        nums[ind], nums[r] = nums[r], nums[ind]
        index = l - 1
        for i in range(l, r):
            if nums[i] < val:
                index += 1
                if index != i:
                    nums[index], nums[i] = nums[i], nums[index]
        index += 1
        nums[r], nums[index] = nums[index], nums[r]
        return index
```

## Leetcode
```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return sorted(nums)[len(nums) - k]
```

```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return heapq.nlargest(k, nums)[-1]
```
