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
