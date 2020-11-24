[Algo]

# Crivo de Eratóstenes

O crivo de Eratóstenes ou peneira de Eratóstenes é um algoritmo para encontrar todos os números primos em um segmento ***[ 1 ; n ]*** usando ***O ( n log registros n )*** operações.

O algoritmo é muito simples: no início, anotamos todos os números entre 2 e n. Marcamos todos os múltiplos apropriados de 2 (visto que 2 é o menor número primo) como compostos. Um múltiplo adequado de um número *x*, é um número maior que *x* e divisível por *x*. Então encontramos o próximo número que não foi marcado como composto, neste caso é 3. O que significa que 3 é primo, e marcamos todos os múltiplos próprios de 3 como compostos. O próximo número não marcado é 5, que é o próximo número primo, e marcamos todos os múltiplos apropriados dele. E continuamos este procedimento até processarmos todos os números da linha.

A ideia por trás é esta: um número é primo se nenhum dos números primos menores o dividir. Como iteramos os números primos em ordem, já marcamos todos os números, que são divisíveis por pelo menos um dos números primos, como divisíveis. Portanto, se chegarmos a uma célula e ela não estiver marcada, ela não será divisível por nenhum número primo menor e, portanto, terá que ser primo.


### Implementação

````cpp
int n;
vector<char> is_prime(n+1, true);
is_prime[0] = is_prime[1] = false;
for (int i = 2; i <= n; i++) {
    if (is_prime[i] && (long long)i * i <= n) {
        for (int j = i * i; j <= n; j += i)
            is_prime[j] = false;
    }
}
````

Esse código marca primeiro todos os números, exceto zero e um, como números primos em potencial, depois começa o processo de peneirar os números compostos. Para isso, itera sobre todos os números de *2* até *n*. Se o número atual *i* é um número primo, ele marca todos os números que são múltiplos de i como números compostos, começando de *i²*. Isso já é uma otimização em vez de uma forma ingênua de implementá-la, e é permitido porque todos os números menores que são múltiplos de *i* necessário também tem um fator principal que é menor que *i*, então todos eles já foram peneirados antes. Desde a *i²* pode facilmente estourar o tipo *int*, a verificação adicional é feita usando o tipo **long long** antes do segundo loop aninhado.

Usando essa implementação, o algoritmo consome ***O ( n )*** da memória (obviamente) e executa ***O ( n log registros n )***


[Algo]: https://github.com/alexistoigo/lab#algo