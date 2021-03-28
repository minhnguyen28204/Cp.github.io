---
layout : post
title : Đồ thị 
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

### Bellman-Ford Algorithm

Thuật toán Bellman-Ford được sử dụng để tìm đường đi ngắn nhất từ một đỉnh xuất phát đến mọi đỉnh khác nó. Thuật toán có thể áp dụng được cho mọi loại đồ thị kể cả đồ thị không chứa chu trình âm. Nếu đồ thị chứa chu trình âm, thuật toán này có thể phát hiện nó.

### Example

![image](https://user-images.githubusercontent.com/69662229/111105696-c0781c00-8510-11eb-9e7e-38afc96a397b.png)

Hãy xem thuật toán Bellman-Ford hoạt động như thế nào trong đồ thị như ở trên:

Mỗi đỉnh của đồ thị được cho một giá trị khoảng cách, nút xuất phát có giá trị bằng không, các nút khác là dương vô cùng.

Thuật toán sẽ tìm cạnh để giảm độ lớn của khoảng cách. Đầu tiên, các nút được thăm từ đỉnh 1 giảm khoảng cách:

![image](https://user-images.githubusercontent.com/69662229/111105724-ccfc7480-8510-11eb-811f-661e16f0f81f.png)

Sau đó, cạnh 2-5 và 3-4 giảm khoảng cách:

![image](https://user-images.githubusercontent.com/69662229/111105754-df76ae00-8510-11eb-9706-d570edb14f3f.png)

Thay đổi cuối cùng:

![image](https://user-images.githubusercontent.com/69662229/111105760-e4d3f880-8510-11eb-80b2-4e95f8a94b43.png)

Sau thay đổi cuối, không còn cạnh nào có thể giảm khoảng cách nữa. Điều này có nghĩa là khoảng cách cuối cùng, chúng ta đã tính thành công khoảng cách ngắn nhất từ 1 đỉnh xuất phát đến các đỉnh còn lại.

Ví dụ: Min dis từ đỉnh 1 đến đỉnh 5 là đường đi như sau:

![image](https://user-images.githubusercontent.com/69662229/111105770-eb627000-8510-11eb-81ab-4929c6903817.png)

### Implementation

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
// do phuc tap O(n*m)
```

## **5. Tìm chu trình âm của đồ thị bằng Bellman-Ford**

Thuật toán Bellman Ford cũng có thể dùng để kiểm tra nếu đồ thị có chu trình âm. Ví dụ như đồ thị sau

![image](https://user-images.githubusercontent.com/69662229/111105829-0af99880-8511-11eb-91f3-2df2a3ca69d9.png)

có chứa chu trình âm 2 -> 3 -> 4 -> 2 với trọng số là -4

Nếu mà đồ thị có chứa chu trình âm, chúng ta có thể giảm khoảng cách vô hạn lần bằng cách lặp lại chu trình âm. Vì thế khoảng cách ngắn nhất không có nghĩa trong trường hợp này.

Một chu trình âm có thể phát hiện bằng cách thực hiện thuật toán n lần. Trong lần thực hiện thứ n, nếu nó giảm đi một khoảng cách bất kì thì đồ thị có chứa 1 chu trình âm. Chú ý rằng thuật toán này có thể dùng để tìm kiếm chu trình âm trong toàn đồ thị bất kể đỉnh xuất phát nào.

## **6. Topological sort bằng BFS, DFS**

### Topological Sorting
Cho một đồ thị với N đỉnh và M cạnh. Yêu cầu trả về số thứ tự của các đỉnh sao cho mỗi đỉnh có số thứ tự bé hơn đều có thể đi đến được đỉnh có số lớn hơn.

Nói cách khác phải tìm một hoán vị của các đỉnh (topological order) để cho tương ứng với các cạnh của đồ thị

Topological order có thể non-unique (không độc nhất).

Topological order không xuất hiện nếu đồ thị có chứa chu trình (cycles).

### The algorithm
Để giải quyết vấn đề này, ta sài DFS hoặc BFS cũng được.

Giả sử đồ thị là một acyclic graph (đồ thị có hướng không có chu trình), sẽ có ít nhất 1 đáp án.

**DFS**

Gọi một dãy T là dãy đánh thứ tự các đỉnh của đồ thị. Ta sẽ dfs những đỉnh chưa được thăm, đến khi không còn cạnh ra thì đỉnh đó là một đỉnh sinks nên ta thêm đỉnh đó vào cuối dãy. Và cứ thế cho đến khi cả N đỉnh đều được thăm

Độ phức tạp cho dfs N đỉnh là O(n) và thăm xấu nhất qua M cạnh là O(N+M).

**BFS**

Đầu tiên ta đánh dấu các đỉnh có đầu vào bằng 0, push các đỉnh đó vào hàng đợi (queue) và đánh dấu vào mảng kết quả.

Bắt đầu lấy từng đỉnh trong queue, duyệt các đỉnh v kề nó và giảm số đỉnh đầu vào của v đi 1, sau đó duyệt các đỉnh v lần nữa, nếu đỉnh v có đầu vào là 0 thì push vô queue và đánh dấu vào mảng kết quả.

### Implementation

**DFS**
```
// a là vector chứa các đỉnh kề với u
// d[u] = 0 là chưa thăm, d[u] = 1 là đã thăm
void dfs(int u) 
{
	if (d[u]) return;
	for (int i=0; i<a[u].size(); i++)
	{
		int v = a[u][i];
		if (!d[v]) dfs(v);
	}
	d[u]=1;
	topsort[cnt]=u;
	cnt--;
}
```

**BFS**
```
//res[] là mảng lưu kết quả topo sort, ans là số lượng đỉnh đã được sắp xếp
// dv[i] lưu số đỉnh đầu vào của i, a[u].pb(v) thì dv[v]++

for(int i=1; i<=n; i++) if (dv[i]==0)
{
  q.push(i);
  ans++;
  res[ans] = i;
}

while (q.size())
{
  int u = q.front();
  q.pop();
  for(int v : a[u])
  {
    dv[v]--;
  }
  for(int v : a[u])
  {
    if (dv[v]==0){
      q.push(v);
      res[++ans] = v;
    }
  }
}
```

## **7. Đường đi Euler**

Một đường đi Euler là một đường đi qua mỗi cạnh của đồ thị đúng một lần duy nhất. Ví dụ đồ thị sau:

![image](https://user-images.githubusercontent.com/69662229/112726303-e53d9d80-8ed9-11eb-9d82-4690313e3f58.png)

Có đường đi Euler từ đỉnh 2 đến đỉnh 5 như sau:

![image](https://user-images.githubusercontent.com/69662229/112726317-fbe3f480-8ed9-11eb-8d53-ae89be336d2a.png)

*Fun fact: Ông Euler phát hiện ra đường đi này vào năm 1736 khi đang giải quyết một bài toán nổi tiếng là bảy cây cầu của Königsberg. Từ đây khai sinh ra lý thuyết đồ thị T.T*

Một chu trình Euler là một đường đi Euler mà xuất phát từ một đỉnh và kết thúc ngay tại đỉnh đó. Ví dụ như đồ thị sau:

![image](https://user-images.githubusercontent.com/69662229/112726409-8af10c80-8eda-11eb-8e31-c5286a9de2c2.png)

có một chu trình Euler từ đỉnh 1.

![image](https://user-images.githubusercontent.com/69662229/112726423-9e03dc80-8eda-11eb-9c00-31f559d9b618.png)

### Khi nào thì có đường đi Euler và chu trình Euler

Đường đi Euler và chu trình Euler xuất hiện dựa vào bậc của các đỉnh. Đầu tiên, một đồ thị vô hướng có đường đi Euler khi và chỉ khi mỗi cạnh đều thuộc cùng một thành phần liên thông và:

- Bậc của mỗi đỉnh là chẵn hoặc
- Có chính xác hai đỉnh bậc lẻ, các đỉnh còn lại bậc chẵn.

Trong trường hợp đầu tiên, Đường đi Euler cũng chính là chu trình. Trong trường hợp thứ hai, hai đỉnh bậc lẻ là đỉnh xuất phát và đỉnh kết thúc của đường đi Euler.

Ví dụ đồ thị sau:

![image](https://user-images.githubusercontent.com/69662229/112726623-a3155b80-8edb-11eb-8a0e-c802b12acf09.png)

Có đỉnh 1, 3 và 4 bậc là 2, và đỉnh 2, 5 có bậc là 3. Có chính xác hai đỉnh bậc lẻ, nên có một đường đi Euler giữa đỉnh 2 và đỉnh 5, nhưng không có chu trình Euler.

Trong một đồ thị có hướng, chúng ta tập trung vào bậc vào và bậc ra của đỉnh. Một đồ thị có hướng chứa đường đi Euler khi và chỉ khi mọi cạnh thuộc cùng 1 thành phần liên thông và:

- Mỗi đỉnh, bậc vào bằng bậc ra hoặc
- Có một đỉnh bậc vào lớn hơn bậc ra, đỉnh khác có bậc ra lớn hơn bậc vào, và các đỉnh còn lại có bậc vào bằng với bậc ra.

Trường hợp 1 thì đường đi Euler cũng chính là chu trình Euler, trong trường hợp hai, đồ thị có chứa đường đi Euler từ đỉnh có bậc ra lớn hơn và kết thúc tại đỉnh có bậc vào lớn hơn.

Ví dụ đồ thị sau:

![image](https://user-images.githubusercontent.com/69662229/112726755-4fefd880-8edc-11eb-8595-f167aed125c0.png)

Đỉnh 1, 3 và 4 có bậc vào là 1 và bậc ra là 1, đỉnh 2 có bậc vào là 1 và bậc ra là 2, đỉnh 5 có bậc vào là 2 và bậc ra là 1. Vì thế, có một đường đi Euler từ đỉnh 2 và kết thúc tại đỉnh 5.

![image](https://user-images.githubusercontent.com/69662229/112726808-89284880-8edc-11eb-8f77-c9e31f9442a9.png)

