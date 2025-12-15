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
