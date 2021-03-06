# Statistic
    Total 12 Easy 12 Medium 0 Hard 0
    
## Two Sum
```python
def twoSum(self, nums, target):
    length = len(nums)
    for i in range(length-1):
        for j in range(i+1,length):
            if nums[i]+nums[j]==target:
                    return i,j
                    break

class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        length = len(nums)
        difdict= {}
        for i in range(length):
            if target - nums[i] in difdict:
                return [difdict[target - nums[i]],i]
            else:
                difdict[nums[i]] = i
```

 ## Jewels and stones
 ```python
 class Solution_1:
    def numJewelsInStones(self, J, S):
        """
        :type J: str
        :type S: str
        :rtype: int
        """
        num = 0
        for str_1 in J:
            if str_1 in S:
                for str_2 in S:
                    if str_2 == str_1:
                        num += 1
        return num
```

## Hamming Distance
version 1
```python
class Solution:
    def hammingDistance(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        x_ = bin(x).replace('0b','')
        y_ = bin(y).replace('0b','')
        len_x = len(x_)
        len_y = len(y_)
        if len_x!=len_y:
            if len_x>len_y:
                y_ = y_.zfill(len_x)
                length = len_x
            else:
                x_ = x_.zfill(len_y)
                length = len_y
        else:
            length = len_x
        count = 0
        for i in range(length):
            if x_[i]!=y_[i]:
                count += 1
        return count
 ```
version 2
```python
class Solution:
    def hammingDistance(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        return bin(x^y).count('1')
```

## Unique Email Addresses
version 1 76ms
```python
class Solution:
    def numUniqueEmails(self, emails):
        """
        :type emails: List[str]
        :rtype: int
        """
        count = 0
        act_emails = set({})
        for str in emails:
            pos = str.index('@')
            # print(pos)
            str_l = str[0: pos]
            str_r = str[pos+1:]
            pos_ = str_l.index('+')
            str_l = str_l[0:pos_]
            str_l = str_l.replace('.', '')
            act_emails.add(str_l+'@'+str_r)
        return len(act_emails)
```
## To Lower Case
version 1 48ms
```python
class Solution:
    def toLowerCase(self, str):
        """
        :type str: str
        :rtype: str
        """
        return str.lower()
```
method 2
```
using ord() to get ASC II number of the character 
then plus 32 to each for getting the lower case
chr() asc II => character
```

##  N-Repeated Element in Size 2N Array
version 1 112ms
```python
class Solution:
    def repeatedNTimes(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        length = len(A)
        half = 0.5 * length
        list_ = [0]*(max(A)+1)
        for _ in A:
            # print(_)
            list_[_] += 1
        return list_.index(half)
```
version 2 84ms
```python 
class Solution:
    def repeatedNTimes(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        return int((sum(A)-sum(set(A)))/(len(A)/2-1))
```
Offical solution 1 84ms:

collections.counter:A counter is a container that 

stores elements as dictionary keys, and their counts are stored as dictionary values.
```python
class Solution:
    def repeatedNTimes(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        count = collections.Counter(A)
        for k in count:
            if count[k] > 1:
                return k
```
## Sort Array By Parity
```python
class Solution:
    def sortArrayByParity(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        List = []
        for num in A:
            if num%2 == 0:
                List.append(num)
        for num in A:
            if num%2 != 0:
                List.append(num)
        return List
```
## flipping-an-imag
method 1 80ms
```python
class Solution:
    def flipAndInvertImage(self, A):
        """
        :type A: List[List[int]]
        :rtype: List[List[int]]
        """
        for line in A:
            line.reverse()
            # print(line)
            for num in range(0,len(line)):
                line[num] = line[num] ^ 1
        return A
```
method 2 72ms
```python
class Solution:
    def flipAndInvertImage(self, A):
        """
        :type A: List[List[int]]
        :rtype: List[List[int]]
        """
        return [[1 - num for num in line[::-1]]for line in A]

```
## Squares of a Sorted Array
```python
class Solution:
    def sortedSquares(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        for num in range(0,len(A)):
            A[num] = A[num]**2
        A.sort()
        return A
```
##  Unique Morse Code Words
method 1 56ms
```python
class Solution:
    def uniqueMorseRepresentations(self, words):
        """
        :type words: List[str]
        :rtype: int
        """
        trans = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
        after_trans = set()
        for word in words:
            trans_word = ''
            temp = []
            for character in word:
                # print(ord(character)-97,trans[ord(character)-97])
                temp.append(trans[ord(character)-97])
            trans_word = ''.join(temp)
            # print(trans_word)
            after_trans.add(trans_word)
        return len(after_trans)
```
## Largest Perimeter Triangle
For the triangle, if we have a,b,c,d(a>b>c>d) four edges, when a b d can form a triangle

a b c can also form a triangle with longer perimeter, cuz we have a < b + d < b + c
```python
class Solution:
    def largestPerimeter(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        A.sort()
        i,j,k = -1,-2,-3
        while abs(k) <= len(A) and abs(j)<=len(A)-1 and abs(i)<=len(A)-2:
            print(A[k]+A[j],A[i]-A[k],A[i]-A[j])
            if A[k]+A[j]>A[i]:
                return A[k]+A[j]+A[i]
            k -= 1
            j -= 1
            i -= 1
        return 0
```

## K Closest Points to Origin
bad implementation lol 2608ms 3.10%
```python
class Solution:
    def merge(self, l1, l2):
        list_ = []
        i, j = 0, 0
        while i < len(l1) or j < len(l2):
            if i == len(l1):
                list_.append(l2[j])
                j += 1
            elif j == len(l2):
                list_.append(l1[i])
                i += 1
            elif l1[i][0]**2+l1[i][1]**2 <= l2[j][0]**2+l2[j][1]**2:
                list_.append(l1[i])
                i += 1
            elif l1[i][0]**2+l1[i][1]**2 > l2[j][0]**2+l2[j][1]**2:
                list_.append(l2[j])
                j += 1
        return list_


    def merge_sort(self, points):
        if len(points) < 2:
            return points
        else:
            half = int(len(points)/2)
            list_1 = self.merge_sort(points[0:half])
            list_2 = self.merge_sort(points[half:])
        return self.merge(list_1, list_2)
    
    def kClosest(self, points, K):
        """
        :type points: List[List[int]]
        :type K: int
        :rtype: List[List[int]]
        """
        list_ = self.merge_sort(points)
        return list_[0:K]

```
method 2 372ms 100%

lambda - anonymous function  
```python
class Solution:
    def kClosest(self, points, K):
        """
        :type points: List[List[int]]
        :type K: int
        :rtype: List[List[int]]
        """       
        return sorted(points,key = lambda x: x[0]**2+x[1]**2)[0:K]
```
## 942. DI String Match

For 'I' movement, if we add the smallest element to the arr, there would be always an increasement comparing with following elements.
```python
class Solution:
    def diStringMatch(self, S: 'str') -> 'List[int]':
        max_ = len(S)
        min_ = 0
        arr = []
        for chr_ in S:
            if chr_ is 'I':
                arr.append(min_)
                min_ += 1
            else:
                arr.append(max_)
                max_ -= 1
        arr.append(min_)
        return arr
```
### 867. Transpose Matrix
```python
class Solution:
    def transpose(self, A: 'List[List[int]]') -> 'List[List[int]]':
        trans = []
        for j in range(0,len(A[0])):
            newarr = []
            for i in range(0,len(A)):
                newarr.append(A[i][j])
            trans.append(newarr)
        return trans
        
```
### 896. Monotonic Array Feb.2.2019
```python
class Solution:
    def isMonotonic(self, A: 'List[int]') -> 'bool':
        if sorted(A)==A or sorted(A,reverse=True)==A:
            return True
        else:
            return False
class Solution:
    def isMonotonic(self, A: 'List[int]') -> 'bool':
        if sorted(A) in [A,A[::-1]]:
            return True
        else:
            return False
    #by lee215
    def isMonotonic(self, A):
        return not {cmp(i, j) for i, j in zip(A, A[1:])} >= {1, -1}
```

### 448. Find All Numbers Disappeared in an Array
Pay attention to the return type!!!
```python
class Solution:
    def findDisappearedNumbers(self, nums: 'List[int]') -> 'List[int]':
        a = set(range(1,len(nums)+1))
        return list(a.difference(set(nums)))
```        

### 69. Majority Element
```python
class Solution:
    def majorityElement(self, nums: 'List[int]') -> 'int':
        # dic = {}
        # for i in nums:
        #     if i in dic:
        #         dic[i] += 1
        #     else:
        #         dic[i] = 1
        # ret = max(dic,key = lambda key: dic[key])
        # return  ret
        
        # counts = collections.Counter(nums)
        # return max(counts.keys(),key = counts.get)
        
        majority_count = len(nums)//2
        for candidate in set(nums):
            if sum(1 for elem in nums if elem == candidate) > majority_count:
                return candidate
```                
## 830. Positions of Large Groups
```python
class Solution:
    def largeGroupPositions(self, S: 'str') -> 'List[List[int]]':
        ret,temp = [],[]
        count = 1
        for i in range(len(S)-1):
            if S[i] == S[i+1]:
                count += 1
            elif S[i] != S[i+1]:
                if count >= 3:
                    temp[1] += 1
                count = 1
                if len(temp) == 2:
                    ret.append(temp)
                temp = []
            if count == 3:
                temp=[i-1,i]
            if count > 3:
                temp[1] += 1
            if i == len(S)-2:
                if count >= 3:
                    temp[1] += 1
                    ret.append(temp)
        return ret
```
