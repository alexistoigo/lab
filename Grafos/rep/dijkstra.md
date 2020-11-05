# Dijkstra

Você recebe um gráfico ponderado direcionado ou não direcionado com **n** vértices e **m** arestas. Os pesos de todas as arestas não podem ser negativas. Também recebe um vértice inicial **s**. Este artigo discute a localização dos comprimentos dos caminhos mais curtos de um vértice inicial **s** para todos os outros vértices, e produzir os caminhos mais curtos.

Esse problema também é chamado de problema de caminhos mais curtos de fonte única (SSP).

# Descrição do Algoritmo

Vamos criar um array ***d[ ]*** onde para cada vértice ***v*** armazenamos o comprimento atual do caminho mais curto de ***s*** para ***v*** no ***d[v]***. Inicialmente ***d[s] = 0***, e para todos os outros vértices, esse comprimento é igual ao infinito. Na implementação, um número suficientemente grande é escolhido como infinito.

***d [ v ] = ∞, v ≠ s***

Além disso, mantemos uma matriz booleana ***u [ ]*** que armazena para cada vértice ***v*** se está marcado. Inicialmente, todos os vértices estão desmarcados:

***u [ v ] = false***

O algoritmo de Dijkstra funciona para ***n*** iterações. Em cada iteração, um vértice não marcado  ***v*** é escolhido o que tem o menor valor ***d[v]***:

***d [to] = min(d[to], d[v] + len)***

Depois que todas essas arestas são verificadas, a iteração atual termina. Finalmente, depois de ***n*** iterações, todos os vértices serão marcados e o algoritmo termina. Afirmamos que os valores encontrados ***d[v]*** são as distâncias dos caminhos mais curtos de ***s*** para todos os vértices ***v***.

Observe que se alguns vértices estão inacessíveis do vértice inicial ***s***, os valores de  ***d[v]*** permanecerão infinitos. Obviamente, as últimas iterações do algoritmo escolherão esses vértices, mas nenhum trabalho útil será feito para eles. Portanto, o algoritmo pode ser interrompido assim que o vértice selecionado tiver distância infinita para ele.

### Implementação

O algoritmo de Dijkstra realiza ***n*** iterações. Em cada iteração ele seleciona um vértice não marcado ***v*** com o menor valor ***d[v]***, marca e verifica todas as bordas ( v , para ) tentando melhorar o valor ***d[to]***.

O tempo de execução do algoritmo consiste em:

- **n** procura por um vértice com o menor valor ***d[v]*** entre ***O(n)*** vértices não marcados;
- **m** tentativas de verificação.

Para a implementação mais simples dessas operações em cada vértice de iteração, a pesquisa requer ***O(n)*** operações, e cada tentatica pode ser realizado em ***O(1)***. Portanto, o comportamento assintótico resultante do algoritmo é: ***O(n²+m)***.

````cpp
const int INF = 1000000000;
vector<vector<pair<int, int>>> adj;

void dijkstra(int s, vector<int> & d, vector<int> & p) {
    int n = adj.size();
    d.assign(n, INF);
    p.assign(n, -1);
    vector<bool> u(n, false);

    d[s] = 0;
    for (int i = 0; i < n; i++) {
        int v = -1;
        for (int j = 0; j < n; j++) {
            if (!u[j] && (v == -1 || d[j] < d[v]))
                v = j;
        }

        if (d[v] == INF)
            break;

        u[v] = true;
        for (auto edge : adj[v]) {
            int to = edge.first;
            int len = edge.second;

            if (d[v] + len < d[to]) {
                d[to] = d[v] + len;
                p[to] = v;
            }
        }
    }
}
````

Aqui o grafo ***adj*** é armazenado como lista de adjacência: para cada vértice ***v*** em ***adj[ v ]*** contém a lista de arestas saindo deste vértice, ou seja, a lista de ***pair<int,int>*** onde o **primeiro elemento do par é o vértice** na outra extremidade da aresta e o **segundo elemento é o peso da aresta**.

A função pega o vértice inicial ***s*** e dois vetores que serão usados como valores de retorno.

Em primeiro lugar, o código inicializa arrays: distâncias ***d[ ]***, rótulos ***v [ ]*** e predecessores/pais ***p [ ]***. Então ele executa ***n*** iterações. Em cada iteração, do vértice ***v***, é selecionado o que tem a menor distância ***d[ v ]*** entre todos os vértices não marcados. Se a distância para o vértice selecionado ***v*** é igual ao infinito, o algoritmo para. Caso contrário, o vértice é marcado e todas as arestas que saem desse vértice são verificadas. Se o relaxamento ao longo da borda for possível (ou seja, distância ***d[ to ]*** pode ser melhorada), a distância ***d[ to ]*** e predecessor ***p [ para ]*** são atualizados.


