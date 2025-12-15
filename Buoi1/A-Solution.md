# Lời giải
Trước hết, một mê cung hợp lệ mà một mê cung mà ở đó chỉ có duy nhất một lối vào và một lối ra. Do đó ta sẽ viết hàm `find_entrance()` để tìm và lưu giữ các lối vào/ra của mê cung vào vector $entrance$
```cpp
void find_entrance(vector<pair<int, int>>& entrance, const vector<vector<char>>& grid, int m, int n) {
    for (int i = 0; i < m; ++i) {
        if (grid[i][0] == '.') {
            if (!visited[i][0]) {
                visited[i][0] = true;
                entrance.push_back({i, 0});
            }
        }
        if (grid[i][n - 1] == '.') {
            if (!visited[i][n - 1]) {
                visited[i][n - 1] = true;
                entrance.push_back({i, n - 1});
            }
        }
    }
    for (int j = 0; j < n; ++j) {
        if (grid[0][j] == '.') {
            if (!visited[0][j]) {
                visited[0][j] = true;
                entrance.push_back({0, j});
            }
        }
        if (grid[m - 1][j] == '.') {
            if (!visited[m - 1][j]) {
                visited[m - 1][j] = true;
                entrance.push_back({m - 1, j});
            }
        }
    }
}
```

Với mỗi lần tìm kiếm, nếu độ dài của vector $entrance$ khác $2$ điều đó chứng tỏ mê cung đó không hợp lệ. Ngược lại, ta tiếp tục kiểm tra xem liệu rằng có tồn tại ít nhất một đường đi từ lối vào mê cung đến lối ra của mê cung hay không.

Ý tưởng bài toán rất đơn giản, ta sử dụng đến thuật toán DFS để kiểm tra. Ta sẽ bắt đầu DFS từ vị trí lối vào của mê cung, với mỗi vị trí $\left(i, j\right)$ trong mê cung $M$, nếu $M[i][j] =$ .' thì ta sẽ DFS ra xung quanh vị trí $\left(i, j \right)$ đó. 

**Lưu ý:** Ta chỉ có thể đi trái, phải, lên, hoặc xuống. Do đó ta sẽ tạo hai mảng di chuyển $dx[]$ và $dy[]$ để duy trì các vị trí qua trái, phải, lên, hoặc xuống
```cpp
bool visited[maxN][maxN];
int dx[] = {-1, 1, 0, 0};
int dy[] = {0, 0, -1, 1};

void dfs(const vector<vector<char>>& grid, int m, int n, int x, int y) {
    visited[x][y] = true;
    for (int i = 0; i < 4; ++i) {
        int nx = x + dx[i];
        int ny = y + dy[i];
        if (nx >= 0 && ny >= 0 && nx <= m - 1 && ny <= n - 1 && !visited[nx][ny] && grid[nx][ny] == '.')
            dfs(grid, m, n, nx, ny);
    }
}
```

Sau khi đã DFS, ta đã duyệt qua các đường đi liên thông với nhau, khi đó nếu cả lối vào và lối ra của mê cung đã được thăm thì mê cung đó luôn tồn tại ít nhât một đường đi từ lối vào đến lối ra, ngược lại thì không.
```cpp
vector<pair<int, int>> entrance;
memset(visited, false, sizeof(visited));
find_entrance(entrance, grid, m, n);
if (entrance.size() != 2) {
    cout << "invalid" << '\n';
    continue;
}
int start_x = entrance[0].first, start_y = entrance[0].second;
int end_x = entrance[1].first, end_y = entrance[1].second;
memset(visited, false, sizeof(visited));
dfs(grid, m, n, start_x, start_y);
if (visited[start_x][start_y] && visited[end_x][end_y]) cout << "valid" << '\n';
else cout << "invalid" << '\n';
```

Độ phức tạp thuật toán cho bài toán này là: $O\left( t \times m \times n\right)$.
