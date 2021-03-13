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

**1. [LIQ](https://vnoi.info/problems/LIQ)**

f[i] = f[j] + 1 nếu a[j] < a[i].

**2. [NKTICK](https://vnoi.info/problems/NKTICK)**

f[1] = a[1]
f[2] = min(f[1]+a[2],r[1])
f[i] = min( f[i-1]+a[i] , f[i-2]+r[i-1] )

**3. [QBMAX](https://vnoi.info/problems/QBMAX)**

f[i][j] là cách đi sao cho đến ô (i,j) đạt giá trị max.

f[i][j] = max(f[i-1][j-1]+a[i][j], max(f[i][j]+a[i][j], f[i+1][j-1]+a[i][j]) ) 

Kết quả là max f[i][m]

**4. [LIS](https://vnoi.info/problems/LIS)**

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

**5. [LATGACH](https://vnoi.info/problems/LATGACH)**

Bài này là số fibanacci, f[i] = f[i-2] + f[i-1].

Còn why nó là số fibonacci thì xem ở đây ._. [Youtube](https://www.youtube.com/watch?v=ucbH-tga7U4&t=464s) (mấy ông Ấn Độ giỏi vlin :vv)

**6. [VSTEPS](https://vnoi.info/problems/VSTEPS)**

f[1] = 1

f[i] += f[i-2] (nếu i-2 không bị hư)

f[i] += f[i-1] (nếu i-1 không bị hư)

**7. [NKPALINS](https://vnoi.info/problems/NKPALIN)**

Ta đảo xâu lại và tìm xâu con chung dài nhất của hai xâu

- Nếu a[i] = b[j] thì f[i][j] = f[i-1][j-1] + 1
- Không thì f[i][j] = max(f[i-1][j],f[i][j-1])

Truy vết:

- i = n, j = n;
- Nếu a[i]=b[j] thì a[i] có trong xâu kết quả, i--, j--.
- Nếu f[i][j] = f[i-1][j] thì i--
- Nếu f[i][j] = f[i][j-1] thì j--

**8. [BONES](https://vnoi.info/problems/BONES)**

f[i] là số lần tổng i xuất hiện (i <= 80)

for i = 1 to S1

for j = 1 to S2

for k = 1 to S3

f[i+j+k]++;
            
Kết quả là i (với i là max (f[i]))

**9. [NKCABLE](https://vnoi.info/problems/NKCABLE)**

f[i] là cách nối từ máy thứ 1 -> máy thứ i

f[0] = 0;
f[1] = +oo (vì có 1 máy thì không thể nối được)
f[i] = min(f[i-1],f[i-2]) + a[i-1]

**10. [NKREZ](https://vnoi.info/problems/NKREZ)**

Sắp xếp các cuộc họp theo thứ tự thời gian kết thúc tăng dần (ki < kj với i < j)

Gọi f[i] là tổng thời gian lớn nhất mà hội trường được sử dụng qua i cuộc họp đầu

f[i] = f[i-1] nếu cuộc họp thứ i không được chọn.

Nếu chọn cuộc họp thứ i, vì mảng f là mảng tăng dần nên ta cần tìm vị trí j lớn nhất sao cho kj < pi -> f[j] + pi - kj = f[i].

Sử dụng chặt nhị phân để tìm vị trí j.

**11. [QBSQUARE](https://vnoi.info/problems/QBSQUARE)**

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

**12. [CNTBULLS](https://vnoi.info/problems/CNTBULLS)**

Cho dãy ban đầu chỉ toàn bò cái, ta sẽ tìm cách thay thế các con bò đực rựa vô sao cho nó ko đánh nhau.

Gọi f[i] là số cách sắp bò đực vào khi xét đến vị trí thứ i.

Nhận thấy rằng nếu i < k+1 thì f[i] = i+1 (có i vị trí để thay và 1 cách là không cho thằng đực rựa nào vào hết)

-> f[i] = f[i-1] + 1 (số cách sắp tối đa ở i-1 con đầu và thêm 1 cách là con ở vị trí thứ i)

Còn nếu i >= k+1 thì f[i] = f[i-1] + f[i-k-1] tức là số cách sắp tối đa của i-1 con đầu và cộng thêm số cách sắp tối đa của i-k-1 con đầu (vì con thứ i-k-1 không đánh nhau với con i :D)

Kết quả là f[n] (nhớ lấy mod)

**13. [PTRANG](https://vnoi.info/problems/PTRANG)**

Gọi f[i] là số cách chia các từ vào dòng sao cho hệ số phạt là min.

Để tính f[i] ta chỉ cần xét mọi vị trí j trước i sao cho tổng độ dài các chữ từ j đến i không vượt quá l và lấy min

f[i] = min(f[i], max(f[j-1], l - sum(j,i)))

Kết quả là f[n].

**14. [V8SCORE](https://vnoi.info/problems/V8SCORE)**

Gọi a[i][j] là điểm môn thứ i của giám khảo j

Gọi f[i][j] là điểm thứ i-1 được cộng vô khi xét 1->i điểm đầu và tạo thành tổng là j.

f[1][0] = 0 (không có bài thi số 0 và tổng bằng 0)

f[1][j] or f[i][0] = INF

Giả sử ta đang xét tới vị giám khảo thứ x, môn thứ i, tổng điểm tạo thành là j: nếu chọn điểm môn thứ i-1 của giám khảo x thì đầu tiên tổng điểm j phải lớn hơn a[i-1][x]; môn được chọn trước môn i-1 của giám khảo x phải bé hơn, tức là f[i-1][j-a[i-1][x]] <= a[i-1][x] (trong đó f[i-1][j-a[i-1][x]] là môn thứ i-2 được chọn và tạo thành tổng j-a[i-1][x]); và a[i-1][x] < f[i][j] thì f[i][j] = a[i-1][x].

Nếu f[k+1][s] = +oo thì không có cách chọn điểm thỏa mãn.

Nếu có cách chọn, ta truy vết để tìm kết quả:

k++, khi mà s != 0 thì push(f[k][s]) vào stack rồi lấy s -= f[k--][s] (tức là push f[k-1][s-f[k][s ban đầu]])

**15. [BCDIV](https://vnoi.info/problems/BCDIV)**

Gọi f[i][j] là số cách chia i phần tử đầu thành j nhóm

f[0][0] = 1 

f[i][j] = f[i-1][j] * j (số cách chia i-1 phần tử đầu vào j nhóm, giờ có thêm phần tử thứ i thì ta có thể bỏ i vô từng j nhóm)

f[i][j] += f[i-1][j-1] (Cộng thêm số cách chia i-1 phần tử đầu thành j-1 nhóm, phần tứ thứ i là nhóm thứ j)

kết quả là f[n][k], pre_calculated rồi truy vấn thôi.

*bài này dell có trên cf à =(((, voj như lìn ấy*

**16. [COND](https://vnoi.info/problems/COND)**

Ta có thể suy nghĩ bài này theo 1 hướng khác, đó là chia các phần tử thành các tập chứa dấu bằng và đặt dấu bé giữa các tập hợp đó, (a1 = a2 = ...) < (ai = ai+1 = ...) < ...

Bài toán quy về số cách chia i phần tử thành j nhóm, kết quả ta chỉ cần for số nhóm (số dấu bé hơn) và cộng lại.

Với mỗi số dấu bé hơn, ta cần tìm số cách đặt dấu bé (tính như bài 15 ở trên) và với mỗi cách đặt dấu sẽ có số cách đặt các phần từ (là n!).

Tính trước mảng f[i][j] như bài 15, tính thêm một mảng g[i] là số cách sắp xếp i phần tử ( g[i] = i! )

Kết quả là ans = 1 (Tôi cũng k hiểu tại sao lại có số 1 ở đây) + f[n] (không có dấu bé nào) + dp[n][k] * f[k] (với k là số tập hợp được chia, 2 <= k < n)

**17. [DTDOI](https://vnoi.info/problems/DTDOI)**

Do max(S) = 1e9 còn sum(a[i]) = 10000 nên ta sẽ tham lam chọn thằng lớn nhất cho đến khi S < sum(a[i]), cho lớn hơn tí là 20000, add là số tờ tiền lớn nhất được chọn.

Gọi f[i] là số đồng tiền ít nhất cần chọn để tạo thành tổng i.

Với mỗi a[j] <= i ta sẽ kiểm tra và lấy min -> f[i] = min(f[i], f[i-a[j]]+1)

Kết quả là f[s] + add.

**18. [THEME](https://vnoi.info/problems/THEME)**

Lợi dụng những đặc điểm sau để thiết kế giải thuật duyệt bình thường vẫn Full Test ngon lành :

- Đoạn cao trào phải có từ 5 nốt nhạc trở lên.
- Những lần xuất hiện của đoạn không được chồng lên nhau ( không có nốt nhạc chung ).

Cho biến i chạy theo khoảng cách giữa 2 nốt thuộc đoạn cao trào này vào hai nốt thuộc đoạn cao trào kia. Vì đề chỉ yêu cầu đoạn cao trào có số lần xuất hiện > 2 nên chỉ cần xét hai đoạn cao trào là đủ. Không nhất thiết phải tuân thủ theo nguyên tắc “chệnh lệch độ cao giữa hai nốt liên tiếp thì chắc chắn giống”, ta vẫn có thể nhận ra rằng 2 nốt cùng vị trí thuộc hai đoạn cao trào khác nhau có độ chênh lệch không đổi. Ta sẽ sử dụng nó làm điều kiện đánh giá. Cho biến j chạy theo vị của nốt nhạc thuộc đoạn cao trào thứ 1 và nốt cùng vị trí thuộc đoạn cao trào thứ 2 sẽ là i + j. So sánh độ chênh lệch nếu phù hợp thì tăng biến đến. Nếu không phù hợp thì khởi tạo lại biến đếm và độ chênh lệch. Lưu ý luôn cập nhật giá trị max từ biến đếm thường xuyên.

*DYNAMIC WAYS WILL BE RELEASED LATER :D*

**19. [ELEVATOR](https://vnoi.info/problems/ELEVATOR)**

Gọi f[i][j] là mảng lưu kết quả khi xét đến loại đá i có độ cao j.

Sắp xếp lại dữ liệu theo a tăng dần.

Đầu tiên ta duyệt qua các loại đá, với mỗi loại đá ta duyệt j theo độ cao tối đa của loại đá đó, rồi ta duyệt k số lượng của loại đá đó.

Nếu độ cao khi xếp k viên đó loại i <= độ cao tối đa của i (tức là k * h[i] <= a[i]) và độ cao tối đa trừ đi độ cao của k viên đá <= độ cao tối đa của viên đá thứ i-1 ( tức là -k* h[i] + j <= a[i-1] ) thì ta sẽ kiểm tra k khối đá đó và lấy max -> f[i][j] = max(f[i][j], f[i-1][j-k * h[i]] + k * h[i]. 

Kết quả là max f[n][j].

**20. [NKPATH](https://vnoi.info/problems/NKPATH)**

Bài này dễ thôi, dộng thẳng 4 vòng for mà làm ._. (100^4)

For p q rồi for i j r kiểm tra nếu ô (i,j) có đến được ô(p,q) hay không, nếu đến được thì f[p][q] += f[i][j]

Kết quả là sum(f[i][n])

**21. [SPSEQ](https://vnoi.info/problems/SPSEQ)**

Gọi f[i] là độ dài dãy con tăng dài nhất khi xét từ 1 đến i.

Gọi g[i] là độ dài dãy con tăng dài nhất khi xét từ n đến i.

Tính f[i] và g[i] như bài LIS (đảo ngược mảng a lại và tính g[i])

![image](https://user-images.githubusercontent.com/69662229/111028667-da005300-83ac-11eb-8ef1-1094f314713b.png)

Như ví dụ trên, giả sử f[i] = 5 còn g[j] = 10 thì ta sẽ lấy đoạn f[i] và thêm 5 đoạn g[j] (chắc chắn sẽ lấy được vì độ dài dãy con tăng dài nhất tại vị trí j là 10 mà) -> kết quả là min(f[i],g[j]) * 2 - 1 (trừ 1 vì nó bị double thằng i).

**22. [LQDGONME](https://vnoi.info/problems/LQDGONME)**

Gọi a[i][j] là phần tử thứ j của hoán vị i.

Gọi f[i] là độ dài dãy con tăng max khi xét đến phần tử a[1][i]

Và d[i][j] là vị trí của phần tử có giá trị bằng j trong hoán vị thứ i

Chọn hoán vị đầu tiên làm hoán vị ban đầu, khi xét đến phần tử thứ i trong hoán vị đầu, điều ta cần làm là xét những phần tử j ở trước nó trong hoán vị. Với mỗi phần tử j, ta xem thứ tự của a[k][i] có lớn hơn a[k][j]  hay không (k <= m). Nếu tất cả các hoán vị đều tuân theo trật tự này. Ta gán f[a(1, i)] = max (f [a(1, i)], f[a(1, j)]+1). Kết quả là max của tấ cả các f.

Cơ sở qhđ : f[i] = 1.

*stolen from cowboycoder :D*

**23. [QBPAL](https://vnoi.info/problems/QBPAL)**

Gọi f[i][j] là số xâu palindrome trong đoạn i -> j

- Ban đầu số xâu palindrome của f[i][j] sẽ bằng f[i+1][j] + f[i][j-1] - f[i+1][j-1]
- Nếu s[i]=s[j] thì f[i][j] += f[i+1][j-1]+1.

Bài này là BigNum :), skip.

**24. [NKH](https://vnoi.info/problems/NKH)**

Bài này làm theo đệ quy ngon lành, gọi thủ tục bktr(i,j,k) với i là vị trí hiện tại của S1, j là vị trí hiện tại của S2 và k là vị trí hiện tại của S.

Nếu S[k] == S1[i] thì bktr(i+1,j,k+1) 

Nếu S[k] == S2[j] thì bktr(i,j+1,k+1)

Mỗi lần đệ quy tiếp thì lưu vị trí vào một mảng res.

Nếu k=n+1 thì xuất mảng res ra và kết thúc chương trình (đã kiếm được 1 đáp án thỏa mãn).

**25. [KINV](https://vnoi.info/problems/KINV)**

Bài này là bài mở rộng hơn của bài [NKINV](https://vn.spoj.com/problems/NKINV/) (tên đọc lẹo cả lưỡi ._.)

Cách giải bài NKINV là ta sử dụng BIT. Khi đọc vô một giá trị x, ta sẽ cộng vô các giá trị (x+1) (vì các giá trị này đã có sẵn nên j < i và lớn hơn x nên tạo thành cặp nghịch thế) đã có sẵn trên BIT và update lại BIT.

```
    res += get(x+1);
    up(x);
```

Thủ tục get

```
    void get(int x)
    {
        int ans = 0;   
        for(; x < N; x += x & -x) ans += bit[x];
        return ans;
    }
    
 ```
 
 Thủ tục update
 
 ```
    void update(int x)
    {
        for(; x > 0; x -= x & -x) bit[x]++;
    }
 ```
 
 **Trở lại với cách giải bài KINV**
 
 Gọi f[k][i] là số dãy nghịch thế độ dài k kết thúc tại a[i].
 
 Ban đầu f[1][i] = 1 (với mọi i), ta có f[k][i] = Σf[k-1][j] với mọi j < i và a[j] > a[i].
 
 Kết quả là sum(f[k][i]).
 
 [Code here](https://pastebin.com/miFt4UA7)
 
 **26. [QBDIVSEQ](https://vnoi.info/problems/QBDIVSEQ)**
 
 Dễ thấy rằng một phần tử mà nhỏ hơn vị trí trước nó bất kì thì ta phải thêm nó vào 1 dãy con tăng mới -> số cách chia ít nhất chính là độ dài của dãy con giảm dài nhất.
 
 **27. HAF1**
 
 Ngủ mai học tiếp, đuối vl =((
