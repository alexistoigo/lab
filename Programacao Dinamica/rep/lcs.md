[Programação Dinâmica]


# Longest Common Subsequence


A maior subsequência comum (LCS) é definida como a maior subsequência comum a todas as sequências fornecidas, desde que os elementos da subsequência não sejam obrigados a ocupar posições consecutivas dentro das sequências originais.

Para entender melhor este problema, vamos supor que nós temos dois arrays, S1 e S2. para isso S1 será igual [B, C, D, A, A, C, D] e S2 será igual a [A, C, D, B, A, C]. A partir disso, tentaremos achar uma sequência que seja comum aos dois arrays.

Algumas subsequências comuns que podemos observar são [B, C], [C, D, A, C], [D, A, C], [A, A, C], [A, C], [C, D]. Dessas sequências, claramente podemos ver que a maior é a sequência [C, D, A, C] e o tamanho dela é 4.

```cpp
#include<bits/stdc++.h>
  

using namespace std;

int lcs( char *X, char *Y, int m, int n ) {  
    int L[m + 1][n + 1];  
    int i, j;  
      
    for (i = 0; i <= m; i++)  {  
        for (j = 0; j <= n; j++) {  
        if (i == 0 || j == 0)  
            L[i][j] = 0;  
      
        else if (X[i - 1] == Y[j - 1])  
            L[i][j] = L[i - 1][j - 1] + 1;  
      
        else
            L[i][j] = max(L[i - 1][j], L[i][j - 1]);  
        }  
    }
          
    return L[m][n];  
}  
 
int main()  {  
    char X[] = "AGGTAB";  
    char Y[] = "GXTXAYB";  
      
    int m = strlen(X);  
    int n = strlen(Y);  
      
    cout << "Length of LCS is " << lcs( X, Y, m, n );  
      
    return 0;  
}  
```
O algorítmo funciona da seguinte maneira.
* Crie uma matriz de dimensões em n+1 X m+1 que n e m são os comprimentos de X e Y respectivamente. A primeira linha e a primeira coluna são preenchidas com zeros.

* Preencha cada célula da tabela usando a seguinte lógica: se o caractere que corresponde à linha atual e à coluna atual corresponderem, preencha a célula atual adicionando um ao elemento diagonal. Aponte uma seta para a célula diagonal.
* Caso contrário, pegue o valor máximo da coluna anterior e o elemento da linha anterior para preencher a célula atual. Aponte uma seta para a célula com valor máximo. Se eles forem iguais, aponte para qualquer um deles.
* O valor na última linha e na última coluna é o comprimento da maior subsequência comum.


[Programação Dinâmica]: https://github.com/alexistoigo/lab/blob/master/Programacao%20Dinamica/main.md#programa%C3%A7%C3%A3o-din%C3%A2mica
