[String]

# Função Z

Suponha que recebamos uma string ***s*** de comprimento ***n***. A ***Função Z*** para esta string é uma matriz de comprimento ***n*** onde o *i-ésimo* elemento é igual ao maior número de caracteres a partir da posição *i* que coincidem com os primeiros caracteres de ***s***.

Em outras palavras, ***z[ i ]*** é o comprimento do prefixo comum mais longo entre **s** e o sufixo de **s** Começando em *i*.

Apresentamos um algoritmo para calcular a função Z em complexibilidade de ***O ( n )***, bem como várias de suas aplicações.

#### Exemplos

Por exemplo, aqui estão os valores da função Z calculada para diferentes strings:

- **"aaaaa"** - [ 0 , 4 , 3 , 2 , 1 ]

- **"aaabaab"** - [ 0 , 2 , 1 , 0 , 2 , 1 , 0 ]

- **"abacaba"** -  [ 0 , 0 , 1 , 0 , 3 , 0 , 1 ]

#### Algoritmo Trivial

A definição formal pode ser representada no seguinte elemento ***O (n²)*** implementação.

````cpp
vector<int> z_function_trivial(string s) {
    int n = (int) s.length();
    vector<int> z(n);
    for (int i = 1; i < n; ++i)
        while (i + z[i] < n && s[z[i]] == s[i + z[i]])
            ++z[i];
    return z;
}
````

Claro, esta não é uma implementação eficiente. Vamos agora mostrar a construção de uma implementação eficiente.

### Algoritmo eficiente para calcular a Função Z

Para obter um algoritmo eficiente, calcularemos os valores de ***z[ i ]*** por sua vez de **i = 1** para **n - 1** mas, ao mesmo tempo, ao calcular um novo valor, tentaremos fazer o melhor uso possível dos valores calculados anteriormente.

Vamos chamar o segmento corresponde aquelas substrings que coincidem com um prefixo de **s**. Por exemplo, o valor da função Z desejada **z[ i ]** é o comprimento da correspondência do segmento começando na posição *i* (e isso termina na posição **i + z[ i ] - 1**).

#### Implementação

````cpp
vector<int> z_function(string s) {
    int n = (int) s.length();
    vector<int> z(n);
    for (int i = 1, l = 0, r = 0; i < n; ++i) {
        if (i <= r)
            z[i] = min (r - i + 1, z[i - l]);
        while (i + z[i] < n && s[z[i]] == s[i + z[i]])
            ++z[i];
        if (i + z[i] - 1 > r)
            l = i, r = i + z[i] - 1;
    }
    return z;
}
````

Toda a solução é dada como uma função que retorna uma matriz de comprimento **n**: a função Z de **s**.

Array ***z*** é inicialmente preenchido com zeros. O segmento de correspondência mais à direita atual é considerado **[ 0 ; 0 ]**.

Dentro do loop para ***i = 1 ... n - 1*** primeiro determinamos o valor inicial ***z[ i ]***: permanecerá zero ou será calculado.

Depois disso, o algoritmo trivial tenta aumentar o valor de ***z[ i ]*** tanto quanto possível.

No final, se for necessário (ou seja, se ***i + z[ i ] - 1 > r***), atualizamos o segmento de correspondência mais à direita ***[ l , r ]***.


[String]: https://github.com/alexistoigo/lab/blob/master/Processamento%20de%20String/main.md#processamento-de-string
