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

**9. NKCABLE**

f[i] là cách nối từ máy thứ 1 -> máy thứ i

f[0] = 0;
f[1] = +oo (vì có 1 máy thì không thể nối được)
f[i] = min(f[i-1],f[i-2]) + a[i-1]

**10. NKREZ**

Sắp xếp các cuộc họp theo thứ tự thời gian kết thúc tăng dần (ki < kj với i < j)

Gọi f[i] là tổng thời gian lớn nhất mà hội trường được sử dụng qua i cuộc họp đầu

f[i] = f[i-1] nếu cuộc họp thứ i không được chọn.

Nếu chọn cuộc họp thứ i, vì mảng f là mảng tăng dần nên ta cần tìm vị trí j lớn nhất sao cho kj < pi -> f[j] + pi - kj = f[i].

Sử dụng chặt nhị phân để tìm vị trí j.

**11. QBSQUARE**

Gọi l[i][j] là số số 1 (or số 0) liên tiếp trên hàng i và xét đến cột j

Gọi c[i][j] là số số 1 (or số 0) liên tiếp trên cột j và xét đến hàng i

Gọi f[i][j] là cạnh của hình vuông lớn nhất có góc phải dưới là a[i][j]

- Rõ ràng, nếu a[i][j] != a[i-1][j-1] thì f[i][j] = 1 (hình vuông chỉ có a[i][j])

- Nếu a[i][j] == a[i-1][j-1] thì f[i][j] = min( c[i][j], l[i][j], f[i-1][j-1]+1 ), vì nếu hai ô kế trên và kế dưới khác a[i][j] thì c[i][j] or l[i][j] = 1 -> diện tích hình vuông max chỉ được 1.

![image](https://user-images.githubusercontent.com/69662229/110774412-9ffb4980-8212-11eb-8510-1417943caeba.png)

- Ví dụ hình trên: f[4][4] = min( c[4][4], l[4][4], f[3][3]+1 ) = min(1,1,2) = 1. 

![image](https://user-images.githubusercontent.com/69662229/110774789-084a2b00-8213-11eb-9ff5-b940525cf20b.png)

Hình vẽ tay nên hơi xâu :v 

- Another ex: f[4][4] = min( c[4][4], l[4][4], f[3][3]+1) = min( 2, 4, 1+1) = 2

Tính l[i][j] từ l[i][j-1] như sau : l[i][j] = l[i][j-1] + 1 nếu a[i][j] == a[i][j-1] , nếu không l[i][j] = 1

Tính c[i][j] tương tự.

**12. CNTBULLS**

Cho dãy ban đầu chỉ toàn bò cái, ta sẽ tìm cách thay thế các con bò đực rựa vô sao cho nó ko đánh nhau.

Gọi f[i] là số cách sắp bò đực vào khi xét đến vị trí thứ i.

Nhận thấy rằng nếu i < k+1 thì f[i] = i+1 (có i vị trí để thay và 1 cách là không cho thằng đực rựa nào vào hết)

-> f[i] = f[i-1] + 1 (số cách sắp tối đa ở i-1 con đầu và thêm 1 cách là con ở vị trí thứ i)

Còn nếu i >= k+1 thì f[i] = f[i-1] + f[i-k-1] tức là số cách sắp tối đa của i-1 con đầu và cộng thêm số cách sắp tối đa của i-k-1 con đầu (vì con thứ i-k-1 không đánh nhau với con i :D)

Kết quả là f[n] (nhớ lấy mod)

**13. PTRANG**

Gọi f[i] là số cách chia các từ vào dòng sao cho hệ số phạt là min.

Để tính f[i] ta chỉ cần xét mọi vị trí j trước i sao cho tổng độ dài các chữ từ j đến i không vượt quá l và lấy min

f[i] = min(f[i], max(f[j-1], l - sum(j,i)))

Kết quả là f[n].

**14. V8SCORE**

Gọi a[i][j] là điểm môn thứ i của giám khảo j

Gọi f[i][j] là điểm thứ i-1 được cộng vô khi xét 1->i điểm đầu và tạo thành tổng là j.

f[1][0] = 0 (không có bài thi số 0 và tổng bằng 0)

f[1][j] or f[i][0] = INF

Giả sử ta đang xét tới vị giám khảo thứ x, môn thứ i, tổng điểm tạo thành là j: nếu chọn điểm môn thứ i-1 của giám khảo x thì đầu tiên tổng điểm j phải lớn hơn a[i-1][x]; môn được chọn trước môn i-1 của giám khảo x phải bé hơn, tức là f[i-1][j-a[i-1][x]] <= a[i-1][x] (trong đó f[i-1][j-a[i-1][x]] là môn thứ i-2 được chọn và tạo thành tổng j-a[i-1][x]); và a[i-1][x] < f[i][j] thì f[i][j] = a[i-1][x].

Nếu f[k+1][s] = +oo thì không có cách chọn điểm thỏa mãn.

Nếu có cách chọn, ta truy vết để tìm kết quả:

k++, khi mà s != 0 thì push(f[k][s]) vào stack rồi lấy s -= f[k--][s] (tức là push f[k-1][s-f[k][s ban đầu]])

**15. BCDIV**

Gọi f[i][j] là số cách chia i phần tử đầu thành j nhóm

f[0][0] = 1 

f[i][j] = f[i-1][j] * j (số cách chia i-1 phần tử đầu vào j nhóm, giờ có thêm phần tử thứ i thì ta có thể bỏ i vô từng j nhóm)

f[i][j] += f[i-1][j-1] (Cộng thêm số cách chia i-1 phần tử đầu thành j-1 nhóm, phần tứ thứ i là nhóm thứ j)

kết quả là f[n][k], pre_calculated rồi truy vấn thôi.

*bài này dell có trên cf à =(((, voj như lìn ấy*

**16. COND**

Ta có thể suy nghĩ bài này theo 1 hướng khác, đó là chia các phần tử thành các tập chứa dấu bằng và đặt dấu bé giữa các tập hợp đó, (a1 = a2 = ...) < (ai = ai+1 = ...) < ...

Bài toán quy về số cách chia i phần tử thành j nhóm, kết quả ta chỉ cần for số nhóm (số dấu bé hơn) và cộng lại.

Với mỗi số dấu bé hơn, ta cần tìm số cách đặt dấu bé (tính như bài 15 ở trên) và với mỗi cách đặt dấu sẽ có số cách đặt các phần từ (là n!).

Tính trước mảng f[i][j] như bài 15, tính thêm một mảng g[i] là số cách sắp xếp i phần tử ( g[i] = i! )

Kết quả là ans = 1 (toàn bộ là dấu bằng) + f[n] (chỉ có 1 dấu bé) + dp[n][k] * f[k] (với k là số dấu bé, 2 <= k < n)
