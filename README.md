# permutations1

def permute(self, nums):
    return [nums] if len(nums) <= 1 else [[x] + y for x in nums for y in self.permute(nums[:nums.index(x)]+nums[nums.index(x)+1:])]
    
    
    
    #permutations2
    
    class Solution:
    def permuteUnique(self, nums):
        res = [[]]
        for num, freq in Counter(nums).items():
            res = self.permuteRec(res, num, freq, 0)
        return res
    
    def permuteRec(self, perms, num, freq, i):
        if freq == 0: return perms
        if i == len(perms[0]): return [p + [num] * freq for p in perms]
        rec1 = self.permuteRec(perms, num, freq, i + 1)
        rec2 = self.permuteRec([p[:i] + [num] + p[i:] for p in perms], num, freq - 1, i + 1)
        return rec1 + rec2
