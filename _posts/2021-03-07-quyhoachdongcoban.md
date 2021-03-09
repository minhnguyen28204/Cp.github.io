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
