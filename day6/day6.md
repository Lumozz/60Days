# 有效的字母异位词

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size() != t.size()){
            return false;
        }

        int record[26] = {0};

        for(char c: s){
            ++record[c - 'a'];
        }

        for(char c:t){
            --record[c - 'a'];
        }

        for(int i: record){
            if (i != 0 ){
                return false;
            }
        }
        return true;   
    }
};
```

#  349. 两个数组的交集

这题的重点在于`unordered_set`的插入，查找操作。

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> a;
        for(int i: nums1){
            a.insert(i);
        }

        unordered_set<int> res;

        for(int i: nums2){
            if(a.find(i) != a.end()){
                res.insert(i);
            }
        }
        
        vector<int> res_v(res.begin(), res.end());

        return res_v;
    }
};
```

# 202. 快乐数

```c++
class Solution {
public:
    int sumNum(int n){
        int res = 0;
        int lower;
        int higher;

        while(n > 0){
            lower = n % 10;
            higher = n / 10;

            res += lower* lower;

            n = higher;
        }
        std::cout << res << std::endl;
        return res;
    }
    bool isHappy(int n) {
        unordered_set<int> sumRes;
        int res;
        while(true){
            res = sumNum(n);
            if (res == 1){
                return true;
            } else if(sumRes.find(res) == sumRes.end()){
                sumRes.insert(res);
                n = res;
            } else {
                return false;
            }
        }
        
    }
};
```

# 1.两数之和

梦开始的地方

```c++
class Solution {
public:
    std::vector<int> twoSum(std::vector<int>& nums, int target) {
        std::unordered_map<int, int> a;
        for (int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if (a.find(complement) != a.end()) {
                return std::vector<int> {a[complement], i};
            }
            a[nums[i]] = i;
        }
        return std::vector<int> {};
    }
};
```

