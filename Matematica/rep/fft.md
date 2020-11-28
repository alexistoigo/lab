[Matemática]

# Transformação rápida de Fourier

Iremos discutir um algoritmo que nos permite multiplicar dois polinômios de comprimento *n* em ***O ( n logn )*** de tempo, que é melhor do que a multiplicação trivial que leva ***O (n²)***. Obviamente, também a multiplicação de dois números longos pode ser reduzida para a multiplicação de polinômios, então também dois números longos podem ser multiplicados em ***O ( n log n )*** tempo (onde *n* é o número de dígitos nos números).

A transformação rápida de Fourier é um método que permite calcular o DFT em ***( n logn )***. A ideia básica do FFT é aplicar dividir para conquistar. Dividimos o vetor de coeficientes do polinômio em dois vetores, calculamos recursivamente a DFT para cada um deles e combinamos os resultados para calcular a DFT do polinômio completo.

Então, que haja um polinômio *A ( x )* com grau *n - 1*, Onde *n* é uma potência de *2*, e *n > 1:*

![fft](https://quicklatex.com/cache3/fd/ql_ed5c8584857bcc05b4fa6a1eb2aad6fd_l3.png)

### Implementação

Aqui apresentamos uma implementação recursiva simples da FFT e da FFT inversa, ambos em uma função, uma vez que a diferença entre a FFT direta e a inversa são mínimas. Para armazenar os números complexos, usamos o tipo complexo no C ++ STL.

````cpp
using cd = complex<double>;
const double PI = acos(-1);

void fft(vector<cd> & a, bool invert) {
    int n = a.size();
    if (n == 1)
        return;

    vector<cd> a0(n / 2), a1(n / 2);
    for (int i = 0; 2 * i < n; i++) {
        a0[i] = a[2*i];
        a1[i] = a[2*i+1];
    }
    fft(a0, invert);
    fft(a1, invert);

    double ang = 2 * PI / n * (invert ? -1 : 1);
    cd w(1), wn(cos(ang), sin(ang));
    for (int i = 0; 2 * i < n; i++) {
        a[i] = a0[i] + w * a1[i];
        a[i + n/2] = a0[i] - w * a1[i];
        if (invert) {
            a[i] /= 2;
            a[i + n/2] /= 2;
        }
        w *= wn;
    }
}
````



[Matemática]: https://github.com/alexistoigo/lab/blob/master/Matematica/main.md#matem%C3%A1tica
