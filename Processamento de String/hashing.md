[String]

# String Hashing

Algoritmos de hash são úteis para resolver diversos problemas.

Queremos resolver o problema de comparar strings de forma eficiente. A forma de força bruta de fazer isso é apenas comparar as letras de ambas as strings, que tem uma complexidade de tempo de ***O ( min (n1,n2) )***  sendo **n1** e **n2** o tamanho das duas strings. Queremos fazer melhor. A ideia por trás das strings é a seguinte: convertemos cada string em um inteiro e os comparamos ao invés das strings. Comparar duas strings é então ***O ( 1 )***.

Para a conversão, precisamos de uma função chamada hash. O objetivo é converter uma string em um inteiro, o chamado hash da string. A seguinte condição deve ser válida: se duas strings ***s*** e ***t*** são iguais ***(s = t)***, então seus hashes também devem ser iguais ***(hash ( s ) = hash ( t ))*** Caso contrário, não poderemos comparar strings.

A direção oposta não precisa se manter. Se os hashes forem iguais ***(hash ( s ) = hash ( t ))***, então as strings não precisam necessariamente ser iguais. Por exemplo, uma função hash válida seria simplesmente ***hash ( s ) = 0*** para cada ***s***. A razão pela qual a direção oposta não precisa se manter, é porque existem muitas strings exponenciais. Se quisermos apenas que esta função hash distinga entre todas as strings que consistem em caracteres minúsculos de comprimento menor do que 15, então o hash não caberia mais em um inteiro de 64 bits (por exemplo, longo sem sinal), porque há tantos deles. E, claro, não queremos comparar inteiros longos arbitrários, porque isso também terá a complexidade ***O ( n )***.

Normalmente, queremos que a função hash mapeie strings em números de um intervalo fixo *[ 0 , m )*, então a comparação de strings é apenas uma comparação de dois inteiros com um comprimento fixo. E claro, queremos que ***hash ( s ) ≠ hash ( t )*** ser muito provável se ***s ≠ t***.

### Cálculo do Hash de uma String

A maneira amplamente usada ára definir o hash de uma string ***s*** de comprimento ***n*** é:

````cpp
long long compute_hash(string const& s) {
    const int p = 31;
    const int m = 1e9 + 9;
    long long hash_value = 0;
    long long p_pow = 1;
    for (char c : s) {
        hash_value = (hash_value + (c - 'a' + 1) * p_pow) % m;
        p_pow = (p_pow * p) % m;
    }
    return hash_value;
}
````

### Problema de Exemplo

##### Procurar por strings duplicadas em uma série de strings

Problema: dada uma lista de ***n*** strings ***s[i]***, cada um não mais que ***m*** caracteres, encontre todas as strings duplicadas e divida-as em grupos.

A partir do algoritmo envolvendo a classificação das strings, obteríamos uma complexidade de tempo de ***O ( n * m * log n )*** onde a ordenação requer ***O ( n * log n )*** comparações e cada comparação leva ***O ( m )***. No entanto, usando hashes, reduzimos o tempo de comparação para ***O ( 1 )***, nos dando um algoritmo que é executado em ***O ( n * m + n log n )***.

Calculamos o hash para cada string, classificamos os hashes junto com os índices e, em seguida, agrupamos os índices por hashes idênticos.

````cpp
vector<vector<int>> group_identical_strings(vector<string> const& s) {
    int n = s.size();
    vector<pair<long long, int>> hashes(n);
    for (int i = 0; i < n; i++)
        hashes[i] = {compute_hash(s[i]), i};

    sort(hashes.begin(), hashes.end());

    vector<vector<int>> groups;
    for (int i = 0; i < n; i++) {
        if (i == 0 || hashes[i].first != hashes[i-1].first)
            groups.emplace_back();
        groups.back().push_back(hashes[i].second);
    }
    return groups;
}
````

### Aplicações de Hashing

Aqui estão algumas aplicações típicas de String Hashing.

- Algoritmo [Rabin-Karp] para correspondência de padrões em uma string em ***O ( n )***.
- Calcular o número de substrings diferentes de uma string em ***O (n² * log n )***.
- Calcular o número de substrings palindrômicos em uma string.


[String]: https://github.com/alexistoigo/lab/blob/master/Processamento%20de%20String/main.md#processamento-de-string
[Rabin-Karp]: https://github.com/alexistoigo/lab/blob/master/Processamento%20de%20String/karp.md#rabin-karp