# 깊이 우선 탐색
 
우선 DFS(Depth first Search)는 탐색 문제에서 주로나오며 이산수학에서도 한 번쯤은 보았을 알고리즘이다.

이 알고리즘을 간단하게 적자면 아래와 같다.
- 자료구조에서 노드와 간선으로 연결된 그래프에서 루트 노드에서 시작하여 차례대로 모든 노드를 한 번씩 방문한다.

DFS는 노드에서 후발 노드로 탐색중 더 이상 탐색할 노드가 없을 경우 backtracking을 통해 탐색하지 않은 노드를 확인하는 과정이 특징적이라고 할 수 있다.

이는 BFS(너비우선탐색)과는 다른 모습을 보여준다.

이러한 특징으로 DFS를 구현할 때 대개는 스택 또는 자기자신을 호출하는 재귀함수로서 구현한다.  
```go
package main

import (
	"log"
)

type Node struct {
	id int
	child []int
}

type Graph []Node

var result []int
var visited []bool

func main() {
	var graph Graph
	graph = append(graph, 
		Node{0, []int{1,2,3}},
		Node{1, []int{4}},
		Node{2, []int{4}},
		Node{3, []int{}},
		Node{4, []int{5,6}},
		Node{5, []int{}},
		Node{6, []int{2}},	
	)

	visited = make([]bool, len(graph))
	
	search(graph, graph[0])
}

func search(graph Graph, node Node) {
	log.Printf("Node: %d", node)
	visited[node.id] = true
	result = append(result, node.id)

	if (len(node.child) != 0) {
		for index, val := range node.child {
			if (visited[val] == true) {
				continue
			}

			search(graph, graph[val])
		}
	}
}
```
