## Bellman-Ford Algorimth
Thuật toán Bellman-Ford được sử dụng để tìm đường đi ngắn nhất từ một đỉnh xuất phát đến mọi đỉnh khác nó. Thuật toán có thể áp dụng được cho mọi loại
đồ thị kể cả đồ thị không chứa chu trình âm. Nếu đồ thị chứa chu trình âm, thuật toán này có thể phát hiện nó.

## Example
![image](https://user-images.githubusercontent.com/69662229/109938591-0ddcc980-7c85-11eb-82ea-3a09e78cec23.png)

Hãy xem thuật toán Bellman-Ford hoạt động như thế nào trong đồ thị như ở trên:

Mỗi đỉnh của đồ thị được cho một giá trị khoảng cách, nút xuất phát có giá trị bằng không, các nút khác là dương vô cùng.

Thuật toán sẽ tìm cạnh để giảm độ lớn của khoảng cách. Đầu tiên, các nút được thăm từ đỉnh 1 giảm khoảng cách:

![image](https://user-images.githubusercontent.com/69662229/109939070-8b083e80-7c85-11eb-8d69-36fbce0e01ca.png)

Sau đó, cạnh 2-5 và 3-4 giảm khoảng cách:

![image](https://user-images.githubusercontent.com/69662229/109939186-a8d5a380-7c85-11eb-887a-bf980f42700d.png)

Thay đổi cuối cùng:

![image](https://user-images.githubusercontent.com/69662229/109939338-d0c50700-7c85-11eb-8076-5632d9c3b593.png)

Sau thay đổi cuối, không còn cạnh nào có thể giảm khoảng cách nữa. Điều này có nghĩa là khoảng cách cuối cùng, chúng ta đã tính thành công khoảng cách ngắn
nhất từ 1 đỉnh xuất phát đến các đỉnh còn lại.

Ví dụ: Min dis từ đỉnh 1 đến đỉnh 5 là đường đi như sau:

![image](https://user-images.githubusercontent.com/69662229/109939673-24cfeb80-7c86-11eb-9cf3-3c9dc92dcf65.png)

## Implementation

Đoạn code sau tính khoảng cách từ đỉnh x đến các đỉnh khác.

Dữ liệu được lưu trữ trong 1 struct trong đó u, v là hai đỉnh và w là khoảng cách giữa hai đỉnh đó.

``` C++

for(int i=1; i<=n; i++) d[i] = inf;
d[x] = 0;
//khoi tao gia tri cho cac nut

for(int i=1; i<n; i++)
{
  //m là số lượng các cạnh của đồ thị
  for(int j=1; j<=m; j++)
  {
    int u = a[j].u;
    int v = a[j].v;
    int w = a[j].w;
    d[v] = min(d[v],d[u]+w);
  }
}

```

Độ phức tạp thuật toán là O(nm).

###### source from competitive programing handbook.
