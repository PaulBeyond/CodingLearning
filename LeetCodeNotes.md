# Leet_Code_Notes

## 差分数组

差分数组本质上来说就是一个数组，可以用O(1)的时间处理区间修改。

设原数组为a数组，差分数组为d数组，则对于i∈[2,n],都有d[i]=a[i]-a[i-1].

当我们需要更新区间[l,r]时候（仅指加减运算），我们仅仅可以只更新d[l]+=x,d[r+1]-=x;

当我们需要单独查询原数组一个点的值的时候，我们不难发现出令SnSn为d[i]的前缀和，那么a[i]=Si;

### 2381. 字母移位 

[题目链接]: https://leetcode.cn/problems/shifting-letters-ii/

#### MyCode

```C++
class Solution {
public:
    string shiftingLetters(string s, vector<vector<int>>& shifts) {        
        vector<vector<char>> trans;
        for(int i = 0; i < 26; i++)
        {
            vector<char> tmp;
            for(int j = 0; j < 26; j++)
            {
                tmp.push_back((char)((i + j) % 26 + 'a'));
            }
            trans.push_back(tmp);
        }

        for(auto & shift : shifts)
        {
            int tmp = (int)(((float)shift[2] - 0.5) * 2 + 26) % 26;
            for(int i = shift[0]; i <= shift[1]; i++)
            {
                s[i] = trans[s[i] - 'a'][tmp];
            }
        }

        return s;        
    }

};
// 问题：复杂度O(n2)，超时
```

#### End Code

