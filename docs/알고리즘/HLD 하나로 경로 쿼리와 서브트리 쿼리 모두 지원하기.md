# HLD 하나로 경로 쿼리와 서브트리 쿼리 모두 지원하기
*이 글은 heavy-light decomposition과 Euler tour trick을 배경지식으로 합니다.*

보통 트리의 경로를 주고 쿼리를 수행하라고 하면 heavy-light decomposition을 합니다. 그리고 서브트리를 주고 쿼리를 수행하라고 하면 Euler tour trick으로 트리를 일자로 폅니다. 그런데

https://www.acmicpc.net/problem/17429

이 문제는 경로 쿼리와 서브트리 쿼리가 모두 주어지고 둘의 분리가 불가능합니다. 이 글에서는 경로 쿼리와 서브트리 쿼리를 모두 지원하는 방법을 소개합니다.

출처는 코드포스 블로그의 [Easiest HLD with subtree queries](https://codeforces.com/blog/entry/53170)라는 글입니다. 세계 탑랭커 중 하나인 Radewoosh님조차 감탄을 금치 못하는 모습을 볼 수 있습니다.

> This blog is 6 months old, but I've just read it and... WOW WOW WOW WOW, it's so great, WOW WOW (sorry, I just have to do it) WOW WOW WOW!!!

# How??
트리에는 이미 루트가 잡혀 있다고 가정합시다. v의 자식 노드를 담은 배열을 tadj[v]라고 하고, 추가로 0으로 초기화된 sz와 in이라는 이름의 배열을 준비합니다. 이제 dfs_sz와 dfs_hld 함수를 다음과 같이 작성합니다.

```cpp
void dfs_sz(int v = 0) {
    sz[v] = 1;
    for(int &u: tadj[v]){
        dfs_sz(u); sz[v]+= sz[u];
        if(sz[u] > sz[tadj[v][0]]) swap(u, tadj[v][0]);
    }
}

void dfs_hld(int v = 0) {
    in[v] = t++;
    for(int u: tadj[v]) top[u] = (u == tadj[v][0]? top[v]:u), dfs_hld(u);
}
```

루트 노드를 `r`이라고 할 때, `dfs_sz(r)`과 `dfs_hld(r)`을 차례대로 실행하면 다음과 같은 일이 벌어집니다.

- `sz[v]`는 `v`를 루트로 하는 서브트리의 크기와 같습니다.
- `v`를 루트로 하는 서브트리는 구간 `in[v]`부터 `in[v]+sz[v]-1`까지에 대응됩니다.
- `v`가 포함되는 heavy path의 꼭대기 정점은 `top[v]`입니다. 게다가 그 정점부터 `v`까지의 경로는 구간 `in[top[v]]`부터 `in[v]`까지에 대응됩니다.

즉 이 코드는 **Euler tour trick과 heavy light decomposition을 동시에** 하는 코드입니다! 심지어 굉장히 짧기까지 합니다. 어떻게 HLD가 두 줄 만에 끝난단 말입니까?

# Why??
정확히 무슨 일이 일어나고 있는 건지 분석해 보면 왜 이게 가능해지는지를 알 수 있습니다.

- 우선 `dfs_sz`는 `sz` 배열을 계산하는데, 트리 DP를 생각해 보면 쉽게 이해할 수 있습니다.
- `if(sz[u] > sz[tadj[v][0]]) swap(u, tadj[v][0]);`을 모든 `u`에 대해 반복하면, `v`의 자식 노드 중 서브트리 크기가 가장 큰 것은 바로 0번째 자식이 됩니다. 따라서 `v`에서 시작하거나 `v`로 내려온 heavy path는 `v`의 0번째 자식을 타고 내려갈 것입니다.
- `dfs_hld`는 각 `v`마다 heavy path의 꼭대기 정점 `top[v]`를 계산합니다. 이때 `u`가 `v`의 0번째 자식이면, `v`로 내려온 heavy path가 그대로 `u`로 내려갑니다. 따라서 `top[u] = top[v]`입니다. 반대로 0번째 자식이 아니면, `u`에서 새로운 heavy path가 시작됩니다. 따라서 `top[u] = u`입니다.
- 마지막으로, heavy path가 0번째 자식을 타고 내려가고, dfs 역시 0번째 자식부터 시작하기 때문에, 방문 순서를 그대로 `in` 배열에 넣으면 한 heavy path 안의 정점들은 연속된 `in` 번호를 갖게 됩니다.

이제 이 코드를 가지고 "수열과 쿼리 13"과 결합하면 맨 위에 주어진 "국제 메시 기구"를 풀 수 있습니다.