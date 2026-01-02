# backtrace
> 回溯法，一般可以解决如下几种问题：<br>
>组合问题：N个数里面按一定规则找出k个数的集合<br>
>切割问题：一个字符串按一定规则有几种切割方式<br>
>子集问题：一个N个数的集合里有多少符合条件的子集<br>
>排列问题：N个数按一定规则全排列，有几种排列方式<br>
>棋盘问题：N皇后，解数独等等<br>

模板：<br>
```
//所有路径集合
List<> allPath  = []
void backTrace (可选列表，已走路径)：
     if(满足结束条件){
        allPath.add(已走路径);
        return;
     }
     for(选择：可选列表){
        做选择
        backTrace（当前可选列表，已走路径）;
        撤销选择
     }
```
- 组合
  ```
    import java.util.*;
    class Solution {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();

        void backtrace(int n, int k, int startIndex){
            if(path.size() == k){
                result.add(new ArrayList<Integer>(path));
                return;
            }
            // 剪枝，当剩下的不满足 k - path.size()时，无需再遍历
            for(int i = startIndex; i <= n; i++){
                path.add(i);
                backtrace(n, k, i+1);
                // 撤销路径中的最后一个元素
                path.remove(path.size() - 1);
            }
        }

        public List<List<Integer>> combine(int n, int k) {
            backtrace(n, k, 1);    
            return result;
        }

    }
  ```

- 组合 III
  ```
    /**
        用path记录组合，result返回结果
        当最小和 > n时，返回空集
        当剩下的数不足 k - path.size()时，无需遍历
    */
    import java.util.*;

    class Solution {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> path = new ArrayList<Integer>();

        void backtrace(int n, int k, int index, int sum){
            if(path.size() == k){
                if(sum == n){
                    result.add(new ArrayList<Integer>(path));
                }
                return;
            }

            for(int i = index; i <= 10 - (k - path.size()); i++){
                if(sum + i > n){
                    break;
                }
                path.add(i);
                sum += i;
                backtrace(n, k, i+1, sum);
                path.remove(path.size() - 1);
                sum -= i;
            }
        }

        public List<List<Integer>> combinationSum3(int k, int n) {
            // 当最小和 > n时，返回空集
            int sum = 0;
            for(int i = 1; i <= k; i++){
                sum += i;
            }
            if(sum > n){
                return result;
            }

            backtrace(n,k,1,0);
            return result;
        }
    }
  ```

- 电话号码
  > 用字符串数组存储每个数字对应的字符串<br>
  > 用StringBuilder构建字符串，方便增减元素

  ```
    import java.util.*;

    class Solution {
        List<String> list = new ArrayList<String>();

        public List<String> letterCombinations(String digits) {
            if(digits == null || digits.length() == 0){
                return list;
            }

            String[] numString = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

            backTaching(digits,numString,0);
            return list;
        }

        StringBuilder temp = new StringBuilder();

        public void backTaching(String digits, String[] numString, int num){
            if(num == digits.length()){
                list.add(temp.toString());
                return;
            }

            String str = numString[digits.charAt(num) - '0'];

            for(int i = 0; i < str.length(); i++) {
                temp.append(str.charAt(i));
                backTaching(digits,numString,num + 1);
                temp.deleteCharAt(temp.length() - 1);
            }
            
        }
    }
  ```