[Geometria]

# Comprimento da união dos segmentos

Dado **n** segmentos em uma linha, cada um descrito por um par de coordenadas (a*i*1, a*i*2). Temos que descobrir a duração de sua união.

O seguinte algoritmo foi proposto por Klee em 1977. Funciona em ***O ( n logn )*** e provou ser assintoticamente ideal.

Nós armazenamos em uma matriz x os pontos finais de todos os segmentos classificados por seus valores. Além disso, armazenamos se é uma extremidade esquerda ou direita de um segmento. Agora iteramos sobre a matriz, mantendo um contador c de segmentos abertos atualmente. Sempre que o elemento atual for uma extremidade esquerda, aumentamos esse contador e, caso contrário, o diminuímos. Para calcular a resposta, pegamos o comprimento entre o último ax valores x*i*-x*i-1*, sempre que chegarmos a uma nova coordenada, e houver pelo menos um segmento aberto.


### Implementação

````cpp
int length_union(const vector<pair<int, int>> &a) {
    int n = a.size();
    vector<pair<int, bool>> x(n*2);
    for (int i = 0; i < n; i++) {
        x[i*2] = {a[i].first, false};
        x[i*2+1] = {a[i].second, true};
    }

    sort(x.begin(), x.end());

    int result = 0;
    int c = 0;
    for (int i = 0; i < n * 2; i++) {
        if (i > 0 && x[i].first > x[i-1].first && c > 0)
            result += x[i].first - x[i-1].first;
        if (x[i].second)
            c--;
        else
            c++;
    }
    return result;
}
````

[Geometria]: https://github.com/alexistoigo/lab/blob/master/Geometria/main.md#geometria