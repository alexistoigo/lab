[Algo]

# Algoritmo Euclidiano para calcular o Maior Divisor Comum

Dados dois inteiros não negativos *a* e *b*, temos de encontrar seu GCD (maior divisor comum), ou seja, o maior número que é um divisor de ambos *a* e *b*. É comumente denotado por ***mdc ( a , b )***.

Quando um dos números é zero, enquanto o outro é diferente de zero, seu maior divisor comum, por definição, é o segundo número. Quando ambos os números são zero, seu maior divisor comum é indefinido (pode ser qualquer número arbitrariamente grande), mas podemos defini-lo como zero. O que nos dá uma regra simples: se um dos números for zero, o maior divisor comum é o outro número.

O algoritmo euclidiano, discutido abaixo, permite encontrar o maior divisor comum de dois números *a* e *b* em ***O ( log min ( a , b ) )***.

### Algoritmo

O algoritmo é extremamente simples:

![Fórmula](https://quicklatex.com/cache3/d6/ql_3d720d273ebc57ad75e3cb3577ba05d6_l3.png)


### Implementação

````cpp
int gcd (int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd (b, a % b);
}
````

Usando o operador ternário em C ++, podemos escrevê-lo como uma linha.

````cpp
int gcd (int a, int b) {
    return b ? gcd (b, a % b) : a;
}
````

E, finalmente, aqui está uma implementação não recursiva:

````cpp
int gcd (int a, int b) {
    while (b) {
        a %= b;
        swap(a, b);
    }
    return a;
}
````


[Algo]: https://github.com/alexistoigo/lab#algo