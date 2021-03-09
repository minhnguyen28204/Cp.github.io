---
layout : post
comments : true
tags : [dp]
title : Quy hoạch động
---
## Beginner

[Tham khảo ở Vnoi](https://vnoi.info/wiki/translate/topcoder/dynamic-programming.md)

Bài tập:

**1. ZigZag**

Gọi f1[i] là cách chọn tối ưu khi xét đến phần tử thứ i và trước đó là a[i] - a[j] < 0

Gọi f2[i] là cách chọn tối ưu khi xét đến phần tử thứ i và trước đó là a[i] - a[j] > 0

Với mỗi j < i, nếu a[i] - a[j] > 0 thì f2[i] = max(f2[i], f1[i]+1), nếu a[i]-a[j]<0 thì f1[i] = max(f1[i],f2[j]+1).

Kết quả là max(f1[i], f2[i]) (Với mọi 1 <= i <= n).

**2. BadNeighbors**

Gọi f[i] là cách chọn tối ưu khi xét đến vị trí thứ i, oneinclu[i] bằng true nếu ở cách chọn thứ i có phần tử đầu tiên, ithinclu[i] bằng true nếu ở cách chọn thứ i có chọn phần tử thứ i.

Tính trước giá trị f[1] và f[2].

Ta sẽ có công thức như sau: 

Nếu f[i-2] + a[i] (tức là chọn phần tử thứ i) > f[i-1] (không chọn phần tử thứ i) thì f[i] = f[i-2] + a[i], oneinclu[i] = oneinclu[i-2], ithinclu[i] = 1;
Ngược lại f[i] = f[i-1];

Nếu (ithinclu[n] = 1 && oneinclu[n] = 1) thì kết quả là max( max(f[n-1], f[n]-a[n]), f[n]-a[1])
Nếu không kq = f[n]

## Intermediate
**1.AvoidRoads**

Gọi f[i][j] là số cách đi đến tọa độ (i,j)-> f[0][0] = 1

blockx[i][j][k] = true nếu đang ở cột k và đi được từ hàng i đến j

blocky[i][j][k] = true nếu đang ở hàng k và đi được từ cột i đến j

f[i][j] += f[i-1][j] nếu (i-1 >= 0 && blockx[i-1][i][j])

f[i][j] += f[i][j-1] nếu (j-1 >= 0 && blocky[j-1][j][i])

Kết quả là f[width][height]

Ai đó chỉ tôi cách nộp bài trên TopCoder đi ._.

**2.ChessMetric**

Gọi f[i][j][k] là số cách đi từ ***start*** đến (i,j) trong k bước.

Ta dùng thuật toán dfs để tính giá trị f[i][j][k]

stx, sty là tọa độ điểm xuất phát; enx, eny là tọa độ điểm kết thúc. f[stx][sty][0] = 1

dfs(x,y,timed) với tọa độ (x,y) và đang trong timed bước

tại x, y ta đi tới các tọa độ liền kề (sài mảng để lưu giá trị các bước kế tiếp), với u, v là tọa độ mới ta có f[u][v][timed+1] += f[x][y][timed];

Nếu u, v chưa thăm thì thăm

Sau khi thăm xong 1 đinh thì đánh vst bằng false lại.

Kết quả là f[enx][eny][num]

```

void dfs(int x, int y, int timed)

{

    vst[x][y] = true;

    for(int i=0; i<16; i++)
    
    {
    
        int u = x + dx[i];
        
        int v = y + dy[i];
        
        if (ok(u,v))
        
        { 
        
            f[u][v][timed+1] += f[x][y][timed];
            
            if (!vst[u][v]) dfs(u,v,timed+1);
            
        }
        
    }
    
    vst[x][y] = false;
    
}

```

## Upper-Intermediate
Cho đồ thị vô hướng G có trọng số dương và N đỉnh.

Ban đầu bạn có số tiền là M. Để đi qua đỉnh i, bạn phải trả số tiền là S[i]. Và đương nhiên, nếu không đủ tiền thì bạn không đi được. Tìm đường đi ngắn nhất từ 1 tới N thỏa mãn tiêu chí trên. Nếu có nhiều đường ngắn nhất, in ra đường với chi phí nhỏ nhất. Giới hạn: 1<N≤100; 0≤M≤100; 0≤S[i]≤100.

Có thể dễ dàng thấy đây là một bài Dijkstra cơ bản, tuy nhiên chỉ khác ở chỗ nó có thêm một điều kiện. Trong bài toán Dijkstra cơ bản ta có Min[i] , là độ dài đường đi ngắn nhất từ 1 tới i. Còn ở đây, chúng ta cần phải quan tâm đến số tiền còn lại. Do đó chúng ta có thể mở rộng mảng này thành Min[i][j] , là độ dài đường đi ngắn nhất tới i, và còn lại số tiền là j. Bằng cách này bài toán đã được đưa về bài toán Dijkstra quen thuộc. Tại mỗi bước ta tìm trạng thái (i,j) có quãng đường ngắn nhất, đánh dấu là đã thăm rồi update cho các trạng thái cạnh nó. Đáp án sẽ là Min[N][j] có giá trị nhỏ nhất (và j lớn nhất trong số các Min[N][j] có cùng giá trị).

-> Bài Roads trên Vnoi

# Giải bài qhđ trên Vnoi.

(Ctrl + f -> search tên bài)

**1. LIQ**

f[i] = f[j] + 1 nếu a[j] < a[i].

**2. NKTICK**

f[1] = a[1]
f[2] = min(f[1]+a[2],r[1])
f[i] = min( f[i-1]+a[i] , f[i-2]+r[i-1] )

**3. QBMAX**

f[i][j] là cách đi sao cho đến ô (i,j) đạt giá trị max.

f[i][j] = max(f[i-1][j-1]+a[i][j], max(f[i][j]+a[i][j], f[i+1][j-1]+a[i][j]) ) 

Kết quả là max f[i][m]

**4. LIS**

###### Sử dụng chặt nhị phân 

Công thức ở bài LIQ: f[i] = f[j] + 1 (nếu a[j] < a[i])

Trong công thức trên nếu ta gán hàm b(f[i]) = a[i] thì ta sẽ có mảng b với ý nghĩa: b(k) là giá trị kết thúc tại dãy con tăng có độ dài là k.

Giả sử đang duyệt tới vị trí i và f[i] = k. Ta gán b(k) = a[i] như trên, nếu có b(k) >= b(k+1) thì ta đã tính sai f(i), vì trước a[i] có 1 phần tử a[j] < a[i] mà f[j] > f[i].

b là dãy tăng nên ta sử dụng chặt nhị phân để tìm kiếm:

 -Khởi tạo dãy b có n phần tử, b(0) = -oo, các phần tử khác bằng +oo.

 -Duyệt i từ 1 đến n, mỗi lần duyệt tìm vị trí k đầu tiên có b(k) >= a[i]. Gán b(k) = a[i] (f[i]=k)
 
 Độ phức tạp là O(nlogn)

###### Sử dụng BIT (binary index tree)

Nếu gán b(a[i]) = f(i), mảng b(x) có ý nghĩa là độ dài dãy con tăng dài nhất kết thúc tại phần tử có giá trị là x.

Để tính f(i) ta cần tìm max từ giá trị 0 -> a[i]-1, sau đó gán f(i) = max + 1 và cập nhập b(a[i]). Sử dụng BIT để tìm max và cập nhập.

Độ phức tạp là O(nlogC) trong đó C là giới hạn giá trị của a[i].

Nếu giới hạn quá lớn thì ta nén số lại và tính.

**5. LATGACH**

Bài này là số fibanacci, f[i] = f[i-2] + f[i-1].

Còn why nó là số fibonacci thì xem ở đây ._. [Youtube](https://www.youtube.com/watch?v=ucbH-tga7U4&t=464s) (mấy ông Ấn Độ giỏi vlin :vv)

**6. VSTEPS**

f[1] = 1

f[i] += f[i-2] (nếu i-2 không bị hư)

f[i] += f[i-1] (nếu i-1 không bị hư)

**7. NKPALINS**

Ta đảo xâu lại và tìm xâu con chung dài nhất của hai xâu

- Nếu a[i] = b[j] thì f[i][j] = f[i-1][j-1] + 1
- Không thì f[i][j] = max(f[i-1][j],f[i][j-1])

Truy vết:

- i = n, j = n;
- Nếu a[i]=b[j] thì a[i] có trong xâu kết quả, i--, j--.
- Nếu f[i][j] = f[i-1][j] thì i--
- Nếu f[i][j] = f[i][j-1] thì j--

**8. BONES**

f[i] là số lần tổng i xuất hiện (i <= 80)

for i = 1 to S1

for j = 1 to S2

for k = 1 to S3

f[i+j+k]++;
            
Kết quả là i (với i là max (f[i]))

