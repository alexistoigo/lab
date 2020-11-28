[Matemática]

# Algoritmo Euclidiano Estendido

Enquanto o [algoritmo euclidiano] calcula apenas o máximo divisor comum (GCD) de dois inteiros *a* e *b*, a versão estendida também encontra uma maneira de representar o GCD em termos de *a* e *b*, ou seja, coeficientes *x* e *y* para qual:

    a ⋅ x + b ⋅ y= mdc ( a , b )
    
É importante notar que sempre podemos encontrar tal representação, por exemplo *mdc ( 55 , 80 ) = 5* portanto, podemos representar 5 como uma combinação linear com os termos *55* e *80*: *55 ⋅ 3 + 80 ⋅ ( - 2 ) = 5*.

### Algoritmo

Vamos denotar o GCD de *a* e *b* com *g*.

As mudanças no algoritmo original são muito simples. Se nos lembrarmos do algoritmo, podemos ver que o algoritmo termina com *b = 0* e *a = g*. Para esses parâmetros, podemos encontrar facilmente coeficientes, a saber ***g ⋅ 1 + 0 ⋅ 0 = g***.

A partir desses coeficientes ***( x , y) = ( 1 , 0 )***, podemos voltar para cima nas chamadas recursivas. Tudo o que precisamos fazer é descobrir como os coeficientes *x* e *y* mudar durante a transição de *( a , b )* para *( b , a mod b )*.

### Implementação

````cpp
int gcd(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}
````

A função recursiva acima retorna o GCD e os valores dos coeficientes para *x* e *y* (que são passados por referência à função).

Essa implementação do algoritmo Euclidiano estendido também produz resultados corretos para inteiros negativos.

#### Versão Iterativa

Também é possível escrever o algoritmo Euclidiano estendido de forma iterativa. Por evitar a recursão, o código será executado um pouco mais rápido do que o recursivo.

````cpp
int gcd(int a, int b, int& x, int& y) {
    x = 1, y = 0;
    int x1 = 0, y1 = 1, a1 = a, b1 = b;
    while (b1) {
        int q = a1 / b1;
        tie(x, x1) = make_tuple(x1, x - q * x1);
        tie(y, y1) = make_tuple(y1, y - q * y1);
        tie(a1, b1) = make_tuple(b1, a1 - q * b1);
    }
    return a1;
}
````


[Matemática]: https://github.com/alexistoigo/lab/blob/master/Matematica/main.md#matem%C3%A1tica
[algoritmo euclidiano]: https://github.com/alexistoigo/lab/blob/master/Matematica/rep/gcd.md#algoritmo-euclidiano-para-calcular-o-maior-divisor-comum