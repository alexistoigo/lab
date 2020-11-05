# Árvore Geradora Mínima - MST

Dado um gráfico não direcionado ponderado. Queremos encontrar uma sub árvore desse grafo que conecte todos os vértices (ou seja, é uma árvore geradora) e tenha o menor peso (ou seja, a soma dos pesos de todas as arestas é mínima) de todas as árvores geradoras possíveis. Essa árvore de abrangência é chamada de árvore de abrangência mínima.

Na imagem da esquerda você pode ver um gráfico não direcionado ponderado, e na imagem da direita você pode ver a árvore de abrangência mínima correspondente.

![before](https://raw.githubusercontent.com/alexistoigo/lab/master/Grafos/rep/MST_before.png) ![after](https://raw.githubusercontent.com/alexistoigo/lab/master/Grafos/rep/MST_after.png)

### Propriedades da árvore de abrangência mínima

- Uma árvore de abrangência mínima de um grafo é única, se o peso de todas as arestas for distinto. Caso contrário, pode haver várias árvores abrangentes mínimas.
- A árvore geradora mínima é também a árvore com o produto mínimo dos pesos das arestas. (Pode ser facilmente comprovado substituindo os pesos de todas as arestas por seus logaritmos)
- Em uma árvore de abrangência mínima de um grafo, o peso máximo de uma aresta é o mínimo possível de todas as árvores de abrangência possíveis desse gráfico.
- A árvore geradora máxima (árvore geradora com a soma dos pesos das arestas sendo máxima) de um gráfico pode ser obtida de forma semelhante à da árvore geradora mínima, mudando os sinais dos pesos de todas as arestas para seus opostos e, em seguida, aplicando qualquer do algoritmo de spanning tree mínimo.

### Algoritmo de Kruskal

Antes da execução do algoritmo, todas as arestas são classificadas por peso (em ordem não decrescente). Em seguida, começa o processo de unificação: escolha todas as arestas da primeira à última e, se as extremidades da aresta selecionada pertencer a diferentes subárvores, essas subárvores são combinadas e a aresta é adicionada à resposta. Depois de iterar por todas as arestas, todos os vértices pertencerão à mesma subárvore e obteremos a resposta.

### Implementação

##### Implementação Simples

O algoritmo descrito acima e está tendo ***O(M logM + N2)*** de complexidade do tempo. A classificação dos nodos requer ***O(M logN)*** (que é o mesmo que ***O(M logM)***) operações. As informações sobre a subárvore a que pertence ao vértice são mantidas com a ajuda de um array **tree_id[]** - para cada vértice ***v***, ***tree_id[v]*** armazena o número da árvore a que ***v*** pertence. Para cada aresta, se pertence às extremidades de diferentes árvores, pode ser determinada em ***O(1)***. Por fim, a união das duas árvores é realizada em ***O(N)*** por um simples passagem no array **tree_id[]**. Dado que o número total de operações de mesclagem é *N - 1*, obtemos o comportamento assintótico de ***O(M logN + N²)***.

````cpp
struct Edge {
    int u, v, weight;
    bool operator<(Edge const& other) {
        return weight < other.weight;
    }
};

int n;
vector<Edge> edges;

int cost = 0;
vector<int> tree_id(n);
vector<Edge> result;
for (int i = 0; i < n; i++)
    tree_id[i] = i;

sort(edges.begin(), edges.end());

for (Edge e : edges) {
    if (tree_id[e.u] != tree_id[e.v]) {
        cost += e.weight;
        result.push_back(e);

        int old_id = tree_id[e.u], new_id = tree_id[e.v];
        for (int i = 0; i < n; i++) {
            if (tree_id[i] == old_id)
                tree_id[i] = new_id;
        }
    }
}
````

##### Implementação Aprimorada

Complexibilidade ***O(M logN)***

````cpp
void make_set(int v) {
    parent[v] = v;
}

int find_set(int v) {
    if (v == parent[v])
        return v;
    return parent[v] = find_set(parent[v]);
}

void union_sets(int a, int b) {
    a = find_set(a);
    b = find_set(b);
    if (a != b)
        parent[b] = a;
}

````