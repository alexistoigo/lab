[Algo]

# Exponenciação Binária

A exponenciação binária é um método que permite calcular ***a^n*** usando apenas ***O ( logn )*** multiplicações (em vez de **O ( n )** multiplicações exigidas pela abordagem ingênua).

Ele também tem aplicações importantes em muitas tarefas não relacionadas à aritmética, uma vez que pode ser usado com qualquer operação que tenha a propriedade de associatividade :

    ( X⋅ Y) ⋅ Z= X⋅ ( Y⋅ Z)

### Descrição do Algoritmo

*a* ao elevado a *n* é expresso ingenuamente como multiplicação por *a*  *n - 1*. No entanto, esta abordagem não é prática para grandes *a* ou *n*.

A ideia de exponenciação binária é dividir o trabalho usando a representação binária do expoente.

Vamos escrever *n* na base 2, por exemplo:

**3^13=3^1101^2=3^8.3^4.3^1**

Desde o numero *n* tem exatamente *[log n] + 1* dígitos na base 2, só precisamos realizar *O ( log n )* multiplicações, se conhecermos as exponenciações de  a^1,a^2,a^4,a^8, ... ,a^[ log n ].

Portanto, só precisamos conhecer uma maneira rápida de computá-los. Felizmente, isso é muito fácil, pois um elemento na sequência é apenas o quadrado do elemento anterior.

### Implementação

Abordagem recursiva:

````cpp
long long binpow(long long a, long long b) {
    if (b == 0)
        return 1;
    long long res = binpow(a, b / 2);
    if (b % 2)
        return res * res * a;
    else
        return res * res;
}
````
A segunda abordagem realiza a mesma tarefa sem recursão. Ele calcula todas as potências em um loop e multiplica aquelas com o conjunto de bits correspondente em *n*. Embora a complexidade de ambas as abordagens seja idêntica, essa abordagem será mais rápida na prática, pois não temos a sobrecarga das chamadas recursivas.

````cpp
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
````

### Alguns Usos:
- Cálculo eficaz de expoentes grandes modulo algum número:
````cpp
long long binpow(long long a, long long b, long long m) {
    a %= m;
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a % m;
        a = a * a % m;
        b >>= 1;
    }
    return res;
}
````

- Calcular números de Fibonacci;
- Aplicar permutação *k* vezes;
- Número de caminhos de comprimento k em um grafo;
- Multiplicar o módulo de dois números *m*.

[Algo]: https://github.com/alexistoigo/lab#algo