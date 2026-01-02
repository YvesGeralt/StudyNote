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