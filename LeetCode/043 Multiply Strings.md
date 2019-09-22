```
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        l = [0] * (len(num1)+len(num2))
        for i in range(len(num1)-1, -1, -1):
            for j in range(len(num2)-1, -1, -1):
                a = (ord(num1[i]) - ord('0'))
                b = (ord(num2[j]) - ord('0'))
                l[i+j] += (a * b) // 10
                l[i+j+1] += (a * b) % 10
        for i in range(len(l)-1, 0, -1):
            if l[i] > 9:
                l[i-1] += l[i] // 10
                l[i] = l[i] % 10
        res = ''.join(map(str, l)).lstrip('0')
        return res or '0'
```
                
## Leetcode
```
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        m, n = len(num1), len(num2)
        pos = [0] * (m + n)
        for i in range(m - 1, -1, -1):
            for j in range(n - 1, -1, -1):
                tmp = (ord(num1[i]) - ord('0')) * (ord(num2[j]) - ord('0'))
                p1, p2 = i + j, i + j + 1
                s = pos[p2] + tmp
                pos[p1] += s // 10
                pos[p2] = s % 10
        ans = ''.join(map(str, pos)).lstrip('0')
        return ans if ans else '0'
```