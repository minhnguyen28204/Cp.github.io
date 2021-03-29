---
layout : post
title : Đồ thị but không phải dijkstra :3 
tags : [graph]
published : true
comments : true
---

**1. [1-Trees and Queries](https://codeforces.com/problemset/problem/1304/E)**

Dịch đề: cho một cây có n đỉnh, có q truy vấn, với mỗi truy vấn x y a b k hỏi có tồn tại đường đi từ a đến b độ dài đúng bằng k sau khi nối thêm cạnh giữa x và y. Một đường đi thỏa mãn có thể đi qua nhiều đỉnh và nhiều cạnh trùng nhau.

Gọi độ dài đường đi trên cây từ a đến b là L. Ta thấy rằng với mọi số nguyên Z, luôn tồn tại một đường đi từ a đến b có độ dài L + 2 * Z (vì ta có thể đi tới và đi lui một cạnh bất kì nào đó vô hạn lần). Vì vậy chúng ta chỉ cần tìm đường đi nhỏ nhất từ a đến b sao cho độ dài của nó cùng tính chẵn lẻ với k (đồng dư với k trên module 2).

Vì đồ thị có dạng cây nên độ dài L là duy nhất. Tuy nhiên, nếu chúng ta thêm 1 cạnh bất kì thì sẽ tồn tại một đường đi có độ dài chẵn lẻ khác với L. Tính chẵn lẻ chỉ thay đổi khi ta đi qua cạnh được thêm một số lần lẻ và độ dài từ x đến y là chẵn. Không có lý do gì mà lại đi qua một cạnh nhiều lần để tìm đường đi ngắn nhất có cùng tính chẵn lẻ, thế nên ta chỉ cần đi qua cạnh được thêm đúng 1 lần.

Vì vậy có 3 trường hợp:

- Độ dài từ a đến b cùng tính chẵn lẻ và <= k thì thỏa mãn.
- Độ dài từ a đến x + độ dài từ y đến b + 1 cùng tính chẵn lẻ và <= k thì thỏa mãn
- Độ dài từ a đến y + độ dài từ x đến b + 1 cùng tính chẵn lẻ và <= k thì thỏa mãn

*Tính độ dài giữa hai đỉnh của một cây bằng LCA*

Nếu không có trường hợp nào thỏa mãn thì in NO.

[Code](https://pastebin.com/8HwYzcfQ)

**2. [Sleepy Game](https://codeforces.com/problemset/problem/936/B)**

Bài này yêu cầu tìm một đường đi từ s đến một đỉnh có bậc ra bằng 0, nếu không thì tìm một chu trình.

Gọi vst[i][j] (0 <= j <= 1): vst[i][0] = 1 tức là Petya đã thăm đỉnh i rồi, vst[i][1] = 1 tức là Vasya đã thăm đỉnh i rồi.

Ta sẽ dfs(u,d) với d là số bước đi hiện tại, bắt đầu dfs(s,0), nếu có một đỉnh v sao cho d % 2 != 0 và bậc ra của v bằng 0 thì Petya có thể win. Nếu có đỉnh v sao cho 
vst[v][1-d%2]=1 tức là gặp được 1 chu trình thì Petya có thể hòa, nếu không Petya thua.

[Code](https://pastebin.com/auhpEKdj)
