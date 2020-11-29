[Estrutura de Dados]

# Stack

Pilhas são um tipo de estrutura, é modelado para funcionar de maneira que último elemento a entrar, é o primeiro a sair - LIFO (Last Input, First Output). Desta forma os elementos só podem entrar ou sair por um lado da estrutura, o topo.

Para entender uma stack, devemos pensar que cada vez que inserimos um elemento, nós o empilhamos em cima do anterior, desta maneira, para remover um elemento de baixo, primeiro é necessário remover os elementos que estão acima dele.

```cpp
#include <bits/stdc++.h>

using namespace std; 

int main () { 
    stack <int> s; 


    s.push(10); //insere o elemento 10 no topo da pilha
    s.push(30); //insere o elemento 30 no topo da pilha
    s.push(20); //insere o elemento 20 no topo da pilha
    s.push(5); //insere o elemento 5 no topo da pilha
    s.push(1); //insere o elemento 1 no topo da pilha
  

    //imprime o elemento do topo da pilha
    cout<<s.top()<<endl;
  
    //remove o elemento do topo da pilha
    s.pop();
  
    //insere o elemento 1 no topo da pilha
    s.push(4);

    //enquanto a pilha nao estiver vazia
    while(!s.empty()){
    	cout<<s.top()<<endl; //imprime o elemento do topo da pilha
    	s.pop(); //remove o elemento do topo da pilha
    }
  
    return 0; 
}
```

Saída para o código acima
```
1
4
5
20
30
10
```

[Estrutura de Dados]: https://github.com/alexistoigo/lab/blob/master/Estrutura%20de%20Dados/main.md#estrutura-de-dados