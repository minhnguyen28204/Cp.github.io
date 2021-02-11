---
layout: post
title: Z Function
tags : [Z]
comments : true
---

# Z Function
Z algorithm hay còn gọi là Z function, là thuật toán áp dụng cho các bài toán so khớp chuỗi.

## Bài toán
Cho một chuỗi S có độ dài n, Z function sẽ tạo ra mảng Z mà tại mỗi vị trí i ta có Zi là độ dài chuỗi con dài nhất là tiền tố của S bắt đầu tại Si. Độ phức tạp là O(n).
## Ý tưởng
Tham khảo ở VNOI.
https://vnoi.info/wiki/translate/codeforces/z-algo.md
## Cài đặt
```C++
z[1] = 0;
for(int k=2, l=1, r=1; k<=n; k++)
{
    int x = 0;
    int kk = k-l+1;
    if (k <= r) x = min(z[kk], r-k+1);
    while (a[x+1] == a[x+k] && k+x <= n) ++x;
    z[k] = x;
    if (r < k + x - 1)
    {
        l = k;
        r = k + x - 1;
    }
}
```
