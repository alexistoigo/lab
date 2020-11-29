# Problema da Mochila (KnapsacK- 0/1)

Imagine que um um ladrão irá roubar um museu com uma mochila que suporta um determinado peso. Ele vê uma quantidade de obras de arte valiosas, cada uma tem um respectivo valor, e um peso. Com essas informações, o ladrão quer saber qual o maior valor que ele pode roubar e carregar em sua mochila?

Esse problema é muito famoso, e tem sua solução resolvida com programação dinâmica, armazenando em uma matriz os valores que ele poderá roubar.

No início do problema, serão dados como entrada uma quantidade n de objetos, e um peso máximo w suportado pela mochila. Após isso, para cada um dos n objetos, será informado o seu respectivo peso e valor. Para resolver o problema então, iremos primeiramente criar 2 arrays de tamanho n, um deles para armazenar o peso e o outro para armazenar o valor de cada objeto. Após isso, é criada uma matriz de tamanho n+1 x w+1, onde serão armazenados a quantidade máxima de peso que o ladrão irá carregar para cada estado da DP.

```cpp
#include<bits/stdc++.h>

using namespace std;

int knapsack(int W, int value[], int weight[], int n){
    int K[n+1][W+1];

    for(int i=0; i<=n; i++){
        for(int j=0; j<=W; j++){
            if(i==0 || j==0)
                K[i][j]=0;
            else if(weight[i-1]<=j)
                K[i][j] = max(value[i-1]+K[i-1][j - weight[i-1]], K[i-1][j]);
            else
                K[i][j] = K[i-1][j];
        }

    }
    return K[n][W];

}

int main(){

    int n, w;

    cin>>n;

    int value[n], weight[n];
    for(int i=0; i<n; i++){
        cin>>value[i]>>weight[i];
    }
    cin >> w;
    cout << knapsack(w, value, weight, n) << '\n';

	return 0;
}
```

Os arrays weight[i], value[i] são, o peso e o valor do pacote i, no qual i {1,…, n}. w é o peso máximo que a mochila pode carregar. No caso de simplesmente ter apenas 1 pacote para escolher. Você calcula K[1][j] para cada j: o que significa o peso máximo da mochila ≥ o peso da 1ª embalagem, ou seja, K[1][j] = weight[1].


Com o limite de peso j, as seleções ótimas entre os pacotes {1, 2, ..., i-1, i} para ter o maior valor terão duas possibilidades:

Se o pacote i não for selecionado, K[i][j] é o valor máximo possível ao selecionar entre os pacotes {1, 2, ..., i - 1} com limite de peso de j. Então você tem K[i][j] = K[i - 1][j]. 

Se o pacote i for selecionado, então K[i][j] = value[i] mais o valor máximo pode ser obtido selecionando-se entre embalagens {1, 2, ..., i - 1} com limite de peso (j-weight[i]). Ou seja, em termos do valor que você tem é K[i][j] = value[i] + K[i-1][j-weight[i]].