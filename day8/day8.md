int main(){
    int count = 0;
    std::string s;
    std::string number = "rebmun"

    while(std::cin >> s){
        for(int i=0; i<s.size(); ++i){
            if(s[i] <= '9' && s[i] >= '0'){
                ++count;
            }
        }
    }
    
    int oldIndex = s.size() - 1;
    
    s.resize(s.size() + count*5);
    
    int trail = s.size() - 1;
    
    for(; oldIndex >=0; --oldIndex){
        if(s[oldIndex] <='9' && s[oldIndex] >='0'){
            for(char c: number){
                s[trail--] = c;
            }
        } else {
            s[trail--] = s[oldIndex];
        }
    }
    
    std::cout << s <<std::endl;

}

# 卡码网 54 替换数字

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

# 541. 反转字符串2

这一题，只要判断`2k`个字符中前`k`个是否比剩余字符串长就可以了。

```c++
class Solution {
public:
    string reverseStr(string s, int k) {
    for(int i = 0; i<s.size(); i+=(2*k)){
        if(i + k < s.size()){
            reverse(s.begin()+i, s.begin() + i+k );
        } else {
            reverse(s.begin() + i, s.end());
        }
    }
    return s;
    }
};
```

# 卡码网 54 替换数字

```c++
#include<iostream>
#include<string>

int main(){
    int count = 0;
    std::string s;
    std::string number = "rebmun"
    
    while(std::cin >> s){
        for(int i=0; i<s.size(); ++i){
            if(s[i] <= '9' && s[i] >= '0'){
                ++count;
            }
        }
    }
    
    int oldIndex = s.size() - 1;
    
    s.resize(s.size() + count*5);
    
    int trail = s.size() - 1;
    
    for(; oldIndex >=0; --oldIndex){
        if(s[oldIndex] <='9' && s[oldIndex] >='0'){
            for(char c: number){
                s[trail--] = c;
            }
        } else {
            s[trail--] = s[oldIndex];
        }
    }
    
    std::cout << s <<std::endl;
    
}
```
