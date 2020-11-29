# Subarray Contíguo de Maior Soma (Algoritmo de Kadane)


Este problema consiste em procurar no array, qual é a subsequência contínua com maior soma. Por exemplo, num array [1, 2, 3, 4, 5], a maior soma é 15, que é a soma do array inteiro. Já no caso de o array for [-1, -2, 3, 4, -2, -1, 15, -7], a maior soma contínua será 19 (3 + 4 + (-2) + (-1) + 15).

A ideia do algoritmo é procurar todos os segmentos contíguos positivos da matriz. E mantenha o controle da soma máxima do segmento contíguo entre todos os segmentos positivos. O funcionamento é bem simples. Enquanto o array de soma atual for positivo, compare ele com o array de soma máxima, se o valor for maior, atribua ao soma máxima. Se em algum momento o array de soma atual for negativo, altere o valor dele para zero, e comece uma nova soma.

```cpp
#include<bits/stdc++.h>

using namespace std; 
  
int maxSubArraySum(int vet[], int size) { 
    int max_total = INT_MIN, max_atual = 0; 
  
    for (int i = 0; i < size; i++) { 
        max_atual = max_atual + vet[i]; 
        max_total = max(max_atual, max_total); 
  
        if (max_atual < 0) 
            max_atual = 0; 
    } 
    return max_total; 
} 

int main() { 
    int vet[] = {12, -4, 2, 1, -2, -1, 5, -3, 2, -1, 8}; 
    int n = sizeof(vet)/sizeof(a[0]); 
    int max_sum = maxSubArraySum(vet, n); 
    cout << max_sum<<'\n'; 
    return 0; 
} 
```