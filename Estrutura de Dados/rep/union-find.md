# Union Find

Uma explicação básica e rápida sobre union find é a seguinte. Você possui vários nodos, que estão contidos em grupos distindos. A qualquer momento, você pode querer saber a qual grupo determinado nodo faz parte. Além disso, você pode juntar 2 grupos formando apenas um. O objetivo do algoritmo, é, sempre que for feito uma consulta, você conseguir dizer se dois nodos estão no mesmo grupo ou não.

A ideia é a seguinte. No início, você marca cada nodo como pertencente a um grupo diferente, composto apenas dele mesmo. Conforme a necessidade, vamos juntar nodos como membros do mesmo grupo e escolher um nodo pai para cada grupo. Cada nodo terá seu nodo “pai”, e aquele que não tem (que é pai de si mesmo), é o patriarca do grupo. Deste modo, para verificar se dois nodos pertencem ao mesmo grupo, basta olhar se o nodo pai deles dois é igual.

```cpp
#include<iostream>

#define MAXN 100001
using namespace std;


int pai[MAXN], peso[MAXN];

int find(int x){
	if(pai[x]==x) return x;

	return pai[x] = find(pai[x]);
}

void join(int x, int y) {
    pai[find(x)] = find(y);
}

int main(){

	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n, b, x, y;

	cin>>n>>b;
	char op;


	for(int i=1; i<=n; i++){
		pai[i] = i;
	}
	for(int i=0; i<b; i++){
		cin>>op>>x>>y;

		if(op == 'F'){
			join(x, y);
		}  
		else if (op == 'C'){
			find(x)==find(y)? cout<<"S\n" : cout<<"N\n";

		}

	}
	return 0;
}

```