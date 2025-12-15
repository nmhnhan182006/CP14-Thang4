# Lời giải
Bài toán yêu cầu ta tìm một lộ trình để đi từ bưu điện qua tất cả các đường đi trong thành phố đúng một lần và quay lại bưu điện. Ta hoàn toàn có thể mô hình hóa bài toán trên thành tìm một chu trình đi qua tất cả các cạnh đúng một lần trong đồ thị có $n$ đỉnh và $m$ cạnh, hay nói cách khác ta cần tìm
một chu trình Euler cho đồ thị trên.

Trước hết, một đồ thị chỉ có chu trình Euler khi và cả chỉ khi tất cả các đỉnh của đồ thị đều có bậc chẵn, nên ta cần phải kiểm tra trước điều kiện này.
```cpp
for (int i = 1; i <= n; ++i) {
    if (adj[i].size() % 2 != 0) {
        cout << "IMPOSSIBLE" << '\n';
        return 0;
    }
}
```
Ta áp dụng thuật toán DFS từ đỉnh $1$ để duyệt qua các đường đi trong chu trình. Với mỗi lần DFS từ đỉnh $u$ sang các đỉnh kề $v$, ta thực hiện xóa đường đi $\left(u, v \right)$ ra khỏi danh sách kề. Bằng cách sử dụng cấu trúc dữ liệu set, ta có thể thực hiện truy vấn trên trong độ phức tạp $O\left(\log n\right)$.

Ngoài ra, ta cũng cần duy trì một vector $trace$ để lưu giữ đường đi trong chu trình.
```cpp
void dfs(int u) {
    while (adj[u].size()) {
        set<int>::iterator it = adj[u].begin();
        int v = *it;
        adj[u].erase(v);
        adj[v].erase(u);
        dfs(v);
    }
    trace.push_back(u);
}
```
Sau khi đã DFS, ta phải cần kiểm tra xem liệu rằng số đường đi trong chu trình có bằng $m + 1$ hay không? Nếu có, điều đó có nghĩa tồn tại chu trình cần tìm, ngược lại thì không.
```cpp
    dfs(1);
    if (int(trace.size()) != m + 1) {
        cout << "IMPOSSIBLE" << '\n';
        return 0;
    }
    for (auto x : trace)
        cout << x << ' ';
```
Độ phức tạp của bài toán này là: $O\left( \log n \times m \times n\right)$.

