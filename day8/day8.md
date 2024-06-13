# 344. 反转字符串
```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        
        char temp;
        int left = 0;
        int right = s.size() - 1;

        while(left < right){
            temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            ++left;
            --right;
        }
        return ;
    }
};
```
