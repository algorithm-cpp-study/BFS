# BFS
BFS (Breadth First Search) : 다차원 배열에서 각 칸을 방문할 때 너비를 우선으로 방문하는 알고리즘  
  
## BFS 과정
1. 시작하는 칸을 큐에 넣고 방문했다는 표시를 남김  
2. 큐에서 원소를 꺼내어 그 칸에 상하좌우로 인접한 칸에 대해 3번을 진행  
3. 해당 칸을 이전에 방문했다면 아무 것도 하지 않고, 처음으로 방문했다면 방문했다는 표시를 남기고 해당 칸을 큐에 삽입  
4. 큐가 빌때까지 2번을 반복  
모든 칸에 큐에 1번씩 들어가므로 시간복잡도는 칸이 N개일때 O(N)  
  
## STL pair
```c++
#include <bits/stdc++.h>

using namespace std;
#define X first
#define Y second
typedef pair<int, int> pii;

int main() {
    cin.tie(0)->sync_with_stdio(0);
    pair<int, int> t1 = make_pair(10, 13);
    pair<int, int> t2 = {4, 6};
    cout << t2.first << ' ' << t2.second << '\n'; // 4 6
    if(t2 < t1) cout << "t2 < t1";
}
```
pair에는 미리 대소관계가 설정되어 있어 편합니다. 알아서 앞쪽의 값을 먼저 비교하고, 이후 뒤쪽의 값을 비교합니다.  
  
## BFS 예시 코드
```c++
#include <bits/stdc++.h>

using namespace std;
#define X first
#define Y second
typedef pair<int, int> pii;
int board[502][502] =
        {{1,1,1,0,1,0,0,0,0,0},
         {1,0,0,0,1,0,0,0,0,0},
         {1,1,1,0,1,0,0,0,0,0},
         {1,1,0,0,1,0,0,0,0,0},
         {0,1,0,0,0,0,0,0,0,0},
         {0,0,0,0,0,0,0,0,0,0},
         {0,0,0,0,0,0,0,0,0,0}}; // 1이 파란 칸, 0이 빨간 칸
bool vis[502][502];
int n = 7, m = 10;
int dx[4] = {1, 0, -1 ,0};
int dy[4] = {0, 1, 0, -1};
int main() {
    cin.tie(0)->sync_with_stdio(0);
    queue<pii> q;
    vis[0][0] = 1;
    q.push({0,0});
    while(!q.empty()) {
        auto cur = q.front(); q.pop();
        cout << '(' << cur.X << ", " << cur.Y << ") -> ";
        for(int dir=0; dir<4; dir++) {
            int nx = cur.X + dx[dir];
            int ny = cur.Y + dy[dir];
            if (nx < 0 || ny < 0 || nx >= n || ny >= m) continue;
            if (vis[nx][ny] || board[nx][ny] != 1) continue;
            vis[nx][ny] = 1;
            q.push({nx, ny});
        }
    }
}
```
범위 체크를 먼저 한 후 방문체크를 해야 한다.  
방문체크를 먼저 하면 vis[-1][0]과 같은 값을 참조할 수 있어 런타임 에러가 날 수 있다.  
