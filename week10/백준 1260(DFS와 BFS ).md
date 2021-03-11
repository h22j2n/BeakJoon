## 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

## 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

## 출력

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

## 예제 입력 1 

```
4 5 1
1 2
1 3
1 4
2 4
3 4
```

## 예제 출력 1 

```
1 2 4 3
1 2 3 4
```

## 예제 입력 2 

```
5 5 3
5 4
5 2
1 2
3 4
3 1
```

## 예제 출력 2 

```
3 1 2 5 4
3 1 4 2 5
```

## 예제 입력 3 

```
1000 1 1000
999 1000
```

## 예제 출력 3 

```
1000 999
1000 999
```



-----------

- DFS(Depth-first Search) - 깊이우선탐색, 그래프에서 가장 최상위 노드부터 하위노드까지 깊게 탐색하고 다시 위로 올라와서 깊게 탐색하는 방법!

- BFS(Breadth-first Search) - 너비우선탐색, 그래프에서 가장 최상위 노드부터 다음 차수(degree)를 모두 탐색하고, 그 다음 차수를 모두 탐색하는 방법!

  ![image-20210224204506592](/Users/heejin/Library/Application Support/typora-user-images/image-20210224204506592.png)

  



``` java
package N1260;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;


public class Practice {
    static int n; //정점의 개수 1~1000
    static int m; //간선의 개수 1~10000
    static int v; //시작점
    static int[][] link; //연결상태
    static boolean[] check; //확인상태


    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        v = Integer.parseInt(st.nextToken());

        check = new boolean[1001];
        link = new int[1001][1001];

        //연결
        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());
            link[x][y] = link[y][x] = 1;
        }

        dfs(v);

        check = new boolean[1001];
        System.out.println();
        bfs();


        
    }

    public static void dfs(int x){
        check[x] = true;
        System.out.print(x + " ");

        for (int i = 1; i <= n; i++) {
            if(link[x][i] == 1 && check[i] == false) dfs(i);
        }
    }

    public static void bfs(){
        Queue<Integer> q = new LinkedList<Integer>();
        q.offer(v); //큐에 시작점을 넣음
        check[v] = true;
        System.out.print(v + " ");

        while(!q.isEmpty()){
            int tmp = q.poll(); //맨앞에 있는 애 꺼내기

            for (int i = 1; i <= n; i++) {
                if(link[tmp][i] == 1 && check[i] == false){
                    q.offer(i);
                    check[i] = true;
                    System.out.print(i + " ");
                }
                
            }
        }
        


    }
    
}
```



