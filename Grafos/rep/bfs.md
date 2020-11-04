# Busca em Largura - BFS

A busca em largura é um dos algoritmos de pesquisa básicos e essenciais em gráficos.
Como resultado de como o algoritmo funciona, o caminho encontrado BFS para qualquer nó é o caminho mais curto para esse nó, ou seja, o caminho que contém o menor número de arestas em gráficos não ponderados (sem pesos nas arestas).

O algoritmo funciona em complexibilidade de  ***O(n+m)***, onde n é o número de vértices e m é o número de arestas.

### Descrição do Algoritmo

O algoritmo tem como entrada um grafo não ponderado e o id do vértice de origem ***s***. O grafo de entrada pode ser direcionado ou não.

O algoritmo pode ser entendido e explicado como uma propagação de fogo no grafo: na etapa zero, apenas a fonte está em chamas. Em cada etapa, o fogo queimando em cada vértice se espalha para todos os seus vizinhos. Numa iteração do algoritmo, o "área do fogo" é expandido em largura por uma unidade.

Mais precisamente, o algoritmo pode ser definido da seguinte maneira: É criada uma fila ***q*** que conterá os vértices a serem processados e um array booleano ***used[]*** que indica para cada vértice, se foi aceso (ou visitado) ou não.

Inicialmente, puxe a fonte ***s*** para a fila e defina: ***used[s] = true***, e para todos os outros vértices ***v*** conjunto ***used[v] = false***. Em seguida, faça um loop até que a fila esteja vazia e, em cada iteração, destaque um vértice da frente da fila. Itere por todas as arestas que saem deste vértice e se alguma dessas arestas for para vértices que ainda não estão acesos, defina-os como usados e coloque-os na fila.

Como resultado, quando a fila está vazia, o "anel de fogo" contém todos os vértices alcançáveis da fonte ***s***, com cada vértice alcançado da maneira mais curta possível. Também é possível calcular a distancia dos caminhos mais curtos (o que requer apenas a manutenção de uma série de comprimentos de caminho ***d[]***) bem como salvar informações para restaurar todos esses caminhos mais curtos (para isso, é necessário manter um array de "pais" ***p[ ]***, que armazena para cada vértice o vértice a partir do qual o alcançamos).

### Implementação

```cpp
vector<vector<int>> adj;  // lista de adjacencia
int n; // numero de nodos
int s; // ponto inicial

queue<int> q;
vector<bool> used(n);
vector<int> d(n), p(n);

q.push(s);
used[s] = true;
p[s] = -1;
while (!q.empty()) {
    int v = q.front();
    q.pop();
    for (int u : adj[v]) {
        if (!used[u]) {
            used[u] = true;
            q.push(u);
            d[u] = d[v] + 1;
            p[u] = v;
        }
    }
}
```
Se tivermos que exibir o caminho mais curto a partir do ponto inicial para algum vértice, pode ser feito da seguinte maneira:

````cpp
if (!used[u]) {
    cout << "Sem caminho!";
} else {
    vector<int> path;
    for (int v = u; v != -1; v = p[v])
        path.push_back(v);
    reverse(path.begin(), path.end());
    cout << "Caminho: ";
    for (int v : path)
        cout << v << " ";
}
````

### Alguns Usos 

- Encontrar o caminho mais curto de uma fonte para outros vértices em um gráfico não ponderado;
- Encontrar todos os componentes conectados em um gráfico não direcionado em O(n+m);
- Encontrar a solução para um problema ou jogo (xadrez por exemplo) ou menor quantidade de determinados calculos para chegar a um resultado com o menor número de movimentos;
- Encontrar o caminho mais curto em um grafo com pesos 0 ou 1;
- Encontrar o ciclo mais curto em um gráfico direcionado não ponderado.




