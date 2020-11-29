# Problema do Troco (coin change)


No problema do troco, basicamente temos uma quantidade moedas com diferentes valores, como 1, 5 e 10 centavos por exemplo. Agora imaginemos que você é um caixa de supermercado, e apenas com esses valores disponíveis de moedas, e precise dar um troco de valor x. Temos que fazer esse valor usando as moedas de forma que um número mínimo de moedas seja usado.

Vamos pegar o caso de o troco ser de 10 centavos. Usando essas moedas, podemos fazer isso das seguintes maneiras:

* Usando 1 moeda de 10 centavos
* Usando duas moedas de 5 centavos
* Usando uma moeda de 5 centavos e 5 moedas de 1 centavo
* Usando 10 moedas de 1 centavo

É possível perceber que a maneira de dar o troco usando o menor número de moedas, é usando uma moeda de 10 centavos.

Para a solução, cada índice do array preenchido da função, representa o valor mínimo para um troco de valor i, e a cada iteração o algoritmo vai comparando com os resultados já calculados, qual o minimo de moedas para aquele troco.

```cpp
int min_coins(int n, int m, int * vet){
    for(int i=1; i<=m; i++){
        dp[i] = INF;
        for(int j=0; j<n; j++){
            if(i-vet[j]>=0){
                dp[i] = min(dp[i], dp[i-vet[j]]+1);
            }else{
                break;
            }
        }
    }

    return dp[m];
}
```