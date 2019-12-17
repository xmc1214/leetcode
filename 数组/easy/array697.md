# leetcode 数组类 数组的度

## 解法一

利用两个unordered_map分别记录每个数组元素出现的次数以及每个元素每次出现的下标,利用第一个unordered_map求出数组的度保存到count中,再次遍历数组如果元素的度与数组的度相等则利用第二个unordered_map求出该元素第count次出现的下标以及第一次出现的下标,两者之差加一就是最短连续数组的长度

```c++
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) {
      int count = 0;
      int size = nums.size();
      unordered_map<int,int> m;
      unordered_map<int,vector<int>>record;
      for(int i = 0; i < size; i++)
      {
        m[nums[i]]++;
        record[nums[i]].push_back(i);
        count = max(count,m[nums[i]]);
      }
      int result = INT_MAX;
      for(int j = 0; j < size; j++)
      {
        if(m[nums[j]] == count)
        {
          int temp = record[nums[j]].at(count - 1) - record[nums[j]].at(0) + 1;
          result = min(result,temp);
        }
      }
      return result;
    }
};
```

## 解法二

区别于解法一的地方是在得到数组的度后利用一个set存储度为数组度的不重复元素,再遍历set分别求出元素第一次以及最后一次出现的下标,result保存最小下标差加一

```c++
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) {
        if (nums.size() == 0) {
            return 0;
        }
        map<int, int> deg;
        int maxDegValue = 0;
        for (auto i : nums) {
            deg[i]++;
            maxDegValue = max(deg[i],maxDegValue);
        }
        if (maxDegValue == 1) {
            return 1;
        }
        set<int> maxDeg;
        for (auto item : deg) {
            if (item.second == maxDegValue) {
                maxDeg.insert(item.first);
            }
        }
        int result = nums.size();
        for (auto item : maxDeg) {    
            int firstIndex = 0;
            int lastIndex = nums.size()-1;
            for (int i = 0; i < nums.size(); i++) {
                if (nums[i] == item) {
                    firstIndex = i;
                    break;
                }
            }
            for (int i = nums.size()-1; i >= 0; i--) {
                if (nums[i] == item) {
                    lastIndex = i;
                    break;
                }
            }
            result = min(result,lastIndex - firstIndex + 1);
        }
        return result;
    }
};
```
