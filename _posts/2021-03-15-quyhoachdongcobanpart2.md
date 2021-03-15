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

f[i] |= !f[i-1] (nếu i-1>=0, tức là trước đó f[i-1] Asen đi trước và đã biết được người thắng thì f[i] Asen đi trước thì người kia sẽ thắng) 

f[i] |= !f[i-k] (nếu i-k>=0)

f[i] |= !f[i-l]

Phép or ( |= ) có nghĩa là chỉ cần có 1 trường hợp (i-1, i-k, i-l) xu mà Boyan thắng thì trường hợp i xu Asen sẽ thắng.
