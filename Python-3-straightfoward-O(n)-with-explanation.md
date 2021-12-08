https://leetcode.com/problems/global-and-local-inversions/discuss/1499983/Python-3-straightfoward-O(n)-with-explanation

Each local inversion is also a global inversion, i.e. number of local <= number of global. Therefore any valid configuration can only have local inversions that satisfy

nums[i] == i+1 and nums[i+1] == i)
class Solution:
    def isIdealPermutation(self, nums: List[int]) -> bool:
        # local <= global
        # search for local reversal
        # if found nums[i] > nums[i+1], it must be nums[i] == i+1 and nums[i+1] == i
        for i in range(len(nums)-1):
            if nums[i] > nums[i+1]:
                if nums[i] != i+1 or nums[i+1] != i:
                    return False
        return True
