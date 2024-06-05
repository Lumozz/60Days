# 704. 二分查找 
二分查找的基本思想非常简单，但是具体实现的时候会发现有非常重要的细节。
## 基本思路
- 记录左右两个边界
- 取中间位置的数
- 当中间位置数等于目标值时，结束；当中间位置数大于目标数时，右边界等于中间位置数。注意，此时已经判断中间位置数大于目标数，因此下一步右边界一定不可能等于目标数；当中间位置数小于目标数，左边界等于中间位置数。

```c++ 

	class Solution {
	public:
	    int search(vector<int>& nums, int target) {
	        int mid = (nums.size()-1) / 2;
	        int right = nums.size() - 1;
	        int left = 0;
	
	        while(left <= right){
	            if(nums[mid] == target){
	                return mid;
	            } else if(nums[mid] < target){
	                left = mid + 1;
	            } else {
	                right = mid - 1;
	            }
	            mid = (right + left) / 2;
	        }
	
	        return -1;
	    }
	};  
```

#  27. 移除元素

```c++  

	class Solution {
	public:
	    int removeElement(vector<int>& nums, int val) {
	        int slow = 0;
	        int fast = 0;
	        for(; fast<nums.size(); ++fast){
	            if(nums[fast] == val){
	                continue;
	            } else if (nums[fast] != val){
	                nums[slow] = nums[fast];
	               ++slow;
	            } 
	        }
	
	        return slow;
	    }
	};  
```