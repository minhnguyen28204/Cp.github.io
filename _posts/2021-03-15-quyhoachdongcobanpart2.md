---
layout : post
comments : true
published : true
title : Quy hoạch động (P2)
tags : [dp]
---
# Giải bài quy hoạch động trên Vnoi (part 2)

**31. [QUAD](https://vnoi.info/problems/QUAD/)**

Tạm thời skip :), chưa biết cách làm

**32. [MCOINS](https://vnoi.info/problems/MCOINS/)**

![image](https://user-images.githubusercontent.com/69662229/111180985-c39ff600-856a-11eb-8909-8a201d5e82eb.png)

Bài cho trẻ con làm =)))

Gọi một mảng f[i], f[i]=1 nếu A thắng khi có i số xu, =0 nếu B thắng khi có i số xu.

f[0] = 0, f[1] = f[k] = f[l] = 1

f[i] or !f[i-1] (nếu i-1>=0, tức là i-1 xu đã biết được người thắng thì với i xu thì người kia sẽ thắng) 

f[i] or !f[i-k] (nếu i-k>=0)

f[i] or !f[i-l]

Phép or có nghĩa là chỉ cần có 1 trường hợp (i-1, i-k, i-l) xu mà Boyan thắng thì trường hợp i xu Asen sẽ thắng.

**33. EQSTR**

Bài này chỉ cần duyệt qua thôi, quy ước a=0, b=1, ..., z=25 thì tại vị trí i thì có 3 cách biến đổi:

- Đổi từ s[i] -> t[i]
- Đổi từ t[i] -> s[i]
- Đổi cả s[i] và t[i] về a

Kiểm tra xem cách đổi nào có số bước ngắn nhất, nếu cách 3 bé hơn hoặc bằng hai cách đầu thì ưu tiên cách 3 trước (đổi về a).

Đọc dữ liệu thì khởi tạo 1 xâu rf rồi dùng vòng while như sau: while (cin >> rf && rf!="[END]")

**34. [MPILOT](https://vnoi.info/problems/MPILOT/)**

Bài này có thể giải theo 2 cách: qhđ hoặc sài một cái heap.

**Cách 1: sử dụng quy hoạch động**

Giả sử ban đầu tất cả đều là lái chính, nhiệm vụ cần chọn ra n/2 thằng làm lái phụ sao cho trả lương ít nhất.

Gọi f[i][j] là độ chênh lệch giữa lương chính và lương phụ khi xét i phi công đầu tiên và có j trợ lái.

Đầu tiên các phi công phải sắp xếp giảm dần theo số tuổi -> với mọi i > 1, ta có thể chọn thằng phi công i làm phụ lái hoặc không chọn

- Nếu chọn phi công i làm phụ lái -> f[i][j] = f[i-1][j-1] + c[i] (kết quả tối ưu của i-1 phi công đầu có j-1 phụ lái, cộng thêm thằng i làm phụ lái là c[i])

Trong đó c[i] là độ chênh lệch lương chính và lương phụ của phi công i

- Nếu không chọn phi công i làm phụ lái -> f[i][j] = f[i-1][j] (kết quả tối ưu của i-1 phi công đầu và có j phụ lái)

Kết quả là sum-f[n][n/2] (sum là tổng lương chính của n phi công)

**làm cách này thì nộp trên voj, trên codeforce không để giới hạn mảng quá 1e6 được :)**

**Cách 2: Sử dụng một cái heap nho nhỏ :3**

Gọi một cái max heap lưu độ chênh lệch

Ta chỉ cần duyệt qua n-1 thằng phi công và lấy n/2 độ chênh lệch lương max.

Mỗi lần duyệt qua thằng i, đẩy độ chênh lệch lương của thằng i vô heap. Nếu i là số lẻ thì thằng top của heap thỏa điều kiện tuổi bé hơn lái chính khác -> lấy thằng top và pop nó khỏi heap, điều này đảm bảo những thằng làm trợ lái đều có thằng lái chính khác lớn tuổi hơn. (không biết giải thích sao nữa ._., cứ tính bằng tay là hiểu)

[Code](https://pastebin.com/ZfNVH0Wb)

**35. [EGG](https://vnoi.info/problems/EGG/)**

Khi thả 1 quả trứng ở tầng x, có hai khả năng xảy ra:

- Trứng vỡ thì ta chỉ cần thử từ những tầng nhỏ hơn và số lượng trứng mất đi 1 quả.
- Trứng không vỡ thì ta chỉ cần thử ở những tầng cao hơn -> số lượng tâng cần thử là tầng cao nhất trừ đi tầng hiện tại và số lượng trứng giữ nguyên.

Nếu chỉ cần 1 quả trứng thì chúng ta sẽ thả từ tầng 1 đến tầng cao nhất nên base case của 1 quả trứng là số tầng hiện tại.

Tương tự, nếu chì còn lại 1 tầng để thử hoặc không còn tầng nào để thử thì kết quả là số tầng. (nhiều trứng ntn cũng chỉ cần thả 1 tầng cuối là biết)

[Code back track](https://pastebin.com/mUC5GNBk)

Để Ac bài này cần chuyển về quy hoạch động, gọi mảng f[i][j] là số lần thả ít nhất để xác định được độ cứng của trứng khi có i quả và j tầng.

Ta có công thức tổng quát theo hướng giải trên là f[n][k] = 1 + min( max(f[n-1][i-1],f[n][k-i]) ) với (1 <= i <= m)

Nếu như ta cố định n và k, xét theo i ta thấy khi i tăng thì i-1 tăng nên f[n-1][i-1] tăng, i tăng thì m-i giảm nên f[n][m-i] giảm.

![image](https://user-images.githubusercontent.com/69662229/111334248-a0d81500-8630-11eb-9c92-50e958644e66.png)

*ảnh cop trên mạng nên hơi bị ngược tí, dp[n][k] là k quả trứng và n tầng*

![image](https://user-images.githubusercontent.com/69662229/111334928-35427780-8631-11eb-96c7-712bdb54d4c9.png)

max(f[n-1][i-1],f[n][m-i]) chính là đường màu tím.

Vậy ta thấy min của max(f[n-1][i-1],f[n][m-i]) chính là điểm giao nhau nó.

Từ đó ta có thể chặt nhị phân để tìm i 

Ta cần tìm vị trí i sao cho f[n-1][i-1] = f[n][m-i] với i trong đoạn [l,r]

Với mỗi vị trí mid = (l+r):2, ta nhận thấy nều f[n-1][mid-1] > f[n][m-mid] thì ta cần tìm một thằng mid mới trong đoạn [l,mid]

Ngược lại nếu f[n][m-mid] > f[n-1][mid-1] thì ta tiếp tục chặt nhị phân trong đoạn [mid,r]

Độ phức tạp là O(n*m*log(m))

[Code stolen từ vnoi mặc dù chả hiểu gì](https://pastebin.com/Y9UBL82t)

[Code chặt nhị phân](https://pastebin.com/Bs2Esrj1)

*Bài méo giải trí tí nào =((*

**36. [SPBINARY](https://vnoi.info/problems/SPBINARY/)**

Gọi f0[i] là số lượng xâu nhị phân độ dài i thỏa mãn đề bài có kết thúc cuối là 0.

f1[i] tương tự nhưng kết thúc cuối là 1

Base case f0[0] = f1[0] = 1

f0[i] bằng tổng của k trường hợp f1[i-1], f1[i-2], ..., f1[i-k]

f1[i] tính tương tự

Kết quả là f1[n] + f0[n]

*Bài này cài bignum mới làm đc*

**37. [HUGEKNAP](https://vnoi.info/problems/HUGEKNAP/)**

Gọi f[i][j] là giá trị nhận được tối đa khi xét i vật đầu và nhét khối lượng là j.

Với mỗi i, nếu w[i] > j thì không thể nhét vật i vào nên f[i][j] = f[i-1][j] (giá trị tối đa nhận được khi xét i-1 vật)

Còn nếu w[i] <= j thì có 2 trường hợp xảy ra:

- Lấy vật thứ i -> f[i][j] = f[i-1][j-a[i]] + v[i]
- Không lấy vật thứ i -> f[i][j] = f[i-1][j]

Truy vết:

Kết quả là f[n][W], gán i = n và j = W, khi mà i khác 0 và j khác 0 thì có hai trường hợp:

- Nếu f[i][j] == f[i-1][j] tức là vật i không được lấy thì i--
- Nếu f[i][j] != f[i-1][j] thì vật i được lấy -> lưu i vào mảng kết quả và j -= w[i]

*Bài này nộp trên cf thì MLE, nộp trên voj thì TLE :)))) chịu*

**38. [DISNEY1](https://vnoi.info/problems/DISNEY1/)

Gọi f[i][j] là chi phí ít nhất để Cuội đi đến i và Bờm đi đến j

f[1][1] = 0 (ban đầu Cuội và Bờm đều ở 1) và mọi f[i][j] = +oo

Vì phải đi theo một dãy tăng dần, giả sử C và B đang ở hai vị trí i, j thì vị trí tiếp theo cần đến là next = max(i,j)+1 để đảm bảo đi hết n vị trí.

Nếu next <= n, có 3 cách để đi:

- Cuội đi đến next, còn Bờm đứng yên -> f[next][j] = min(f[next][j], f[i][j] + a[i][next])
- Bờm đi đến next, còn Cuội đứng yên -> f[i][next] = min(f[i][next], f[i][j] + a[j][next])
- C và B đều đi đến next -> f[next][next] = min(f[next][next], f[i][j] + a[i][next] + a[j][next])

Nếu next = n+1 thì C và B đã đi hết n vị trí nên ta lấy res = min(f[i][j] + a[i][1] + a[j][1])

Kết quả là res

**39. [LQDFIBO](https://vnoi.info/problems/LQDFIBO/)**

Skip tiếp, lười code bignum lắm 

**40. [Bishwock](https://codeforces.com/problemset/problem/991/D)**

Bài này tham lam là được, gọi biến pre lưu số ô trống của cột trước i, khi xét đến cột thứ i có ba trường hợp xảy ra:

- Cả hai ô cột i đều trống -> nếu cột i-1 có 2 ô trống (pre=2) thì ta sẽ cho một bishwock vào hai ô cột i-1 và 1 ô cột i, còn nếu cột i-1 có 1 ô trống (pre=1) thì vừa đủ để nhét bishwock vào. -> cập nhập lại pre mới
- Chỉ có một ô cột i trống -> nếu pre = 2 thì ta mới nhét bishwock vào được.
- Không có ô nào cột i trống thì không nhét được gì hết -> cập nhập pre = 0.

Mỗi lần nhét tăng biến đếm lên, kết quả là biến đếm đó.

**41. [Tetrahedron](https://codeforces.com/problemset/problem/166/E)**

Tại một đỉnh bất kì có thể được đi qua từ 3 đỉnh còn lại, ta chỉ quan tâm cách đi tới đỉnh D, coi ba đỉnh ABC như một.

Gọi wD là cách đi tới đỉnh D, wabc là cách đi tới 3 đỉnh A, B, C. wD = 1, wabc=0

Với mỗi lần đi wD sẽ bằng tổng số cách đi từ A, B, C trước đó -> wD = (3 * wabc)

wabc sẽ bằng tổng số cách đi từ ba đỉnh còn lại tức là wabc = (2 * wabc + wD)

Kết quả là wD sau n lần cập nhập.

**42. [LSFIGHT](https://vnoi.info/problems/LSFIGHT/)**

Gọi f[i][j] bằng true nếu người thứ i có khả năng đứng bên trái người thứ j, nếu f[i][i] = true tức là người i có khả năng chiến thắng.

Để tính được f[i][j] ta cần xét mọi người k giữa i và j nếu như i có thể đứng bên trái k, k có thể đứng bên trái j, và một trong hai người i hoặc j có thể thắng k thì f[i][j] = true.

Ta duyệt khoảng cách, với mỗi khoảng cách ta tính i j tương ứng, kết quả là số lượng f[i][i] true với 1<=i<=n.

**43. [INCVN](https://vnoi.info/problems/INCVN/)**

Gọi f[i][j] là số lượng dãy con tăng có độ dài là j khi xét i phần tử đầu.

Theo công thức basic của basic là f[i][k] += f[j][k-1] với mọi j sao cho thỏa a[j] < a[i]

Base case là f[i][1] = 1 với mọi i

Dùng một BIT 2 chiều như bài KINV và cài đặt y hệt bài KINV (khác chỗ công thức và kết quả là sum(f[i][k]) với i >= k) 

**NHỚ FOR I XONG MỚI FOR K ._. FOR K TRƯỚC LÀ ĂN LÌN**

*t mệt mỏi với mấy cái for quá =((*

[Code](https://pastebin.com/Pdrs1N6J)

**44. [DISNEY2](https://vnoi.info/problems/DISNEY2/)**

Y hệt như bài Disney1 nhưng không có trường hợp i và j đến cùng lúc next. Thế thôi :D.

![image](https://user-images.githubusercontent.com/69662229/111647341-a1eb7c80-87bf-11eb-8564-f62aeb64944c.png)

=)) 

**45. [CTNOWN](https://vnoi.info/problems/CTNOWN/)**

Bội số chung nhỏ nhất của một tập số bằng tích của lũy thừa cao nhất của các số nguyên tố khác nhau tạo thành các số trong tập đó. (chắc là z :v, cấp 2 học r mà quên gần hết)

![image](https://user-images.githubusercontent.com/69662229/111722654-81530f00-881f-11eb-8c1f-192a31d3c6e8.png)

Nguồn wiki

-> Phân tích số thành tổng các lũy thừa của số nguyên tố và kiểm tra.

Gọi mảng d[i] chứa các số nguyên tố bé hơn 350.

f[i][j] là bội số chung nhỏ nhất của các số được phân tích từ i sao cho lớn nhất và số cuối có dạng d[j]^k.

f[0][j] = 1, f[i][0] = 1

f[i][j] = max (f[i-h][j-1]) với h = d[j]^k sao cho h <= i.

**46. [HAOI5000](https://vnoi.info/problems/HAOI5000/)**

Bài này sài two pointer, ban đầu ta tính khoảng cách từ máy 1 đến các máy có học sinh khác, gọi biến lưu khoảng cách đó là now, tính thêm số học sinh nằm trong khoảng (1,n/2+1) và lưu vào biến cnt.

Mảng c[i] lưu số lượng học sinh tại máy i.

Giả sử vị trí hiện tại là pos.

Khi dịch qua bên phải 1 đơn vị thì khoảng cách mới sẽ là vị trí (l,r) = (pos+1,n/2+2), ta nhận thấy rằng vị trí tới các máy nằm trong khoảng (l,r-1) sẽ giảm đi 1 đơn vị còn nếu n lẻ thì vị trí vòng cung từ r+1 trở về l-1 sẽ tăng, n chẵn thì vị trí r trở về l-1 tăng.

-> Giả sử vị trí tới k thằng học sinh đều tăng, ta chỉ cần cộng biến now lên k và trừ đi 2 lần số học sinh trong đoạn (l,r-1) và xét thêm số học sinh ở vị trí r trong các trường hợp của n là tính được biến now tại vị trí l.

-> now += k - 2 x (cnt-c[l-1]) - n % 2 x (c[r])

Giải thích ct: do cnt là số lượng học sinh từ đoạn (i, n/2+i) tức là (l,r-1) nên ta trừ đi c[l-1] là ra số lượng học sinh trong đoạn giảm khoảng cách. n % 2 x c[r] là nếu n là số chẵn thì vị trí r tăng nên không cần trừ c[r], còn nếu n lẻ thì vị trí r giữ nguyên khoảng cách nên sẽ trừ đi c[r].

cnt mới sẽ cộng thêm số lượng học sinh ở vị trí r trừ đi số học sinh ở vị trí l-1

Cập nhập biến now và lấy max là kết quả.

**47. [NKTOSS](https://vnoi.info/problems/NKTOSS/)**

bignum nên skip =(

**48. [NTSEQ](https://vnoi.info/problems/NTSEQ/)**

Bài này áp dụng từ bài dãy con tăng độ dài k có thể vét được 61đ :v 

*AC bài này còn dễ hơn cách vét điểm ._.*

Khởi tạo một mảng pair bit[N], với bit[i].fi là độ dài dãy con tăng dài nhất kết thúc tại giá trị i, bit[i].se là số lượng dãy con tăng dài nhất kết thúc tại giá trị i.

Get(int x) là lấy max độ dài các dãy con tăng dài nhất kết thúc tại các giá trị <= x, khởi tạo biến ans = ii(0,0), nếu mà ans.fi < bit[x].fi thì cập nhập ans, còn nếu ans.fi == bit[x].fi thì ans.se += bit[x].se

Cập nhập thì ngược lại.

Kết quả là Get(n-1).

[Code](https://pastebin.com/12FZXUp8)

[Code không AC, áp dụng phương pháp bài INCVN là tìm độ dài của dãy con tăng dài nhất rồi tìm số lượng dãy con tăng có độ dài bằng nó](https://pastebin.com/ZajPaDGB)

**49. [LEM5](https://vnoi.info/problems/LEM5/)**

Gọi f[i][j] là độ dài cấp số cộng dài nhất có công sai là d khi xét i phần tử đầu.

Vì a[i] khá lớn ( |a[i]| <= 1e9 ) nên ta cần nén lại dãy số để dễ dàng tính toán, ta thấy công sai d <= 100 nên ta sẽ sort lại dãy ban đầu, kiểm tra nếu a[i+1] lớn hơn a[i] 100 đơn vị thì ta cho a[i+1] = a[i]+101 (a[1] = 0) -> a[i] sẽ tối đa tầm 1e8 và dương.

Sau đó ta chỉ cần sử dụng một mảng đánh dấu g[i] với ý nghĩa là vị trí a[g[i]] = i.

Với mỗi f[i][j], nếu a[i]-j >= 0 và g[a[i]-j] > 0 thì f[i][j] = f[g[a[i]-j]][j] + 1, nếu không thì f[i][j] = 1.

Kết quả là max f[i][j].

**50. [IVANA](https://vnoi.info/problems/IVANA/)**

*chắc cày xong bài này qua đồ thị cày, sắp thi khu vực r ;-;*
