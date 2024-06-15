<style></style>

# 151.翻转字符串里的单词

这一题思路很重要，要不容易写乱。

有了思路也容易写乱，还是直接上卡哥代码=。=

```c++
class Solution {
public:
    void reverse(string& s, int start, int end){ //翻转，区间写法：左闭右闭 []
        for (int i = start, j = end; i < j; i++, j--) {
            swap(s[i], s[j]);
        }
    }

    void removeExtraSpaces(string& s) {//去除所有空格并在相邻单词之间添加空格, 快慢指针。
        int slow = 0;   //整体思想参考https://programmercarl.com/0027.移除元素.html
        for (int i = 0; i < s.size(); ++i) { //
            if (s[i] != ' ') { //遇到非空格就处理，即删除所有空格。
                if (slow != 0) s[slow++] = ' '; //手动控制空格，给单词之间添加空格。slow != 0说明不是第一个单词，需要在单词前添加空格。
                while (i < s.size() && s[i] != ' ') { //补上该单词，遇到空格说明单词结束。
                    s[slow++] = s[i++];
                }
            }
        }
        s.resize(slow); 
    }

    string reverseWords(string s) {
        removeExtraSpaces(s); 
        reverse(s, 0, s.size() - 1);
        int start = 0; 
        for (int i = 0; i <= s.size(); ++i) {
            if (i == s.size() || s[i] == ' ') { 
                reverse(s, start, i - 1); 
                start = i + 1; 
            }
        }
        return s;
    }
};
```

# 

<style></style>

# 55.右旋转字符串

与上一题思路类似，整体反转+局部反转：

```c++
#include<iostream>
#include<algorithm>
using namespace std;
int main() {
    int n;
    string s;
    cin >> n;
    cin >> s;
    int len = s.size(); //获取长度

    reverse(s.begin(), s.end()); // 整体反转
    reverse(s.begin(), s.begin() + n); // 先反转前一段，长度n
    reverse(s.begin() + n, s.end()); // 再反转后一段

    cout << s << endl;

} 
```
