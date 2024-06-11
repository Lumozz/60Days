# 977.有序数组的平方 
这个题目还是很简单的，重点在于想清楚结束时，判断结束条件，执行最后动作，递增/递减三者之间的先后顺序关系，要不然循环判断条件又不知道改写大于还是大于等于了。
这份代码是先生成空vector,直接push_back新元素，然后反转vector。也可以直接生成所需尺寸的vector，然后直接在相应位置添加新元素。

```c++  

class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> res;
        int left = 0;
        int right = nums.size() - 1;
        while(left <= right){
            if(nums[left]*nums[left]>=nums[right]*nums[right]){
                // res.insert(res.begin(), nums[left]*nums[left]);
                res.push_back(nums[left]*nums[left]);
                ++left;
            } else {
                // res.insert(res.begin(), nums[right]*nums[right]);
                res.push_back(nums[right]*nums[right]);
                --right;
            }
        }
        vector<int> res2;
        vector<int>::reverse_iterator iter = res.rbegin();
        for(; iter != res.rend(); ++iter){
            res2.push_back(*iter);
        }
        return res2;
    }
};  

```
# 长度最小的子数组
去年九月份做的题，不会了=。=

```c++  

class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int result = INT32_MAX;
        int sum = 0;
        int i = 0;
        int subLength = 0;

        for(int j=0; j<nums.size(); ++j){
            sum += nums[j];
            while (sum >= target){
                subLength = (j - i + 1);
                result = result < subLength? result: subLength;
                sum -= nums[i++];
            }
        }
        return result == INT32_MAX? 0: result;
    }
};  

```

# 螺旋矩阵 II
题目没什么难的们就是得仔细仔细仔细仔细
```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
    vector<int> m(n, 0);
    vector<vector<int>> matrix(n, m);

    int u = 0; //赋值上下左右边界
    int d = n - 1;
    int l = 0;
    int r = n - 1;

    int count = 1;
    while(true)
    {
        for(int i = l; i <= r; ++i) matrix[u][i] = count++; //向右移动直到最右
        if(++ u > d) break; //重新设定上边界，若上边界大于下边界，则遍历遍历完成，下同
        for(int i = u; i <= d; ++i) matrix[i][r] = count++; //向下
        if(-- r < l) break; //重新设定有边界
        for(int i = r; i >= l; --i) matrix[d][i] = count++; //向左
        if(-- d < u) break; //重新设定下边界
        for(int i = d; i >= u; --i) matrix[i][l] = count++; //向上
        if(++ l > r) break; //重新设定左边界
    }
    return matrix;
    
    }
};
```
