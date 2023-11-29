#剑指 Offer 45. 把数组排成最小的数
<https://leetcode.cn/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/>

***
## 解题思路
1. 输入的数组是int 应该先转成str形式
2. 比较的实质就是 x+y 与 y+x 的大小 
   1. 如果 x+y > y+x，说明y应该放在x前面
   2. 反之，则说明x应该在y前面
3. 通过冒泡的方式，遍历整个数组，排序。就可以得到一个最小的密码。
4. 最后在用join得到题目需要的输出格式

****
## 代码实现：
````python
import functools

class Solution:
    def minNumber(self, nums: List[int]) -> str:
        def cmp(a, b):
            if a + b == b + a:
                return 0
            elif a + b > b + a:
                return 1
            else:
                return -1

        nums_s = list(map(str, nums))
        nums_s.sort(key=functools.cmp_to_key(cmp))
        return ''.join(nums_s)
````
````python
#map函数的用法，替代for循环遍历数组，代码更简洁。
map(function,list)
    #fucntion为map调用的函数
    #list为需要遍历的数组，对list中每一个元素进行function函数操作
````

这里使用了 functools.cmp_to_key 自定义排序函数。

````python
import functools
def cmp(a, b):
    if a + b == b + a:  # 
        return 0
    elif a + b > b + a:
        return 1        # 1 相反
    else:
        return -1       # -1 保持
````

##自己想法的代码实现
````python
class Solution:
    def crackPassword(self, password: List[int]) -> str:
        nums = []
        for i in range(len(password)):
            nums.append(str(password[i]))

        for i in range(len(password)):
            for j in range(i, len(password)):
                if nums[i] + nums[j] < nums[j] + nums[i]:
                    continue
                else:
                    nums[i], nums[j] = nums[j], nums[i]

        return ''.join(nums)
````

思路与题解相同，代码实现不同。
1. 题解使用map函数替代了for循环，代码更简洁
2. 题解使用了functools函数包中的functools.cmp_to_key 自定义函数排序，替代了冒泡排序。
3. 题解在用时上48ms > 60ms，运行时间更快。
***


