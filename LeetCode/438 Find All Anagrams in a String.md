```
from collections import Counter
class Solution:
    def findAnagrams(self, s, p):
        res = []
        l = len(p)
        pCounter = Counter(p)
        sCounter = Counter(s[:l-1])
        for i in range(l-1,len(s)):
            sCounter[s[i]] += 1  
            if sCounter == pCounter:    
                res.append(i-l+1)  
            temp = s[i - l + 1]
            sCounter[temp] -= 1  
            if sCounter[temp] == 0:
                del sCounter[temp]
        return res
```
## Leetcode
```
from collections import Counter
class Solution:
    def findAnagrams(self, s, p):
        ans = []
        d = Counter(p)
        ls, lp, ld = len(s), len(p), len(d)
        start, end = 0, 0
        while end < ls:
            val = s[end]
            if val in d:
                d[val] -= 1
                if d[val] == 0: ld -= 1
            end += 1
            while ld == 0:
                temp = s[start]
                if temp in d:
                    d[temp] += 1
                    if d[temp] > 0:
                        ld += 1
                if end - start == lp:
                    ans.append(start)
                start += 1
        return ans
```