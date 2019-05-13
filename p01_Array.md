#### 0001 Two Sum

```
给定一个数组 nums 和一个目标数 target， 
返回数组中相加能得到 target 的第一对数字的下标

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```



1. 暴力解法, Time =O(n^2), Space = O(1)

   * CPP

     ```c++
     /**
      * 暴力解法
      * Time Complexity: O(n^2)
      * Space Complexity: O(1)
      */
     class Solution {
     public:
         vector<int> twoSum(vector<int>& nums, int target) {
             for(int i = 0 ; i < nums.size() ; i ++)
                 for(int j = i + 1 ; j < nums.size() ; j ++)
                     if(nums[i] + nums[j] == target)
                         return {i, j};
     
             throw invalid_argument("the input has no solution");
         }
     };
     ```

     

   * Java

2. 查找表

   * CPP

     ```c++
     /**
      * 建立查找表， hashmap.exists( hashmap[index] - target ) 
      * Time Complexity: O(n)
      * Space Complexity: O(n)
      */
     class Solution {
     public:
         // vector 作为 List 来使用， 返回的结果是 [index_1, index_2]
         vector<int> twoSum(vector<int>& nums, int target) {
             unordered_map<int,int> record;
             
             for(int i = 0 ; i < nums.size() ; i ++)
                 record[nums[i]] = i;
     
             for(int i = 0 ; i < nums.size() ; i ++){
                 unordered_map<int,int>::iterator iter = record.find(target - nums[i]);
                 if(iter != record.end() && iter->second != i)
                     return {i, iter->second};
             }
     
             throw invalid_argument("the input has no solution");
         }
     };
     ```

     

   * Java

     

