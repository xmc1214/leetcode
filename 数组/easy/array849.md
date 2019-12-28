# leetcode 数组类 到最近的人的最大距离

## 解法一

遍历数组利用双指针分别记录每个元素左边最近的人的距离以及右边最近的人的距离,取两者中的最小值,ans保存所有最小值中的最大值

```c++
class Solution {
public:
    int maxDistToClosest(vector<int>& seats) {
       int N = seats.size();
        int prev = -1, future = 0;
        int ans = 0;

        for (int i = 0; i < N; ++i) {
            if (seats[i] == 1) {
                prev = i;
            } else {
                while (future < N && seats[future] == 0 || future < i)
                    future++;

                int left = prev == -1 ? N : i - prev;
                int right = future == N ? N : future - i;
                ans = max(ans, min(left, right));
            }
        }
        return ans;
    }
};
```
