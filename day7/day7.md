# 454. 四数相加2

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> ab;
        for(int a: nums1){
            for(int b: nums2){
                ++ab[a + b];
            }
        }
        int count = 0;
        for(int c: nums3){
            for(int d: nums4){
                if(ab.find(-(c+d)) != ab.end()){
                    count += ab[-(c+d)];
                }
            }
        }
        return count;
    }
};
```

# 383. 赎金信

```c++
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        vector<int> nums(26, 0);
        for(char c: magazine){
            ++nums[c - 'a'];
        }
        for(char c: ransomNote){
            --nums[c - 'a'];
            if(nums[c - 'a'] < 0){
                return false;
            }
        }
        return true;
    }
};
```

# 15 三数之和

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;

        for(int i = 0; i<nums.size()-2; ++i){
            if(i>0 && nums[i] == nums[i-1]){
                continue;
            }
            int left = i+1;
            int right = nums.size() - 1;
    
            while(left < right){
                if(nums[i] + nums[left] + nums[right] > 0){
                    --right;
                } else if(nums[i] + nums[left] + nums[right] < 0){
                    ++left;
                } else {
                    res.push_back({nums[i], nums[left], nums[right]});
                    ++left;
                    --right;
                    while(left < right && nums[left] == nums[left - 1]) {
                        ++left;
                    }
                    while(left < right && nums[right] == nums[right + 1]) {
                        --right;
                    }
                }
                }
                
            }
        
        return res;
    }
};

```

# 四数之和

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        if(nums.size() < 4){
            return
        }
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        for(int p=0; p<nums.size()-3; ++p){
            if(p>0 && nums[p] == nums[p-1]){
                continue;
            }
            for(int q=p+1; q<nums.size()-2; ++q){
                if(q>1 && nums[q] == nums[q-1]){
                    continue;
                }
                int left = q+1;
                int right = nums.size()-1;
                while(left < right){
                    if(nums[p] + nums[q] + nums[left] + nums[right] > target){
                        --right;
                    } else if(nums[p] + nums[q] + nums[left] + nums[right] < target){
                        ++left;
                    } else {
                        res.push_back({nums[p], nums[q], nums[left], nums[right]});
                        --right;
                        ++left;
                        while(left < right && nums[left] == nums[left-1]){
                            ++left;
                        }
                        while(left < right && nums[right] == nums[right+1]){
                            --right;
                        }
                    }
                }
                
            }
        }
        return res;
    }
};
```

