# Busca em Profundidade - DFS

A DFS é um dos principais algoritmos de grafos.

A busca em profundidade encontra o primeiro caminho lexicográfico no gráfico de um vértice de origem ***u*** para cada vértice. A DFS também encontrará os caminhos mais curtos em uma árvore (porque existe apenas um caminho simples), mas em grafos gerais este não é o caso, para tal consulte a [Busca em Largura - BFS].

O algoritmo funciona em complexibilidade ***O(m+n)***, tempo onde n é o número de vértices e m é o número de arestas, assim como  BFS.

### Descrição do Algoritmo

A ideia por trás do DFS é ir o mais fundo possível no gráfico e retroceder quando estiver em um vértice sem nenhum vértice adjacente não visitado.

É muito fácil descrever/implementar o algoritmo recursivamente. Iniciamos a busca no vértice **u**. Depois de visitar **u**, realizamos uma DFS para cada vértice adjacente que não visitamos antes. Desta forma, visitamos todos os vértices que são alcançáveis a partir do vértice inicial.

### Implementação

````cpp
vector<vector<int>> adj; // lista de adjacencia para o grafo
int n; // numero de vertices

vector<bool> visited;

void dfs(int v) {
    visited[v] = true;
    for (int u : adj[v]) {
        if (!visited[u])
            dfs(u);
    }
}
````

Esta é a implementação mais simples da DFS. Também pode ser útil para calcular os tempos de entrada e saída e a cor do vértice. Coloriremos todos os vértices com a cor 0, se não os visitamos, com a cor 1 se os visitamos, e com a cor 2, se já saímos do vértice.

Aqui está uma implementação genérica que adicionalmente calcula a descrição acima:

````cpp
vector<vector<int>> adj; // lista de adjacencia para o grafo
int n; // numero de vertices

vector<int> cor;

vector<int> entrada, saida;
int tempo = 0;

void dfs(int v) {
    entrada[v] = tempo++;
    cor[v] = 1;
    for (int u : adj[v])
        if (cor[u] == 0)
            dfs(u);
    cor[v] = 2;
    saida[v] = tempo++;
}
````

### Alguns Usos 

- Encontrar qualquer caminho no grafo do vértice de origem **u** para todos os vértices;
- Verificar se um vértice em uma árvore é ancestral de algum outro vértice;
- Encontrar o ancestral comum mais baixo ([LCA]) de dois vértices;
- Classificação topológica;
- Verificar se um determinado grafo é acíclico e encontre os ciclos em um grafo;
- Encontrar componentes fortemente conectados em um grafo direcionado;
- Encontrar pontes em um grafo não direcionado.


[Busca em Largura - BFS]: https://github.com/alexistoigo/lab/blob/master/Grafos/rep/bfs.md#busca-em-largura---bfs
[LCA]: https://github.com/alexistoigo/lab/blob/master/Grafos/rep/lca.md#menor-ancestral-comum---lca
