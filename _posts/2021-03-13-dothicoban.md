---
layout : post
title : Kiến thức đồ thị 
comments : true
tags : [graph]
---
# Một số kiến thức cần biết về đồ thị

## **1. BFS**

BFS là thuật toán duyệt đồ thị theo chiều rộng, khi thăm 1 đỉnh ta sẽ ưu tiên thăm các đỉnh kề với nó và đẩy các đỉnh thăm vào một hàng đợi, tiếp tục như vậy cho đến khi thăm hết các đỉnh.

Mã giải
```
queue q
push(đỉnh xuất phát)
while (q không rỗng)
{
  lấy đỉnh u từ q
  duyệt các đỉnh v kề u
  {
    nếu chưa thăm v thì đánh dấu đã thăm v và push(v) vào queue
  }
}
```

## **2. DFS**

Khác với BFS, DFS duyệt đồ thị theo chiều sâu, thuật toán này sẽ thăm các đỉnh cho đến khi hết thăm được nữa xong mới bắt đầu quay lại thăm nhánh khác. Ta cài đặt DFS bằng đệ quy.

Mã giải
```
DFS(u)
{
  đánh dấu u đã thăm
  duyệt các đỉnh v kề với u
  {
    nếu v chưa thăm thì thăm v
  }
  // trong một vài trường hợp cần đánh dấu lại u chưa thăm
  đánh dấu u chưa thăm
}
```

## **3. Dijkstra tìm đường đi ngắn nhất**

Thuật toán Dijkstra tìm đường đi ngắn nhất từ 1 đỉnh tới các đỉnh còn lại của đồ thị, giống như Bellman-Ford. Điểm tối ưu của Dijkstra là hiệu quả hơn và có thể sử dụng để thực hiện các đồ thị lớn. Tuy nhiên, thuật toán yêu cầu đồ thị không chứa cạnh có trọng số âm.

Giống như Bellman-Ford, Dijkstra định các giá trị của các đỉnh và giảm nó trong khi tìm kiếm. Thuật toán này hiệu quả, bởi vì nó chỉ thực hiện qua mỗi cạnh một lần, sử dụng giả thuyết là đồ thị không có cạnh trọng số âm.

**Example**

Dưới đây là cách mà thuật toán Dijkstra hoạt động trong đồ thị bên dưới, đỉnh xuất phát là 1:

![image](https://user-images.githubusercontent.com/69662229/111036031-0e3a3a80-83d2-11eb-9e08-3c49c06b74a8.png)

Như Bellman-Ford, ban đầu khoảng cách của đỉnh xuất phát là 0 và khoảng cách của các đỉnh khác là dương vô cùng.

Tại mỗi bước, Dijkstra chọn một đỉnh mà chưa được thăm và khoảng cách nhỏ nhất có thể. Đỉnh đầu tiền là đỉnh 1 với khoảng cách là 0.

Khi mà đỉnh đã được chọn, thuật toán bắt đầu thăm qua mọi cạnh ra từ đỉnh và giảm khoảng cách:

![image](https://user-images.githubusercontent.com/69662229/111036047-1abe9300-83d2-11eb-94e2-a938dc2bc50f.png)

Trong trường hợp trên, các cạnh từ đỉnh 1 giảm khoảng cách của đỉnh 2, 4 và 5, khoảng cách của chúng bây giờ là 5, 9 và 1.

Đỉnh tiếp theo được thực hiện là 5 với khoảng cách bằng 1. Lần thực hiện này giảm khoảng cách của đỉnh 4 từ 9 xuống 3:

![image](https://user-images.githubusercontent.com/69662229/111036056-27db8200-83d2-11eb-91bd-6b1e28666fb9.png)

Sau đó, đỉnh tiếp theo là 4, giảm khoảng cách của đỉnh 3 xuống 9:

![image](https://user-images.githubusercontent.com/69662229/111036075-3c1f7f00-83d2-11eb-8be1-d7ad41ae9760.png)

Một điều đáng chú ý trong thuật toán Dijkstra đó là bất cứ khi nào một đỉnh đã được thăm thì khoảng cách của nó đã tối ưu. Ví dụ, tại thời điểm này của thuật toán, khoảng cách 0, 1, 3 là khoảng cách ngắn nhất của đỉnh 1, 5 và 4.

Sau đó, thuật toán thăm hai đỉnh cuối, và kết quả cuối cùng như sau:

![image](https://user-images.githubusercontent.com/69662229/111036078-40e43300-83d2-11eb-9a49-12c075b97462.png)

Mã giải
```
Gọi d[u] là độ dài nhỏ nhất khi đi từ đỉnh xuất phát đến u
d[start] = 0, d[i] = +oo

hàng đợi ưu tiên q.
push(đỉnh xuất phát,độ dài đang xét ở đỉnh xuất phát //thường là 0)
while (q khác rỗng)
{
  lấy đỉnh u và độ dài đang xét ở đỉnh u, gọi tắt là du
  nếu d[u] != du thì tiếp tục không xét đỉnh này
  duyệt các đỉnh v kề với u
  {
    uv là độ dài từ u tới v
    nếu d[v] > d[u] + uv thì cập nhập d[v] = d[u] + uv và push(v, d[v])
  }
}
```

## **4. Bellman-Ford tìm đường đi ngắn nhất trên đồ thị có trọng số âm**


## **5. Tìm chu trình âm của đồ thị bằng Bellman-Ford**


## **6. Topological sort bằng BFS, DFS**
