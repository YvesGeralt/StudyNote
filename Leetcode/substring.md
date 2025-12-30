# substring

- 和为k的子数组
  > 使用前缀和 + 哈希表的思想来降低时间复杂度<br>
  > `pre[j] - pre[i] = k` ==> `pre[j] - k = pre[i]`
  ```
    import java.util.HashMap;

    class Solution {
        public int subarraySum(int[] nums, int k) {
            int count = 0;
            int pre = 0;

            HashMap<Integer,Integer> map = new HashMap<>();
            map.put(0,1);
            for(int i = 0; i < nums.length; i++){
                pre += nums[i];
                if(map.containsKey(pre - k)){
                    count += map.get(pre - k);
                }
                /**
                    从map中获取键为sum的值（即之前出现过的前缀和为sum的次数），如果sum不存在于map中，则返回默认值0。
                    将这个值加1，表示当前前缀和sum又出现了一次。
                */
                map.put(pre,map.getOrDefault(pre,0) + 1);
            }

            return count;
        }
    }
  ```

- 滑动窗口最大值
  > 采用双端队列，维护滑动窗口最大值在队头，不维护滑动窗口内最大值之前的元素
  ```
    import java.util.*;

    class Solution {
        public int[] maxSlidingWindow(int[] nums, int k) {
            int len = nums.length;
            int[] result = new int[len - k + 1];
            Deque<Integer> deque = new ArrayDeque<>();

            for(int i = 0; i < len; i++){
                // 移除队头，若已不在窗口内
                if(!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                    deque.pollFirst();
                }

                // 移除队尾，比当前元素小
                while(!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                    deque.pollLast();
                }

                deque.offerLast(i);

                if(i >= k - 1) {
                    result[i - k + 1] = nums[deque.peekFirst()];
                }
            }
            return result;
        }
    }
  ```