# graph

### BFS
> BFS,广度优先搜索，以起始点为中心一圈一圈进行搜索，一旦遇到终点，记录之前走过的节点就是一条最短路。结束条件是queue为空
代码模板<br>
```
void bfs(起始状态){
	queue<element_type> q;//创建队列
    q.push(起始状态入队)；
    while(!q.empty()){//当队列非空
        if(当前状态x方向可走)
            q.push(当前状态+x);//该状态入队
        if(当前状态向y方向可走)
            q.push(当前状态+y);//该状态入队
        …………………
        处理(队顶)q.top();
        相应操作；
        q.pop();//队首弹出队
    }//一次循环结束，执行下一次循环
}
```

- 腐烂的橘子
```
import java.util.*;

class Solution {
    private static final int[][] DIRECTIONS = {{-1,0},{1,0},{0,-1},{0,1}};

    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int columns = grid[0].length;
        int fresh = 0;
        List<int[]> q = new ArrayList<>();
        for(int i = 0; i < rows; i++){
            for(int j = 0; j < columns; j++){
                if(grid[i][j] == 1){
                    fresh++; // 统计新鲜橘子数量
                } else if(grid[i][j] == 2){
                    q.add(new int[]{i,j}); // 将腐烂橘子入队
                }
            }
        }

        int time = 0;
        while(fresh > 0 && !q.isEmpty()){
            time++;
            // 保存当前层的队列
            List<int[]> tmp = q;
            // 清空队列，保存下一层
            q = new ArrayList<>();
            for(int[] pos : tmp) {
                for(int[] d : DIRECTIONS) {
                    int i = pos[0] + d[0];
                    int j = pos[1] + d[1];
                    if(0 <= i && i < rows && 0 <= j && j < columns && grid[i][j] == 1){
                        fresh--;
                        grid[i][j] = 2;
                        q.add(new int[]{i,j});
                    }
                }
            }
        }

        return fresh > 0 ? -1 : time;
    }
}
```

- 二叉树的层序遍历
```
import java.util.*;
class Solution {

    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        List<TreeNode> q = new ArrayList<>();

        if(root == null){
            return result;
        }

        q.add(root);

        while(!q.isEmpty()){
            List<TreeNode> tmp = q;
            q = new ArrayList<>();
            List<Integer> row = new ArrayList<>();

            for(TreeNode t : tmp){
                row.add(t.val);
                if(t.left != null){
                    q.add(t.left);
                }
                if(t.right != null){
                    q.add(t.right);
                }
            }

            result.add(row);
        }
        

        return result;
    }
}
```