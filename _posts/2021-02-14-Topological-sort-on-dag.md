---
layout : post
title : Topological Sort on DAGs
tags : [graph,toposort]
---
## Topological Sorting
Cho một đồ thị với N đỉnh và N cạnh. Yêu cầu trả về số thứ tự của các đỉnh sao cho mỗi đỉnh có số thứ tự bé hơn đều có thể đi đến được đỉnh có số lớn hơn.

Nói cách khác phải tìm một hoán vị của các đỉnh (topological order) để cho tương ứng với các cạnh của đồ thị

Topological order có thể non-unique (không độc nhất).

Topological order không xuất hiện nếu đồ thị có chứa chu trình (cycles).

## The algorithm
Để giải quyết vấn đề này, ta sài Depth-first-search (DFS).

Giả sử đồ thị là một acyclic graph (đồ thị có hướng không có chu trình), sẽ có ít nhất 1 đáp án.

Gọi một dãy *T* là dãy đánh thứ tự các đỉnh của đồ thị. Ta sẽ dfs những đỉnh chưa được thăm, đến khi không còn cạnh ra thì đỉnh đó là một đỉnh *sinks* nên ta thêm đỉnh đó vào cuối dãy. Và cứ thế cho đến khi cả N đỉnh đều được thăm

Độ phức tạp cho dfs N đỉnh là O(n) và thăm xấu nhất qua M cạnh là O(N+M).

## Implementation
``` C++
// a là vector chứa các đỉnh kề với u
// d[u] = 0 là chưa thăm, d[u] = 1 là đã thăm
void dfs(int u) 
{
	if (d[u]) return;
	for (int i=0; i<a[u].size(); i++)
	{
		int v = a[u][i];
		if (!d[v]) dfs(v);
	}
	d[u]=1;
	topsort[cnt]=u;
	cnt--;
}
```
