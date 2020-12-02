[Geometria]

# Encontrando área de polígono

Deixe um polígono simples (ou seja, sem auto intersecção, não necessariamente convexo). É necessário calcular sua área de acordo com seus vértices.

A complexibilidade para este algoritmo é ***O (N)***

### Método 1

Isso é fácil de fazer se percorrermos todas as arestas e adicionarmos áreas de trapézio delimitadas por cada aresta e eixo x. A área precisa ser sinalizada para que a área extra seja reduzida. Portanto, a fórmula é a seguinte:

![polygon](https://quicklatex.com/cache3/d7/ql_19408e2289499b4d047221f2eee903d7_l3.png)

#### Implementação

````cpp
double area(const vector<point>& fig) {
    double res = 0;
    for (unsigned i = 0; i < fig.size(); i++) {
        point p = i ? fig[i - 1] : fig.back();
        point q = fig[i];
        res += (p.x - q.x) * (p.y + q.y);
    }
    return fabs(res) / 2;
}
````

### Método 2

Podemos escolher um ponto O arbitrariamente, itera sobre todas as arestas adicionando a área orientada do triângulo formado pela aresta e ponto O. Novamente, devido ao sinal de área, a área extra será reduzida.

Este método é melhor, pois pode ser generalizado para casos mais complexos (como quando alguns lados são arcos em vez de linhas retas)



[Geometria]: https://github.com/alexistoigo/lab/blob/master/Geometria/main.md#geometria