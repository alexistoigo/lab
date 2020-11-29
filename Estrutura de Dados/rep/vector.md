[Estrutura de Dados]

# Vector

Tem comportamento semelhante ao de arrays normais. A principal diferença é a capacidade de ter tamanho dinâmico.

Ao criar um vector, não é necessário informar o tamanho. Conforme for usando a estrutura, é possível adicionar um elemento no final do array.

```cpp
#include<iostream>
#include<vector>

using namespace std;

int main(){
    vector<int> vet; //declara o array
    
    vet.push_back(3); //adiciona o valor 3 ao final do array
    vet.push_back(5);  //adiciona o valor 5 ao final do array
    vet.push_back(3);  //adiciona o valor 3 ao final do array
    vet.push_back(1);  //adiciona o valor 1 ao final do array

    for(auto i:vet){
        cout<<i<<' ';
    }

    cout<<'\n';
}

```
Exemplo de Saída para o código acima:
```
3 5 3 1
```


[Estrutura de Dados]: https://github.com/alexistoigo/lab/blob/master/Estrutura%20de%20Dados/main.md#estrutura-de-dados
