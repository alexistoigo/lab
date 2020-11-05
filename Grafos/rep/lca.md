[Grafos]

# Menor Ancestral Comum - LCA

Dada uma árvore ***G***. Dadas as consultas do formulário **(v1,v2)**, para cada consulta, você precisa encontrar o menor ancestral comum, ou seja, um vértice ***v*** que se encontra no caminho da ***raiz*** para ***v1*** e o caminho da***raiz*** para ***v2***, e o vértice deve ser o mais baixo. Em outras palavras, o vértice desejado ***v*** é o ancestral mais inferior de **v1** e **v2**. É óbvio que seu menor ancestral comum está no caminho mais curto de **v1** e **v2**. Também se **v1** é o ancestral de **v2**, **v1** é o seu menor ancestral comum.

### Descrição do Algoritmo

Antes de responder às query, precisamos **pré-processar** a árvore. Fazemos um percurso [DFS] começando na raiz e construímos uma lista **euler** que armazena a ordem dos vértices que visitamos (um vértice é adicionado à lista quando o visitamos pela primeira vez e após o retorno dos percursos [DFS] para seus filhos). Isso também é chamado de passeio de Euler (Euler Tour) pela árvore. É claro que o tamanho desta lista será ***O(N)***. Também precisamos construir um array ***first [ 0 .. N- 1 ]*** que armazena para cada vértice ***i*** sua primeira ocorrência no passeio de euler. Ou seja, a primeira posição em **euler** de tal modo que ***euler [ first [ i ] ] = i***. Também usando o [DFS], podemos encontrar a altura de cada nó (distância da raiz até ele) e armazená-lo na matriz ***height [ 0 .. N- 1 ]***.

Então, como podemos responder as querys usando o passeio de Euler e os dois arrays adicionais? Suponha que a consulta seja um par de ***v1*** e ***v2***. Considere os vértices que visitamos no passeio de Euler entre a primeira visita de **v1** e a primeira visita de **v2**. É fácil ver que o ***LCA (v1,v2)*** é o vértice com a altura mais baixa neste caminho. Já percebemos que o LCA deve fazer parte do caminho mais curto entre **v1** e **v2**. É claro que também deve ser o vértice com a menor altura. E no passeio de Euler, usamos essencialmente o caminho mais curto, exceto que, adicionalmente, visitamos todas as subárvores que encontramos no caminho. Mas todos os vértices nessas subárvores são mais baixos na árvore do que o LCA e, portanto, têm uma altura maior. Então o ***LCA (v1,v2)*** pode ser determinado exclusivamente encontrando o vértice com a menor altura no passeio de Euler entre ***fist (v1)*** e ***first (v2)***.

Vamos ilustrar essa ideia. Considere o seguinte grafo e o passeio de Euler com as alturas correspondentes:

![lca-euler](https://raw.githubusercontent.com/alexistoigo/lab/master/Grafos/rep/LCA_Euler.png)

Vertices: | 1 | 2 | 5 | 2 | 6 | 2 | 1 | 3 | 1 | 4 | 7 | 4 | 1 |

Heights:  | 1 | 2 | 3 | 2 | 3 | 2 | 1 | 2 | 1 | 2 | 3 | 2 | 1 |

O passeio começando no vértice **6** e termina em **4**, sendo os vértices [ 6 , 2 , 1 , 3 , 1 , 4 ]. Entre esses vértices, o vértice **1** tem a altura mais baixa, portanto ***LCA (6, 4) = 1***.

Para recapitular: para responder a uma query, precisamos apenas encontrar o vértice com menor altura na matriz **euler** na faixa de ***first [v1]*** para ***first [v2]***.

Usando Sqrt-Decomposition , é possível obter uma solução respondendo a cada consulta em ***O (√N)*** com pré-processamento em tempo ***O (N)***.

Usando uma [Árvore de Segmentos], é possível responder a cada consulta em ***O ( logN)*** com pré-processamento em ***O ( N)***.

### Implementação

Na seguinte implementação do algoritmo LCA, uma [Árvore de Segmentos] é usada.

````cpp
struct LCA {
    vector<int> height, euler, first, segtree;
    vector<bool> visited;
    int n;

    LCA(vector<vector<int>> &adj, int root = 0) {
        n = adj.size();
        height.resize(n);
        first.resize(n);
        euler.reserve(n * 2);
        visited.assign(n, false);
        dfs(adj, root);
        int m = euler.size();
        segtree.resize(m * 4);
        build(1, 0, m - 1);
    }

    void dfs(vector<vector<int>> &adj, int node, int h = 0) {
        visited[node] = true;
        height[node] = h;
        first[node] = euler.size();
        euler.push_back(node);
        for (auto to : adj[node]) {
            if (!visited[to]) {
                dfs(adj, to, h + 1);
                euler.push_back(node);
            }
        }
    }

    void build(int node, int b, int e) {
        if (b == e) {
            segtree[node] = euler[b];
        } else {
            int mid = (b + e) / 2;
            build(node << 1, b, mid);
            build(node << 1 | 1, mid + 1, e);
            int l = segtree[node << 1], r = segtree[node << 1 | 1];
            segtree[node] = (height[l] < height[r]) ? l : r;
        }
    }

    int query(int node, int b, int e, int L, int R) {
        if (b > R || e < L)
            return -1;
        if (b >= L && e <= R)
            return segtree[node];
        int mid = (b + e) >> 1;

        int left = query(node << 1, b, mid, L, R);
        int right = query(node << 1 | 1, mid + 1, e, L, R);
        if (left == -1) return right;
        if (right == -1) return left;
        return height[left] < height[right] ? left : right;
    }

    int lca(int u, int v) {
        int left = first[u], right = first[v];
        if (left > right)
            swap(left, right);
        return query(1, 0, euler.size() - 1, left, right);
    }
};
````



[Grafos]: https://github.com/alexistoigo/lab/blob/master/Grafos/main.md#grafos
[DFS]: https://github.com/alexistoigo/lab/blob/master/Grafos/rep/dfs.md#busca-em-profundidade---dfs
[Árvore de Segmentos]: todo