# Lời giải
Vì mỗi căn phòng được ngăn cách bởi các bức tường (`#`), và mỗi phòng là một tập hợp các dấu `.` liên tiếp theo các hướng trái, phải, lên, hoặc xuống. Ta đưa bài toán về đếm số các thành phần `.` liên thông với nhau trong bản đồ có kích thước $n \times m$.

Ta có thể sử dụng thuật toán DFS để giải quyết bài toán này. Do ta có bốn hướng đi khả thi (trái, phải, lên, xuống) ta duy trì hai mảng di chuyển $dx[]$ và $dy[]$ để duy trì các hướng đi.

```cpp
int dx[] = {-1, 1, 0, 0};
int dy[] = {0, 0, -1, 1};

void dfs(int x, int y) {
    visited[x][y] = true;
    for (int i = 0; i < 4; ++i) {
        int nx = x + dx[i];
        int ny = y + dy[i];
        if (0 <= nx && nx <= n - 1 && 0 <= ny && ny <= m - 1 && !visited[nx][ny] && grid[nx][ny] == '.')
            dfs(nx, ny);
    }
}
```

Với mỗi lần DFS, ta duyệt qua các thành phần `.` liên thông với nhau. Điều đó cũng có nghĩa là số lần ta DFS cũng chính là số căn phòng bản đồ.
```cpp
int res = 0;
for (int i = 0; i < n; ++i) {
    for (int j = 0; j < m; ++j) {
        if (!visited[i][j] && grid[i][j] == '.') {
            res++;
            dfs(i, j);
        }
    }
}    
cout << res << '\n';
```
Độ phức tạp cho bài toán này là $O\left(n \times m \right)$