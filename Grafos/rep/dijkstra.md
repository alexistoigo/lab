# Dijkstra

Você recebe um gráfico ponderado direcionado ou não direcionado com **n** vértices e **m** arestas. Os pesos de todas as arestas não podem ser negativas. Também recebe um vértice inicial **s**. Este artigo discute a localização dos comprimentos dos caminhos mais curtos de um vértice inicial **s** para todos os outros vértices, e produzir os caminhos mais curtos.

Esse problema também é chamado de problema de caminhos mais curtos de fonte única (SSP).

# Descrição do Algoritmo

Vamos criar um array ***d[]*** onde para cada vértice ***v*** armazenamos o comprimento atual do caminho mais curto de ***s*** para ***v*** no ***d[v]***. Inicialmente ***d[s] = 0***, e para todos os outros vértices, esse comprimento é igual ao infinito. Na implementação, um número suficientemente grande é escolhido como infinito.

$d[ v ] = \infty , v \neq s$