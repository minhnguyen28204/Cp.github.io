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
