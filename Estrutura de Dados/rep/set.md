[Estrutura de Dados]

# Set

Um set é um contêiner que possui um conjunto de objetos exclusivos, ou seja cada elemento pode aparecer no set apenas uma vez. Depois de adicionado, um valor não pode ser modificado dentro do set, apenas podem ser removidos.

Ao adicionar um valor em um set, ele fica posicionado de acordo com uma ordem interna da estrutura (ordem crescente). Também é possível criar um set não ordenado através da estrutura unordered_set.

Os contêineres set são geralmente mais lentos do que os contêineres unordered_set no acesso a elementos individuais por sua chave, porém, eles permitem a iteração direta em subconjuntos com base em sua ordem.


```cpp
#include<iostream>
#include<set>

using namespace std;

int main(){
    set<int> my_set; //declara o set
    
    
    my_set.insert(1); // insere 1 no set
    my_set.insert(12); // insere 12 no set
    my_set.insert(5); // insere 5 no set
    my_set.insert(1); // não faz a insersão, pois o valor 1 já existe no set

	cout << "tamanho do set: "<< my_set.size() << endl;

	// percorre e imprime os valores do set
	for(auto i : my_set)
		cout<<i<<endl;

    cout<<'\n';
}
```
Exemplo de Saída para o código acima:
```
tamanho do set: 3
1
5
12
```


