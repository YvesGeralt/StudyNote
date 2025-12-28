# slidingWindow

- 无重复字符的最长子串
  > 用左右指针界定滑动窗口范围，而不一定要将元素存入队列内
  ```
    import java.util.*;
    import java.lang.Math.*;

    class Solution {
        public int lengthOfLongestSubstring(String s) {
            if(s.length() == 0) return 0;

            HashMap<Character, Integer> map = new HashMap<Character, Integer>();
            int max = 0;
            int left = 0;
            for(int i = 0; i < s.length(); i++){
                if(map.containsKey(s.charAt(i))){
                    // 若s[i] 出现在滑动窗口内, 左指针移动到map.get(s.charAt(i)) + 1，否则不动
                    left = Math.max(left, map.get(s.charAt(i)) + 1);
                }
                map.put(s.charAt(i), i);
                max = Math.max(max, i - left + 1);
            }

            return max;
        }
    }
  ```

- 找到字符串中所有字母异位词
  > 用一个长为26的数组来存储每个字母的出现次数，下标为`s.charAt(i) - 'a'`
  ```
    /**
        用滑动窗口枚举 s 的所有长为 n 的子串 s′在滑的同时，维护 s′的每种字母的出现次数。
        如果 s′的每种字母的出现次数，和 p 的每种字母的出现次数都相同，
        那么 s′是 p 的异位词，把 s′左端点下标加入答案。

    */
    import java.util.*;

    class Solution {
        public List<Integer> findAnagrams(String s, String p) {
            // 统计p的每种字母出现次数
            int[] cntP = new int[26];
            for(char c : p.toCharArray()){
                cntP[c - 'a'] ++; 
            }

            List<Integer> ans = new ArrayList<>();
            // 统计s的长为p.length()的子串s'的每种字母出现次数
            int[] cntS = new int[26];
            for(int right = 0; right < s.length(); right ++){
                cntS[s.charAt(right) - 'a'] ++; // 右端点字母进入窗口
                int left = right - p.length() + 1;
                if(left < 0){ // 窗口不足
                    continue;
                }
                if(Arrays.equals(cntS,cntP)){
                    ans.add(left);
                }
                cntS[s.charAt(left) - 'a'] --;// 左端点字母离开窗口
            }
            return ans;
        }
    }
  ```