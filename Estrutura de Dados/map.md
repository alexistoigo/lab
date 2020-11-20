#Map

O mapa é uma estrutura associativa que armazena elementos em chave-valor. Para usar o map e suas funções no C++, é preciso incluir a biblioteca \<map> ou a biblioteca padrão do C++ com toda a STL inclusa \<bits/stdc++.h> 

Mapas são geralmente usados ​​para classificar e identificar exclusivamente os elementos, ou seja, cada elemento armazenado no map possui um valor correspondente associado a essa chave.

Em um mapa, os elementos dentro dele são sempre ordenados por sua chave seguindo um critério de ordenação próprio (strings em ordem alfabética, números em ordem crescente). É possível também criar mapas não ordenados (unordered_map).

Um map geralmente será mais lento que um unordered_map para acessar elementos individuais por sua chave, porém um map permite uma iteração direta com base em sua ordem predefinida.

Toda chave é exclusiva, ou seja, não se pode ter duas chaves iguais. Já os valores se comportam de forma que um valor pode ser associado a várias chaves.

Por exemplo, podemos associar espécies de animais, com o seu respectivo número de patas: 

“Cachorro” => 4

“Gato” => 4

“Galinha” => 2

Se acessarmos o valor da chave "cachorro", obteremos o número 4 como retorno.

```cpp
#include<iostream>
#include<map>

using namespace std;

int main(){

    // inicializa um map, com o tipo da chave sendo string, e seu valor associado sendo int
    map<string, int> my_map;

    //coloca os valores no mapa
    my_map["gato"] = 4;
    my_map["cachorro"] = 4;
    my_map["galinha"] = 2;

    // imprime o valor correspondente a chave "galinha" 
    cout << "o valor associado com a chave galinha é "<<my_map["galinha"] << endl;


    // itera sobre o mapa (iteracao em ordem alfabética das chaves)
    for(auto i : my_map) {
        //i.first retorna a chave e i.second retorna o valor
        cout<<i.first<<" "<<i.second<<endl;
    }
    return 0;
}
```

```
o valor associado com a chave galinha é 2
cachorro 4
galinha 2
gato 4
```


Se no mesmo código trocarmos a declaração de map para unordered_map, ao iterarmos, os valores serão apresentados em uma ordem diferente na iteração

```cpp
#include<iostream>
#include<unordered_map>

using namespace std;

int main(){

    // inicializa um map, com o tipo da chave sendo string, e seu valor associado sendo int
    map<string, int> my_map;
```

Saída para o mesmo código, porém com unordered_map
```
2
galinha 2
cachorro 4
gato 4
```

Algumas funções da biblioteca de map também são de grande utilidade:

* size: retorna o tamanho do map
* begin: aponta para o primeiro elemento do map
* end: aponta para a posição após o último elemento do map
* find: retorna se determinada chave existe no map

```cpp
#include<iostream>
#include<map>

using namespace std;

int main(){

    // inicializa um map, com o tipo da chave sendo string, e seu valor associado sendo int
    map<string, int> my_map;

    //coloca os valores no mapa
    my_map["gato"] = 4;
    my_map["cachorro"] = 4;
    my_map["galinha"] = 2;

    // entra no if se a chave cachorro existe no map 
    if (my_map.find("cachorro") != my_map.end()){
        cout<<my_map["cachorro"]<<endl;
    }else{
        cout<<"A chave 'cachorro' não existe no map"<<endl;
    }

    return 0;
}
```
Saída esperada
```
4
```