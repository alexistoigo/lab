[Grafos]

# Floyd-Warshall

Dado um gráfico não direcionado ***G*** com ***n*** vértices. A tarefa é encontrar o caminho mais curto de ***d {i, j}*** entre cada par de vértices **i** e **j**.

O gráfico **pode** ter arestas de peso negativo, mas nenhum ciclo de peso negativo (pois o caminho mais curto é indefinido).

Este algoritmo também pode ser usado para detectar a presença de ciclos negativos. O gráfico tem um ciclo negativo se no final do algoritmo, a distância de um vérticev para si mesmo é negativo.

### Descrição do Algoritmo

A ideia principal do algoritmo é particionar o processo de localização do caminho mais curto entre dois vértices em várias fases.

Vamos numerar os vértices começando de **1** a **n**. A matriz de distâncias é **d[ ][ ]**.

Antes k-ésima fase ***(k = 1 ... n)***, ***d[ i ][ j ]*** para quaisquer vértices **i** e **j** armazena o comprimento do caminho mais curto entre o vértice **i** e **j**, que contém apenas os vértices **{ 1 , 2 , . . . , k - 1 }** como vértices no caminho.

Em outras palavras, antes k-ésima fase o valor de ***d[ i ][ j ]*** é igual ao comprimento do caminho mais curto do vértice **i** para o vértice **j**, se este caminho puder inserir um vértice com números menores que k (o início e o fim do caminho não são restritos por esta propriedade).

É fácil ter certeza de que essa propriedade é válida para a primeira fase. Para **k = 0**, podemos preencher a matriz com ***d[ i ] [ j ] = W j*** se existe uma borda **i** e **j** com peso ***W j*** e ***d[ i ][ j ] = ∞*** se não existe uma vantagem. Na prática ∞ será algum valor alto. Este é um requisito para o algoritmo.

Descobrimos que podemos recalcular o comprimento de todos os pares **(i , j)** na **k-ª** fase da seguinte maneira:
 
    d[i][j] = min(d[i][j], d[i][k] + d[k][j])
    
Assim, todo o trabalho que é exigido na **k-ª** fase é iterar sobre todos os pares de vértices e recalcular o comprimento do caminho mais curto entre eles. Como resultado, após a n-ésima fase, o valor ***d[ i ][ j ]*** na matriz de distância é o comprimento do caminho mais curto entre **i** e **j**, ou é ∞ se o caminho entre os vértices **i** e **j** não existe.

A complexidade de tempo deste algoritmo é obviamente ***O(n³)***.

### Implementação

***d[ ][ ]*** é uma matriz 2D de tamanho **n × n**, que é preenchido de acordo com o **0-ésima** fase conforme explicado anteriormente. Também vamos definir **d[ i ] [ i ] = 0** para qualquer *i* no *0-ª* fase.

````cpp
for (int k = 0; k < n; ++k) {
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            d[i][j] = min(d[i][j], d[i][k] + d[k][j]); 
        }
    }
}
````

É assumido que se não houver aresta entre quaisquer dois vértices **i** e **j**, então a matriz em ***d[ i ][ j ]*** contém um grande número (grande o suficiente para ser maior do que o comprimento de qualquer caminho neste grafo). Então, esse caminho sempre será inútil para pegar, e o algoritmo funcionará corretamente.

[Grafos]: https://github.com/alexistoigo/lab/blob/master/Grafos/main.md#grafos
