# Convex Hull

Este algoritmo tem como objetivo considerar N pontos de um plano, e gerar um casco convexo, ou seja, o menor polígono convexo que contém todos os pontos dados.

O algoritmo primeiro procura pelos pontos  os pontos A e B mais à esquerda e mais à direita. No caso de existirem vários desses pontos, o mais baixo entre a esquerda (coordenada Y mais baixa) é considerado como A, e o mais alto entre a direita (coordenada Y mais alta) é tomado como B.

Após isso, é traçada uma linha entre os pontos  A e B. Isso divide todos os outros pontos em dois conjuntos, S1 e S2, onde S1 contém todos os pontos acima da linha que conecta A e B, e S2 contém todos os pontos abaixo da linha que une A e B. Os pontos que se encontram na linha que une A e B podem pertencer a qualquer um dos conjuntos. Os pontos A e B pertencem a ambos os conjuntos. Agora o algoritmo constrói o conjunto superior S1 e o conjunto inferior S2 e, a seguir, os combina para obter a resposta.

Para obter o conjunto superior, classificamos todos os pontos pela coordenada x. Para cada ponto, verificamos se - o ponto atual é o último ponto (que definimos como B), ou se a orientação entre a linha entre A e o ponto atual e a linha entre o ponto atual e B é no sentido horário. Nesses casos, o ponto atual pertence ao conjunto superior S1. A verificação da natureza no sentido horário ou anti-horário pode ser feita verificando a orientação .

Se o ponto dado pertencer ao conjunto superior, verificamos o ângulo formado pela linha que liga o penúltimo ponto e o último ponto do casco convexo superior, com a linha que conecta o último ponto do casco convexo superior e o ponto atual. Se o ângulo não for no sentido horário, removemos o ponto mais recente adicionado ao casco convexo superior, pois o ponto atual será capaz de conter o ponto anterior, uma vez que seja adicionado ao casco convexo.

A mesma lógica se aplica ao conjunto inferior S2. Se qualquer um - o ponto atual é B, ou a orientação das linhas, formadas por A e o ponto atual e o ponto atual e B, for anti-horário - então ele pertence a S2.

Se o ponto fornecido pertence ao conjunto inferior, agimos de forma semelhante a um ponto no conjunto superior, exceto que verificamos uma orientação anti-horária em vez de uma orientação horária. Assim, se o ângulo formado pela linha que liga o penúltimo ponto e o último ponto no casco convexo inferior, com a linha que conecta o último ponto no casco convexo inferior e o ponto atual não for anti-horário, removemos o ponto mais recente adicionado ao casco convexo inferior, pois o ponto atual será capaz de conter o ponto anterior, uma vez adicionado ao casco.

O casco convexo final é obtido a partir da união do casco convexo superior e inferior.

O código funciona envinado um vetor com todas as coordenadas dos pontos do plano para a funçao convex_hull que modifica este vetor deixando apenas os pontos que fazem parte da convex hull. 

```cpp

#include<bits/stdc++.h>

using namespace std;

struct pt {
    double x, y;
};

bool cmp(pt a, pt b) {
    return a.x < b.x || (a.x == b.x && a.y < b.y);
}

bool cw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) < 0;
}

bool ccw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) > 0;
}

void convex_hull(vector<pt>& a) {
    if (a.size() == 1)
        return;

    sort(a.begin(), a.end(), &cmp);
    pt p1 = a[0], p2 = a.back();
    vector<pt> up, down;
    up.push_back(p1);
    down.push_back(p1);
    for (int i = 1; i < (int)a.size(); i++) {
        if (i == a.size() - 1 || cw(p1, a[i], p2)) {
            while (up.size() >= 2 && !cw(up[up.size()-2], up[up.size()-1], a[i]))
                up.pop_back();
            up.push_back(a[i]);
        }
        if (i == a.size() - 1 || ccw(p1, a[i], p2)) {
            while(down.size() >= 2 && !ccw(down[down.size()-2], down[down.size()-1], a[i]))
                down.pop_back();
            down.push_back(a[i]);
        }
    }

    a.clear();
    for (int i = 0; i < (int)up.size(); i++)
        a.push_back(up[i]);
    for (int i = down.size() - 2; i > 0; i--)
        a.push_back(down[i]);
}
 
double dist(pt a, pt b) { 
    return sqrt((a.x - b.x) * (a.x - b.x) 
                + (a.y - b.y) * (a.y - b.y)); 
} 
  
double perimeter(vector<pt> ans) { 
    double perimeter = 0.0; 
  
    for (int i = 0; i < ans.size() - 1; i++) { 
        perimeter += dist(ans[i], ans[i + 1]); 
    } 
  
    perimeter += dist(ans[0], ans[ans.size() - 1]); 
  
    return perimeter; 
} 

int main(){

	int n;

	cin>>n;
    vector<pt> vet;
    pt p;
    for(int i=0; i<n; i++){
        cin>>p.x>>p.y;
        vet.push_back(p);
    }

    convex_hull(vet);


    cout<<"pontos que fazem parte da convex hull:\n";
    for(auto i: vet){
        cout<<"("<< i.x <<","<<i.y<<")\n";
    }
	return 0;
}
```